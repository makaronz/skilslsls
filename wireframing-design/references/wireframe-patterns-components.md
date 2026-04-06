# Wireframe Patterns & Components

Common wireframe patterns, reusable UI components, standard layouts, and structural building blocks for creating consistent, effective wireframes across web and mobile platforms.

---

## Navigation Patterns

Navigation is the skeleton of any wireframe. Choose patterns based on content depth, user tasks, and platform.

### Top Navigation Bar

```
┌──────────────────────────────────────────┐
│ [Logo]  Home  Products  About  Contact   │
└──────────────────────────────────────────┘
```

**When to use:** Marketing sites, corporate sites, simple web apps with fewer than 7 primary sections.

**Variants:**
- **Centered logo:** Logo in the middle with nav items split on both sides
- **Sticky header:** Fixed on scroll for persistent access
- **Collapsible:** Transforms to hamburger menu below tablet breakpoints

### Sidebar Navigation

```
┌────────┬───────────────────────────┐
│ Logo   │                           │
│        │                           │
│ ▸ Dash │      Content Area         │
│ ▸ Users│                           │
│ ▸ Data │                           │
│ ▸ Sett │                           │
└────────┴───────────────────────────┘
```

**When to use:** SaaS dashboards, admin panels, tools with deep navigation hierarchies, applications with 8+ sections.

**Variants:**
- **Collapsible sidebar:** Icon-only mode for more content space
- **Multi-level:** Expandable sub-menus for nested navigation
- **Mini + flyout:** Compact icons that expand on hover

### Tab Navigation

```
┌──────┬──────┬──────┬──────┐
│ Tab1 │ Tab2 │ Tab3 │ Tab4 │
├──────┴──────┴──────┴──────┤
│       Tab Content          │
└────────────────────────────┘
```

**When to use:** Content that can be categorized into parallel sections, settings pages, profile views.

**Rules:**
- Keep to 2–7 tabs maximum
- Active tab must be visually distinct
- Consider scrollable tabs on mobile

### Bottom Tab Bar (Mobile)

```
┌────────────────────────────┐
│                            │
│      Screen Content        │
│                            │
├──────┬──────┬──────┬──────┤
│ Home │ Srch │ Cart │ Prof │
└──────┴──────┴──────┴──────┘
```

**When to use:** Mobile apps with 3–5 primary destinations that users switch between frequently.

---

## Page Layout Patterns

### Single Column Layout

```
┌────────────────────────────┐
│          Header            │
├────────────────────────────┤
│                            │
│    Content (max-width)     │
│                            │
├────────────────────────────┤
│          Footer            │
└────────────────────────────┘
```

**Best for:** Blog posts, articles, focused reading experiences, mobile-first designs, onboarding flows.

**Content width:** 600–800px for readability (65–75 characters per line).

### Two-Column Layout (Content + Sidebar)

```
┌────────────────────────────────┐
│           Header               │
├────────────────────┬───────────┤
│                    │           │
│  Main Content      │  Sidebar  │
│  (2/3 width)       │  (1/3)    │
│                    │           │
├────────────────────┴───────────┤
│           Footer               │
└────────────────────────────────┘
```

**Best for:** Documentation, news sites, e-commerce product pages, dashboards with filters.

### Grid / Card Layout

```
┌────────────────────────────────────┐
│            Header                  │
├──────────┬──────────┬──────────────┤
│ ┌──────┐ │ ┌──────┐ │ ┌──────┐    │
│ │ Card │ │ │ Card │ │ │ Card │    │
│ │  1   │ │ │  2   │ │ │  3   │    │
│ └──────┘ │ └──────┘ │ └──────┘    │
│ ┌──────┐ │ ┌──────┐ │ ┌──────┐    │
│ │ Card │ │ │ Card │ │ │ Card │    │
│ │  4   │ │ │  5   │ │ │  6   │    │
│ └──────┘ │ └──────┘ │ └──────┘    │
└──────────┴──────────┴──────────────┘
```

**Best for:** Product listings, portfolios, image galleries, dashboard widgets, search results.

**Grid guidance:**
- Use 12-column grid for maximum flexibility
- Cards: 3-column on desktop, 2 on tablet, 1 on mobile
- Maintain consistent card aspect ratios within a grid

### Split Screen Layout

```
┌───────────────┬───────────────┐
│               │               │
│   Left Panel  │  Right Panel  │
│   (Image/     │  (Form/       │
│    Branding)  │   Content)    │
│               │               │
└───────────────┴───────────────┘
```

**Best for:** Login/signup pages, landing pages with strong imagery, comparison views, onboarding.

---

## Common UI Components

### Hero Section Variants

**Centered Hero:**
```
┌────────────────────────────────┐
│                                │
│       [Headline Text]          │
│    [Supporting description]    │
│      [Primary CTA Button]      │
│                                │
└────────────────────────────────┘
```

**Hero with Image:**
```
┌──────────────┬─────────────────┐
│ Headline     │                 │
│ Description  │   [Hero Image]  │
│ [CTA Button] │                 │
└──────────────┴─────────────────┘
```

### Card Component

Cards are the most versatile wireframe component. Standard card anatomy:

```
┌──────────────────────┐
│  [Image / Thumbnail] │  ← Media (optional)
├──────────────────────┤
│  Category Label      │  ← Metadata
│  Card Title          │  ← Primary content
│  Description text    │  ← Secondary content
│  that can wrap...    │
├──────────────────────┤
│  [Action] [Action]   │  ← Actions (optional)
└──────────────────────┘
```

**Card variants:**
| Variant | Use Case | Key Element |
|---------|----------|-------------|
| Product card | E-commerce | Price, rating, add-to-cart |
| Article card | Blog, news | Author, date, read time |
| Profile card | Social, team | Avatar, name, role |
| Stat card | Dashboard | Metric, trend, sparkline |
| Action card | Settings | Toggle, description |

### Form Patterns

**Single Column Form (Recommended):**
```
┌────────────────────────────┐
│  Form Title                │
│                            │
│  Label                     │
│  ┌──────────────────────┐  │
│  │ Input field           │  │
│  └──────────────────────┘  │
│  Helper text               │
│                            │
│  Label                     │
│  ┌──────────────────────┐  │
│  │ Input field           │  │
│  └──────────────────────┘  │
│                            │
│  ┌──────────────────────┐  │
│  │   Submit Button       │  │
│  └──────────────────────┘  │
└────────────────────────────┘
```

**Form best practices for wireframes:**
- One column performs better than multi-column (UX research)
- Group related fields with section headers
- Place labels above fields (not inline) for accessibility
- Show required vs optional indicators
- Position primary action button left-aligned or full-width on mobile

### Data Table Pattern

```
┌────────────────────────────────────────┐
│ [Search...]  [Filter ▾]  [+ Add New]   │
├──────┬──────────┬────────┬─────────────┤
│ ☐    │ Name ▾   │ Status │ Actions     │
├──────┼──────────┼────────┼─────────────┤
│ ☐    │ Item A   │ Active │ Edit Delete │
│ ☐    │ Item B   │ Draft  │ Edit Delete │
│ ☐    │ Item C   │ Active │ Edit Delete │
├──────┴──────────┴────────┴─────────────┤
│ Showing 1-3 of 24    [◀] 1 2 3 [▶]    │
└────────────────────────────────────────┘
```

**Include in wireframe:** Search, filters, sortable columns, bulk selection, pagination, row actions.

### Modal / Dialog Pattern

```
┌────────────────────────────────────┐
│  ░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░  │
│  ░░ ┌──────────────────────┐ ░░  │
│  ░░ │ Modal Title        ✕ │ ░░  │
│  ░░ ├──────────────────────┤ ░░  │
│  ░░ │                      │ ░░  │
│  ░░ │   Modal Content      │ ░░  │
│  ░░ │                      │ ░░  │
│  ░░ ├──────────────────────┤ ░░  │
│  ░░ │ [Cancel] [Confirm]   │ ░░  │
│  ░░ └──────────────────────┘ ░░  │
│  ░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░  │
└────────────────────────────────────┘
```

**Modal guidelines:**
- Maximum width: 600px (small), 900px (large)
- Always include a close mechanism (X button + clicking overlay)
- Destructive actions require explicit confirmation
- Avoid nested modals — use a drawer or new page instead

---

## Responsive Wireframe Considerations

When wireframing components, document how they adapt:

| Component | Desktop | Tablet | Mobile |
|-----------|---------|--------|--------|
| Nav | Full horizontal | Condensed + hamburger | Hamburger only |
| Grid | 3–4 columns | 2 columns | 1 column stacked |
| Sidebar | Visible | Collapsible | Hidden (overlay) |
| Table | Full columns | Scrollable | Card view |
| Hero | Side-by-side | Stacked | Stacked, smaller |
| Modal | Centered overlay | Centered overlay | Full-screen sheet |

---

## Component Naming Conventions

Consistent naming in wireframes prevents confusion during handoff:

| Element Type | Naming Pattern | Example |
|-------------|---------------|----------|
| Page | `[Feature] - [View]` | `Dashboard - Overview` |
| Component | `[Type] / [Variant]` | `Card / Product` |
| State | `[Component] - [State]` | `Button - Disabled` |
| Breakpoint | `[Page] - [Device]` | `Home - Mobile` |

---

## Pattern Selection Checklist

Before choosing a wireframe pattern, verify:
- [ ] Pattern supports the primary user task for this screen
- [ ] Pattern scales appropriately for expected content volume
- [ ] Pattern has an established responsive adaptation strategy
- [ ] Pattern aligns with platform conventions (web vs iOS vs Android)
- [ ] Pattern supports accessibility requirements (keyboard nav, screen readers)
- [ ] Pattern is documented in or compatible with the design system
