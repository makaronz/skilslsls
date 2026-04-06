# Power BI Data Modeling Guide

Best practices for building performant, maintainable data models in Power BI using star schema design.

---

## Star Schema Design

### Why Star Schema

Power BI's DAX engine (VertiPaq) is optimized for star schema models. Benefits:
- **Performance**: Columnar compression is most effective with narrow, high-cardinality fact tables and wide, low-cardinality dimension tables
- **Simplicity**: Business users understand "facts and dimensions" intuitively
- **DAX correctness**: Filter context propagates predictably through star schema relationships

### Model Architecture

```
dim_Date ──────┐
dim_Customer ──┤
dim_Product ───┼── fact_Sales
dim_Store ─────┤
dim_Promotion ─┘
```

Rules:
- **One-to-many relationships** from dimension to fact (dimension side = "1", fact side = "*")
- **Single-direction filtering** from dimension to fact (default, most performant)
- **Avoid bi-directional filters** unless absolutely necessary — they create ambiguity and performance issues
- **No direct relationships between fact tables** — always go through shared (conformed) dimensions

## Date Table

Every Power BI model needs a dedicated date table:

```dax
DateTable = 
ADDCOLUMNS(
    CALENDAR(DATE(2020,1,1), DATE(2026,12,31)),
    "Year", YEAR([Date]),
    "Quarter", "Q" & QUARTER([Date]),
    "MonthNum", MONTH([Date]),
    "MonthName", FORMAT([Date], "MMMM"),
    "WeekNum", WEEKNUM([Date]),
    "DayOfWeek", FORMAT([Date], "dddd"),
    "IsWeekend", IF(WEEKDAY([Date],2) > 5, TRUE, FALSE),
    "FiscalYear", IF(MONTH([Date]) >= 7, YEAR([Date]) + 1, YEAR([Date])),
    "FiscalQuarter", "FQ" & SWITCH(TRUE(), MONTH([Date]) >= 7 && MONTH([Date]) <= 9, 1, MONTH([Date]) >= 10, 2, MONTH([Date]) <= 3, 3, 4)
)
```

Mark it as the date table: `Table Tools > Mark as Date Table`. This enables time intelligence functions like `SAMEPERIODLASTYEAR`, `DATESYTD`, etc.

## Relationship Best Practices

| Scenario | Approach | Rationale |
|----------|----------|-----------|
| Fact to dimension | One-to-many, single direction | Standard star schema |
| Role-playing dimension (e.g., OrderDate, ShipDate) | Create inactive relationships, use USERELATIONSHIP in measures | Avoids ambiguity |
| Many-to-many | Bridge table (factless fact) | Direct M:M relationships have unpredictable behavior |
| Self-referencing hierarchy | PATH functions in calculated columns | Flattens hierarchy for slicing |

### Role-Playing Dimensions Example

```dax
Ship Date Revenue = 
CALCULATE(
    SUM(fact_Sales[Revenue]),
    USERELATIONSHIP(fact_Sales[ShipDate], dim_Date[Date])
)
```

## Performance Optimization

### Reducing Model Size

| Technique | Impact | How |
|-----------|--------|-----|
| Remove unused columns | High | Delete columns not referenced in any visual, measure, or relationship |
| Reduce cardinality | High | Round timestamps to date, bucket continuous values |
| Disable Auto Date/Time | Medium | File > Options > Data Load > uncheck "Auto Date/Time" |
| Use integer keys | Medium | Replace text keys with integer surrogate keys |
| Summarize in Power Query | High | Pre-aggregate where detailed rows are not needed |

### Storage Modes

| Mode | Description | Best For |
|------|-------------|---------|
| Import | Data loaded into memory | Best performance, most common |
| DirectQuery | Queries sent to source at runtime | Real-time data, very large datasets |
| Dual | Imported when possible, DirectQuery when needed | Dimension tables in composite models |
| Composite | Mix of Import and DirectQuery | Large fact tables (DQ) with imported dimensions |

### Aggregation Tables

For large datasets, create pre-aggregated tables:
1. Build a summary table (e.g., daily totals by product and region) in Power Query
2. Set it as an aggregation table in the model
3. Power BI automatically routes queries to the aggregation when sufficient, and falls back to detail for drill-through

## Common Modeling Mistakes

| Mistake | Problem | Fix |
|---------|---------|-----|
| Single flat table | Poor performance, incorrect totals | Normalize into star schema |
| Bi-directional relationships everywhere | Ambiguous filter propagation, slow queries | Use single-direction; apply bi-directional only where needed in specific measures |
| Calculated columns for measures | Increases model size | Use DAX measures instead |
| Too many tables | Complex model, hard to maintain | Consolidate related tables |
