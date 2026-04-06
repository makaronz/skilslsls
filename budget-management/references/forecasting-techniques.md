# Forecasting Techniques

Methods for projecting revenue, expenses, and cash flow to support budget planning and financial decision-making.

---

## Forecasting Methods Overview

| Method | Best For | Data Required | Complexity | Accuracy |
|--------|---------|---------------|-----------|----------|
| Straight-Line | Stable, predictable metrics | 2+ years of historical data | Low | Moderate |
| Moving Average | Smoothing volatile data | 6-12 months of data | Low | Moderate |
| Exponential Smoothing | Trend-following with recent bias | 12+ months of data | Medium | Good |
| Regression Analysis | Identifying driver relationships | Dependent + independent variables | Medium | Good |
| Scenario Modeling | Strategic planning under uncertainty | Assumptions for each scenario | Medium | Variable |
| Driver-Based | Operational forecasting | KPI and operational data | High | High |
| Monte Carlo | Risk quantification | Probability distributions | High | High |

## Straight-Line Forecasting

Apply a constant growth rate based on historical trend:

```
Forecast = Last Period Actual × (1 + Average Growth Rate)
```

Calculate the average growth rate from 3-5 years of historical data. Works well for mature businesses with stable trajectories. Fails when the market is shifting or the company is scaling rapidly.

## Moving Average

Smooth out short-term fluctuations to identify the underlying trend:

- **Simple Moving Average (SMA)**: Average of the last N periods. Equal weight to all periods.
- **Weighted Moving Average (WMA)**: Assign higher weights to recent periods to reflect the current trend more closely.

| Period | Actual | 3-Month SMA | 3-Month WMA (3,2,1) |
|--------|--------|-------------|---------------------|
| Jan | 100 | — | — |
| Feb | 110 | — | — |
| Mar | 105 | 105.0 | 105.8 |
| Apr | 115 | 110.0 | 111.7 |
| May | 120 | 113.3 | 115.8 |

## Driver-Based Forecasting

Build the forecast from operational drivers rather than top-down estimates:

### Revenue Drivers Example (SaaS)

```
Monthly Revenue = 
  (Beginning MRR)
  + (New Customers × Average Contract Value / 12)
  + (Expansion MRR from upsells)
  - (Churned MRR)
  = Ending MRR
```

Each driver is forecast independently:
- New customers from marketing pipeline conversion rates
- Expansion from product usage triggers and sales capacity
- Churn from historical retention curves by cohort

### Expense Drivers Example

```
Headcount Cost = Planned Hires × Average Fully-Loaded Cost × Months Remaining
Infrastructure Cost = Forecasted Users × Cost Per User × Utilization Factor
```

## Scenario Modeling

Build three scenarios to bracket the range of outcomes:

| Assumption | Bear Case | Base Case | Bull Case |
|-----------|-----------|-----------|-----------|
| Revenue growth | 5% | 15% | 25% |
| Customer churn | 8% | 5% | 3% |
| Headcount additions | +5 | +12 | +20 |
| Marketing spend | $200K | $400K | $600K |

Weight scenarios by probability (e.g., Bear 20%, Base 60%, Bull 20%) to calculate an expected value.

## Rolling Forecast Best Practices

Replace the static annual budget with a rolling forecast that extends 12-18 months forward and updates monthly or quarterly:

1. **Update actuals**: Replace the completed month's forecast with actual results
2. **Extend the horizon**: Add a new month at the end to maintain the rolling window
3. **Adjust assumptions**: Revise key drivers based on the latest data and market conditions
4. **Variance commentary**: Document why actuals deviated from the prior forecast
5. **Reforecast cadence**: Monthly for high-growth businesses, quarterly for stable ones

Rolling forecasts improve accuracy because they incorporate the latest information rather than locking in assumptions made 12 months prior.
