# Dimensional Modeling Patterns

Star schema, snowflake schema, fact table types, and slowly changing dimension (SCD) implementations for data warehouse design.

---

## Schema Types

### Star Schema

The star schema is the foundation of dimensional modeling. A central fact table connects directly to denormalized dimension tables via foreign keys.

```
          dim_customer
              |
dim_date -- fact_sales -- dim_product
              |
          dim_store
```

**Advantages**: Simple queries with few joins, fast aggregation, intuitive for business users. **Tradeoffs**: Dimension redundancy increases storage (marginal with modern columnar storage).

### Snowflake Schema

Normalize dimension tables into sub-dimensions to reduce data redundancy:

```
dim_date -- fact_sales -- dim_product -- dim_category
                |                          |
            dim_store -- dim_region    dim_brand
```

**Use when**: Dimension tables are very large, storage cost is a concern, or upstream sources are already normalized and transformation budget is limited. **Tradeoff**: More joins slow query performance.

### Galaxy Schema (Fact Constellation)

Multiple fact tables share conformed dimensions. Common in enterprise warehouses:

```
dim_date -- fact_sales -- dim_product -- fact_inventory -- dim_warehouse
              |
          dim_customer -- fact_returns
```

## Fact Table Types

| Type | Grain | Example | Characteristics |
|------|-------|---------|----------------|
| Transaction | One row per event | Sale, click, payment | Most granular, largest volume |
| Periodic Snapshot | One row per entity per period | Monthly account balance | Regular intervals, aggregated |
| Accumulating Snapshot | One row per process instance | Order lifecycle (placed → shipped → delivered) | Multiple date columns, updated as process progresses |
| Factless Fact | Records events with no measures | Student enrolled in course | Useful for coverage and eligibility analysis |

### Additive, Semi-Additive, Non-Additive Measures

- **Additive**: Can be summed across all dimensions (revenue, quantity sold)
- **Semi-Additive**: Can be summed across some dimensions but not time (account balance — average or latest across time, sum across accounts)
- **Non-Additive**: Cannot be summed (ratios, percentages — store components and calculate in the query)

## Slowly Changing Dimensions (SCD)

| SCD Type | Strategy | History Preserved | Example |
|----------|----------|-------------------|---------|
| Type 0 | Retain original | No changes allowed | Date of birth |
| Type 1 | Overwrite | No | Fix a misspelled name |
| Type 2 | Add new row | Full history | Track customer address changes over time |
| Type 3 | Add new column | Limited (current + previous only) | Store previous and current region |
| Type 4 | History table | Full history in separate table | Mini-dimension for rapidly changing attributes |
| Type 6 | Hybrid (1+2+3) | Full history with current flag | Combines Type 2 rows with Type 1 current value column |

### SCD Type 2 Implementation

Add surrogate key, effective date range, and current flag:

| surrogate_key | natural_key | name | city | effective_start | effective_end | is_current |
|--------------|-------------|------|------|----------------|--------------|-----------|
| 1001 | C-100 | Jane Smith | Chicago | 2023-01-01 | 2024-06-30 | N |
| 1002 | C-100 | Jane Smith | Austin | 2024-07-01 | 9999-12-31 | Y |

Join fact tables to dimension using the surrogate key to get the attribute values as of the transaction date.

## Conformed Dimensions

Conformed dimensions are shared across multiple fact tables with identical keys, attributes, and values. Examples:
- **Date dimension**: Universal calendar with fiscal periods, holidays, and week numbering
- **Customer dimension**: Single customer master shared by sales, support, and marketing facts
- **Product dimension**: Consistent product hierarchy across sales, inventory, and returns

Building conformed dimensions is the most important architectural decision in a data warehouse — it enables cross-process analysis and consistent reporting.
