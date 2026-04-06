# Dashboard Design Patterns

Principles and patterns for designing effective business intelligence dashboards that drive decision-making.

---

## Dashboard Types

| Type | Purpose | Audience | Refresh Rate | Interaction Level |
|------|---------|----------|-------------|------------------|
| Strategic | Track high-level KPIs and trends | Executives, board | Daily/Weekly | Low — view only |
| Analytical | Explore data to find insights | Analysts, managers | Near real-time | High — filters, drill-down |
| Operational | Monitor live processes and alerts | Operations teams | Real-time | Medium — alerts, actions |
| Tactical | Track team/department performance | Team leads | Daily | Medium — filters |

## Layout Patterns

### Inverted Pyramid

Place the most important information at the top and progressively add detail as users scroll down:
- **Row 1**: KPI summary cards (3-6 metrics)
- **Row 2**: Primary trend chart (full width)
- **Row 3**: Two comparison charts side by side
- **Row 4**: Detail table with drill-through capability

### Z-Pattern

Follow the natural eye movement pattern (top-left → top-right → bottom-left → bottom-right):
- **Top-left**: Most critical KPI or chart
- **Top-right**: Supporting context or trend
- **Bottom-left**: Secondary analysis
- **Bottom-right**: Detail or action items

## Visual Encoding Best Practices

### Chart Selection Guide

| Data Relationship | Recommended Chart | Avoid |
|------------------|-------------------|-------|
| Trend over time | Line chart | Pie chart |
| Part of whole | Stacked bar, treemap | 3D pie chart |
| Comparison | Bar chart (horizontal for many categories) | Radar chart for non-experts |
| Distribution | Histogram, box plot | Table of numbers |
| Correlation | Scatter plot | Dual-axis line chart |
| KPI status | Card with trend indicator | Gauge (low data density) |

### Color Usage

- Limit the palette to 5-7 colors maximum per dashboard
- Use sequential palettes (light to dark) for magnitude
- Use diverging palettes (red-white-green) for variance from a midpoint
- Reserve red for negative/alerts and green for positive/on-track
- Ensure accessibility: test with color blindness simulators and always include a non-color indicator (shape, label, pattern)

## Interactivity Design

### Filter Hierarchy

Organize filters from broad to specific:
1. **Global filters** (time period, business unit) — apply to all visuals
2. **Section filters** — apply to a group of related charts
3. **Visual-level filters** — apply to individual charts via click interaction

### Drill-Down Patterns

- **Drill-down**: Click a bar segment to see its components (Region → Country → City)
- **Drill-through**: Click a data point to navigate to a detailed sub-page
- **Cross-filter**: Clicking one chart filters all other charts on the page

### Tooltip Enrichment

Configure tooltips to show contextual detail on hover without cluttering the visual surface:
- Current value and comparison (vs. prior period, vs. target)
- Percentage of total
- Trend direction and magnitude

## Performance Guidelines

- **Limit visuals per page**: 8-12 maximum; each visual triggers a query
- **Pre-aggregate data**: Use summary tables rather than querying raw fact tables
- **Paginate detail tables**: Show 10-20 rows by default with scrolling or pagination
- **Lazy-load tabs**: Only query data for the visible tab; defer hidden tabs until selected
- **Cache results**: Enable dashboard caching for reports that refresh daily rather than live
