# Accessibility Testing Methods

Comprehensive guide to testing tools, manual testing procedures, automated testing strategies, and testing workflows for design accessibility.

---

## Testing Strategy Overview

### The Testing Pyramid for Accessibility

Effective accessibility testing combines automated, semi-automated, and manual methods:

| Testing Layer | Coverage | Catches | Effort | When to Use |
|---------------|----------|---------|--------|-------------|
| Automated scanning | ~30–40% of WCAG issues | Contrast failures, missing alt text, missing labels, heading structure | Low | Every build/commit |
| Semi-automated (guided) | ~20–30% of issues | Focus order, keyboard traps, ARIA usage, dynamic content | Medium | Sprint reviews, QA cycles |
| Manual expert review | ~20–30% of issues | Usability with AT, cognitive accessibility, flow logic | High | Milestone reviews, release candidates |
| User testing with disabilities | Remaining ~10–20% | Real-world usage barriers, AT compatibility, workflow issues | Highest | Pre-launch, major redesigns |

**Key insight:** Automated tools alone catch only 30–40% of accessibility issues. Manual testing is essential.

---

## Automated Testing Tools

### Design Phase Tools (Figma/Sketch Plugins)

| Tool | What It Tests | Integration | Cost |
|------|--------------|-------------|------|
| **Stark** | Color contrast, vision simulation, focus order | Figma, Sketch, Adobe XD | Free tier + paid |
| **A11y - Color Contrast Checker** | WCAG contrast ratios for text and UI | Figma plugin | Free |
| **Able** | Contrast checking with color blindness simulation | Figma plugin | Free |
| **Color Blind** | Simulates 8 types of color vision deficiency | Figma plugin | Free |
| **Axe for Designers** | Automated accessibility annotations | Figma plugin | Free |
| **Include** | Accessibility annotations and documentation | Figma plugin | Free |

**Design-phase testing workflow:**
1. Run contrast checker on all text/background combinations
2. Simulate color blindness on key screens
3. Annotate focus order on interactive screens
4. Verify touch target sizes with measurement tools
5. Document accessibility specifications in design handoff

### Development Phase Tools

| Tool | Type | What It Tests | Best For |
|------|------|--------------|----------|
| **axe DevTools** | Browser extension + CI | WCAG A/AA violations in rendered HTML | Comprehensive automated testing |
| **WAVE** | Browser extension + API | Visual overlay of accessibility issues | Quick visual identification |
| **Lighthouse** | Chrome DevTools + CI | Accessibility score + specific violations | Performance + accessibility combo |
| **Pa11y** | CLI + CI integration | WCAG 2.1 automated checks | Build pipeline integration |
| **jest-axe** | Unit test library | Component-level accessibility | React/Vue component testing |
| **cypress-axe** | E2E test library | Page-level accessibility in test flows | Integration testing |
| **IBM Equal Access** | Browser extension + CI | WCAG + IBM requirements | Enterprise compliance |

### Automated Testing Limitations

**What automated tools CAN detect:**
- Missing alt text on images
- Insufficient color contrast ratios
- Missing form labels
- Empty headings or broken heading hierarchy
- Missing page language attribute
- Duplicate IDs
- Missing ARIA attributes on dynamic content

**What automated tools CANNOT detect:**
- Whether alt text is meaningful and accurate
- Whether focus order is logical (only that elements are focusable)
- Whether ARIA roles are used correctly in context
- Whether content is understandable to real users
- Whether keyboard interactions follow expected patterns
- Whether screen reader announcements make sense
- Whether error messages are helpful
- Cognitive accessibility issues

---

## Manual Testing Procedures

### Keyboard Testing Protocol

**Equipment needed:** Physical keyboard (no screen reader running for initial keyboard test)

**Step-by-step keyboard test:**

1. **Start at the top of the page.** Press Tab.
2. **Track focus movement.** Does it go to the first interactive element? Is focus visible?
3. **Tab through every interactive element.** Note the order. Does it match visual layout?
4. **At each element, test interaction:**
   - Buttons: Press Enter and Space — both should activate
   - Links: Press Enter — should navigate
   - Checkboxes: Press Space — should toggle
   - Radio buttons: Use Arrow keys — should move between options
   - Dropdowns: Arrow keys to browse, Enter to select, Esc to close
   - Tabs: Arrow keys between tab headers
5. **Open a modal/dialog.** Is focus trapped inside? Does Esc close it? Does focus return?
6. **Skip navigation:** Is there a "Skip to content" link that appears on first Tab?
7. **Complete a full user task** using only keyboard. Note any blocking issues.

**Keyboard test report template:**

```markdown
| Page/Screen | Issue | Element | Expected Behavior | Actual Behavior | Severity |
|------------|-------|---------|-------------------|-----------------|----------|
| Home | Missing focus | Search icon | Visible focus ring | No visible indicator | High |
| Settings | Keyboard trap | Color picker | Esc to exit | Cannot exit with keyboard | Critical |
```

### Screen Reader Testing

**Recommended screen readers for testing:**

| Screen Reader | Platform | Browser | Market Share | Priority |
|---------------|----------|---------|-------------|----------|
| **NVDA** | Windows | Firefox, Chrome | ~40% (desktop) | Test first |
| **JAWS** | Windows | Chrome, Edge | ~30% (desktop) | Test second |
| **VoiceOver** | macOS/iOS | Safari | ~25% (mobile) | Test for Apple |
| **TalkBack** | Android | Chrome | ~5% (mobile) | Test for Android |

**Screen reader testing protocol:**

1. **Page load announcement:** What is announced when the page loads? Is the page title read?
2. **Landmark navigation:** Use screen reader landmarks to jump between regions (header, main, nav, footer). Are they present and labeled?
3. **Heading navigation:** Use heading navigation (H key in NVDA/JAWS). Is the hierarchy logical? Are headings descriptive?
4. **Image descriptions:** Navigate to images. Are alt texts meaningful? Are decorative images skipped?
5. **Form interaction:** Navigate to a form. Are labels announced for each field? Are required fields indicated? Are error messages announced?
6. **Dynamic content:** Trigger content changes (notifications, loading states, error messages). Are they announced via aria-live or equivalent?
7. **Table navigation:** If tables exist, navigate using table commands. Are headers announced for each cell?

### Color and Vision Testing

**Color contrast testing steps:**
1. Use a contrast checker tool on every text/background combination
2. Check interactive element boundaries against their backgrounds
3. Verify focus indicators against adjacent colors
4. Test disabled state text (often fails contrast)
5. Check placeholder text contrast (use visible labels instead when possible)

**Color blindness simulation testing:**

| Type | Prevalence | What It Affects | Test Focus |
|------|-----------|----------------|------------|
| Protanopia (no red) | 1% of males | Red/green distinction | Error states, success indicators |
| Deuteranopia (no green) | 1% of males | Red/green distinction | Status indicators, charts |
| Tritanopia (no blue) | 0.003% | Blue/yellow distinction | Link colors, highlights |
| Achromatopsia (no color) | 0.003% | All color distinction | Information conveyed by color alone |

**Simulation tools:** Stark (Figma), Color Oracle (desktop), Chrome DevTools (Rendering panel)

---

## Component-Level Testing Checklist

### Buttons
- [ ] Visible label or aria-label
- [ ] Keyboard operable (Enter + Space)
- [ ] Focus indicator visible (3:1 contrast)
- [ ] Disabled state communicated (aria-disabled)
- [ ] Loading state announced
- [ ] Icon-only buttons have accessible name

### Forms
- [ ] Every input has a visible label (not placeholder-only)
- [ ] Required fields indicated visually and programmatically
- [ ] Error messages associated with fields (aria-describedby)
- [ ] Error messages appear in text (not color alone)
- [ ] Autocomplete attributes present for personal data fields
- [ ] Form instructions appear before the form

### Navigation
- [ ] Current page/section indicated (aria-current)
- [ ] Skip navigation link present
- [ ] Navigation landmark (nav element) used
- [ ] Mobile menu accessible via keyboard
- [ ] Dropdown menus keyboard operable
- [ ] Breadcrumbs labeled (aria-label="Breadcrumb")

### Modals and Dialogs
- [ ] Focus moves to modal when opened
- [ ] Focus trapped inside modal
- [ ] Esc key closes modal
- [ ] Focus returns to trigger on close
- [ ] Modal has accessible name (aria-labelledby or aria-label)
- [ ] Background content inert (aria-hidden or inert attribute)

### Data Tables
- [ ] Table headers (th) defined for columns and/or rows
- [ ] Caption or aria-label describes the table
- [ ] Complex tables use scope or headers attributes
- [ ] Sortable columns indicate sort state (aria-sort)

### Notifications and Alerts
- [ ] Success/error messages use aria-live regions
- [ ] Toast notifications announced (role="alert" or aria-live="assertive")
- [ ] Status updates use aria-live="polite"
- [ ] Users have enough time to read messages

---

## Testing Workflow Integration

### Design Phase Testing

| Activity | Who | Tools | Output |
|----------|-----|-------|--------|
| Contrast check on color palette | Designer | Stark, A11y plugin | Annotated color system |
| Focus order annotation | Designer | Manual annotation | Focus flow diagrams |
| Touch target size audit | Designer | Measurement plugin | Size specifications |
| Vision simulation | Designer | Color Blind plugin | Simulation screenshots |
| Heading hierarchy review | Designer | Manual | Heading outline document |

### Development Phase Testing

| Activity | Who | Tools | Output |
|----------|-----|-------|--------|
| Automated scan per component | Developer | jest-axe, axe-core | Test results in CI |
| Keyboard test per page | QA / Developer | Physical keyboard | Keyboard test report |
| Screen reader spot-check | QA | NVDA or VoiceOver | Screen reader test report |
| Full automated scan per page | CI pipeline | Pa11y, Lighthouse | Automated report |

### Pre-Release Testing

| Activity | Who | Tools | Output |
|----------|-----|-------|--------|
| Full manual keyboard audit | QA specialist | Keyboard + checklist | Complete keyboard report |
| Full screen reader audit | Accessibility specialist | NVDA + JAWS + VoiceOver | AT compatibility report |
| Zoom and reflow testing | QA | Browser zoom 200%–400% | Zoom test report |
| User testing with disabilities | UX researcher | Participants with diverse disabilities | Usability findings report |

---

## Testing Documentation Templates

### Accessibility Test Report

```markdown
## Accessibility Test Report

Project: [Name]
Version: [X.X]
Date: [Date]
Tester: [Name]
Target: WCAG 2.1 AA

### Summary
- Issues found: [X total] ([X critical], [X major], [X minor])
- Pages tested: [X of Y]
- Automated score: [X/100] (Lighthouse)
- Manual test coverage: [Keyboard / Screen Reader / Color]

### Critical Issues (Must Fix Before Launch)
| # | Page | Issue | WCAG Criterion | Impact | Recommended Fix |
|---|------|-------|---------------|--------|----------------|
| 1 | [Page] | [Description] | [X.X.X] | [Users affected] | [Fix] |

### Major Issues (Fix Within Sprint)
| # | Page | Issue | WCAG Criterion | Impact | Recommended Fix |
|---|------|-------|---------------|--------|----------------|

### Minor Issues (Fix When Possible)
| # | Page | Issue | WCAG Criterion | Impact | Recommended Fix |
|---|------|-------|---------------|--------|----------------|

### Passed Criteria
[List WCAG criteria that passed verification]
```
