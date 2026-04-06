# Dashboard Examples

Practical examples and patterns for building professional Excel dashboards that communicate data insights effectively.

---

## Executive Summary Dashboard

The executive summary dashboard provides a high-level view of organizational KPIs on a single sheet. Structure it with a header row containing the reporting period, last-refresh timestamp, and navigation buttons.

### Layout Pattern

| Row | Section | Content |
|-----|---------|---------|
| 1-3 | Header | Company logo, title, date range selector |
| 4-8 | KPI Cards | 4-6 metric tiles with sparklines |
| 9-20 | Primary Chart | Revenue or pipeline trend chart |
| 21-30 | Secondary Charts | Two side-by-side charts (pie + bar) |
| 31-35 | Data Table | Top 10 detail rows with conditional formatting |

### KPI Card Design

Create each KPI card in a merged cell block (3 rows × 2 columns). Include:
- Metric name in small, muted font
- Current value in large, bold font
- Trend arrow (▲ or ▼) with conditional color (green/red)
- Sparkline in the bottom row using `SPARKLINE` or the built-in sparkline feature
- Period-over-period percentage change

Formula for trend arrow: `=IF(B2>B3,"▲","▼")` combined with conditional formatting rules that apply green fill when the value increases and red fill when it decreases.

## Sales Performance Dashboard

Design a sales dashboard with these interactive elements:

### Slicer Configuration

Use slicers connected to pivot tables for filtering by region, product line, sales rep, and quarter. Place slicers horizontally across the top of the dashboard. Set slicer styles to match the corporate color palette and configure multi-select behavior.

### Dynamic Charts

Create charts that respond to slicer selections by basing them on pivot table data. Key charts include:
- **Quota Attainment Gauge**: Use a doughnut chart with two series to simulate a gauge. The first series represents attainment percentage, the second fills the remainder.
- **Pipeline Waterfall**: Use a waterfall chart to show stage-by-stage pipeline progression from lead to close.
- **Rep Leaderboard**: Horizontal bar chart sorted descending by revenue, with target line overlay.

### Named Ranges for Dynamic Data

Define named ranges using `OFFSET` and `COUNTA` to create self-expanding data references:
```
=OFFSET(Sales!$A$1,0,0,COUNTA(Sales!$A:$A),6)
```

## Financial Reporting Dashboard

### Variance Analysis Layout

Build a financial dashboard showing actual vs. budget with variance columns. Use conditional formatting to highlight variances exceeding ±5% with red or green backgrounds. Structure the P&L with collapsible grouping rows for revenue categories, COGS, operating expenses, and net income.

### Rolling Forecast Section

Include a 12-month rolling view where historical months show actuals and future months show forecasts. Use a helper row with `=IF(MONTH(A1)<=MONTH(TODAY()),"Actual","Forecast")` to drive conditional formatting that visually distinguishes actual from projected data.

## Dashboard Best Practices

- **Color Palette**: Limit to 3-5 colors. Use one accent color for emphasis and neutral tones for structure.
- **Font Consistency**: Use a single sans-serif font family (Calibri or Segoe UI) with no more than three sizes.
- **Alignment**: Left-align text, right-align numbers, center headers.
- **White Space**: Leave empty rows and columns between sections for visual breathing room.
- **Print Area**: Define print areas and page breaks so dashboards print cleanly on A4 or Letter.
- **Protection**: Protect dashboard sheets while leaving slicer and input cells unlocked using `Review > Protect Sheet` with specific cell exceptions.
