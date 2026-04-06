# Dashboard Design Guide

Create effective executive and operational dashboards that drive decision-making.

---

## Dashboard Types

| Type | Audience | Refresh Rate | Focus | Example |
|------|----------|-------------|-------|---------|
| Strategic | C-Suite, VP | Weekly/Monthly | KPI trends, goals | Revenue dashboard |
| Analytical | Analysts, Managers | Daily | Deep-dive, drill-down | Funnel analysis |
| Operational | Teams, Ops | Real-time/Hourly | Monitor, alert | System health |
| Tactical | Managers | Daily | Action items | Sales pipeline |

---

## Layout Framework

### The Inverted Pyramid

```
┌─────────────────────────────────────┐
│  KEY METRICS (3-5 KPI cards)        │  ← Glanceable summary
├──────────────────┬──────────────────┤
│  PRIMARY CHART   │  SECONDARY CHART │  ← Main story
├──────────────────┴──────────────────┤
│  SUPPORTING DETAILS / TABLES        │  ← Drill-down
└─────────────────────────────────────┘
```

### KPI Card Design

Each KPI card should include:
- **Metric name**: Clear, unambiguous label
- **Current value**: Large, prominent number
- **Trend indicator**: Arrow or sparkline showing direction
- **Comparison**: vs. previous period, target, or benchmark
- **Status color**: Green/yellow/red based on threshold

### Grid System
- Use 12-column grid for responsive layouts
- KPI cards: 2-4 columns each (3-6 cards per row)
- Charts: 6-12 columns depending on complexity
- Tables: Full width (12 columns)

---

## Executive Dashboard Best Practices

### Content Strategy
- **Maximum 5-7 KPIs** on a single view
- **One primary metric** that tells the main story
- **Comparison context**: Always show vs. target, previous period, or benchmark
- **Trend lines**: Show direction over 6-12 data points minimum
- **Filters**: Keep minimal (date range, segment, region)

### Storytelling Structure
1. **Headlines**: What happened? (KPI summary)
2. **Context**: Is this good or bad? (vs. targets/benchmarks)
3. **Drivers**: Why did it happen? (breakdown charts)
4. **Actions**: What should we do? (drill-down to details)

---

## Interactive Features

| Feature | Purpose | Best For |
|---------|---------|----------|
| Filters | Scope data | Date range, segment, region |
| Drill-down | Explore details | Click chart → detailed view |
| Tooltips | Additional info | Hover for exact values |
| Cross-filtering | Related insights | Click one chart filters others |
| Bookmarks | Save views | Analyst-specific configurations |
| Alerts | Proactive notification | Threshold breaches |

---

## Tool-Specific Implementation

### Tableau
- Use calculated fields for KPI logic
- Implement parameter actions for interactivity
- Use containers for responsive layout
- Optimize extract schedules for performance

### Power BI
- Use DAX measures for business logic
- Implement bookmarks for guided navigation
- Use row-level security for data access
- Configure scheduled refresh in Power BI Service

### Looker / Mode / Metabase
- Define metrics in semantic layer (LookML for Looker)
- Build reusable components
- Implement caching for performance
- Use embeddable dashboards for external sharing

---

## Performance Optimization

| Issue | Cause | Solution |
|-------|-------|----------|
| Slow loading | Too many queries | Pre-aggregate, use extracts |
| Sluggish filters | Full table scans | Index filter columns, use parameters |
| Timeout errors | Complex calculations | Simplify, move to data layer |
| Large data volume | No summarization | Aggregate before visualization |

---

## Dashboard Review Checklist

- [ ] Every metric has clear label, value, and context
- [ ] Colors are meaningful and consistent
- [ ] Layout follows reading order (top-left → bottom-right)
- [ ] Filters affect all relevant charts
- [ ] Mobile/tablet layout works (if required)
- [ ] Load time under 5 seconds
- [ ] Data refresh schedule documented
- [ ] Access permissions configured
- [ ] Annotations explain anomalies or one-time events
