# Forecasting Techniques

Comprehensive comparison of forecasting methods from classical to modern machine learning approaches.

---

## Method Selection Guide

| Method | Best For | Data Requirement | Interpretability | Accuracy |
|--------|---------|-----------------|-----------------|----------|
| Naive/Seasonal Naive | Baselines | Minimal | Perfect | Low |
| Exponential Smoothing | Smooth trends + seasonality | 2+ seasonal cycles | High | Medium |
| ARIMA/SARIMA | Stationary/differenced series | 50+ observations | Medium | Medium-High |
| Prophet | Business metrics with events | 1+ years daily | High | Medium-High |
| LSTM/GRU | Complex nonlinear patterns | Thousands of points | Low | High |
| XGBoost/LightGBM | Feature-rich tabular | Hundreds+ with features | Medium | High |
| Transformer models | Multiple related series | Very large datasets | Low | Very High |

---

## Exponential Smoothing (ETS)

### Model Types

| Error | Trend | Seasonal | Model Code | Use Case |
|-------|-------|----------|------------|----------|
| Additive | None | None | (A,N,N) | Level only |
| Additive | Additive | None | (A,A,N) | Trend, no seasonality |
| Additive | Additive | Additive | (A,A,A) | Trend + additive seasonality |
| Additive | Additive | Multiplicative | (A,A,M) | Growing seasonal amplitude |
| Additive | Damped | Additive | (A,Ad,A) | Decaying trend + seasonality |

```python
from statsmodels.tsa.holtwinters import ExponentialSmoothing

model = ExponentialSmoothing(
    train, trend='add', seasonal='mul', 
    seasonal_periods=12, damped_trend=True
).fit(optimized=True)

forecast = model.forecast(steps=12)
```

---

## Machine Learning Approaches

### Feature Engineering for Time Series

| Feature Type | Examples | Purpose |
|-------------|---------|---------|
| Lag features | y(t-1), y(t-7), y(t-365) | Autoregressive patterns |
| Rolling statistics | 7-day mean, 30-day std | Smoothed trends |
| Calendar features | Day of week, month, holiday flag | Seasonal patterns |
| Fourier features | sin/cos at various frequencies | Smooth seasonality |
| External features | Weather, price, promotions | Causal relationships |
| Interaction features | Holiday × day_of_week | Combined effects |

### XGBoost/LightGBM for Forecasting

```python
import lightgbm as lgb

# Create features
def create_features(df):
    df['dayofweek'] = df.index.dayofweek
    df['month'] = df.index.month
    df['lag_1'] = df['y'].shift(1)
    df['lag_7'] = df['y'].shift(7)
    df['rolling_7_mean'] = df['y'].rolling(7).mean()
    df['rolling_30_mean'] = df['y'].rolling(30).mean()
    return df

model = lgb.LGBMRegressor(
    n_estimators=1000, learning_rate=0.05,
    max_depth=6, num_leaves=31
)
model.fit(X_train, y_train,
          eval_set=[(X_val, y_val)],
          callbacks=[lgb.early_stopping(50)])
```

### Deep Learning (LSTM)

```python
import tensorflow as tf

model = tf.keras.Sequential([
    tf.keras.layers.LSTM(64, return_sequences=True, input_shape=(seq_len, n_features)),
    tf.keras.layers.Dropout(0.2),
    tf.keras.layers.LSTM(32),
    tf.keras.layers.Dropout(0.2),
    tf.keras.layers.Dense(forecast_horizon)
])
model.compile(optimizer='adam', loss='mse')
```

---

## Evaluation Metrics

| Metric | Formula | Interpretation | Best For |
|--------|---------|---------------|----------|
| MAE | mean(abs(y - ŷ)) | Average absolute error | General purpose |
| RMSE | sqrt(mean((y - ŷ)²)) | Penalizes large errors | When large errors are costly |
| MAPE | mean(abs((y - ŷ)/y)) × 100 | Percentage error | Comparing across scales |
| sMAPE | mean(2*abs(y-ŷ)/(abs(y)+abs(ŷ))) | Symmetric percentage | Avoids MAPE asymmetry |
| MASE | MAE / MAE_naive | Scaled vs. naive baseline | Universal comparison |

### Cross-Validation for Time Series

**Time Series Split (Walk-Forward):**
```
Fold 1: Train [1-100]    → Test [101-120]
Fold 2: Train [1-120]    → Test [121-140]
Fold 3: Train [1-140]    → Test [141-160]
```

Never shuffle time series data. Always maintain temporal order.

---

## Ensemble Methods

### Simple Averaging
```python
forecast = (arima_forecast + prophet_forecast + lgbm_forecast) / 3
```

### Weighted Averaging
```python
# Weights based on validation performance
weights = [0.3, 0.5, 0.2]  # Based on inverse MAPE
forecast = sum(w * f for w, f in zip(weights, forecasts))
```

### Stacking
- Train multiple base models
- Use their predictions as features for a meta-model
- Meta-model learns optimal combination weights
