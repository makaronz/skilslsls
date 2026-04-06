# Wireframe Annotation & Documentation

Best practices for annotating wireframes, writing design specifications, preparing developer handoff documentation, and ensuring wireframe deliverables communicate design intent clearly.

---

## Why Annotations Matter

Wireframes without annotations are open to interpretation. Annotations bridge the gap between what a wireframe *shows* and what it *means*. They document:
- **Behavior** — What happens when a user interacts with an element
- **Content rules** — Character limits, dynamic content sources, fallbacks
- **Business logic** — Conditions, permissions, visibility rules
- **Technical requirements** — API dependencies, data sources, performance targets
- **Accessibility** — Focus order, screen reader behavior, ARIA roles

---

## Annotation Types

### 1. Interaction Annotations
Describe what happens when users interact with elements.

**Format:**
```
[Element] + [Trigger] → [Result]
```

**Examples:**
- "Search input + focus → Expand to full width, show recent searches dropdown"
- "Delete button + click → Show confirmation modal: 'Delete this item? This cannot be undone.'"
- "Card + hover → Elevate shadow, show quick-action buttons (Edit, Delete)"
- "Submit button + click (form valid) → Show loading spinner, POST to /api/submit"
- "Submit button + click (form invalid) → Highlight invalid fields, scroll to first error"

### 2. Content Annotations
Define content rules, limits, and dynamic behavior.

| Element | Content Rule |
|---------|-------------|
| Page title | Max 60 characters, sourced from CMS |
| Product description | Max 200 chars on card, full text on detail page |
| User avatar | Display initials if no image uploaded |
| Price | Format: $X,XXX.XX — show "Free" if $0 |
| Date | Display relative time if < 7 days, otherwise MM/DD/YYYY |
| Empty state | Show illustration + "No items yet" + CTA to create first |

### 3. Conditional Logic Annotations
Document visibility rules and state-dependent behavior.

**Format:**
```
IF [condition] THEN [display/behavior]
ELSE [alternative]
```

**Examples:**
```
IF user.role === "admin" THEN show "Settings" in navigation
ELSE hide "Settings" nav item

IF cart.items.length === 0 THEN show empty cart illustration
ELSE show cart items list with subtotal

IF subscription.status === "trial" THEN show upgrade banner
ELSE IF subscription.status === "expired" THEN show renewal modal
ELSE hide promotional elements
```

### 4. Technical Annotations
Specify data sources, API endpoints, and performance expectations.

```
Data Source: GET /api/v2/dashboard/metrics
Refresh: Auto-refresh every 60 seconds
Loading: Show skeleton screen while fetching
Error: Display "Unable to load data" with retry button
Cache: Cache for 5 minutes client-side
```

### 5. Accessibility Annotations
Document a11y requirements directly on wireframes.

| Element | Annotation |
|---------|------------|
| Navigation | Landmark: `<nav aria-label="Main navigation">` |
| Search | `role="search"`, auto-announce result count |
| Modal | Trap focus, return focus on close, `aria-modal="true"` |
| Icon button | `aria-label` required: "Close", "Delete", "Edit" |
| Tab order | Document custom tab order with numbered indicators |
| Skip link | "Skip to main content" link as first focusable element |
| Live region | Cart count update: `aria-live="polite"` |

---

## Annotation Placement Standards

### Numbering System
Use a numbered callout system to keep wireframes clean:

```
┌──────────────────────────────┐
│ [Logo] [Nav] [Search①] [②]  │
├──────────────────────────────┤
│                              │
│   ┌──────────────────┐       │
│   │  Hero Section ③  │       │
│   │  [CTA Button ④]  │       │
│   └──────────────────┘       │
│                              │
│   Product Grid ⑤             │
│   ┌────┐ ┌────┐ ┌────┐      │
│   │    │ │    │ │    │      │
│   └────┘ └────┘ └────┘      │
└──────────────────────────────┘

Annotations:
① Search: Expands on focus, shows autocomplete after 2 chars
② Profile: Shows dropdown with Account, Orders, Sign Out
③ Hero: Rotates 3 promotions, 5-second interval, pause on hover
④ CTA: Primary action, links to /signup, track click event
⑤ Grid: Loads 12 items initially, infinite scroll adds 12 more
```

### Placement Rules
1. **Never obscure the wireframe** — Annotations go outside or in a companion panel
2. **Use consistent callout style** — Numbered circles, colored pins, or lettered markers
3. **Group by type** — Separate interaction notes from content rules from tech specs
4. **Layer annotations** — Use toggleable layers in design tools for different audiences

---

## Documentation Deliverables

### Screen-Level Documentation

Each wireframed screen should include:

```markdown
## Screen: [Screen Name]

**Purpose:** [What this screen helps the user accomplish]
**Entry Points:** [How users arrive at this screen]
**Exit Points:** [Where users go from this screen]
**User Story:** As a [role], I want to [action] so that [benefit]

### Layout Notes
- [Grid structure, column layout]
- [Key spacing and hierarchy decisions]
- [Responsive behavior summary]

### Component Inventory
| Component | Variant | State(s) | Notes |
|-----------|---------|----------|-------|
| Header | Sticky | Default, Scrolled | Compact on scroll |
| Product Card | Grid | Default, Hover, Sold Out | 3-col desktop |
| Filter Panel | Sidebar | Open, Collapsed | Overlay on mobile |

### Interaction Notes
1. [Interaction annotation]
2. [Interaction annotation]

### Content Requirements
| Element | Source | Rules |
|---------|--------|-------|
| Title | CMS | Max 80 chars |
| Image | Upload | 16:9 ratio, fallback gradient |

### Edge Cases
- Empty state: [Description]
- Error state: [Description]
- Loading state: [Description]
- Permission denied: [Description]
```

### Flow-Level Documentation

Document how screens connect in a user flow:

```markdown
## Flow: [Flow Name]

**Goal:** [What the user is trying to accomplish]
**Screens:** [List of screens in this flow]
**Happy Path:** Screen A → Screen B → Screen C → Success
**Error Paths:**
- Form validation fails → Stay on Screen B, show inline errors
- Payment declined → Screen B with error banner, retry option
- Session expired → Redirect to login, return to Screen B after auth

### Decision Points
| Screen | Decision | Path A | Path B |
|--------|----------|--------|--------|
| Checkout | Has account? | Express checkout | Guest checkout form |
| Payment | Payment method | Credit card form | PayPal redirect |
```

---

## Developer Handoff Best Practices

### Specification Format

Structure specs so developers can find information quickly:

**Spacing & Layout:**
```
Page max-width: 1200px
Content padding: 24px (desktop), 16px (mobile)
Section spacing: 48px between sections
Card grid gap: 24px
Card padding: 16px
```

**Typography:**
```
H1: 32px / 40px line-height / Bold / Primary color
H2: 24px / 32px line-height / Semi-bold / Primary color
Body: 16px / 24px line-height / Regular / Secondary color
Caption: 12px / 16px line-height / Regular / Tertiary color
```

**Interactive States:**
```
Button - Default: bg-blue-600, text-white, rounded-8
Button - Hover: bg-blue-700, cursor-pointer
Button - Active: bg-blue-800, scale(0.98)
Button - Disabled: bg-gray-300, text-gray-500, cursor-not-allowed
Button - Loading: Show spinner, disable click, maintain width
```

### Handoff Checklist

- [ ] All screens annotated with interaction behavior
- [ ] Responsive breakpoints documented (mobile, tablet, desktop)
- [ ] Component states documented (default, hover, active, disabled, error, loading, empty)
- [ ] Content character limits and truncation rules specified
- [ ] Conditional visibility rules documented with logic
- [ ] Accessibility requirements annotated (focus order, ARIA labels, landmarks)
- [ ] Error states and validation rules defined
- [ ] Loading states and skeleton screens specified
- [ ] Animation and transition specs included (duration, easing)
- [ ] API data dependencies mapped to UI elements
- [ ] Design tokens referenced (not hardcoded values)
- [ ] Edge cases documented (long text, missing data, permissions)

---

## Annotation Tools & Techniques

### Figma Annotation Workflow
1. Create a dedicated "Annotations" page or layer group
2. Use sticky-note components with consistent styling
3. Color-code by type: blue (interaction), green (content), orange (technical), purple (a11y)
4. Use Figma's built-in commenting for discussion threads
5. Link annotations to specific components using connectors

### Annotation Component Library

Create reusable annotation components:

| Component | Color | Use For |
|-----------|-------|--------|
| Interaction Note | Blue | Click, hover, swipe behavior |
| Content Rule | Green | Character limits, dynamic content |
| Tech Spec | Orange | API endpoints, data sources |
| A11y Note | Purple | ARIA labels, focus order, landmarks |
| Conditional | Yellow | IF/THEN logic, permission rules |
| Question | Red | Unresolved design decisions |

### Documentation Platforms

| Platform | Best For | Features |
|----------|---------|----------|
| Figma (Dev Mode) | Integrated handoff | Auto-specs, code snippets, inspect |
| Zeroheight | Design system docs | Figma sync, live components |
| Notion | Team wiki | Flexible, embed Figma frames |
| Confluence | Enterprise teams | JIRA integration, approvals |
| Storybook | Component docs | Live code examples, visual tests |

---

## Version Control for Wireframes

### Naming Convention
```
[Project]-[Screen]-[Version]-[Status]
Example: AppName-Dashboard-v2.1-Review
```

**Status labels:**
- `Draft` — Work in progress, not ready for review
- `Review` — Ready for feedback
- `Approved` — Signed off, ready for development
- `Shipped` — Implemented in production

### Change Log Format
```markdown
## Wireframe Change Log

### v2.1 (2024-03-15)
- Added empty state for dashboard when no projects exist
- Revised navigation: moved Settings to profile dropdown
- Updated card layout from 4-column to 3-column grid

### v2.0 (2024-03-10)
- Major revision: Redesigned dashboard layout
- Added sidebar navigation (replaced top nav)
- New metric cards row above project grid

### v1.0 (2024-03-01)
- Initial wireframes for 8 core screens
- Basic navigation and page structure
```

---

## Common Documentation Mistakes

1. **Under-annotating** — Assuming developers will "figure it out" leads to misimplementation
2. **Over-annotating** — Documenting obvious behavior clutters the wireframe
3. **Stale documentation** — Annotations that don't match the current wireframe version
4. **Missing edge cases** — Only documenting the happy path leaves gaps in implementation
5. **No audience separation** — Mixing developer specs with stakeholder presentations
6. **Hardcoded values** — Using pixel values instead of design tokens
7. **Missing responsive notes** — Only documenting desktop behavior
8. **No interaction documentation** — Wireframes showing only static states

---

## Quality Checklist for Wireframe Documentation

- [ ] Every screen has a documented purpose and user story
- [ ] All interactive elements have behavior annotations
- [ ] Content rules are specified (limits, sources, fallbacks)
- [ ] Conditional logic is documented in IF/THEN format
- [ ] Responsive behavior is annotated for all breakpoints
- [ ] Accessibility requirements are explicitly called out
- [ ] Edge cases are documented (empty, error, loading, permission)
- [ ] Annotations use consistent formatting and terminology
- [ ] Version history is maintained with change descriptions
- [ ] Handoff checklist is completed before passing to development
