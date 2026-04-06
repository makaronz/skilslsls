# Data Visualization Best Practices

Select and design effective charts and graphs that communicate data insights clearly.

---

## Chart Selection Guide

| Data Relationship | Best Chart Types | Avoid |
|------------------|-----------------|-------|
| Comparison (few categories) | Bar chart, column chart | Pie chart with 7+ slices |
| Comparison (many categories) | Horizontal bar, lollipop | Cluttered column charts |
| Trend over time | Line chart, area chart | Bar chart for continuous time |
| Part-to-whole | Stacked bar, treemap, pie (≤5) | 3D pie charts |
| Distribution | Histogram, box plot, violin | Bar chart for continuous data |
| Correlation | Scatter plot, bubble chart | Line chart for non-sequential data |
| Geographic | Choropleth, dot map | Over-saturated color maps |
| Hierarchical | Treemap, sunburst | Nested pie charts |
| Flow/process | Sankey diagram, funnel | Complex network diagrams |

---

## Design Principles

### Color Usage

**Color Palettes by Purpose:**
| Purpose | Palette Type | Example |
|---------|-------------|---------|
| Categories | Qualitative | Distinct hues (blue, orange, green) |
| Sequential values | Sequential | Light to dark single hue |
| Diverging values | Diverging | Blue → white → red |
| Highlighting | Accent | Gray base + one accent color |
| Status/sentiment | Semantic | Red (bad), yellow (caution), green (good) |

**Color Rules:**
- Limit to 5-7 distinct colors per chart
- Ensure sufficient contrast for accessibility
- Use colorblind-safe palettes (avoid red-green only)
- Gray out non-essential elements to focus attention
- Maintain consistent color meaning across all charts

### Typography
- Title: 14-18pt, bold
- Subtitle/context: 12-14pt, regular
- Axis labels: 10-12pt
- Data labels: 9-11pt
- Use sans-serif fonts for screen display

### Layout and Composition
- Place the most important chart top-left (reading order)
- Align charts on a grid
- Maintain consistent spacing
- Remove unnecessary gridlines, borders, and backgrounds
- Use white space effectively

---

## Data-Ink Ratio

Maximize the proportion of ink devoted to data:

**Remove:**
- 3D effects and shadows
- Excessive gridlines
- Decorative elements
- Redundant labels
- Chart borders
- Background colors (unless meaningful)

**Keep:**
- Data points and lines
- Axis labels
- Clear titles
- Essential reference lines
- Annotations that add context

---

## Annotation Strategies

| Annotation Type | When to Use | Example |
|----------------|-------------|---------|
| Direct labels | Few data points | Label bars/points directly |
| Callout | Highlight anomaly | Arrow pointing to spike |
| Reference line | Benchmark/target | Horizontal line at target |
| Shaded region | Period/range | Gray band for recession |
| Text annotation | Context needed | "Product launch" at date |

---

## Accessibility Guidelines

- Provide text alternatives for all charts
- Use patterns or textures in addition to color
- Ensure minimum 4.5:1 contrast ratio for text
- Test with colorblind simulators
- Support screen reader descriptions
- Make interactive elements keyboard-navigable
- Provide data tables as alternatives to complex visualizations

---

## Common Mistakes

| Mistake | Problem | Fix |
|---------|---------|-----|
| Truncated y-axis | Exaggerates differences | Start at zero for bar charts |
| Dual y-axes | Misleading correlations | Use separate charts or index values |
| Too many colors | Visual overload | Highlight key series, gray others |
| Pie chart for comparison | Hard to compare angles | Use horizontal bar chart |
| Overloaded dashboard | Information overload | Curate, prioritize, paginate |
| Missing context | Numbers without meaning | Add benchmarks, comparisons, targets |
