# Generalized Linear Models (GLM) Comprehensive Guide

Build GLMs for non-normal response variables with appropriate link functions and distributions.

---

## GLM Framework

### Components

Every GLM has three components:

| Component | Description | Example (Poisson) |
|-----------|-------------|-------------------|
| Random | Distribution of Y | Poisson (count data) |
| Systematic | Linear predictor η = Xβ | η = β₀ + β₁x₁ + β₂x₂ |
| Link function | Connects E(Y) to η | log(μ) = η |

### Common GLM Families

| Distribution | Link | Response Type | Example Use Case |
|-------------|------|--------------|-----------------|
| Gaussian | Identity | Continuous | Prices, measurements |
| Binomial | Logit | Binary/proportion | Pass/fail, conversion rate |
| Poisson | Log | Count | Events, visits, defects |
| Negative Binomial | Log | Overdispersed count | Insurance claims |
| Gamma | Log or Inverse | Positive continuous | Duration, costs |
| Tweedie | Log | Mixed zero + positive | Insurance losses |
| Inverse Gaussian | Inverse squared | Positive, right-skewed | Response times |

---

## Poisson Regression

### When to Use
- Response is a count (0, 1, 2, ...)
- Mean approximately equals variance
- Events occur independently

### Implementation

```python
import statsmodels.api as sm

# Poisson GLM
poisson_model = sm.GLM(
    y_count, X_with_const,
    family=sm.families.Poisson(link=sm.families.links.Log())
).fit()

print(poisson_model.summary())

# Interpret coefficients
# exp(β) = rate ratio (multiplicative effect on count)
print("Rate ratios:", np.exp(poisson_model.params))
```

### Handling Overdispersion

When variance > mean (common in real data):

**Test for Overdispersion:**
```python
# Pearson chi-squared / df should be close to 1
pearson_chi2 = poisson_model.pearson_chi2
df_resid = poisson_model.df_resid
dispersion = pearson_chi2 / df_resid
print(f"Dispersion: {dispersion:.2f}")  # > 1.5 suggests overdispersion
```

**Solutions:**
1. Quasi-Poisson: Adjusts standard errors for overdispersion
2. Negative Binomial: Adds dispersion parameter
3. Zero-Inflated models: When excess zeros cause overdispersion

---

## Negative Binomial Regression

```python
from statsmodels.discrete.discrete_model import NegativeBinomial

nb_model = NegativeBinomial(y_count, X_with_const).fit()
print(nb_model.summary())

# Alpha parameter > 0 indicates overdispersion
print(f"Alpha (dispersion): {nb_model.params[-1]:.4f}")
```

---

## Gamma Regression

### When to Use
- Positive continuous response (costs, durations, amounts)
- Variance proportional to mean squared
- Right-skewed distribution

```python
gamma_model = sm.GLM(
    y_positive, X_with_const,
    family=sm.families.Gamma(link=sm.families.links.Log())
).fit()

# Predictions on original scale
predictions = gamma_model.predict(X_new)  # Already on response scale
```

---

## Model Diagnostics

### Residual Types

| Residual | Definition | Use |
|----------|-----------|-----|
| Deviance | Contribution to model deviance | Default diagnostic |
| Pearson | (y - μ) / sqrt(V(μ)) | Check variance function |
| Anscombe | Variance-stabilized | Near-normal distribution |
| Working | Used in IRLS algorithm | Technical diagnostics |

### Diagnostic Plots
1. **Residuals vs Fitted**: Check for patterns (should be random)
2. **QQ Plot of Deviance Residuals**: Check distributional assumption
3. **Scale-Location**: Check homogeneity of variance
4. **Cook's Distance**: Identify influential observations

### Goodness of Fit

| Metric | Description | Interpretation |
|--------|-------------|---------------|
| Deviance | -2 * (log L_model - log L_saturated) | Lower is better |
| Pearson χ² | Σ(y - μ)² / V(μ) | ≈ df_resid if good fit |
| AIC | -2*logL + 2k | Compare non-nested models |
| Pseudo R² | 1 - (deviance / null deviance) | % deviance explained |

---

## Practical Guidelines

### Choosing the Right GLM

1. **Examine the response variable**: Distribution, range, variance pattern
2. **Check mean-variance relationship**: Plot variance vs mean across groups
3. **Consider zero-inflation**: Many zeros may need special models
4. **Compare link functions**: Try log, identity, inverse for same family
5. **Validate with residuals**: Check assumptions after fitting
6. **Cross-validate**: Compare predictive performance across families
