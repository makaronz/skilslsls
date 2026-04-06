# Time Series Case Studies

Real-world applications of time series analysis across industries.

---

## Case Study 1: Retail Demand Forecasting

### Problem
A retail chain needs to forecast daily product demand across 500 stores for inventory optimization.

### Approach

**Data:**
- 3 years of daily sales data per product per store
- External features: holidays, weather, promotions, events

**Model Selection:**
| Level | Model | Why |
|-------|-------|-----|
| Store-product | LightGBM | Handles many features, fast training |
| Category rollup | Prophet | Interpretable, handles holidays well |
| Total company | SARIMA + Prophet ensemble | Robust at aggregate level |

**Feature Engineering:**
- Lag features: 1, 7, 14, 28, 365 days
- Rolling means: 7, 14, 30-day windows
- Promotion flags with lead/lag windows
- Store-specific holiday effects
- Weather features (temperature, precipitation)

### Results
| Metric | Before | After | Improvement |
|--------|--------|-------|------------|
| MAPE (daily, store-SKU) | 42% | 28% | 33% reduction |
| Stockout rate | 8.5% | 4.2% | 51% reduction |
| Overstock waste | $2.1M/year | $1.3M/year | 38% reduction |

### Key Lessons
- Hierarchical forecasting (bottom-up + top-down reconciliation) improved consistency
- Promotion and holiday features had the largest impact
- Simple models at aggregate level, complex at granular level

---

## Case Study 2: Financial Time Series

### Problem
Predict daily stock price volatility for risk management and portfolio optimization.

### Approach

**Models Used:**
- GARCH(1,1) for volatility clustering
- EGARCH for asymmetric volatility (leverage effect)
- HAR-RV using realized volatility at multiple horizons

**Implementation:**
```python
from arch import arch_model

# GARCH(1,1) model
garch = arch_model(returns, vol='Garch', p=1, q=1, 
                    mean='AR', lags=1, dist='t')
result = garch.fit(disp='off')

# Forecast volatility
forecasts = result.forecast(horizon=5)
variance_forecast = forecasts.variance.iloc[-1]
```

### Key Insights
- Financial returns exhibit volatility clustering (GARCH captures this)
- Negative returns increase volatility more than positive (leverage effect)
- Multi-horizon models (HAR) outperform single-frequency models
- Regime-switching models handle market transitions better

---

## Case Study 3: Anomaly Detection in IoT Sensor Data

### Problem
Detect equipment failures from sensor readings before they cause downtime.

### Approach

**Method 1: Statistical Process Control**
- Fit baseline ARIMA to normal operation data
- Flag observations outside prediction intervals
- Threshold: 3σ for immediate alert, 2σ for warning

**Method 2: Isolation Forest on Features**
```python
from sklearn.ensemble import IsolationForest

features = create_time_features(sensor_data)  # Lags, rolling stats
iso_forest = IsolationForest(contamination=0.01, random_state=42)
anomaly_labels = iso_forest.fit_predict(features)
```

**Method 3: LSTM Autoencoder**
- Train on normal operation data
- Reconstruction error as anomaly score
- Threshold based on training error distribution

### Results
| Method | Precision | Recall | Lead Time |
|--------|-----------|--------|-----------|
| Statistical (3σ) | 78% | 65% | 2 hours |
| Isolation Forest | 85% | 72% | 4 hours |
| LSTM Autoencoder | 91% | 84% | 6 hours |
| Ensemble (all three) | 93% | 88% | 5 hours |

---

## Case Study 4: Web Traffic Forecasting

### Problem
Forecast website traffic to optimize server capacity and ad revenue planning.

### Approach

**Characteristics:**
- Strong weekly and yearly seasonality
- Holiday spikes (Black Friday, Christmas)
- Trend changes from product launches and SEO

**Model: Prophet with Custom Configuration**
```python
m = Prophet(
    changepoint_prior_scale=0.1,
    seasonality_mode='multiplicative',
    yearly_seasonality=10,
    weekly_seasonality=5
)

# Custom holidays
m.add_country_holidays(country_name='US')

# Custom events
m.add_regressor('product_launch', prior_scale=20)
m.add_regressor('marketing_campaign', prior_scale=10)
```

### Results
- 30-day forecast MAPE: 8.2%
- Server provisioning accuracy: 95% (previously 78%)
- Annual savings on over-provisioning: $340K

### Key Lessons
- Multiplicative seasonality essential for growing traffic
- Product launches and campaigns need explicit modeling
- Weekly data patterns different on holidays — conditional seasonality helps
