# Power BI Visualization Best Practices

Guidelines for designing effective, accessible, and performant Power BI reports and dashboards.

---

## Report Layout Design

### Page Layout Patterns

| Pattern | Structure | Best For |
|---------|-----------|---------|
| Executive Summary | KPI cards (top) → Primary chart (middle) → Detail table (bottom) | C-suite dashboards |
| Drill-Through | Overview page with navigation → Detail pages per topic | Complex data stories |
| Tab Navigation | Bookmarks or page navigator for topic switching | Multi-topic reports |
| Guided Analytics | Page 1: Question → Page 2: Filter → Page 3: Answer | Self-service analytics |

### Grid and Spacing

- Use a 12-column grid (Power BI snap-to-grid) for consistent alignment
- Maintain 8-16px padding between visuals
- Keep consistent margins on all four sides of the page
- Align visual tops and lefts — misalignment is the most common amateur mistake

## Visual Selection Guide

| Data Question | Recommended Visual | Avoid |
|--------------|-------------------|-------|
| How does a value trend over time? | Line chart | Pie chart |
| How do categories compare? | Bar chart (horizontal for many) | 3D chart |
| What proportion of the whole? | Stacked bar, treemap, donut | Pie chart (>5 slices) |
| What is the KPI status? | Card with conditional formatting | Gauge (low information density) |
| How are two variables related? | Scatter plot | Dual-axis line chart |
| What is the geographic distribution? | Map (filled or bubble) | Table of region names |
| What is the detailed breakdown? | Matrix with conditional formatting | Large ungrouped table |

## Formatting Standards

### Color

- Use a consistent color palette across the entire report (define in Theme JSON)
- Sequential palette (light to dark of one hue) for magnitude
- Diverging palette (red-white-blue) for variance from a target
- Reserve red for negative/alerts and green for positive — but add a secondary indicator (icon, text) for accessibility
- Maximum 7 colors per chart; use "Other" bucket for additional categories

### Typography

| Element | Font | Size | Weight |
|---------|------|------|--------|
| Report title | Segoe UI | 20-24pt | Bold |
| Section header | Segoe UI | 14-16pt | Semibold |
| Visual title | Segoe UI | 11-12pt | Semibold |
| Data labels | Segoe UI | 9-10pt | Regular |
| Axis labels | Segoe UI | 9-10pt | Regular |

### Conditional Formatting

Apply conditional formatting to:
- KPI cards (background color or font color based on target attainment)
- Matrix cells (color scale for heatmap effect)
- Table columns (data bars for quick visual comparison)
- Icon sets (traffic light icons for status indicators)

## Interactivity

### Cross-Filtering vs. Cross-Highlighting

| Mode | Behavior | When to Use |
|------|----------|-------------|
| Cross-Highlight (default) | Other visuals gray out non-selected data | When context is important |
| Cross-Filter | Other visuals remove non-selected data | When focus is important |
| None | No interaction between visuals | When visuals are independent topics |

Configure per visual: `Format > Edit interactions`.

### Bookmarks and Navigation

- Create bookmarks for different views of the same data (e.g., by region, by product)
- Add bookmark navigator buttons for tab-like navigation
- Use bookmarks with selection pane to show/hide visual groups
- Combine with buttons for a polished, app-like experience

### Drill-Through Pages

Design detail pages that users reach by right-clicking a data point:
1. Create a new report page
2. Add a drill-through filter (e.g., Product Name) to the Drill-through well
3. Design the detail page with visuals filtered to the drill-through context
4. Power BI automatically adds a Back button

## Performance Optimization

| Technique | Impact | Implementation |
|-----------|--------|---------------|
| Limit visuals per page | High | 8-12 max; each visual triggers a DAX query |
| Use Import mode | High | Prefer import over DirectQuery for most scenarios |
| Reduce table cardinality | High | Summarize in Power Query before loading |
| Avoid custom visuals with large data | Medium | Test custom visuals for performance before deploying |
| Use report-level filters | Medium | Filter early to reduce data processed by all visuals |
| Enable query reduction | Medium | File > Options > Query reduction > Add Apply button to slicers |

## Accessibility

- Add alt text to every visual (Visual > General > Alt Text)
- Ensure sufficient color contrast (4.5:1 ratio for text)
- Set tab order for keyboard navigation (View > Tab Order)
- Use descriptive visual titles that explain the chart's purpose
- Avoid relying on color alone to convey information — add icons, labels, or patterns
