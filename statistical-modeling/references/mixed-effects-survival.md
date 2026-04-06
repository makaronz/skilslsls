# Mixed Effects and Survival Analysis

Model hierarchical data with mixed effects and time-to-event data with survival analysis.

---

## Mixed Effects Models

### When to Use
- Data has hierarchical/nested structure (students within schools, patients within hospitals)
- Repeated measures on same subjects
- Need to account for correlation within groups
- Interest in both group-level and population-level effects

### Model Components

| Component | Description | Example |
|-----------|-------------|---------|
| Fixed effects | Population-level parameters | Treatment effect, age |
| Random intercepts | Group-specific baseline | Each school's average |
| Random slopes | Group-specific trends | Each school's treatment response |
| Residual error | Within-group variation | Individual variability |

### Model Specification

```python
import statsmodels.formula.api as smf

# Random intercept model
model1 = smf.mixedlm(
    "score ~ treatment + age + gender",
    data=df,
    groups=df["school_id"]
).fit()

# Random intercept + random slope
model2 = smf.mixedlm(
    "score ~ treatment + age + gender",
    data=df,
    groups=df["school_id"],
    re_formula="~treatment"  # Random slope for treatment
).fit()

print(model2.summary())
```

### Interpretation

| Output | Interpretation |
|--------|---------------|
| Fixed effect coefficient | Average effect across all groups |
| Random effect variance | Variability in effect across groups |
| ICC (Intraclass Correlation) | Proportion of variance between groups |
| Conditional prediction | Prediction for specific group |
| Marginal prediction | Average prediction across groups |

### ICC Calculation
```
ICC = var(random intercept) / (var(random intercept) + var(residual))
```
- ICC > 0.1: Mixed model justified (>10% of variance between groups)
- ICC < 0.05: Regular regression may suffice

---

## Survival Analysis

### Key Concepts

| Concept | Definition |
|---------|-----------|
| Survival function S(t) | Probability of surviving beyond time t |
| Hazard function h(t) | Instantaneous failure rate at time t |
| Censoring | Observation ends before event occurs |
| Right censoring | Most common: subject still alive at study end |

### Kaplan-Meier Estimator

Non-parametric survival curve estimation:

```python
from lifelines import KaplanMeierFitter

kmf = KaplanMeierFitter()
kmf.fit(durations=df['time'], event_observed=df['event'])

# Plot survival curve
kmf.plot_survival_function()

# Median survival time
print(f"Median survival: {kmf.median_survival_time_}")

# Compare groups
from lifelines.statistics import logrank_test
results = logrank_test(
    durations_A=group_a['time'], event_observed_A=group_a['event'],
    durations_B=group_b['time'], event_observed_B=group_b['event']
)
print(f"Log-rank test p-value: {results.p_value:.4f}")
```

### Cox Proportional Hazards Model

Semi-parametric model for assessing covariate effects on survival:

```python
from lifelines import CoxPHFitter

cph = CoxPHFitter()
cph.fit(df, duration_col='time', event_col='event')
cph.print_summary()

# Hazard ratios
print("Hazard Ratios:")
print(np.exp(cph.params_))

# Check proportional hazards assumption
cph.check_assumptions(df, p_value_threshold=0.05)
```

### Hazard Ratio Interpretation

| HR Value | Interpretation | Example |
|----------|---------------|---------|
| HR = 1.0 | No effect | No difference between groups |
| HR = 1.5 | 50% higher hazard | Treatment group fails 50% faster |
| HR = 0.7 | 30% lower hazard | Treatment reduces hazard by 30% |
| HR = 2.0 | Double the hazard | Exposure doubles risk |

---

## Accelerated Failure Time (AFT) Models

Parametric alternative to Cox model:

| Distribution | Hazard Shape | Use Case |
|-------------|-------------|----------|
| Exponential | Constant | Simple, baseline comparison |
| Weibull | Monotonic (increasing or decreasing) | Most common parametric |
| Log-normal | Hump-shaped | Non-monotonic hazard |
| Log-logistic | Hump-shaped, flexible | Medical treatment effects |

```python
from lifelines import WeibullAFTFitter

aft = WeibullAFTFitter()
aft.fit(df, duration_col='time', event_col='event')
aft.print_summary()

# Acceleration factor: exp(coef) > 1 means longer survival
```

---

## Model Selection and Validation

### Comparing Survival Models

| Metric | Description | Use |
|--------|-------------|-----|
| Concordance index (C-index) | Discrimination ability | Compare model ranking accuracy |
| AIC/BIC | Information criteria | Compare parametric models |
| Log-likelihood ratio test | Nested model comparison | Test if added variables improve fit |
| Brier score | Calibration at specific times | Assess predicted probabilities |

### Time-Dependent ROC
```python
from lifelines.utils import concordance_index

c_index = concordance_index(
    df['time'], -cph.predict_partial_hazard(df), df['event']
)
print(f"C-index: {c_index:.3f}")  # > 0.7 is good, > 0.8 is excellent
```
