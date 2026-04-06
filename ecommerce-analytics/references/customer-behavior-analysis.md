# Customer Behavior Analysis

Techniques for understanding customer journeys, building cohort analyses, and modeling customer lifetime value.

---

## Cohort Analysis

### Building Acquisition Cohorts

Group customers by the month (or week) of their first purchase and track their behavior over subsequent periods:

| Cohort (Acquisition Month) | Month 0 | Month 1 | Month 2 | Month 3 | Month 6 | Month 12 |
|---------------------------|---------|---------|---------|---------|---------|----------|
| Jan 2024 (1,000 customers) | 100% | 28% | 22% | 18% | 12% | 8% |
| Feb 2024 (1,200 customers) | 100% | 31% | 25% | 20% | 14% | — |
| Mar 2024 (900 customers) | 100% | 25% | 19% | 16% | — | — |

**Reading the table**: 28% of Jan 2024 customers made another purchase in Month 1. If Feb 2024 shows higher retention, investigate what changed (new onboarding flow, seasonal effect, channel mix shift).

### Behavioral Cohorts

Group by behavior rather than acquisition date:
- **First purchase category**: Do electronics buyers retain differently from apparel buyers?
- **Acquisition channel**: Organic vs. paid vs. referral retention curves
- **First order value**: High AOV first-purchasers vs. low AOV — which cohort has higher CLV?
- **Device type**: Mobile vs. desktop first-purchase retention

## Customer Lifetime Value (CLV) Models

### Historical CLV

```
Historical CLV = Sum of all revenue from a customer to date
```

Simple but backward-looking. Useful for segmentation but does not predict future value.

### Predictive CLV — BG/NBD + Gamma-Gamma Model

The standard probabilistic approach for non-contractual, continuous purchase settings:

**BG/NBD Model** predicts future purchase frequency:
- Inputs: Recency (time since last purchase), Frequency (repeat purchase count), T (customer age)
- Output: Expected number of future transactions in a given period

**Gamma-Gamma Model** predicts average transaction value:
- Input: Historical average transaction value and frequency
- Output: Expected average transaction value

**Combined CLV**:
```
Predicted CLV = Expected Transactions × Expected Avg Value × Discount Factor
```

### RFM Segmentation

Score customers on three dimensions:

| Dimension | Score 5 (Best) | Score 1 (Worst) |
|-----------|---------------|-----------------|
| Recency | Purchased in last 7 days | No purchase in 180+ days |
| Frequency | 20+ purchases | 1 purchase |
| Monetary | Top 20% by revenue | Bottom 20% by revenue |

Combine scores into segments:

| RFM Segment | Scores | Strategy |
|------------|--------|----------|
| Champions | 5-5-5, 5-5-4 | Reward loyalty, request referrals |
| Loyal Customers | 4-4-4, 4-5-4 | Upsell premium products |
| At Risk | 2-3-3, 2-2-3 | Win-back campaign with personalized offer |
| Lost | 1-1-1, 1-1-2 | Low-cost reactivation or suppress from paid campaigns |

## Journey Analysis

### Path Analysis

Map the most common page sequences leading to conversion:

1. Extract session-level page sequences from analytics
2. Filter to sessions that resulted in a purchase
3. Identify the top 10 conversion paths
4. Compare with top 10 paths that did not convert
5. Look for friction points where converting and non-converting paths diverge

### Session Replay Analysis

Use tools like Hotjar, FullStory, or LogRocket to watch real user sessions. Focus on:
- Sessions where cart abandonment occurred — identify UI friction
- Sessions with rage clicks (rapid repeated clicks) — identify broken elements
- Sessions with high scroll depth but no conversion — identify interest without action

### Customer Journey Mapping

Create journey maps for key personas:

| Stage | Touchpoints | Customer Emotion | Metrics | Optimization |
|-------|------------|-----------------|---------|-------------|
| Awareness | Social ad, blog, referral | Curious | Impressions, CTR | Creative testing |
| Consideration | Product page, reviews, comparison | Evaluating | Time on page, add-to-cart rate | Social proof, content |
| Purchase | Cart, checkout, payment | Anxious | Cart abandonment, checkout completion | UX simplification, trust signals |
| Post-Purchase | Confirmation, shipping, delivery | Expectant | Delivery satisfaction, support tickets | Proactive communication |
| Retention | Email, loyalty program, reorder | Loyal or lapsed | Repeat rate, NPS, CLV | Personalized engagement |
