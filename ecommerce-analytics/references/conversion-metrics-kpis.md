# Conversion Metrics & KPIs

Setting up KPI tracking, defining conversion events, and benchmarking e-commerce performance.

---

## Core Conversion Metrics

### Conversion Rate by Stage

| Stage | Metric | Formula | Benchmark (B2C) |
|-------|--------|---------|-----------------|
| Visit → Product View | Browse Rate | Product Page Views / Sessions × 100 | 40-60% |
| Product View → Add to Cart | Add-to-Cart Rate | Add to Cart Events / Product Page Views × 100 | 8-12% |
| Add to Cart → Checkout Start | Cart-to-Checkout Rate | Checkout Starts / Add to Cart Events × 100 | 45-65% |
| Checkout Start → Purchase | Checkout Completion Rate | Purchases / Checkout Starts × 100 | 40-60% |
| Visit → Purchase | Overall Conversion Rate | Purchases / Sessions × 100 | 1.5-3.5% |

### Revenue Metrics

| Metric | Formula | Benchmark | Optimization Lever |
|--------|---------|-----------|-------------------|
| Average Order Value (AOV) | Total Revenue / Number of Orders | $50-150 (varies by vertical) | Bundling, upsell, free shipping threshold |
| Revenue Per Visitor (RPV) | Total Revenue / Total Visitors | $1-5 (B2C) | Conversion rate × AOV |
| Revenue Per Email Sent | Email Revenue / Emails Sent | $0.05-0.15 | Segmentation, personalization |
| Customer Lifetime Value (CLV) | Avg Order Value × Purchase Frequency × Avg Lifespan | 3-5× CAC target | Retention, repeat purchase rate |
| Cart Abandonment Rate | (Carts Created − Purchases) / Carts Created × 100 | 65-75% | Checkout UX, trust signals, retargeting |

## KPI Tracking Setup

### Event Taxonomy

Define a consistent event naming convention:

| Event Name | Trigger | Required Properties |
|-----------|---------|-------------------|
| `page_view` | Any page loads | page_type, page_title |
| `product_viewed` | Product detail page loads | product_id, product_name, price, category |
| `product_added` | Add to cart click | product_id, quantity, price, cart_value |
| `checkout_started` | Checkout page loads | cart_value, item_count |
| `payment_info_added` | Payment details entered | payment_method |
| `order_completed` | Purchase confirmed | order_id, revenue, tax, shipping, items[] |
| `product_searched` | Search executed | search_term, results_count |

### GA4 E-Commerce Configuration

Enable Enhanced E-Commerce in GA4 by pushing the standard e-commerce events through the data layer:

```javascript
dataLayer.push({
  event: 'purchase',
  ecommerce: {
    transaction_id: 'T-12345',
    value: 125.00,
    currency: 'USD',
    items: [{
      item_id: 'SKU-001',
      item_name: 'Widget Pro',
      price: 125.00,
      quantity: 1
    }]
  }
});
```

## Benchmarking by Vertical

| Vertical | Conversion Rate | AOV | Cart Abandonment |
|----------|----------------|-----|-----------------|
| Fashion/Apparel | 1.5-2.5% | $80-120 | 70-75% |
| Electronics | 1.0-2.0% | $150-300 | 72-78% |
| Health & Beauty | 2.5-4.0% | $40-80 | 65-72% |
| Food & Grocery | 3.0-5.0% | $50-100 | 60-70% |
| Home & Garden | 1.5-2.5% | $100-200 | 68-75% |
| B2B / Wholesale | 2.0-3.5% | $200-1000+ | 75-85% |

## Reporting Cadence

| Report | Frequency | Audience | Key Metrics |
|--------|-----------|----------|-------------|
| Flash Report | Daily | Marketing, Ops | Revenue, sessions, conversion rate, AOV |
| Performance Review | Weekly | Growth team | Channel performance, funnel conversion, top products |
| Business Review | Monthly | Leadership | Revenue vs. plan, CLV trends, cohort retention |
| Strategic Review | Quarterly | Executive | YoY growth, market share, category performance |
