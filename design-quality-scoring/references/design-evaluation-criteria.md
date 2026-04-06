# Design Evaluation Criteria

Detailed evaluation dimensions, quality indicators, and assessment criteria for comprehensive design quality measurement.

---

## Visual Design Evaluation

### Color System Assessment

**Harmony and Coherence:**

| Criterion | Score 1–3 (Poor) | Score 4–6 (Adequate) | Score 7–8 (Good) | Score 9–10 (Excellent) |
|-----------|-----------------|---------------------|------------------|------------------------|
| Palette Cohesion | Random or clashing colors | Basic coordination but inconsistent application | Harmonious palette with minor inconsistencies | Perfectly coordinated with purposeful relationships |
| Semantic Usage | Colors used arbitrarily | Some semantic meaning but inconsistent | Consistent semantic colors with few exceptions | Every color choice communicates meaning clearly |
| Contrast Hierarchy | Flat, everything same weight | Some contrast differentiation | Clear visual layers through contrast | Masterful use of contrast to guide attention |
| Brand Alignment | No brand connection | Loosely related to brand | Clearly on-brand with minor deviations | Perfect brand expression through color |

**Technical Color Criteria:**
- Primary palette: 1 primary + 1–2 secondary + neutrals
- Accessibility: All text combinations meet WCAG AA (4.5:1 for normal, 3:1 for large)
- State colors: Distinct colors for success, warning, error, info
- Dark mode: Palette adapts correctly if dark mode is supported
- Consistency: Same color values used throughout (no one-off hex codes)

### Typography Assessment

**Typographic Quality Indicators:**

| Criterion | Measurement | Target | Scoring |
|-----------|-------------|--------|---------|
| Hierarchy Levels | Count distinct heading styles | 3–5 levels | < 3 = low, 3–5 = good, > 5 = excessive |
| Body Readability | Font size × line height | 16px+ at 1.5–1.7 | Deduct for < 16px or < 1.4 line height |
| Line Length | Characters per line | 60–75 chars | Deduct for < 45 or > 85 characters |
| Font Families | Count distinct families | 1–2 families | Deduct for 3+ families |
| Weight Usage | Distinct font weights used | 2–4 weights | Deduct for 1 (flat) or 5+ (chaotic) |
| Vertical Rhythm | Consistent baseline spacing | Multiples of base unit | Check heading, body, caption spacing alignment |

**Typography Scoring Rubric:**

```
10/10: Perfect hierarchy, rhythm, readability. Type alone tells the story.
 8/10: Strong hierarchy, minor rhythm inconsistencies.
 6/10: Readable but hierarchy unclear or rhythm broken.
 4/10: Hard to scan, poor hierarchy, inconsistent sizing.
 2/10: Barely readable, no typographic system evident.
```

### Layout and Composition

**Grid System Evaluation:**

| Criterion | What to Check | Scoring Guide |
|-----------|--------------|---------------|
| Grid Adherence | All elements align to defined grid | -1 for each off-grid element |
| Column Usage | Appropriate column spans for content | Content fits naturally within columns |
| Gutter Consistency | Same gutter width throughout | No gutter variations without justification |
| Margin Consistency | Page margins consistent across screens | Check all four sides on every screen |
| Responsive Grid | Grid adapts logically at breakpoints | 12→8→4 column progression or similar |

**Whitespace Assessment:**
- Breathing room around content groups
- Consistent padding within components
- Intentional spacing hierarchy (tight grouping → related, wide spacing → separate)
- No awkward gaps or cramped sections
- Whitespace serves visual hierarchy (more space = more importance)

---

## User Experience Evaluation

### Information Architecture Quality

| Criterion | Poor (1–3) | Adequate (4–6) | Good (7–8) | Excellent (9–10) |
|-----------|-----------|----------------|-----------|------------------|
| Navigation Structure | Confusing, items hard to find | Functional but not intuitive | Logical and learnable | Immediately intuitive, zero friction |
| Content Grouping | Random or illogical grouping | Basic grouping with some oddities | Logical groups with clear labels | Perfect mental model match |
| Label Clarity | Jargon, ambiguous labels | Mostly clear with few confusing items | Clear, consistent labeling | Self-explanatory, user-tested labels |
| Depth vs. Breadth | Too deep (many clicks) or too wide (overwhelming) | Slightly imbalanced | Well-balanced hierarchy | Optimal depth for user tasks |

### Interaction Design Quality

**Affordance Evaluation:**
- Clickable elements look clickable (buttons have button styling)
- Non-clickable elements don't look interactive
- Input fields clearly indicate editability
- Drag handles visually suggest draggability
- Links are distinguishable from regular text

**Feedback Quality:**

| Interaction | Expected Feedback | Timing | Scoring |
|-------------|-------------------|--------|---------|
| Button click | Visual state change + action result | < 100ms visual, < 1s result | -2 if no visual feedback |
| Form submit | Loading state → success/error message | Immediate loading indicator | -2 if no loading state |
| Data loading | Skeleton or spinner | Within 200ms of trigger | -1 if no loading indicator |
| Destructive action | Confirmation dialog or undo option | Before action executes | -3 if no confirmation |
| Error occurrence | Specific error message + recovery path | Immediately on detection | -2 if generic message only |

**State Completeness Matrix:**

For each interactive component, verify all states are designed:

| Component | Default | Hover | Active/Pressed | Focus | Disabled | Loading | Error | Empty | Success |
|-----------|---------|-------|---------------|-------|----------|---------|-------|-------|---------|
| Button | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ | — | — | — |
| Input Field | ✅ | ✅ | ✅ | ✅ | ✅ | — | ✅ | ✅ | ✅ |
| Card | ✅ | ✅ | ✅ | ✅ | — | ✅ | ✅ | ✅ | — |
| Dropdown | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ | — |
| Toggle | ✅ | ✅ | ✅ | ✅ | ✅ | — | — | — | — |

Score: Deduct 0.5 per missing critical state (hover, focus, error). Deduct 0.25 per missing non-critical state.

### Task Flow Evaluation

**Flow Efficiency Metrics:**

| Metric | Definition | Target | Scoring |
|--------|-----------|--------|---------|
| Steps to Complete | Number of user actions for primary task | Minimum viable steps | +1 per unnecessary step deducted |
| Decision Points | Moments user must choose | Minimize cognitive load | Each ambiguous decision -0.5 |
| Error Recovery Steps | Actions needed to recover from error | ≤ 2 steps | > 3 steps = -1 |
| Orientation Clarity | User always knows where they are | 100% of screens | Each unclear state -0.5 |

---

## Consistency Evaluation

### Design System Adherence

| Area | What to Check | Severity if Inconsistent |
|------|--------------|-------------------------|
| Component Variants | Same component looks identical across screens | High — breaks user trust |
| Spacing Scale | All spacing uses defined scale values | Medium — creates visual noise |
| Color Tokens | No one-off color values | Medium — undermines system |
| Typography Tokens | All text uses defined styles | Medium — creates confusion |
| Icon Style | All icons same style/weight/size grid | Low — subtle but cumulative |
| Border Radius | Consistent radius across component types | Low — feels unpolished |
| Shadow System | Consistent elevation scale | Low — affects polish perception |

### Pattern Consistency

Evaluate whether similar interactions are handled the same way:

- All modals open/close the same way
- All forms validate using the same pattern
- All lists/tables sort and filter consistently
- All empty states follow the same template
- All error messages use the same format
- Navigation patterns are identical across sections

**Consistency Score = (Consistent Patterns / Total Pattern Instances) × 10**

---

## Responsiveness Evaluation

### Breakpoint Quality Assessment

| Breakpoint | Screen Width | Key Criteria |
|------------|-------------|---------------|
| Mobile Small | 320–375px | Content fits, no horizontal scroll, readable text |
| Mobile Large | 376–428px | Touch targets 44px+, thumb-zone navigation |
| Tablet Portrait | 768px | Appropriate column count, not just stretched mobile |
| Tablet Landscape | 1024px | Utilizes horizontal space, not just padded tablet |
| Desktop | 1280–1440px | Full layout, optimal reading width |
| Large Desktop | 1920px+ | Content doesn't stretch uncomfortably |

**Responsive Scoring Criteria:**
- Each breakpoint should feel intentionally designed, not just reflowed
- Content priority should shift appropriately (hide less important items on mobile)
- Navigation should adapt (hamburger, tabs, sidebar based on context)
- Images and media should resize and crop appropriately
- Touch targets must increase on touch devices

---

## Accessibility Evaluation Criteria

### WCAG Compliance Scoring

| Level | Criteria Count | Must-Pass Items |
|-------|---------------|------------------|
| A (Minimum) | 30 criteria | All must pass for basic compliance |
| AA (Standard) | 20 additional | Required for most projects |
| AAA (Enhanced) | 28 additional | Aspirational, apply where feasible |

**Key Accessibility Scoring Items:**

| Criterion | Pass/Fail | Impact if Failed |
|-----------|----------|------------------|
| Text contrast ≥ 4.5:1 | Pass/Fail | High — affects readability |
| Focus indicators visible | Pass/Fail | High — keyboard users blocked |
| Form labels present | Pass/Fail | High — screen reader users blocked |
| Heading hierarchy logical | Pass/Fail | Medium — navigation difficulty |
| Touch targets ≥ 44px | Pass/Fail | Medium — mobile usability |
| Color not sole indicator | Pass/Fail | Medium — colorblind users affected |
| Reduced motion supported | Pass/Fail | Low — motion-sensitive users |

---

## Brand and Emotional Design

### Brand Expression Scoring

| Criterion | Evaluation Question | Scoring Guide |
|-----------|--------------------|--------------|
| Visual Identity | Does the design immediately feel like the brand? | Compare against brand guidelines |
| Tone of Voice | Does the copy match brand personality? | Review headlines, CTAs, error messages |
| Emotional Response | Does the design evoke the intended feeling? | Trust, excitement, calm, energy |
| Differentiation | Does it stand out from competitors? | Compare against 3 competitors |
| Memorability | Would users remember this design? | Identify distinctive elements |

### Delight and Polish Indicators

- Micro-interactions enhance understanding (not just decoration)
- Empty states are thoughtfully designed with helpful CTAs
- Loading experiences reduce perceived wait time
- Transitions are smooth and purposeful
- Unexpected touches that create positive moments
- Attention to edge cases shows care

---

## Cross-Dimensional Evaluation Matrix

Use this matrix for comprehensive evaluation across all criteria:

```markdown
## Evaluation Summary

| Dimension | Score | Confidence | Key Finding | Priority Fix |
|-----------|-------|------------|-------------|-------------|
| Visual Design | _/10 | High/Med/Low | [Observation] | [Action] |
| User Experience | _/10 | High/Med/Low | [Observation] | [Action] |
| Consistency | _/10 | High/Med/Low | [Observation] | [Action] |
| Responsiveness | _/10 | High/Med/Low | [Observation] | [Action] |
| Accessibility | _/10 | High/Med/Low | [Observation] | [Action] |
| Brand & Polish | _/10 | High/Med/Low | [Observation] | [Action] |

Weighted Score: _/10
Recommendation: [Ship / Iterate / Rework]
```
