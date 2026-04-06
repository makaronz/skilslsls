# Assistive Technology Considerations

Design considerations for screen readers, keyboard navigation, switch devices, voice control, and other assistive technologies.

---

## Assistive Technology Landscape

### Types of Assistive Technology

| Technology | Users | How It Works | Design Impact |
|-----------|-------|-------------|---------------|
| **Screen readers** | Blind and low-vision users | Reads page content aloud, navigates via keyboard shortcuts | Semantic structure, alt text, ARIA, focus management |
| **Screen magnifiers** | Low-vision users | Enlarges portions of the screen (2–16×) | Layouts must reflow, no fixed positioning traps |
| **Voice control** | Motor-impaired users, hands-free users | Operates UI via voice commands ("click Submit") | Visible labels must match accessible names |
| **Switch devices** | Severe motor impairments | Navigate with 1–2 switches (scan and select) | Simple focus order, large targets, minimal steps |
| **Eye tracking** | Severe motor impairments | Control cursor with eye movement | Large targets, dwell-click tolerance, rest areas |
| **Braille displays** | Blind and deafblind users | Converts text to braille in real-time | Semantic text, proper headings, no image-only text |
| **Alternative keyboards** | Motor impairments, one-handed use | Modified keyboard layouts, on-screen keyboards | Standard keyboard patterns, no complex key combos |
| **Head pointers / mouth sticks** | Motor impairments | Physical pointing device operated by head/mouth | Large targets, forgiving click areas |

### Usage Statistics and Priority

| Assistive Technology | Approximate Users | Testing Priority |
|---------------------|-------------------|------------------|
| Screen readers | ~7.5 million (US) | **Critical** — test with NVDA and VoiceOver |
| Screen magnifiers | ~6.5 million (US) | **High** — test at 200% and 400% zoom |
| Voice control | ~3 million (US, growing fast) | **High** — test label matching |
| Switch/scanning | ~500K (US) | **Medium** — ensure keyboard access covers this |
| Braille displays | ~100K (US) | **Medium** — semantic structure covers most needs |

---

## Screen Reader Design Considerations

### How Screen Readers Parse Content

Screen readers build an "accessibility tree" from the DOM:

```
Page Title
├─ Banner (header landmark)
│  ├─ Navigation: "Main Navigation"
│  │  ├─ Link: "Home"
│  │  ├─ Link: "Products" (current page)
│  │  └─ Link: "Contact"
│  └─ Search: "Search the site"
├─ Main Content
│  ├─ Heading Level 1: "Products"
│  ├─ Heading Level 2: "Featured"
│  │  ├─ Article: "Product A"
│  │  └─ Article: "Product B"
│  └─ Heading Level 2: "All Products"
└─ Footer (contentinfo landmark)
```

### Design Specifications for Screen Readers

**Heading Structure:**
- One H1 per page (page title)
- H2 for major sections
- H3–H6 for subsections (never skip levels)
- Headings must be descriptive (not "Section 1" but "Account Settings")

**Landmark Regions:**

| Landmark | HTML Element | Purpose | Design Consideration |
|----------|-------------|---------|---------------------|
| Banner | `<header>` | Site-wide header | One per page, contains logo + nav |
| Navigation | `<nav>` | Navigation groups | Label each nav ("Main", "Footer", "Breadcrumb") |
| Main | `<main>` | Primary content | One per page, skip-nav target |
| Complementary | `<aside>` | Related content | Sidebar, related links |
| Contentinfo | `<footer>` | Site-wide footer | One per page, contains legal + links |
| Search | `<search>` or role="search" | Search functionality | Label the search region |
| Form | `<form>` | Significant forms | Label with form purpose |

**Link and Button Design:**

| Pattern | Accessible Name Source | Design Requirement |
|---------|----------------------|--------------------|
| Text link | Link text content | Text must describe destination ("View pricing" not "Click here") |
| Image link | Alt text on image | Alt text describes destination |
| Icon button | aria-label | Specify label in design annotations |
| Button with icon + text | Text content | Icon can be aria-hidden |
| "Read more" links | aria-label or visually hidden text | "Read more about [topic]" for unique context |

**Live Regions for Dynamic Content:**

| Content Change | ARIA Live Setting | Urgency | Example |
|---------------|-------------------|---------|--------|
| Success message | aria-live="polite" | Low — read after current content | "Changes saved successfully" |
| Error alert | role="alert" (assertive) | High — interrupt immediately | "Payment failed. Check card details." |
| Loading status | aria-live="polite" + aria-busy | Low — informational | "Loading results..." |
| Chat message | aria-live="polite" | Medium — read when convenient | New message notification |
| Countdown timer | aria-live="off" (announce on request) | Varies | Avoid constant announcements |

---

## Screen Magnifier Considerations

### Design for Magnified Views

Screen magnifier users see only a small portion of the screen at 2–16× zoom. Design implications:

**Layout Requirements:**
- Content must reflow at 400% zoom (WCAG 1.4.10 — Level AA)
- No horizontal scrolling at 320px viewport width
- Information should not require seeing two distant areas simultaneously
- Related content must be spatially close (e.g., labels near inputs, errors near fields)

**Common Magnification Problems:**

| Problem | Why It's an Issue | Design Fix |
|---------|------------------|------------|
| Fixed position elements | Block content underneath when zoomed | Allow dismissal or make scrollable |
| Tooltips far from trigger | User can't see trigger and tooltip simultaneously | Position tooltips adjacent to trigger |
| Error messages at page top | User filling form at bottom can't see error summary | Inline errors next to each field |
| Multi-column layouts | Content split across magnified views | Single column at narrow viewports |
| Notification badges | Tiny indicators lost when zoomed elsewhere | Use text labels, not just badges |

**Reflow Testing:**
1. Set browser to 320px wide (or zoom to 400%)
2. Verify all content is accessible in single column
3. Confirm no horizontal scrollbar appears
4. Check that images scale or hide appropriately
5. Verify forms remain usable in narrow layout

---

## Voice Control Considerations

### How Voice Control Works

Voice control software (Dragon NaturallySpeaking, Voice Control on macOS/iOS, Voice Access on Android) allows users to:
- Say visible text to click elements ("Click Submit")
- Say numbers overlaid on interactive elements
- Dictate text input
- Navigate with voice commands ("scroll down", "go back")

### Design Requirements for Voice Control

**Label Matching Rule (WCAG 2.5.3 — Level A):**
The visible label of a control must match (or be contained within) its accessible name.

| Situation | Visible Label | Accessible Name | Voice Command | Works? |
|-----------|--------------|-----------------|---------------|--------|
| Correct | "Submit Order" | "Submit Order" | "Click Submit Order" | ✅ |
| Correct | "Submit" | "Submit Order" | "Click Submit" | ✅ (contained) |
| Incorrect | "Go" | "Submit Order" | "Click Go" | ❌ (no match) |
| Incorrect | "Submit" | "Send form data" | "Click Submit" | ❌ (not contained) |

**Design implications:**
- Don't override visible labels with different aria-labels
- Ensure icon buttons have aria-labels matching any visible tooltip
- Keep labels concise and unique — "Submit" on multiple buttons causes ambiguity

**Touch/Click Target Considerations:**
- Voice control click accuracy is lower than mouse — larger targets help
- Closely spaced interactive elements cause misclicks
- Minimum 8px spacing between adjacent interactive elements

---

## Switch Device and Scanning Considerations

### How Switch Access Works

Switch users navigate by scanning through interactive elements one at a time:
1. System highlights elements sequentially (auto-scan) or on switch press (manual scan)
2. User activates a switch when the desired element is highlighted
3. One switch: auto-scan + select. Two switches: next + select.

### Design for Switch Users

**Minimize interaction steps:**
- Every additional focusable element adds scanning time
- Group related actions to reduce scan distance
- Provide shortcuts for common actions
- Consider scan order carefully (most important actions first)

**Focus group design:**

| Pattern | Switch Experience | Design Recommendation |
|---------|------------------|----------------------|
| Long navigation menu | Must scan through every item | Collapsible nav, skip links |
| Grid of cards | Scans every card sequentially | Provide list/compact view option |
| Complex form | Scans every field and button | Minimize fields, logical grouping |
| Modal with 10 buttons | Must scan all options | Reduce options, most common first |

---

## Cognitive Accessibility Considerations

### Design Patterns for Cognitive Accessibility

| Principle | Implementation | Why It Matters |
|-----------|---------------|----------------|
| Clear language | Short sentences, common words, no jargon | Comprehension disabilities, non-native speakers |
| Consistent navigation | Same nav position and structure on every page | Reduces memory load, builds familiarity |
| Predictable behavior | Elements behave as expected, no surprises | Reduces anxiety, prevents confusion |
| Error prevention | Validate before submit, confirm destructive actions | Reduces cognitive load of error recovery |
| Progress indicators | Show step counts, progress bars, breadcrumbs | Reduces uncertainty and anxiety |
| Simple layouts | One primary action per screen, clear hierarchy | Reduces decision paralysis |
| Sufficient time | No auto-advancing carousels, adjustable timeouts | Processing speed varies widely |
| Multiple input modes | Don't rely solely on memory, recognition over recall | Supports different cognitive strengths |

### Cognitive Load Reduction Checklist

- [ ] Each page has one clear primary action
- [ ] Instructions are visible (not hidden behind tooltips)
- [ ] Forms show expected format before input
- [ ] Long processes broken into clearly labeled steps
- [ ] Important actions are undoable
- [ ] No time limits (or adjustable time limits)
- [ ] Content is chunked with clear headings
- [ ] Icons have text labels (not icon-only)
- [ ] Confirmation before irreversible actions
- [ ] Help is always available and in the same location

---

## Design Annotation Standards for Assistive Technology

### What to Annotate in Design Files

For designs to be implemented accessibly, annotate:

| Element | Annotation Needed | Example |
|---------|-------------------|--------|
| Images | Alt text specification | alt="Team meeting in progress" or alt="" (decorative) |
| Icon buttons | Accessible name | aria-label="Close dialog" |
| Headings | Heading level | H1, H2, H3 |
| Landmarks | Region type + label | nav aria-label="Main navigation" |
| Focus order | Tab sequence numbers | 1, 2, 3... across interactive elements |
| Live regions | Update behavior | "Announce as polite/assertive on change" |
| Custom widgets | Keyboard interaction | "Arrow keys to navigate, Enter to select" |
| Error messages | Association method | "Error linked to input via aria-describedby" |
| Skip links | Presence and target | "Skip to main content" → main region |
| Modal behavior | Focus management | "Trap focus, Esc to close, return to trigger" |

### Annotation Template

```markdown
## Accessibility Annotations: [Screen Name]

### Landmarks
- Header: <header> with site logo and main nav
- Main: <main> containing primary content
- Footer: <footer> with legal links

### Heading Hierarchy
- H1: "[Page Title]"
- H2: "[Section 1]" | H2: "[Section 2]"
- H3: "[Subsection]" under Section 1

### Focus Order
1. Skip to content link
2. Logo (home link)
3. Nav items (left to right)
4. Search input
5. Main content interactive elements (top to bottom)
6. Footer links

### Interactive Elements
| Element | Type | Accessible Name | Keyboard | Notes |
|---------|------|----------------|----------|-------|
| [Element] | Button | "[Name]" | Enter/Space | [Notes] |
| [Element] | Link | "[Name]" | Enter | [Notes] |

### Dynamic Content
| Trigger | Content Change | Announcement | Priority |
|---------|---------------|-------------|----------|
| Form submit | Success message | aria-live="polite" | After current |
| Validation | Error message | role="alert" | Immediate |
```
