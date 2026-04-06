# Model Validation Techniques

Comprehensive guide to validating statistical models for reliable inference and prediction.

---

## Cross-Validation Methods

### Method Selection

| Method | When to Use | Bias | Variance | Computational Cost |
|--------|-----------|------|----------|-------------------|
| Hold-out (train/test) | Large datasets (>10K) | Medium | High | Very low |
| K-Fold CV (k=5 or 10) | Medium datasets | Low | Medium | Moderate |
| Leave-One-Out (LOO) | Small datasets (<100) | Very low | High | High |
| Stratified K-Fold | Imbalanced classes | Low | Medium | Moderate |
| Time Series Split | Temporal data | Low | Medium | Moderate |
| Repeated K-Fold | Robust estimation | Very low | Low | High |
| Nested CV | Model selection + evaluation | Low | Low | Very high |

### K-Fold Cross-Validation

```python
from sklearn.model_selection import cross_val_score, KFold

kf = KFold(n_splits=10, shuffle=True, random_state=42)
scores = cross_val_score(model, X, y, cv=kf, scoring='neg_mean_squared_error')

print(f"RMSE: {np.sqrt(-scores.mean()):.4f} ± {np.sqrt(-scores).std():.4f}")
```

### Nested Cross-Validation

For unbiased model selection and evaluation:
```
Outer loop (evaluation): 5-fold
  └── Inner loop (tuning): 5-fold within each outer fold
```

```python
from sklearn.model_selection import cross_val_score, GridSearchCV

inner_cv = KFold(n_splits=5, shuffle=True, random_state=42)
outer_cv = KFold(n_splits=5, shuffle=True, random_state=42)

# Inner loop: hyperparameter tuning
grid_search = GridSearchCV(estimator=model, param_grid=param_grid, cv=inner_cv)

# Outer loop: unbiased evaluation
nested_scores = cross_val_score(grid_search, X, y, cv=outer_cv, scoring='accuracy')
print(f"Nested CV accuracy: {nested_scores.mean():.3f} ± {nested_scores.std():.3f}")
```

---

## Residual Analysis

### Residual Diagnostic Plots

| Plot | What to Check | Healthy Pattern |
|------|--------------|----------------|
| Residuals vs Fitted | Linearity, homoscedasticity | Random scatter around zero |
| QQ Plot | Normality of residuals | Points on diagonal line |
| Scale-Location | Constant variance | Flat trend line |
| Residuals vs Leverage | Influential points | No points beyond Cook's distance |
| Residuals vs Predictors | Missed nonlinearity | Random scatter for each predictor |
| Residual histogram | Distribution shape | Approximately normal |

### Formal Tests

| Test | Null Hypothesis | Package |
|------|----------------|---------|
| Shapiro-Wilk | Residuals are normally distributed | `scipy.stats.shapiro` |
| Breusch-Pagan | Homoscedastic residuals | `statsmodels.het_breuschpagan` |
| Durbin-Watson | No autocorrelation | `statsmodels.durbin_watson` |
| Ramsey RESET | Model is correctly specified | `statsmodels.linear_harvey_collier` |

---

## Overfitting Detection

### Signs of Overfitting

| Indicator | Evidence |
|-----------|---------|
| Train-test gap | Training R² >> Test R² |
| Complex model wins on train | But simpler model wins on test |
| Unstable coefficients | Large changes with small data changes |
| Very large coefficients | Regularized model much better |
| Perfect training fit | R² = 1.0 (suspicious) |

### Prevention Strategies

| Strategy | How | When |
|----------|-----|------|
| Cross-validation | K-fold to estimate true performance | Always |
| Regularization | L1/L2 penalty on coefficients | Many predictors |
| Feature selection | Remove irrelevant predictors | High dimensionality |
| Early stopping | Stop training when validation worsens | Iterative algorithms |
| Ensemble methods | Average multiple models | Complex relationships |
| Simpler model | Fewer parameters | Small datasets |

---

## Bootstrap Methods

### Bootstrap Confidence Intervals

```python
from scipy import stats

def bootstrap_ci(data, statistic_fn, n_bootstrap=10000, alpha=0.05):
    n = len(data)
    bootstrap_stats = []
    for _ in range(n_bootstrap):
        sample = np.random.choice(data, size=n, replace=True)
        bootstrap_stats.append(statistic_fn(sample))
    
    lower = np.percentile(bootstrap_stats, 100 * alpha/2)
    upper = np.percentile(bootstrap_stats, 100 * (1 - alpha/2))
    return lower, upper

# Bootstrap 95% CI for median
ci = bootstrap_ci(data, np.median)
print(f"95% CI for median: ({ci[0]:.2f}, {ci[1]:.2f})")
```

### Bootstrap for Regression Coefficients
- Resample observations with replacement
- Refit model on each bootstrap sample
- Compute percentile intervals for each coefficient
- More robust than asymptotic standard errors when assumptions are violated

---

## Calibration Assessment

### For Classification Models

```python
from sklearn.calibration import calibration_curve

prob_true, prob_pred = calibration_curve(y_test, y_prob, n_bins=10)
# Plot prob_pred vs prob_true — perfect calibration is diagonal
```

### Hosmer-Lemeshow Test
- Groups predictions into deciles
- Compares observed vs expected events in each group
- p-value > 0.05 suggests adequate calibration

### Calibration Methods
- **Platt scaling**: Fit logistic regression on model outputs
- **Isotonic regression**: Non-parametric monotonic calibration
- **Temperature scaling**: Divide logits by learned temperature
