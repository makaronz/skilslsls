# Cloud Warehouse Comparison

Feature comparison of Snowflake, Amazon Redshift, Google BigQuery, and Azure Synapse Analytics.

---

## Architecture Comparison

| Feature | Snowflake | Redshift | BigQuery | Synapse Analytics |
|---------|-----------|----------|----------|-------------------|
| Architecture | Shared data, separate compute | Shared-nothing cluster | Serverless, slot-based | Dedicated SQL pool or serverless |
| Storage/Compute Separation | Yes (core design) | Yes (RA3 nodes) | Yes (native) | Yes (serverless mode) |
| Scaling | Instant (resize warehouse) | Minutes (add nodes) | Automatic (slots) | Minutes (scale DWU) |
| Concurrency | Multi-cluster auto-scale | WLM queues (limited) | 2,000 concurrent slots | Workload management |
| Storage Format | Proprietary columnar (micro-partitions) | Columnar (blocks) | Capacitor (proprietary columnar) | Columnar (CCI) |
| Pricing Model | Per-second compute + storage | Per-hour node + storage | Per-query (on-demand) or slots (flat-rate) | Per-DWU-hour + storage |

## Feature Comparison

### Data Loading

| Feature | Snowflake | Redshift | BigQuery | Synapse |
|---------|-----------|----------|----------|---------|
| Streaming ingest | Snowpipe (auto) | Kinesis Firehose | Storage Write API | Event Hubs |
| Batch loading | COPY INTO (S3, GCS, Azure) | COPY (S3) | Load jobs (GCS) | COPY/Polybase |
| Semi-structured data | VARIANT type (native JSON) | SUPER type | Native JSON, ARRAY, STRUCT | JSON support |
| Change data capture | Streams + Tasks | Manual | BigQuery CDC (preview) | Change tracking |

### Query Performance

| Feature | Snowflake | Redshift | BigQuery | Synapse |
|---------|-----------|----------|----------|---------|
| Auto-optimization | Auto-clustering, search optimization | Automatic tuning (ATO) | Automatic slot management | Adaptive query processing |
| Materialized views | Yes (auto-refresh) | Yes (auto-refresh) | Yes (auto-refresh) | Yes |
| Result caching | 24-hour cache (free) | Result cache | Cache on repeated queries | Result set caching |
| Query profiling | Query Profile (visual) | EXPLAIN + system tables | Execution Details | Query Store |

### Security and Governance

| Feature | Snowflake | Redshift | BigQuery | Synapse |
|---------|-----------|----------|----------|---------|
| Column-level security | Yes (masking policies) | Yes | Yes (policy tags) | Yes (dynamic data masking) |
| Row-level security | Yes (row access policies) | Yes | Yes (row-level security) | Yes |
| Data sharing | Secure Data Sharing (cross-account) | Data Sharing (RA3) | Analytics Hub | Data Share |
| Encryption | Always-on (AES-256), customer-managed keys | AES-256, KMS | Default encryption, CMEK | TDE, CMEK |

## Cost Optimization Strategies

### Snowflake
- Use auto-suspend on warehouses (default 5 min, reduce to 1 min for intermittent workloads)
- Right-size warehouses: start with X-Small, scale up only when query duration is unacceptable
- Separate warehouses for ETL and BI to avoid contention
- Use resource monitors to set credit spending alerts and limits

### Redshift
- Use Reserved Instances for predictable workloads (up to 75% savings)
- Enable Concurrency Scaling for burst workloads (1 hour free per 24 hours)
- Use Redshift Spectrum to query cold data in S3 without loading it
- Right-size clusters using Advisor recommendations

### BigQuery
- Use partitioned and clustered tables to reduce bytes scanned
- Monitor slot utilization and switch to flat-rate pricing when predictable
- Set up custom cost controls with project-level quotas
- Use BigQuery BI Engine for sub-second cached analytical queries

### Synapse
- Use serverless SQL pool for ad-hoc exploration (pay per TB scanned)
- Pause dedicated SQL pools during off-hours
- Use result set caching for repeated executive dashboard queries
- Leverage Synapse Link for real-time analytics on operational data without ETL

## Selection Guidance

- **Choose Snowflake** when you need multi-cloud flexibility, strong data sharing, and simplicity in scaling
- **Choose Redshift** when deeply invested in AWS and need tight integration with the AWS ecosystem
- **Choose BigQuery** when running on GCP, want serverless simplicity, or have unpredictable query patterns
- **Choose Synapse** when running on Azure and need tight integration with Power BI, Data Factory, and the Microsoft ecosystem
