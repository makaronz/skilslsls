# Data Mining Case Studies

Practical examples of data mining applications across industries, illustrating methodology, techniques, and business impact.

---

## Case Study 1: Customer Churn Prediction — Telecom

### Business Context

A telecom provider with 5 million subscribers experienced 2.5% monthly churn, costing approximately $15M per month in lost revenue. The goal was to identify at-risk customers 30 days before churn and trigger targeted retention offers.

### Data and Features

| Feature Category | Examples | Source |
|-----------------|----------|--------|
| Usage patterns | Call minutes, data usage, SMS count (30/60/90 day trends) | CDR system |
| Billing | Payment history, late payments, plan changes | Billing platform |
| Customer service | Ticket count, complaint topics, NPS score | CRM |
| Account | Tenure, contract type, device age | Customer database |
| Network quality | Dropped calls, coverage score at home location | Network ops |

### Methodology

1. **Data preparation**: Joined 12 tables, created 85 features, handled 8% missing data with median imputation
2. **Feature engineering**: Created trend features (usage change over 30/60/90 days), ratio features (complaints per month of tenure), and binary flags (any late payment in last 90 days)
3. **Model selection**: Compared Logistic Regression, Random Forest, and XGBoost on stratified 5-fold cross-validation
4. **Evaluation**: Optimized for recall at 80% precision (business requirement to limit wasted retention offers)

### Results

XGBoost achieved 0.87 AUC-ROC and 78% recall at 82% precision. Top predictive features were 30-day usage decline, complaint count in last 60 days, and months remaining on contract. Deploying the model with automated retention offers reduced monthly churn from 2.5% to 1.9%, saving approximately $3.6M per month.

## Case Study 2: Market Basket Analysis — Retail

### Business Context

A grocery chain wanted to optimize product placement, cross-promotions, and recommendation systems across 200 stores. Transaction data covered 18 months of purchases.

### Methodology

Applied the Apriori algorithm to discover frequent itemsets and association rules:

| Metric | Definition | Threshold |
|--------|-----------|-----------|
| Support | Proportion of transactions containing the itemset | ≥ 0.5% |
| Confidence | P(B|A) — probability of B given A is purchased | ≥ 30% |
| Lift | Confidence / P(B) — how much more likely B is given A | ≥ 1.5 |

### Key Findings

| Rule | Support | Confidence | Lift | Action Taken |
|------|---------|-----------|------|-------------|
| Chips → Salsa | 2.1% | 45% | 3.2 | Co-located in store layout |
| Baby Formula → Diapers | 1.8% | 62% | 4.1 | Bundle discount created |
| Pasta + Sauce → Parmesan | 1.2% | 38% | 2.8 | Cross-aisle end cap promotion |
| Coffee → Creamer → Filters | 0.9% | 41% | 3.5 | Coffee station bundle display |

### Impact

Store layout optimization based on association rules increased basket size by 8% in test stores. Cross-promotion campaigns generated 12% higher redemption rates compared to non-data-driven promotions.

## Case Study 3: Fraud Detection — Financial Services

### Business Context

A payment processor handled 50 million transactions daily and needed real-time fraud scoring with sub-100ms latency. The fraud rate was approximately 0.05% (highly imbalanced).

### Approach

1. **Feature engineering**: Created velocity features (transactions per hour per card), geographic features (distance from last transaction), merchant risk scores, and device fingerprinting signals
2. **Two-stage model**: Stage 1 (rules engine) filtered obvious fraud and obvious legitimate transactions. Stage 2 (ML model) scored the ambiguous middle tier.
3. **Model**: LightGBM trained on 6 months of labeled data with cost-sensitive learning (false negative cost = 50× false positive cost)
4. **Deployment**: Model served via low-latency inference API with feature store for real-time feature computation

### Results

The system achieved 92% fraud detection rate with a 0.3% false positive rate. Compared to the previous rules-only system, it caught 35% more fraud while reducing false declines by 40%. Annual fraud losses decreased by $12M.

## Lessons Learned Across Cases

- **Feature engineering drives performance**: In all three cases, engineered features (trends, ratios, velocities) outperformed raw features
- **Business constraints shape the model**: Precision-recall tradeoffs, latency requirements, and interpretability needs all influence algorithm choice
- **Monitoring is essential**: Models degrade as customer behavior and fraud patterns evolve — schedule quarterly retraining at minimum
- **Start with baselines**: Simple models (logistic regression, rule sets) establish benchmarks that justify the complexity of advanced methods
