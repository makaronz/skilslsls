# ETL Monitoring and Alerting

Strategies for monitoring data pipeline health, detecting failures, and configuring actionable alerts.

---

## Monitoring Dimensions

| Dimension | What to Monitor | Why It Matters |
|-----------|----------------|---------------|
| Freshness | When was the data last updated? | Stale data leads to incorrect decisions |
| Volume | How many rows were processed? | Unexpected drops/spikes indicate source issues or bugs |
| Quality | Do values pass validation rules? | Bad data propagates downstream and erodes trust |
| Performance | How long did the pipeline take? | SLA compliance, resource cost optimization |
| Cost | How much compute/storage was consumed? | Budget management, efficiency tracking |

## Pipeline Health Metrics

### Freshness Monitoring

Track the timestamp of the most recent record in each critical table:

```sql
SELECT MAX(updated_at) AS latest_record,
       CURRENT_TIMESTAMP - MAX(updated_at) AS data_lag
FROM fact_orders;
```

Set alerts when `data_lag` exceeds the expected refresh interval plus a buffer (e.g., if the pipeline runs hourly, alert at 90 minutes).

### Volume Monitoring

Compare current load volume against historical baselines:

```sql
WITH daily_counts AS (
    SELECT load_date, COUNT(*) AS row_count
    FROM fact_orders
    GROUP BY load_date
    ORDER BY load_date DESC
    LIMIT 30
)
SELECT load_date, row_count,
       AVG(row_count) OVER (ORDER BY load_date ROWS BETWEEN 7 PRECEDING AND 1 PRECEDING) AS rolling_avg,
       (row_count - AVG(row_count) OVER (ORDER BY load_date ROWS BETWEEN 7 PRECEDING AND 1 PRECEDING))
       / NULLIF(AVG(row_count) OVER (ORDER BY load_date ROWS BETWEEN 7 PRECEDING AND 1 PRECEDING), 0) * 100 AS pct_deviation
FROM daily_counts;
```

Alert when deviation exceeds ±30% from the rolling average.

### Quality Monitoring

Track data quality metrics per pipeline run:

| Metric | Calculation | Alert Threshold |
|--------|------------|----------------|
| Null rate per column | COUNT(NULLS) / COUNT(*) × 100 | > 5% for required fields |
| Duplicate rate | (COUNT(*) − COUNT(DISTINCT pk)) / COUNT(*) × 100 | > 0% for primary keys |
| Schema drift | Compare current schema to expected | Any unexpected column change |
| Referential integrity | Orphan FK count | > 0 orphan records |
| Value distribution | Standard deviation of key metrics | > 3σ from historical norm |

## Alerting Strategy

### Severity Levels

| Level | Criteria | Response Time | Notification Channel |
|-------|----------|--------------|---------------------|
| P1 — Critical | Pipeline failure affecting production dashboards or downstream systems | 15 minutes | PagerDuty + Slack + Email |
| P2 — High | Data quality violation above threshold, significant volume anomaly | 1 hour | Slack + Email |
| P3 — Medium | Performance degradation, minor volume deviation | 4 hours | Slack |
| P4 — Low | Informational (successful completion, cost report) | Next business day | Email digest |

### Alert Design Principles

1. **Actionable**: Every alert should have a clear owner and a runbook link explaining what to do
2. **Specific**: Include the table name, pipeline name, metric value, and threshold in the alert message
3. **Deduplicated**: Suppress repeated alerts for the same incident within a cooldown window
4. **Escalating**: If P2 is not acknowledged in 2 hours, auto-escalate to P1
5. **Low noise**: Tune thresholds to achieve < 5% false positive rate; review noisy alerts monthly

### Example Alert Message

```
🔴 P1 — Pipeline Failure: orders_daily_load
Status: FAILED at 2024-06-15 03:45 UTC
Error: Timeout waiting for source API response after 300s
Impact: fact_orders table stale (last update: 2024-06-14 03:30 UTC)
Runbook: https://wiki.internal/runbooks/orders-pipeline
Owner: @data-eng-oncall
```

## Observability Stack

| Component | Recommended Tools | Purpose |
|-----------|------------------|---------|
| Pipeline orchestration logs | Airflow UI, Dagster Dagit, Prefect Cloud | Task-level status, duration, logs |
| Data quality | Great Expectations, dbt tests, Monte Carlo | Validation results, anomaly detection |
| Infrastructure metrics | Datadog, Grafana + Prometheus | CPU, memory, query duration |
| Alerting | PagerDuty, Opsgenie, Slack webhooks | Incident management and routing |
| Cost tracking | Cloud billing dashboards, Kubecost | Compute and storage cost per pipeline |
