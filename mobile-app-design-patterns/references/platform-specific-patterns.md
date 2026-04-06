# Platform-Specific Design Patterns

Comprehensive guide to iOS and Android design guidelines, platform differences, Human Interface Guidelines (HIG) vs Material Design conventions, and strategies for designing apps that feel native on each platform.

---

## Platform Design Philosophy

### iOS (Human Interface Guidelines)

Apple's design philosophy emphasizes:
- **Clarity** — Text is legible, icons are precise, adornments are subtle and purposeful
- **Deference** — The UI helps users understand and interact with content without competing with it
- **Depth** — Visual layers and realistic motion convey hierarchy and facilitate understanding

### Android (Material Design 3)

Google's Material Design philosophy emphasizes:
- **Material as metaphor** — A unified theory of a rationalized space and motion system
- **Bold, graphic, intentional** — Typography, grids, color, and imagery guide design decisions
- **Motion provides meaning** — Subtle, appropriate animation aids focus and maintains spatial relationships
- **Personal** — Dynamic color and customization through Material You

---

## Navigation Patterns

### Tab Bar / Bottom Navigation

| Aspect | iOS | Android |
|--------|-----|----------|
| **Name** | Tab Bar | Bottom Navigation / Navigation Bar |
| **Position** | Bottom of screen | Bottom of screen |
| **Max items** | 5 (recommended) | 3–5 (required) |
| **Labels** | Always visible with icons | Always visible with icons |
| **Active indicator** | Tinted icon + label | Pill-shaped indicator behind icon |
| **Scrollable** | No | No |
| **Badge style** | Red circle with count | Small dot or number |
| **More tab** | "More" tab for overflow | Avoid; use navigation drawer |

**iOS Tab Bar:**
```
┌──────┬──────┬──────┬──────┬──────┐
│ ○    │ ○    │ ●    │ ○    │ ○    │
│ Home │ Srch │ Feed │ Notif│ Prof │
└──────┴──────┴──────┴──────┴──────┘
```

**Android Bottom Navigation:**
```
┌────────┬────────┬────────┬────────┐
│  ○    │ [─●─] │  ○    │  ○    │
│  Home  │  Feed  │  Chat  │ Profile│
└────────┴────────┴────────┴────────┘
        ▲ Pill indicator (M3 style)
```

### Navigation Stack / Back Navigation

| Aspect | iOS | Android |
|--------|-----|----------|
| **Back button** | "< Back" text button (top-left) | ← Arrow icon (top-left) |
| **System back** | Edge swipe from left | System back gesture or button |
| **Navigation bar** | Large title collapses on scroll | Top app bar with title |
| **Title alignment** | Center-aligned (default) | Left-aligned (default) |
| **Action items** | Right side of nav bar | Right side, icon-only |

### Drawer / Side Navigation

| Aspect | iOS | Android |
|--------|-----|----------|
| **Usage** | Rarely used; prefer tab bar | Common for 6+ destinations |
| **Opening** | No standard gesture | Swipe from left edge, or hamburger icon |
| **Style** | Full-screen takeover | Overlay drawer with scrim |
| **Recommendation** | Avoid on iOS | Use for complex navigation hierarchies |

---

## Core UI Components

### Action Sheets / Bottom Sheets

| Aspect | iOS | Android |
|--------|-----|----------|
| **Name** | Action Sheet | Bottom Sheet |
| **Trigger** | Contextual actions, share | Contextual actions, details |
| **Dismiss** | Tap cancel or outside | Swipe down or tap scrim |
| **Height** | Fixed (content height) | Expandable (peek, half, full) |
| **Drag indicator** | Not shown | Shown at top center |
| **Cancel button** | Explicit cancel action | Implicit (swipe/tap scrim) |

**iOS Action Sheet:**
```
┌────────────────────────┐
│  Share Photo             │
│  Save to Album           │
│  Copy Link               │
│────────────────────────┤
│  Delete (destructive/red)│
├────────────────────────┤
│  Cancel (bold)           │
└────────────────────────┘
```

**Android Bottom Sheet:**
```
┌────────────────────────┐
│        ────             │  ← Drag handle
│  Sheet Title             │
│                          │
│  ○  Share                │
│  ○  Save                 │
│  ○  Copy Link            │
│  ○  Delete               │
└────────────────────────┘
```

### Alerts / Dialogs

| Aspect | iOS | Android |
|--------|-----|----------|
| **Name** | Alert | Dialog |
| **Title** | Short, centered | Left-aligned |
| **Message** | Centered body text | Left-aligned body text |
| **Buttons** | Stacked or side-by-side | Always side-by-side, right-aligned |
| **Dismissal** | Tap button only | Tap button or outside (optional) |
| **Destructive action** | Red text | Red or caution color |
| **Button style** | Text buttons | Text buttons (Filled for emphasis) |

### Lists & Tables

| Aspect | iOS | Android |
|--------|-----|----------|
| **Grouped style** | Inset grouped (rounded cards) | Outlined or elevated cards |
| **Disclosure** | Chevron (>) on right | No indicator (entire row tappable) |
| **Swipe actions** | Swipe to reveal actions | Swipe to dismiss (limited) |
| **Separators** | Thin inset lines | Full-width dividers or none |
| **Selection** | Checkmark on right | Checkbox on left |
| **Editing** | Drag handles + delete circles | Drag handles + long-press |

### Switches & Toggles

| Aspect | iOS | Android |
|--------|-----|----------|
| **Style** | Rounded pill toggle | Rounded toggle with track + thumb |
| **On color** | Green (default) | Primary color |
| **Off color** | Gray | Gray outline |
| **Size** | Fixed (51x31pt) | Material 3 specs |
| **Labels** | Label on left, toggle on right | Label on left, toggle on right |
| **Icon** | No icon in toggle | Optional icon in thumb (M3) |

---

## Typography

| Aspect | iOS | Android |
|--------|-----|----------|
| **System font** | SF Pro (San Francisco) | Roboto / Google Sans |
| **Dynamic Type** | Required for accessibility | Scalable text via sp units |
| **Large Title** | 34pt, used at top of scrollable views | Headline Large: 32sp |
| **Body** | 17pt | Body Large: 16sp |
| **Caption** | 12pt | Body Small: 12sp |
| **Weight range** | Ultralight → Black | Thin → Black |

### Type Scale Comparison

| Purpose | iOS (pt) | Android (sp) |
|---------|----------|---------------|
| Screen title | 34 (Large Title) | 28–32 (Headline) |
| Section header | 22 (Title 1) | 22–24 (Title) |
| Body text | 17 (Body) | 16 (Body Large) |
| Secondary text | 15 (Subheadline) | 14 (Body Medium) |
| Caption | 12 (Caption 1) | 12 (Body Small) |
| Button | 17 (Body, semibold) | 14 (Label Large) |

---

## Spacing & Layout

| Aspect | iOS | Android |
|--------|-----|----------|
| **Base unit** | 8pt grid | 4dp / 8dp grid |
| **Screen margins** | 16pt (standard), 20pt (large) | 16dp (compact), 24dp (medium) |
| **Safe area** | Dynamic (notch, home indicator) | System insets |
| **Touch target** | 44x44pt minimum | 48x48dp minimum |
| **Corner radius** | System default varies (8–16pt) | 12–28dp (M3 uses varied radii) |

### Safe Areas

**iOS Safe Areas:**
```
┌──────────────────────┐
│ Status Bar (Dynamic)   │  ← Safe area inset top
├──────────────────────┤
│                        │
│     Safe Content       │
│     Area               │
│                        │
├──────────────────────┤
│    Home Indicator      │  ← Safe area inset bottom
└──────────────────────┘
```

---

## Color & Theming

| Aspect | iOS | Android |
|--------|-----|----------|
| **System colors** | Named semantic colors (label, secondaryLabel) | Material color roles (onSurface, primary) |
| **Dark mode** | Required support | Required support |
| **Tint color** | Single accent/tint color | Primary + secondary + tertiary colors |
| **Dynamic color** | Limited (tint color) | Material You: wallpaper-derived palette |
| **Elevation** | No shadow system | Tonal elevation (color-based, not shadow) |

---

## Cross-Platform Design Strategy

### Option 1: Platform-Native Design

Design unique UI for each platform following respective guidelines.

**Pros:** Best user experience, feels native, follows platform conventions
**Cons:** Higher design + development cost, two designs to maintain
**Best for:** Consumer apps, apps where native feel is critical

### Option 2: Unified Design with Platform Adaptations

Single design language with key platform-specific adaptations.

**What to adapt per platform:**
- Navigation pattern (tab bar position, back navigation)
- System fonts and type scales
- Button styles (iOS: text buttons, Android: filled/outlined)
- Bottom sheet behavior and styling
- Icon style (SF Symbols vs Material Icons)

**What to keep consistent:**
- Brand colors and imagery
- Content structure and information hierarchy
- Feature set and user flows
- Custom illustrations and graphics

**Best for:** Most apps, balanced approach

### Option 3: Fully Unified Design

Identical design across both platforms using a custom design system.

**Pros:** Lowest cost, consistent brand experience
**Cons:** Won't feel fully native on either platform, may confuse users
**Best for:** Internal tools, MVPs, rapid prototyping

---

## Platform-Specific Checklist

### iOS Design Checklist
- [ ] Support Dynamic Type (text scales with system setting)
- [ ] Respect safe areas (notch, home indicator, status bar)
- [ ] Use SF Symbols for system icons
- [ ] Support dark mode with semantic colors
- [ ] Use standard iOS navigation patterns (push/pop, tab bar)
- [ ] Minimum 44x44pt touch targets
- [ ] Support swipe-to-go-back gesture
- [ ] Use haptic feedback for key interactions

### Android Design Checklist
- [ ] Follow Material Design 3 component specs
- [ ] Support Material You dynamic color
- [ ] Use Material Icons or custom icon set
- [ ] Support dark theme
- [ ] Handle system back gesture / back button
- [ ] Minimum 48x48dp touch targets
- [ ] Support predictive back animation (Android 14+)
- [ ] Handle edge-to-edge display (draw behind system bars)
