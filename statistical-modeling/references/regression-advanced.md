# Advanced Regression Techniques

Build and validate regression models for inference and prediction with proper diagnostics.

---

## Linear Regression Deep Dive

### Assumptions and Diagnostics

| Assumption | Diagnostic Test | Visual Check | Violation Fix |
|-----------|----------------|--------------|--------------|
| Linearity | Ramsey RESET test | Residual vs fitted plot | Transform variables, add polynomials |
| Normality of residuals | Shapiro-Wilk, K-S test | QQ plot | Bootstrap, robust SEs, transform Y |
| Homoscedasticity | Breusch-Pagan, White test | Residual vs fitted plot | WLS, robust standard errors |
| No multicollinearity | VIF (Variance Inflation Factor) | Correlation matrix | Remove or combine variables |
| Independence | Durbin-Watson test | Residual autocorrelation | Time series methods, GLS |
| No influential outliers | Cook's distance, leverage | Influence plot | Investigate, robust regression |

### VIF Interpretation

| VIF Value | Interpretation | Action |
|-----------|---------------|--------|
| 1 | No multicollinearity | None needed |
| 1-5 | Low-moderate | Acceptable |
| 5-10 | High | Investigate, consider removing |
| > 10 | Severe | Remove or combine predictors |

```python
from statsmodels.stats.outliers_influence import variance_inflation_factor

vif_data = pd.DataFrame()
vif_data["Variable"] = X.columns
vif_data["VIF"] = [variance_inflation_factor(X.values, i) for i in range(X.shape[1])]
print(vif_data.sort_values("VIF", ascending=False))
```

---

## Logistic Regression

### Model Interpretation

| Component | Interpretation |
|-----------|---------------|
| Coefficient (β) | Log-odds change per unit increase in X |
| Odds Ratio (e^β) | Multiplicative change in odds per unit X |
| Marginal Effect | Probability change (depends on baseline) |

### Performance Metrics

| Metric | Use Case | Formula |
|--------|---------|---------|
| AUC-ROC | Overall discrimination | Area under ROC curve |
| Log-loss | Probability calibration | -mean(y*log(p) + (1-y)*log(1-p)) |
| Precision | Minimize false positives | TP / (TP + FP) |
| Recall | Minimize false negatives | TP / (TP + FN) |
| F1-Score | Balance precision/recall | 2 × (P × R) / (P + R) |
| Brier Score | Calibration quality | mean((p - y)²) |

### Threshold Selection

```python
from sklearn.metrics import precision_recall_curve

precisions, recalls, thresholds = precision_recall_curve(y_test, y_prob)

# Choose threshold based on business requirements:
# - High recall (catch all positives): lower threshold (0.3-0.4)
# - High precision (minimize false alarms): higher threshold (0.6-0.7)
# - Balanced: F1-optimal threshold
```

---

## Regularization

### Comparison

| Method | Penalty | Effect on Coefficients | Best For |
|--------|---------|----------------------|----------|
| Ridge (L2) | λΣβ² | Shrinks toward zero | Many moderate predictors |
| Lasso (L1) | λΣ|β| | Drives some to exactly zero | Feature selection |
| Elastic Net | α*L1 + (1-α)*L2 | Combination | Correlated predictors + selection |

### Lambda Selection

```python
from sklearn.linear_model import LassoCV

lasso_cv = LassoCV(alphas=np.logspace(-4, 1, 100), cv=10)
lasso_cv.fit(X_train, y_train)
print(f"Best alpha: {lasso_cv.alpha_:.4f}")
print(f"Non-zero features: {np.sum(lasso_cv.coef_ != 0)}")
```

---

## Polynomial and Interaction Terms

### When to Use

| Pattern | Solution | Example |
|---------|----------|---------|
| Curvilinear relationship | Polynomial terms | `y ~ x + x²` |
| Effect depends on another variable | Interaction term | `y ~ x1 + x2 + x1:x2` |
| Diminishing returns | Log transform | `y ~ log(x)` |
| Multiplicative relationship | Log-log model | `log(y) ~ log(x)` |

### Best Practices
- Center variables before creating interactions (reduce multicollinearity)
- Include main effects when including interactions
- Limit polynomial degree to 2-3 (higher overfits)
- Use cross-validation to assess if complexity is justified

---

## Model Comparison

### Nested Model Comparison
- **Likelihood Ratio Test**: Compare nested models (restricted vs. full)
- **F-test**: Does adding variables significantly improve R²?

### Non-Nested Model Comparison
- **AIC/BIC**: Lower is better, BIC penalizes complexity more
- **Cross-validated RMSE**: Out-of-sample prediction error
- **Adjusted R²**: R² penalized for number of predictors

```python
import statsmodels.api as sm

model1 = sm.OLS(y, X1).fit()
model2 = sm.OLS(y, X2).fit()  # X2 includes X1 + additional variables

# Likelihood ratio test
lr_stat = 2 * (model2.llf - model1.llf)
p_value = chi2.sf(lr_stat, df=X2.shape[1] - X1.shape[1])
```
