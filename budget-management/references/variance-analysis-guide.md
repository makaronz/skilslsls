# Variance Analysis Guide

Techniques for analyzing budget-to-actual variances, identifying root causes, and driving corrective action.

---

## Variance Types

| Variance | Formula | Favorable When |
|----------|---------|---------------|
| Revenue Variance | Actual Revenue − Budgeted Revenue | Positive (actual > budget) |
| Expense Variance | Budgeted Expense − Actual Expense | Positive (actual < budget) |
| Volume Variance | (Actual Units − Budget Units) × Budget Price | Actual units exceed plan |
| Price Variance | (Actual Price − Budget Price) × Actual Units | Actual price exceeds plan (revenue) |
| Mix Variance | Change in product/channel mix impact on margin | Shift toward higher-margin products |
| Efficiency Variance | (Standard Hours − Actual Hours) × Standard Rate | Fewer hours than planned |

## Decomposition Framework

Break total variance into actionable components:

### Revenue Variance Decomposition

```
Total Revenue Variance = Volume Variance + Price Variance + Mix Variance

Volume Variance = (Actual Quantity − Budget Quantity) × Budget Average Price
Price Variance  = (Actual Price − Budget Price) × Actual Quantity
Mix Variance    = Σ[(Actual Mix% − Budget Mix%) × Budget Margin × Total Actual Volume]
```

This decomposition reveals whether a revenue shortfall is caused by selling fewer units, discounting prices, or shifting toward lower-value products.

### Expense Variance Decomposition

```
Total Expense Variance = Rate Variance + Volume Variance + Timing Variance

Rate Variance   = (Actual Rate − Budget Rate) × Actual Volume
Volume Variance = (Actual Volume − Budget Volume) × Budget Rate
Timing Variance = Spend recognized in different periods than budgeted
```

## Materiality Thresholds

Not every variance requires investigation. Define materiality thresholds to focus on impactful deviations:

| Variance Size | Action Required |
|--------------|-----------------|
| < 2% of budget | No action — within normal fluctuation |
| 2-5% of budget | Document the cause in the monthly commentary |
| 5-10% of budget | Investigate root cause, propose corrective action |
| > 10% of budget | Escalate to management with a remediation plan and updated forecast |

Adjust thresholds by line item — a 5% variance on a $10M revenue line ($500K) matters more than 5% on a $50K office supplies line ($2.5K).

## Root Cause Analysis

When investigating a significant variance, use the Five Whys framework:

1. **What** is the variance? (Revenue came in $200K below budget)
2. **Where** did it occur? (Enterprise segment, EMEA region)
3. **When** did it start? (Appeared in March, widened in April)
4. **Why** did it happen? (Two large deals slipped to Q3 due to procurement delays)
5. **What action** will correct it? (Accelerate pipeline in other regions, pull forward Q3 deals)

## Variance Reporting Template

### Monthly Variance Report Structure

1. **Executive Summary**: Top 3-5 variances with business impact in one paragraph
2. **P&L Variance Table**: Line-by-line actual vs. budget with dollar and percentage variance
3. **Variance Commentary**: For each material line item, explain the cause and expected trajectory
4. **Forecast Update**: Revised full-year outlook based on year-to-date performance
5. **Action Items**: Specific corrective actions with owners and deadlines

### Visualization Best Practices

- Use **waterfall charts** to show how individual variances bridge from budget to actual
- Use **traffic light indicators** (green/yellow/red) for quick scanning of line item health
- Show **trend lines** of monthly variance to identify whether gaps are widening or closing
- Include **rolling 3-month average** variance to smooth one-time items
