# Responsive Design Patterns & Techniques

Comprehensive guide to responsive design patterns, flexible images, CSS media queries, layout techniques, and adaptive component strategies for building interfaces that work across all screen sizes.

---

## Core Responsive Layout Patterns

### 1. Mostly Fluid

The most common responsive pattern. Uses a fluid grid that stacks on small screens and adds columns on larger screens with a max-width container.

```
Mobile (< 768px):        Tablet (768px+):        Desktop (1024px+):
┌────────────┐      ┌─────┬─────┐      ┌───┬───┬───┐
│     A      │      │  A  │  B  │      │ A │ B │ C │
├────────────┤      ├─────┼─────┤      ├───┴───┴───┤
│     B      │      │  C  │  D  │      │   D   │ E │
├────────────┤      ├─────┴─────┤      └───────┴───┘
│     C      │      │     E     │
├────────────┤      └───────────┘
│     D      │
├────────────┤
│     E      │
└────────────┘
```

**Best for:** Most websites, content-driven pages, marketing sites.

```css
.container {
  display: grid;
  grid-template-columns: 1fr;
  gap: 16px;
  max-width: 1200px;
  margin: 0 auto;
}

@media (min-width: 768px) {
  .container {
    grid-template-columns: repeat(2, 1fr);
  }
}

@media (min-width: 1024px) {
  .container {
    grid-template-columns: repeat(3, 1fr);
  }
}
```

### 2. Column Drop

Columns stack vertically as viewport narrows. Columns drop one at a time from right to left.

```
Desktop:              Tablet:              Mobile:
┌───┬───┬───┐      ┌─────┬─────┐      ┌────────┐
│ A │ B │ C │      │  A  │  B  │      │   A    │
│   │   │   │      ├─────┴─────┤      ├────────┤
│   │   │   │      │     C     │      │   B    │
└───┴───┴───┘      └───────────┘      ├────────┤
                                          │   C    │
                                          └────────┘
```

**Best for:** Dashboards, admin panels, content with sidebar.

### 3. Layout Shifter

The most responsive pattern — layout changes significantly at each breakpoint with content reordering.

```
Mobile:              Tablet:                 Desktop:
┌────────┐      ┌──────────────┐      ┌───┬──────────┐
│   A    │      │    A       B   │      │   │    A     │
├────────┤      ├──────────────┤      │ C ├──────────┤
│   B    │      │       C        │      │   │    B     │
├────────┤      └──────────────┘      └───┴──────────┘
│   C    │
└────────┘
```

**Best for:** Complex applications, marketing sites with creative layouts. Requires more CSS but offers maximum design flexibility.

### 4. Off-Canvas

Content lives off-screen and slides in on user action. Common for navigation and filters on mobile.

```
Mobile (closed):     Mobile (open):          Desktop:
┌────────┐      ┌────┬────────┐      ┌────┬─────────┐
│ [☰] Hdr │      │    │        │      │    │         │
├────────┤      │ Nav│ Content│      │ Nav│ Content │
│        │      │    │ (dimmed)│      │    │         │
│ Content│      │    │        │      │    │         │
│        │      └────┴────────┘      └────┴─────────┘
└────────┘
```

**Best for:** Apps with navigation drawers, filter panels, mobile-first experiences.

---

## Responsive Component Techniques

### Flexible Images

Images must never overflow their containers. Here are the essential techniques:

**Basic Responsive Image:**
```css
img {
  max-width: 100%;
  height: auto;
  display: block;
}
```

**Art Direction with `<picture>`:**
```html
<picture>
  <source media="(min-width: 1024px)" srcset="hero-wide.jpg">
  <source media="(min-width: 768px)" srcset="hero-medium.jpg">
  <img src="hero-mobile.jpg" alt="Hero image">
</picture>
```

**Resolution Switching with `srcset`:**
```html
<img 
  src="photo-400.jpg"
  srcset="photo-400.jpg 400w, photo-800.jpg 800w, photo-1200.jpg 1200w"
  sizes="(min-width: 1024px) 33vw, (min-width: 768px) 50vw, 100vw"
  alt="Responsive photo"
>
```

**Aspect Ratio Control:**
```css
.image-container {
  aspect-ratio: 16 / 9;
  overflow: hidden;
}

.image-container img {
  width: 100%;
  height: 100%;
  object-fit: cover;  /* Maintains aspect ratio, crops excess */
}
```

### Responsive Typography

**Fluid Type Scale:**
```css
/* Base: 16px at 320px viewport, 20px at 1200px viewport */
body {
  font-size: clamp(1rem, 0.909rem + 0.45vw, 1.25rem);
}

/* Heading scale */
h1 { font-size: clamp(2rem, 1.5rem + 2.5vw, 3.5rem); }
h2 { font-size: clamp(1.5rem, 1.2rem + 1.5vw, 2.5rem); }
h3 { font-size: clamp(1.25rem, 1.1rem + 0.75vw, 1.75rem); }
```

**Line Length Control:**
```css
/* Optimal line length: 45–75 characters */
.prose {
  max-width: 65ch;  /* ch = width of '0' character */
  margin: 0 auto;
}
```

### Responsive Navigation

| Pattern | Breakpoint Behavior | Best For |
|---------|--------------------|---------|
| **Hamburger menu** | Full nav → icon + drawer | Apps, complex navigation |
| **Priority+** | Hide overflow items in "More" dropdown | Content sites, medium nav |
| **Tab bar (bottom)** | Horizontal nav → fixed bottom bar | Mobile apps, 3–5 items |
| **Accordion** | Horizontal → expandable sections | Deep hierarchical nav |

### Responsive Tables

**Strategy 1: Horizontal Scroll**
```css
.table-wrapper {
  overflow-x: auto;
  -webkit-overflow-scrolling: touch;
}
```

**Strategy 2: Card Transformation**
```css
@media (max-width: 767px) {
  table, thead, tbody, tr, th, td {
    display: block;
  }
  
  thead { display: none; }
  
  td {
    position: relative;
    padding-left: 50%;
  }
  
  td::before {
    content: attr(data-label);
    position: absolute;
    left: 16px;
    font-weight: bold;
  }
}
```

**Strategy 3: Column Prioritization**
```css
@media (max-width: 767px) {
  .col-priority-low { display: none; }
}

@media (max-width: 479px) {
  .col-priority-medium { display: none; }
}
```

---

## CSS Media Query Techniques

### Media Query Types

```css
/* Viewport width (most common) */
@media (min-width: 768px) { }

/* Orientation */
@media (orientation: landscape) { }

/* Hover capability (touch vs mouse) */
@media (hover: hover) {
  .button:hover { background: blue; }
}

/* Pointer precision */
@media (pointer: coarse) {
  .button { min-height: 48px; }  /* Larger touch targets */
}

/* Reduced motion preference */
@media (prefers-reduced-motion: reduce) {
  * { animation-duration: 0.01ms !important; }
}

/* Dark mode preference */
@media (prefers-color-scheme: dark) {
  :root { --bg: #1a1a1a; --text: #f5f5f5; }
}

/* High contrast preference */
@media (forced-colors: active) {
  .button { border: 2px solid ButtonText; }
}

/* Print styles */
@media print {
  .no-print { display: none; }
  body { font-size: 12pt; }
}
```

### Range Syntax (Modern CSS)

```css
/* Modern range syntax (Level 4 Media Queries) */
@media (width >= 768px) { }
@media (768px <= width <= 1023px) { }
@media (width < 768px) { }
```

### Media Query Organization

**Option 1: Component-grouped (Recommended)**
```css
.header { /* base styles */ }
@media (min-width: 768px) { .header { /* tablet */ } }
@media (min-width: 1024px) { .header { /* desktop */ } }

.card { /* base styles */ }
@media (min-width: 768px) { .card { /* tablet */ } }
```

**Option 2: Breakpoint-grouped**
```css
/* All base styles */
.header { }
.card { }

/* All tablet styles */
@media (min-width: 768px) {
  .header { }
  .card { }
}
```

---

## Responsive Design Patterns for Common Elements

### Responsive Cards Grid

```css
.cards-grid {
  display: grid;
  grid-template-columns: repeat(auto-fill, minmax(280px, 1fr));
  gap: 24px;
}
```

This single declaration creates a responsive grid that:
- Shows 1 column on narrow screens
- Adds columns as space allows (minimum 280px per card)
- Distributes remaining space evenly
- Requires zero media queries

### Responsive Spacing System

```css
:root {
  --section-padding: clamp(2rem, 5vw, 6rem);
  --container-padding: clamp(1rem, 3vw, 3rem);
  --card-padding: clamp(1rem, 2vw, 2rem);
  --stack-gap: clamp(1.5rem, 3vw, 3rem);
}
```

### Responsive Video Embed

```css
.video-wrapper {
  aspect-ratio: 16 / 9;
  width: 100%;
}

.video-wrapper iframe {
  width: 100%;
  height: 100%;
}
```

---

## Performance Considerations

### Responsive Images Performance

| Technique | Benefit | When to Use |
|-----------|---------|------------|
| `srcset` + `sizes` | Serve right-sized images | All content images |
| `loading="lazy"` | Defer off-screen images | Below-the-fold images |
| `fetchpriority="high"` | Prioritize critical images | Hero images, LCP |
| WebP/AVIF with `<picture>` | Smaller file sizes | All images (with fallback) |
| CSS `content-visibility` | Skip rendering off-screen | Long pages with many sections |

### Critical CSS

Inline critical above-the-fold CSS and defer the rest:

```html
<head>
  <style>
    /* Critical CSS: above-the-fold layout and typography */
    .header { /* ... */ }
    .hero { /* ... */ }
  </style>
  <link rel="preload" href="styles.css" as="style" onload="this.rel='stylesheet'">
</head>
```

---

## Responsive Design Anti-Patterns

1. **Fixed-width elements** — Using `width: 500px` instead of `max-width` or percentages
2. **Device-specific breakpoints** — Targeting exact device widths instead of content needs
3. **Hiding content on mobile** — Using `display: none` excessively instead of redesigning
4. **Separate mobile site** — Building m.example.com instead of responsive design
5. **Ignoring touch** — Small click targets, hover-dependent interactions on mobile
6. **Viewport meta tag missing** — Must include `<meta name="viewport" content="width=device-width, initial-scale=1">`
7. **Horizontal overflow** — Elements breaking out of the viewport on mobile
8. **Unoptimized images** — Serving desktop-sized images to mobile devices

---

## Quick Reference: Responsive CSS Techniques

| Technique | CSS Property | Use Case |
|-----------|-------------|----------|
| Fluid widths | `width: 100%; max-width: 1200px` | Containers |
| Flexible images | `max-width: 100%; height: auto` | All images |
| CSS Grid auto-fill | `repeat(auto-fill, minmax(X, 1fr))` | Card grids |
| Flexbox wrap | `flex-wrap: wrap` | Inline elements |
| Clamp | `clamp(min, preferred, max)` | Typography, spacing |
| Aspect ratio | `aspect-ratio: 16/9` | Media containers |
| Container queries | `@container (min-width: X)` | Reusable components |
| Object fit | `object-fit: cover` | Image cropping |
| Viewport units | `vh, vw, dvh, svh` | Full-screen sections |
| Logical properties | `margin-inline, padding-block` | RTL-friendly spacing |
