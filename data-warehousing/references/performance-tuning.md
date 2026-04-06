# Performance Tuning

Indexing, partitioning, query optimization, and storage strategies for data warehouse performance.

---

## Partitioning Strategies

### Range Partitioning

Divide tables by a range of values, most commonly by date:

```sql
CREATE TABLE fact_sales (
    sale_id BIGINT,
    sale_date DATE,
    amount DECIMAL(12,2)
)
PARTITION BY RANGE (sale_date) (
    PARTITION p_2024_q1 VALUES LESS THAN ('2024-04-01'),
    PARTITION p_2024_q2 VALUES LESS THAN ('2024-07-01'),
    PARTITION p_2024_q3 VALUES LESS THAN ('2024-10-01'),
    PARTITION p_2024_q4 VALUES LESS THAN ('2025-01-01')
);
```

Benefits: Partition pruning eliminates scanning irrelevant time ranges. Partition-level operations (drop, archive) are instant compared to row-level deletes.

### Hash Partitioning

Distribute rows evenly across N partitions using a hash function on the partition key. Use for:
- Large dimension tables where no natural range exists
- Parallel query execution across partitions
- Even data distribution to prevent hot spots

### Clustering / Sort Keys

In columnar warehouses (Redshift, BigQuery, Snowflake), define cluster or sort keys to co-locate related rows:

| Warehouse | Feature | Syntax |
|-----------|---------|--------|
| Redshift | Sort Key | `SORTKEY (sale_date)` or `COMPOUND SORTKEY (region, sale_date)` |
| BigQuery | Clustering | `CLUSTER BY sale_date, region` |
| Snowflake | Clustering Key | `CLUSTER BY (sale_date, region)` |

Choose clustering columns based on the most common WHERE and JOIN predicates in analytical queries.

## Indexing Strategies

### Columnar Storage (Default in Modern Warehouses)

Modern cloud warehouses use columnar storage, which provides implicit indexing benefits:
- Only scanned columns are read from disk
- Column-level compression reduces I/O
- Zone maps / min-max metadata enable automatic block pruning

### Materialized Views

Pre-compute expensive aggregations and joins:

```sql
CREATE MATERIALIZED VIEW mv_daily_sales AS
SELECT sale_date, region, product_category,
       SUM(amount) as total_revenue,
       COUNT(*) as transaction_count
FROM fact_sales
JOIN dim_product USING (product_key)
GROUP BY sale_date, region, product_category;
```

Refresh strategies:
- **Full refresh**: Rebuild entirely — simple but slow for large views
- **Incremental refresh**: Update only changed data — faster but requires the warehouse to support it
- **Automatic refresh**: Let the warehouse decide when to refresh (Snowflake, BigQuery)

## Query Optimization

### Common Anti-Patterns

| Anti-Pattern | Problem | Solution |
|-------------|---------|----------|
| `SELECT *` | Reads all columns in columnar storage | Specify only needed columns |
| Functions on filter columns | Prevents partition pruning | `WHERE sale_date >= '2024-01-01'` instead of `WHERE YEAR(sale_date) = 2024` |
| Cross joins | Cartesian product explosion | Always join on explicit keys |
| Correlated subqueries | Executes once per row | Rewrite as JOIN or CTE |
| Excessive CTEs | Can prevent optimizer from pushing predicates | Flatten when performance suffers |

### Query Profiling

Use the warehouse's explain/profile tools:
- **Redshift**: `EXPLAIN` and `STL_QUERY_METRICS`
- **BigQuery**: Query Execution Details in the console
- **Snowflake**: Query Profile viewer (graphical execution plan)

Look for: full table scans, spilling to disk, skewed distribution, and unnecessary shuffles.

## Storage Optimization

### Data Lifecycle Management

| Data Age | Storage Tier | Access Pattern | Action |
|----------|-------------|---------------|--------|
| 0-3 months | Hot (SSD / standard) | Frequent queries | Full access, no compression changes |
| 3-12 months | Warm | Occasional queries | Move to cheaper storage tier |
| 1-3 years | Cold | Rare, ad-hoc | Archive to object storage (S3, GCS) |
| 3+ years | Archive | Compliance only | Deep archive, restore on request |

### Compression

- Let the warehouse auto-select compression encoding (Redshift ENCODE AUTO, Snowflake automatic)
- For manual tuning, use RLE for low-cardinality sorted columns, ZSTD for general purpose, and Delta for sequential integers
- Monitor compression ratios and recompress after major data loads if the ratio degrades
