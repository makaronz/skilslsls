# Advanced ETL Patterns

Complex extraction, transformation, and loading patterns for production data pipeline architectures.

---

## Change Data Capture (CDC)

### Log-Based CDC

Read database transaction logs to capture inserts, updates, and deletes in real time:

| Tool | Source Databases | Delivery | Latency |
|------|-----------------|----------|---------|
| Debezium | PostgreSQL, MySQL, MongoDB, SQL Server, Oracle | Kafka topics | Seconds |
| AWS DMS | All major RDBMS + NoSQL | Kinesis, S3, Redshift | Seconds-minutes |
| Fivetran | 150+ connectors | Warehouse direct | Minutes |
| Airbyte | 300+ connectors (open source) | Warehouse, lake | Minutes |

Log-based CDC avoids polling queries that add load to the source database. It captures the complete change stream including deletes, which query-based approaches often miss.

### Implementing CDC with Debezium

1. Deploy Debezium as a Kafka Connect connector
2. Configure the source connector to read the WAL (PostgreSQL) or binlog (MySQL)
3. Each table change produces a Kafka message with `before` and `after` states
4. Downstream consumers (Flink, Spark, or a warehouse loader) process the change events
5. Apply changes to the target using merge/upsert logic

## Slowly Changing Dimension (SCD) Loading

### SCD Type 2 Merge Pattern

```sql
MERGE INTO dim_customer AS target
USING staging_customer AS source
ON target.customer_id = source.customer_id AND target.is_current = TRUE

WHEN MATCHED AND (target.city <> source.city OR target.tier <> source.tier) THEN
    UPDATE SET is_current = FALSE, effective_end = CURRENT_DATE

WHEN NOT MATCHED THEN
    INSERT (customer_id, name, city, tier, effective_start, effective_end, is_current)
    VALUES (source.customer_id, source.name, source.city, source.tier, CURRENT_DATE, '9999-12-31', TRUE);

-- Insert new current row for changed records
INSERT INTO dim_customer (customer_id, name, city, tier, effective_start, effective_end, is_current)
SELECT s.customer_id, s.name, s.city, s.tier, CURRENT_DATE, '9999-12-31', TRUE
FROM staging_customer s
JOIN dim_customer d ON s.customer_id = d.customer_id
WHERE d.is_current = FALSE AND d.effective_end = CURRENT_DATE;
```

## Data Quality Patterns

### Validation Framework

Implement validation at each pipeline stage:

| Stage | Validation | Action on Failure |
|-------|-----------|------------------|
| Extract | Row count matches source, schema drift detection | Alert + halt |
| Transform | Null check on required fields, range validation, referential integrity | Quarantine bad rows |
| Load | Row count reconciliation, duplicate detection, freshness check | Alert + retry |

### Great Expectations Integration

Define expectations as code:

```python
expectation_suite = {
    "expectations": [
        {"type": "expect_column_values_to_not_be_null", "kwargs": {"column": "order_id"}},
        {"type": "expect_column_values_to_be_between", "kwargs": {"column": "amount", "min_value": 0, "max_value": 100000}},
        {"type": "expect_column_values_to_be_unique", "kwargs": {"column": "order_id"}},
        {"type": "expect_table_row_count_to_be_between", "kwargs": {"min_value": 1000, "max_value": 500000}}
    ]
}
```

## Idempotent Loading Patterns

### Partition Overwrite

Replace entire partitions on each run to ensure idempotency:

```sql
-- Delete existing data for the partition
DELETE FROM fact_orders WHERE order_date = '2024-01-15';

-- Insert fresh data
INSERT INTO fact_orders
SELECT * FROM staging_orders WHERE order_date = '2024-01-15';
```

### Merge/Upsert

For dimension tables or aggregation tables:

```sql
MERGE INTO target_table AS t
USING source_table AS s
ON t.primary_key = s.primary_key
WHEN MATCHED THEN UPDATE SET t.col1 = s.col1, t.col2 = s.col2
WHEN NOT MATCHED THEN INSERT (primary_key, col1, col2) VALUES (s.primary_key, s.col1, s.col2);
```

## Late-Arriving Data

Handle data that arrives after its partition has already been processed:

1. **Reprocess partition**: Re-run the pipeline for the affected partition (simple but expensive)
2. **Delta merge**: Apply late arrivals as incremental updates to the existing partition
3. **Bi-temporal modeling**: Track both event time and processing time to maintain an accurate historical record

## Pipeline Orchestration Patterns

| Pattern | Description | Use Case |
|---------|-------------|----------|
| Fan-out / Fan-in | Parallelize independent tasks, then converge | Processing multiple source tables, then building a combined fact |
| Sensor / Trigger | Wait for external event (file arrival, API signal) before starting | Dependency on upstream systems |
| Backfill | Re-process historical date ranges | Schema change, bug fix, new feature |
| Circuit Breaker | Halt pipeline if error rate exceeds threshold | Preventing bad data from propagating downstream |
