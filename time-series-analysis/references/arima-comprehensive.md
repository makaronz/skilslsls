# ARIMA Comprehensive Guide

Build, diagnose, and optimize ARIMA and SARIMA models for time series forecasting.

---

## ARIMA Components

### Model Notation: ARIMA(p, d, q)

| Parameter | Name | Description | How to Determine |
|-----------|------|-------------|-----------------|
| p | AR order | Number of autoregressive lags | PACF plot (significant lags) |
| d | Differencing | Number of differences for stationarity | ADF test, visual inspection |
| q | MA order | Number of moving average lags | ACF plot (significant lags) |

### SARIMA Extension: ARIMA(p,d,q)(P,D,Q)[s]

| Parameter | Description | Example (Monthly Data) |
|-----------|-------------|----------------------|
| P | Seasonal AR order | Seasonal PACF at lag s |
| D | Seasonal differencing | Usually 0 or 1 |
| Q | Seasonal MA order | Seasonal ACF at lag s |
| s | Seasonal period | 12 for monthly, 4 for quarterly |

---

## Model Building Process

### Step 1: Stationarity Testing

```python
from statsmodels.tsa.stattools import adfuller

result = adfuller(series)
print(f'ADF Statistic: {result[0]:.4f}')
print(f'p-value: {result[1]:.4f}')
# p-value < 0.05 → stationary (no differencing needed)
# p-value > 0.05 → non-stationary (differencing required)
```

**Achieving Stationarity:**
- First difference: `d=1` removes linear trend
- Second difference: `d=2` for quadratic trends (rare)
- Seasonal difference: `D=1` removes seasonal pattern
- Log transform: Stabilizes variance before differencing

### Step 2: ACF and PACF Analysis

| Plot Pattern | Interpretation | Model Suggestion |
|-------------|----------------|-----------------|
| ACF cuts off after lag q | MA(q) signature | Set q to cutoff lag |
| PACF cuts off after lag p | AR(p) signature | Set p to cutoff lag |
| Both decay gradually | Mixed ARMA | Use auto_arima or try multiple |
| Spikes at seasonal lags | Seasonal component | Add (P,D,Q)[s] |

### Step 3: Model Fitting

```python
from statsmodels.tsa.statespace.sarimax import SARIMAX

model = SARIMAX(train_data, 
                order=(1, 1, 1),
                seasonal_order=(1, 1, 1, 12),
                enforce_stationarity=False,
                enforce_invertibility=False)
results = model.fit(disp=False)
print(results.summary())
```

### Step 4: Diagnostics

**Residual Checks:**
- **Ljung-Box test**: p-value > 0.05 → residuals are white noise (good)
- **Residual ACF**: No significant autocorrelation remaining
- **Normal distribution**: QQ-plot approximately straight line
- **Homoscedasticity**: Constant variance over time

```python
results.plot_diagnostics(figsize=(12, 8))
plt.show()

from statsmodels.stats.diagnostic import acorr_ljungbox
lb_test = acorr_ljungbox(results.resid, lags=20)
print(lb_test)  # All p-values should be > 0.05
```

---

## Model Selection

### Information Criteria

| Criterion | Formula | Preference |
|-----------|---------|-----------|
| AIC | -2*log(L) + 2*k | Lower is better |
| BIC | -2*log(L) + k*log(n) | Lower, penalizes complexity more |
| AICc | AIC + 2k(k+1)/(n-k-1) | Better for small samples |

### Automated Selection

```python
import pmdarima as pm

auto_model = pm.auto_arima(
    train_data,
    start_p=0, max_p=5,
    start_q=0, max_q=5,
    d=None,  # Auto-detect
    seasonal=True, m=12,
    start_P=0, max_P=2,
    start_Q=0, max_Q=2,
    D=None,
    trace=True,
    error_action='ignore',
    suppress_warnings=True,
    stepwise=True,
    information_criterion='aic'
)
print(auto_model.summary())
```

---

## Common Pitfalls

| Pitfall | Symptom | Fix |
|---------|---------|-----|
| Over-differencing | ACF of residuals has negative lag-1 | Reduce d |
| Over-fitting | Great training, poor test performance | Use BIC, reduce p+q |
| Ignoring seasonality | Residual ACF spikes at seasonal lags | Add seasonal component |
| Non-constant variance | Fan-shaped residuals | Log or Box-Cox transform |
| Structural breaks | Poor fit at change points | Split series or use regime models |
