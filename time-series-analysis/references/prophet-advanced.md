# Prophet Advanced Guide

Master Facebook Prophet for scalable, interpretable time series forecasting.

---

## Prophet Architecture

### Model Components

Prophet decomposes time series as: **y(t) = g(t) + s(t) + h(t) + ε(t)**

| Component | Symbol | Description |
|-----------|--------|-------------|
| Trend | g(t) | Piecewise linear or logistic growth |
| Seasonality | s(t) | Fourier series (yearly, weekly, daily) |
| Holidays | h(t) | Known events with custom windows |
| Error | ε(t) | Normally distributed residuals |

---

## Configuration Guide

### Trend Configuration

```python
from prophet import Prophet

# Linear growth (default)
m = Prophet(growth='linear')

# Logistic growth (saturating)
m = Prophet(growth='logistic')
df['cap'] = 1000  # Upper bound
df['floor'] = 0   # Lower bound

# Changepoint tuning
m = Prophet(
    changepoint_prior_scale=0.05,  # Flexibility (default: 0.05)
    changepoint_range=0.8,         # First 80% of data for changepoints
    n_changepoints=25              # Number of potential changepoints
)
```

| Parameter | Low Value | High Value | Effect |
|-----------|-----------|------------|--------|
| `changepoint_prior_scale` | 0.001 | 0.5 | Trend flexibility |
| `n_changepoints` | 10 | 50 | Potential break points |
| `changepoint_range` | 0.5 | 0.9 | Where changepoints can occur |

### Seasonality Configuration

```python
m = Prophet(
    yearly_seasonality=True,    # Auto or integer (Fourier order)
    weekly_seasonality=True,
    daily_seasonality=False     # Enable for sub-daily data
)

# Custom seasonality
m.add_seasonality(
    name='monthly',
    period=30.5,
    fourier_order=5,
    prior_scale=0.1
)

# Conditional seasonality
def is_summer(ds):
    return ds.dt.month.isin([6, 7, 8])

m.add_seasonality(
    name='summer_weekly',
    period=7,
    fourier_order=3,
    condition_name='is_summer'
)
df['is_summer'] = is_summer(df['ds'])
```

### Holiday Configuration

```python
holidays = pd.DataFrame({
    'holiday': 'black_friday',
    'ds': pd.to_datetime(['2022-11-25', '2023-11-24', '2024-11-29']),
    'lower_window': -1,    # 1 day before
    'upper_window': 1,     # 1 day after
    'prior_scale': 10.0    # Impact strength
})

m = Prophet(holidays=holidays)
```

---

## Advanced Features

### Additional Regressors

```python
m = Prophet()
m.add_regressor('temperature', prior_scale=0.5, mode='additive')
m.add_regressor('promotion', prior_scale=10, mode='multiplicative')

# Regressors must be in training AND future dataframes
future = m.make_future_dataframe(periods=30)
future['temperature'] = forecast_temperature_values
future['promotion'] = planned_promotion_flags
```

### Multiplicative Seasonality

Use when seasonal effect scales with trend:
```python
m = Prophet(seasonality_mode='multiplicative')
# Useful for: Revenue, web traffic, anything that grows
```

### Cross-Validation

```python
from prophet.diagnostics import cross_validation, performance_metrics

# Time series cross-validation
df_cv = cross_validation(
    m,
    initial='730 days',   # Training period
    period='180 days',    # Spacing between cutoffs
    horizon='365 days'    # Forecast horizon
)

df_p = performance_metrics(df_cv)
print(df_p[['horizon', 'mape', 'rmse', 'mae']].tail())
```

---

## Hyperparameter Tuning

### Recommended Search Space

| Parameter | Range | Impact |
|-----------|-------|--------|
| `changepoint_prior_scale` | [0.001, 0.5] | Most impactful |
| `seasonality_prior_scale` | [0.01, 10] | Seasonality smoothness |
| `holidays_prior_scale` | [0.01, 10] | Holiday effect strength |
| `seasonality_mode` | ['additive', 'multiplicative'] | Scaling behavior |
| `yearly_seasonality` | [5, 15] Fourier order | Yearly pattern detail |
| `weekly_seasonality` | [3, 7] Fourier order | Weekly pattern detail |

---

## When to Use Prophet

| Scenario | Prophet Good? | Alternative |
|----------|--------------|-------------|
| Business metrics with seasonality | Yes | — |
| Multiple strong seasonalities | Yes | — |
| Known holidays/events | Excellent | — |
| Very short series (< 2 periods) | No | ARIMA, ETS |
| High-frequency (seconds/minutes) | No | ARIMA, ML models |
| Complex multivariate relationships | Partial | VAR, ML models |
| Need prediction intervals | Yes | — |
| Non-technical stakeholders | Excellent | — |
