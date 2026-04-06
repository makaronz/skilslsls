# Analytics Tools Implementation

Guide to implementing and configuring e-commerce analytics tools for comprehensive tracking and reporting.

---

## Analytics Stack Architecture

```
Data Collection Layer
├── GA4 (web + app analytics)
├── Meta Pixel (ad attribution)
├── Server-Side GTM (reliable event delivery)
└── CDP (Segment / RudderStack)

Data Storage Layer
├── BigQuery / Snowflake (raw event data)
├── Data warehouse (transformed models)
└── Customer Data Platform (unified profiles)

Analysis Layer
├── Looker / Power BI (dashboards)
├── Amplitude / Mixpanel (product analytics)
└── Jupyter / dbt (ad-hoc analysis)
```

## Google Analytics 4 (GA4) Setup

### E-Commerce Event Implementation

Implement the full GA4 e-commerce event flow via Google Tag Manager:

| Event | Required Parameters | GTM Trigger |
|-------|-------------------|-------------|
| `view_item_list` | items[], item_list_name | Category page load |
| `select_item` | items[] | Product click from list |
| `view_item` | items[], value, currency | PDP load |
| `add_to_cart` | items[], value, currency | Add to cart button click |
| `remove_from_cart` | items[], value, currency | Remove from cart click |
| `begin_checkout` | items[], value, currency, coupon | Checkout page load |
| `add_shipping_info` | items[], shipping_tier | Shipping step completion |
| `add_payment_info` | items[], payment_type | Payment step completion |
| `purchase` | transaction_id, value, currency, tax, shipping, items[] | Order confirmation page |

### Data Layer Implementation

Push structured data to the GTM data layer on each page:

```javascript
window.dataLayer = window.dataLayer || [];
window.dataLayer.push({
  event: 'view_item',
  ecommerce: {
    currency: 'USD',
    value: 49.99,
    items: [{
      item_id: 'SKU-123',
      item_name: 'Premium Widget',
      item_category: 'Widgets',
      item_brand: 'Acme',
      price: 49.99,
      quantity: 1
    }]
  }
});
```

### Custom Dimensions and Metrics

Configure custom dimensions in GA4 for deeper segmentation:

| Custom Dimension | Scope | Example Values | Use Case |
|-----------------|-------|---------------|----------|
| Customer Type | User | new, returning, VIP | Segment reports by customer value |
| Subscription Status | User | free, trial, paid | Analyze behavior by subscription tier |
| Product Margin Tier | Item | high, medium, low | Weight conversion by profitability |
| Experiment Variant | Event | control, variant_a | Measure A/B test impact |

## Server-Side Tracking

### Why Server-Side

Client-side tracking is increasingly unreliable due to ad blockers (25-40% of users), ITP/ETP browser restrictions, and cookie limitations. Server-side tracking solves this by sending events from your server rather than the browser.

### Implementation with Server-Side GTM

1. Deploy a server-side GTM container on Cloud Run, App Engine, or a VM
2. Configure a transport URL pointing to your server container
3. Send events from the web container to the server container
4. The server container forwards events to GA4, Meta CAPI, and other endpoints

Benefits:
- First-party data collection (your domain, your cookies)
- Enrichment before sending to vendors (add customer tier, CLV)
- Reduced page weight (fewer third-party scripts)
- Better data quality and consistency

## Attribution Setup

### Multi-Touch Attribution Models

| Model | Logic | Best For |
|-------|-------|---------|
| Last Click | 100% credit to last touchpoint | Baseline, simple |
| First Click | 100% credit to first touchpoint | Brand awareness analysis |
| Linear | Equal credit across all touchpoints | Understanding full journey |
| Time Decay | More credit to recent touchpoints | Short sales cycles |
| Position-Based (U-shaped) | 40% first, 40% last, 20% middle | Balanced view |
| Data-Driven (GA4) | ML-based allocation | Most accurate (requires volume) |

Enable GA4's data-driven attribution model when you have sufficient conversion volume (typically 300+ conversions per month per conversion action). Fall back to position-based for lower volumes.
