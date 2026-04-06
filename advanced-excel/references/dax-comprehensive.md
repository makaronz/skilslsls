# DAX Comprehensive Reference

Deep reference for Data Analysis Expressions (DAX) used in Power Pivot, Power BI, and Analysis Services tabular models within Excel environments.

---

## DAX Evaluation Context

Understanding evaluation context is foundational to writing correct DAX. There are two contexts:

### Row Context

Row context exists when DAX iterates over a table row by row. It is created by:
- Calculated columns (each row evaluates independently)
- Iterator functions (`SUMX`, `AVERAGEX`, `FILTER`, `ADDCOLUMNS`)

Within row context, column references return the value for the current row.

### Filter Context

Filter context defines which rows are visible for aggregation. It is created by:
- Slicers and report filters
- Row and column headers in pivot tables
- `CALCULATE` function arguments

`CALCULATE` is the only function that can modify filter context. It converts row context to filter context through context transition.

## Essential DAX Patterns

### Time Intelligence

```dax
Year-to-Date Sales =
CALCULATE(
    SUM(Sales[Amount]),
    DATESYTD(Calendar[Date])
)

Same Period Last Year =
CALCULATE(
    SUM(Sales[Amount]),
    SAMEPERIODLASTYEAR(Calendar[Date])
)

Rolling 3-Month Average =
AVERAGEX(
    DATESINPERIOD(Calendar[Date], MAX(Calendar[Date]), -3, MONTH),
    CALCULATE(SUM(Sales[Amount]))
)
```

A proper date table is required: continuous dates, no gaps, with Year, Quarter, Month, and Day columns. Mark it as a date table in Power Pivot.

### Ranking and TopN

```dax
Product Rank =
RANKX(
    ALL(Products[ProductName]),
    [Total Sales],
    ,
    DESC,
    DENSE
)

Top 10 Flag =
IF([Product Rank] <= 10, "Top 10", "Other")
```

### Parent-Child Hierarchies

Flatten organizational or account hierarchies using `PATH`, `PATHITEM`, and `PATHLENGTH`:

```dax
OrgPath = PATH(Employee[EmployeeID], Employee[ManagerID])
Level1 = LOOKUPVALUE(Employee[Name], Employee[EmployeeID], PATHITEM(Employee[OrgPath], 1, INTEGER))
Depth = PATHLENGTH(Employee[OrgPath])
```

## Performance Optimization

| Technique | Impact | When to Apply |
|-----------|--------|---------------|
| Use `SUMMARIZE` over `VALUES` for grouping | Medium | Multi-column groupings |
| Replace `FILTER` with `KEEPFILTERS` | High | Large tables with many rows |
| Avoid nested `CALCULATE` | Medium | Complex measures |
| Use variables (`VAR`/`RETURN`) | High | Repeated sub-expressions |
| Prefer `DISTINCTCOUNT` over `COUNTROWS(DISTINCT())` | Low | Counting unique values |

### Variable Pattern

```dax
Profit Margin =
VAR TotalRevenue = SUM(Sales[Revenue])
VAR TotalCost = SUM(Sales[Cost])
RETURN
IF(TotalRevenue = 0, BLANK(), DIVIDE(TotalRevenue - TotalCost, TotalRevenue))
```

Variables are evaluated once and reused, improving both readability and performance.

## Common Pitfalls

- **Circular dependency**: A calculated column referencing a measure that filters the same table. Break the cycle by restructuring.
- **Context transition in iterators**: Using `CALCULATE` inside `SUMX` triggers context transition for every row — intentional when needed but expensive on large tables.
- **BLANK vs. zero**: DAX treats BLANK and zero differently in division and aggregation. Use `IF(ISBLANK(...))` to handle explicitly.
