# WCAG Compliance Standards

Comprehensive guide to WCAG 2.1 and 2.2 guidelines, conformance levels, and compliance strategies for design accessibility reviews.

---

## WCAG Overview and Structure

### What WCAG Covers

The Web Content Accessibility Guidelines (WCAG) are organized around four principles known as POUR:

| Principle | Meaning | Design Impact |
|-----------|---------|---------------|
| **Perceivable** | Information must be presentable in ways users can perceive | Text alternatives, captions, contrast, adaptable layouts |
| **Operable** | Interface components must be operable by all users | Keyboard access, timing, seizure prevention, navigation |
| **Understandable** | Information and operation must be understandable | Readable text, predictable behavior, input assistance |
| **Robust** | Content must be robust enough for diverse user agents | Semantic markup, parsing, assistive technology compatibility |

### Conformance Levels

| Level | Description | When Required | Typical Application |
|-------|-------------|--------------|---------------------|
| **A** | Minimum accessibility | Legal baseline in many jurisdictions | Removes the most severe barriers |
| **AA** | Standard accessibility | Required by ADA, Section 508, EN 301 549, EAA | Industry standard for web and apps |
| **AAA** | Enhanced accessibility | Not typically required site-wide | Applied selectively for maximum inclusion |

**Recommendation:** Target WCAG 2.1 AA as the minimum. Apply AAA criteria where feasible, especially for content-heavy pages.

### WCAG 2.1 vs 2.2 Differences

**WCAG 2.2 (October 2023) additions:**

| New Criterion | Level | What It Requires | Design Impact |
|---------------|-------|-----------------|---------------|
| 2.4.11 Focus Not Obscured (Minimum) | AA | Focused element is at least partially visible | Sticky headers/footers must not fully cover focused items |
| 2.4.12 Focus Not Obscured (Enhanced) | AAA | Focused element is fully visible | More aggressive scroll/layout behavior on focus |
| 2.4.13 Focus Appearance | AAA | Focus indicator meets size and contrast requirements | Minimum 2px outline with 3:1 contrast |
| 2.5.7 Dragging Movements | AA | Single-pointer alternative for drag operations | Provide buttons/menus as alternatives to drag |
| 2.5.8 Target Size (Minimum) | AA | 24×24px minimum target size (with exceptions) | Small icons and links need spacing or sizing |
| 3.2.6 Consistent Help | A | Help mechanisms are in consistent locations | Keep help links/chat in same position across pages |
| 3.3.7 Redundant Entry | A | Don't ask for same info twice in a process | Auto-fill repeated fields in multi-step forms |
| 3.3.8 Accessible Authentication (Minimum) | AA | No cognitive function tests for login | Allow paste in password fields, offer alternatives to CAPTCHA |
| 3.3.9 Accessible Authentication (Enhanced) | AAA | No object or image recognition for login | No image-based CAPTCHA at all |

**Removed in WCAG 2.2:** 4.1.1 Parsing (moved to non-normative note as browsers now handle parsing errors).

---

## Perceivable Requirements

### 1.1 Text Alternatives

| Content Type | Required Alternative | Design Specification |
|-------------|---------------------|---------------------|
| Informative images | Descriptive alt text | Include alt text in design annotations |
| Decorative images | Empty alt (alt="") | Mark as decorative in design spec |
| Complex images (charts, diagrams) | Long description | Provide text equivalent nearby or linked |
| Icon buttons | Accessible name | Specify aria-label in component design |
| Video content | Captions + audio description | Include caption track and description track |
| Audio content | Transcript | Provide text transcript |

### 1.3 Adaptable Content

**Information and Relationships (1.3.1 — Level A):**
- Visual hierarchy must map to semantic structure
- Headings that look like headings must be coded as headings
- Lists that look like lists must use list markup
- Tables must have header cells identified
- Form fields must have associated labels

**Meaningful Sequence (1.3.2 — Level A):**
- Reading order in design must match DOM/code order
- Multi-column layouts must have clear reading sequence
- CSS-reordered elements must maintain logical flow

**Orientation (1.3.4 — Level AA, WCAG 2.1):**
- Content must work in both portrait and landscape
- Don't lock orientation unless essential (e.g., piano app)

### 1.4 Distinguishable Content

**Color Contrast Requirements:**

| Text Type | AA Ratio | AAA Ratio | How to Verify |
|-----------|----------|-----------|---------------|
| Normal text (< 18px / < 14px bold) | 4.5:1 | 7:1 | WebAIM, Stark, Colour Contrast Analyser |
| Large text (≥ 18px / ≥ 14px bold) | 3:1 | 4.5:1 | Same tools, large text threshold |
| UI components and graphics | 3:1 | — | Borders, icons, form controls vs background |
| Focus indicators | 3:1 | — | Focus ring against adjacent colors |
| Placeholder text | 4.5:1 | 7:1 | Often fails — use visible labels instead |

**Non-Text Contrast (1.4.11 — Level AA, WCAG 2.1):**
UI components and meaningful graphics must have 3:1 contrast:
- Form field borders against background
- Icon buttons against surrounding area
- Chart lines/bars against background
- Custom checkboxes and radio buttons
- State indicators (active tabs, selected items)

**Text Spacing (1.4.12 — Level AA, WCAG 2.1):**
Content must remain readable when users override:
- Line height to 1.5× font size
- Paragraph spacing to 2× font size
- Letter spacing to 0.12× font size
- Word spacing to 0.16× font size

**Design implication:** Don't use fixed-height containers for text. Allow text to reflow.

**Content on Hover/Focus (1.4.13 — Level AA, WCAG 2.1):**
Tooltips and popovers triggered by hover/focus must be:
- Dismissible (Escape key closes without moving focus)
- Hoverable (user can move pointer over the tooltip)
- Persistent (stays visible until dismissed or trigger loses focus)

---

## Operable Requirements

### 2.1 Keyboard Accessible

**Keyboard Operation (2.1.1 — Level A):**
Every function must be operable via keyboard:

| Component | Expected Keyboard Behavior |
|-----------|---------------------------|
| Links | Enter to activate |
| Buttons | Enter or Space to activate |
| Checkboxes | Space to toggle |
| Radio buttons | Arrow keys to move between options |
| Tabs | Arrow keys between tabs, Tab to enter content |
| Dropdowns/menus | Arrow keys to navigate, Enter to select, Esc to close |
| Modals | Tab trapped inside, Esc to close, focus returned on close |
| Sliders | Arrow keys to adjust value |
| Drag and drop | Alternative keyboard mechanism required |

**No Keyboard Trap (2.1.2 — Level A):**
- Users must be able to navigate away from every component using keyboard
- Modals must allow Esc to close
- Custom widgets must not trap focus

### 2.4 Navigable

**Focus Order (2.4.3 — Level A):**
- Tab order matches visual layout order (left-to-right, top-to-bottom)
- Modals receive focus when opened
- Focus returns to trigger when modal closes
- Dynamically added content receives focus appropriately

**Focus Visible (2.4.7 — Level AA):**
- All focusable elements must have visible focus indicators
- Default browser focus rings should not be removed without replacement
- Custom focus styles: minimum 2px solid outline with 3:1 contrast against adjacent colors

**Design specification for focus states:**
```
Focus ring: 2px solid [brand-color]
Focus offset: 2px (space between element and ring)
Contrast: 3:1 against adjacent background
Consistent: Same style across all interactive elements
```

### 2.5 Input Modalities

**Target Size (2.5.5 — Level AAA / 2.5.8 — Level AA in WCAG 2.2):**

| Standard | Minimum Size | Exceptions |
|----------|-------------|------------|
| WCAG 2.2 AA (2.5.8) | 24×24px | Inline links, user-agent controls, essential sizing |
| WCAG 2.1 AAA (2.5.5) | 44×44px | Same exceptions |
| Apple HIG | 44×44pt | Recommended for iOS |
| Material Design | 48×48dp | Recommended for Android |

**Spacing alternative:** If a target is smaller than 24px, ensure 24px of non-overlapping spacing around it.

---

## Understandable Requirements

### 3.3 Input Assistance

**Error Identification (3.3.1 — Level A):**
- Errors must be identified in text (not color alone)
- Error messages must describe what went wrong
- Erroneous fields must be visually identified

**Labels or Instructions (3.3.2 — Level A):**
- Every input has a visible label (not just placeholder)
- Required fields are indicated
- Format requirements are stated before input (e.g., "MM/DD/YYYY")

**Error Suggestion (3.3.3 — Level AA):**
- Suggest corrections when possible ("Did you mean gmail.com?")
- Provide format examples alongside validation messages

**Error Prevention (3.3.4 — Level AA):**
For legal, financial, or data-modifying submissions:
- Reversible: submissions can be undone
- Checked: data is validated before submission
- Confirmed: user can review and confirm before final submission

---

## Compliance Verification Checklist

### Quick AA Compliance Check

**Perceivable:**
- [ ] All images have appropriate alt text
- [ ] Video has captions
- [ ] Text contrast ≥ 4.5:1 (normal) / 3:1 (large)
- [ ] UI component contrast ≥ 3:1
- [ ] Content works at 200% zoom
- [ ] Content adapts to portrait and landscape

**Operable:**
- [ ] All functionality available via keyboard
- [ ] No keyboard traps
- [ ] Focus order is logical
- [ ] Focus indicators are visible
- [ ] Target sizes ≥ 24×24px (WCAG 2.2)
- [ ] Timing can be adjusted or extended

**Understandable:**
- [ ] Page language is specified
- [ ] Navigation is consistent
- [ ] Error messages are descriptive
- [ ] Labels are present for all inputs
- [ ] Help is in consistent locations

**Robust:**
- [ ] Valid, semantic HTML structure
- [ ] ARIA used correctly where needed
- [ ] Status messages announced to assistive technology

---

## Legal and Regulatory Context

| Regulation | Region | WCAG Requirement | Key Deadline |
|-----------|--------|-----------------|-------------|
| ADA Title III | USA | WCAG 2.1 AA (DOJ 2024 rule) | April 2026 (state/local gov) |
| Section 508 | USA (federal) | WCAG 2.0 AA (updating to 2.1) | Currently enforced |
| EN 301 549 | EU | WCAG 2.1 AA | Currently enforced |
| European Accessibility Act | EU | WCAG 2.1 AA minimum | June 2025 |
| AODA | Ontario, Canada | WCAG 2.0 AA | Currently enforced |
| Equality Act 2010 | UK | WCAG 2.1 AA (public sector) | Currently enforced |

**Design team implication:** Accessibility is not optional — it is a legal requirement in most markets. Build WCAG AA compliance into the design process from the start, not as a retrofit.
