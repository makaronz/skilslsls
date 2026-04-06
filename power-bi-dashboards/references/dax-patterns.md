# DAX Patterns for Power BI

Essential and advanced DAX patterns for building measures and calculated columns in Power BI dashboards.

---

## Foundational Patterns

### CALCULATE and Filter Modification

`CALCULATE` is the most important DAX function — it evaluates an expression in a modified filter context:

```dax
Online Sales = 
CALCULATE(
    SUM(Sales[Amount]),
    Sales[Channel] = "Online"
)

YTD Sales = 
CALCULATE(
    SUM(Sales[Amount]),
    DATESYTD(DateTable[Date])
)
```

### ALL, ALLEXCEPT, and REMOVEFILTERS

Control which filters are active:

```dax
// Percentage of total (ignore all filters on Product)
Product % of Total = 
DIVIDE(
    SUM(Sales[Amount]),
    CALCULATE(SUM(Sales[Amount]), ALL(Product))
)

// Percentage within category (keep Category filter, remove everything else)
% Within Category = 
DIVIDE(
    SUM(Sales[Amount]),
    CALCULATE(SUM(Sales[Amount]), ALLEXCEPT(Product, Product[Category]))
)
```

## Time Intelligence Patterns

### Period-over-Period Comparisons

```dax
PY Sales = 
CALCULATE(
    SUM(Sales[Amount]),
    SAMEPERIODLASTYEAR(DateTable[Date])
)

YoY Growth % = 
VAR CurrentPeriod = SUM(Sales[Amount])
VAR PriorPeriod = [PY Sales]
RETURN
DIVIDE(CurrentPeriod - PriorPeriod, PriorPeriod)

MoM Growth % = 
VAR CurrentMonth = SUM(Sales[Amount])
VAR PriorMonth = CALCULATE(SUM(Sales[Amount]), DATEADD(DateTable[Date], -1, MONTH))
RETURN
DIVIDE(CurrentMonth - PriorMonth, PriorMonth)
```

### Running Total

```dax
Running Total = 
CALCULATE(
    SUM(Sales[Amount]),
    FILTER(
        ALL(DateTable[Date]),
        DateTable[Date] <= MAX(DateTable[Date])
    )
)
```

### Moving Average

```dax
3-Month Moving Avg = 
AVERAGEX(
    DATESINPERIOD(DateTable[Date], MAX(DateTable[Date]), -3, MONTH),
    CALCULATE(SUM(Sales[Amount]))
)
```

## Advanced Patterns

### Dynamic Ranking

```dax
Product Rank = 
IF(
    HASONEVALUE(Product[ProductName]),
    RANKX(
        ALLSELECTED(Product[ProductName]),
        [Total Sales],
        ,
        DESC,
        DENSE
    )
)

// Top N with "Other" bucket
Top N Display = 
VAR CurrentRank = [Product Rank]
VAR TopN = SELECTEDVALUE(TopN_Parameter[Value], 10)
RETURN
IF(CurrentRank <= TopN, SELECTEDVALUE(Product[ProductName]), "Other")
```

### Switch Measure (Dynamic Metric Selection)

Allow users to switch between metrics using a slicer:

```dax
Selected Metric = 
SWITCH(
    SELECTEDVALUE(MetricSelector[Metric]),
    "Revenue", SUM(Sales[Amount]),
    "Units", SUM(Sales[Quantity]),
    "AOV", DIVIDE(SUM(Sales[Amount]), DISTINCTCOUNT(Sales[OrderID])),
    "Margin", DIVIDE(SUM(Sales[Amount]) - SUM(Sales[Cost]), SUM(Sales[Amount])),
    SUM(Sales[Amount])  // Default
)
```

### Semi-Additive Measures (Snapshots)

For measures like inventory balance that should not sum across time:

```dax
Latest Inventory = 
CALCULATE(
    SUM(Inventory[Quantity]),
    LASTDATE(DateTable[Date])
)

// Period-end balance
End of Month Balance = 
CALCULATE(
    SUM(Accounts[Balance]),
    LASTDATE(DateTable[Date])
)
```

## Performance Tips

| Tip | Description |
|-----|-------------|
| Use variables | Compute repeated expressions once with `VAR` / `RETURN` |
| Avoid `FILTER(table, ...)` on large tables | Use column-level filters in `CALCULATE` instead |
| Prefer `DIVIDE` over `/` | Handles division by zero gracefully |
| Minimize iterator functions | `SUMX` and `AVERAGEX` iterate row by row — expensive on large tables |
| Test with DAX Studio | Profile query performance and identify bottlenecks |

## Debugging DAX

| Issue | Diagnosis | Tool |
|-------|-----------|------|
| Unexpected blank | Filter context removes all rows | Add `HASONEVALUE` checks, inspect with DAX Studio |
| Wrong totals | Incorrect filter propagation | Check relationship direction, use `ALL` / `ALLEXCEPT` |
| Slow measure | Complex iterator or large table scan | Profile with Performance Analyzer, simplify expression |
| Circular dependency | Calculated column references measure that filters same table | Restructure to break the cycle |
