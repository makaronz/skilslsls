# Touch Gestures & Interactions

Comprehensive guide to touch gesture design, gesture types, interaction patterns, haptic feedback, and best practices for creating intuitive touch interfaces on mobile devices.

---

## Core Touch Gestures

### Gesture Reference

| Gesture | Description | Common Use | Reversible? |
|---------|------------|-----------|-------------|
| **Tap** | Single finger touch and release | Select, activate, toggle | Varies |
| **Double Tap** | Two quick taps in same location | Zoom in, like/favorite | Yes |
| **Long Press** | Touch and hold (~500ms) | Context menu, selection mode, drag | Yes |
| **Swipe** | Quick directional drag and release | Navigate, dismiss, reveal actions | Usually |
| **Drag** | Touch, hold, and move | Reorder, move objects, scroll | Yes |
| **Pinch** | Two fingers moving together | Zoom out | Yes |
| **Spread** | Two fingers moving apart | Zoom in | Yes |
| **Rotate** | Two fingers rotating | Rotate images/maps | Yes |
| **Edge Swipe** | Swipe from screen edge | Back navigation (iOS/Android) | Yes |

---

## Tap Interactions

### Tap Design Guidelines

**Touch Target Sizing:**

| Platform | Minimum Size | Recommended Size | Spacing Between Targets |
|----------|-------------|-----------------|------------------------|
| iOS | 44 x 44 pt | 44 x 44 pt | 8pt minimum |
| Android | 48 x 48 dp | 48 x 48 dp | 8dp minimum |
| WCAG 2.5.8 | 24 x 24 CSS px | 44 x 44 CSS px | No adjacent overlap |

**Touch Target Expansion:**
When visual size must be smaller than minimum touch target, expand the invisible hit area:

```
Visible:     Actual touch area:
  ┌──┐      ┌──────────┐
  │✕✕│      │          │
  └──┘      │   ┌──┐   │
              │   │✕✕│   │
              │   └──┘   │
              │          │
              └──────────┘
              44x44pt hit area
```

### Tap States

Every tappable element needs clear state feedback:

| State | Visual Feedback | Timing |
|-------|----------------|--------|
| Default | Normal appearance | — |
| Pressed | Slight opacity reduction or highlight | Immediate on touch |
| Released | Return to default + action result | On finger lift |
| Disabled | Reduced opacity (0.38–0.5) | — |
| Focused | Outline/ring (keyboard/accessibility) | On focus event |

### Tap Timing
- **Standard tap:** < 300ms touch duration
- **Long press threshold:** 500ms (iOS) / 400ms (Android default)
- **Double tap window:** < 300ms between taps
- **Tap delay (web):** Remove 300ms delay with `touch-action: manipulation`

---

## Swipe Interactions

### Swipe Directions & Common Actions

| Direction | Common Action | Example |
|-----------|--------------|----------|
| **Swipe Left** | Reveal destructive actions | Delete email, remove item |
| **Swipe Right** | Reveal positive actions | Archive, mark as read |
| **Swipe Down** | Pull to refresh, dismiss | Refresh feed, close modal |
| **Swipe Up** | Load more, expand sheet | Scroll, expand bottom sheet |
| **Edge Swipe Left** | Go back (iOS) | Navigate to previous screen |
| **Edge Swipe Right** | Go forward (rare) | Navigate forward |

### Swipe-to-Reveal Actions

```
Default state:
┌────────────────────────────┐
│  📧  Email subject line    │
│     Preview text...        │
└────────────────────────────┘

Swiped left:
┌───────────────────┬────┬────┐
│  📧  Email subject  │Flag│ Del│
│     Preview text.. │ 🚩 │ 🗑  │
└───────────────────┴────┴────┘

Full swipe (direct action):
┌────────────────────────────┐
│  ✓  Archived                │
└────────────────────────────┘
```

### Swipe Design Rules

| Rule | Guideline |
|------|----------|
| **Discoverability** | Swipe actions are hidden; provide alternative tap access too |
| **Visual feedback** | Show action icons/colors as user swipes |
| **Thresholds** | Partial swipe reveals; full swipe executes |
| **Destructive actions** | Place on opposite side from positive actions |
| **Maximum actions** | 2–3 per swipe direction |
| **Undo** | Always provide undo for destructive swipe actions |
| **Consistency** | Same swipe patterns throughout the app |

### Pull-to-Refresh

```
Pulling:                    Refreshing:
     ▽                           ▽
     |                       [↻ spinning]
     |                           |
┌──────────────┐      ┌──────────────┐
│  Content     │      │  Updating... │
│  pulled      │      │              │
│  down        │      │  Content     │
└──────────────┘      └──────────────┘
```

**Pull-to-Refresh Guidelines:**
- Use only at the top of scrollable lists
- Show a spinner or loading indicator
- Provide haptic feedback when threshold is reached
- Set reasonable refresh threshold (~64dp of pull)
- Don't use for non-list content (use a refresh button instead)

---

## Long Press Interactions

### Common Long Press Actions

| Context | Long Press Action |
|---------|-------------------|
| List item | Enter selection mode / Context menu |
| Image | Preview (peek), save, share |
| Link | Preview URL, open options |
| Text | Enter text selection mode |
| App icon | Quick actions menu (iOS) |
| Map pin | Drag to reposition |
| Reorderable list | Initiate drag-to-reorder |

### Long Press Design Guidelines

1. **Discoverability** — Long press is hidden; never make it the only way to access important features
2. **Feedback** — Provide visual + haptic feedback when long press activates
3. **Duration** — 400–500ms is the standard threshold
4. **Cancel** — User should be able to cancel by dragging finger away
5. **Progressive** — Can show tooltip/preview first, then full context menu

### Context Menus

**iOS Context Menu (Long Press):**
```
┌──────────────────┐
│ ┌────────────┐  │
│ │  [Preview]  │  │
│ │   of item   │  │
│ └────────────┘  │
│                  │
│ ┌────────────┐  │
│ │ Copy       │  │
│ │ Share      │  │
│ │ Favorite   │  │
│ │────────────┤  │
│ │ Delete 🗑  │  │
│ └────────────┘  │
└──────────────────┘
```

---

## Pinch & Zoom

### Pinch-to-Zoom Guidelines

| Rule | Guideline |
|------|----------|
| **Content types** | Images, maps, documents, diagrams |
| **Min zoom** | Usually 1x (original size) or fit-to-screen |
| **Max zoom** | 3–5x for images, unlimited for maps |
| **Double-tap zoom** | Toggle between fit-to-width and 2x zoom |
| **Momentum** | Apply inertia to zoom gesture |
| **Boundaries** | Elastic bounce at min/max zoom levels |
| **Pan when zoomed** | Allow single-finger panning when zoomed in |

### Zoom UI Patterns

**Image Viewer:**
```
Default (1x):           Zoomed (2x):           Zoomed + Pan:
┌────────────┐      ┌────────────┐      ┌────────────┐
│            │      │            │      │            │
│  [Full     │      │  [Cropped  │      │  [Panned   │
│   Image]   │      │   2x view] │      │   view]    │
│            │      │            │      │            │
└────────────┘      └────────────┘      └────────────┘
Pinch out to zoom        Drag to pan
Double-tap to zoom       Double-tap to reset
```

---

## Drag & Drop

### Drag-to-Reorder

```
Initiate:              Dragging:              Dropped:
┌────────────┐   ┌────────────┐   ┌────────────┐
│ ≡ Item A    │   │ ≡ Item B    │   │ ≡ Item B    │
│ ≡ Item B    │   │ ────────── │   │ ≡ Item C    │
│ ≡ Item C    │   │ │ Item A  │ │   │ ≡ Item A    │
│ ≡ Item D    │   │ ────────── │   │ ≡ Item D    │
└────────────┘   │ ≡ Item C    │   └────────────┘
                   │ ≡ Item D    │
 Long press to      └────────────┘
 initiate           Item A floats
                   above others
```

### Drag Guidelines

| Rule | Guideline |
|------|----------|
| Initiation | Long press (500ms) or dedicated drag handle (≡) |
| Visual feedback | Lift item (elevation/shadow), show drop target |
| Haptic feedback | Light impact on pickup, medium on drop |
| Cancel | Drag to original position or release outside valid targets |
| Auto-scroll | Scroll list when dragging near edges |
| Accessibility | Provide alternative reorder (buttons) for non-touch users |

---

## Haptic Feedback

### iOS Haptic Types

| Haptic Type | When to Use | Example |
|------------|------------|----------|
| **Impact (Light)** | Subtle confirmation | Toggle switch, selection |
| **Impact (Medium)** | Standard confirmation | Drop after drag, snap to position |
| **Impact (Heavy)** | Significant action | Delete confirmed |
| **Selection** | Moving through options | Picker scroll, slider snap |
| **Success** | Positive completion | Payment success, save |
| **Warning** | Caution needed | Approaching limit, shake alert |
| **Error** | Action failed | Invalid input, operation error |

### Android Haptic Types

| Haptic Type | When to Use |
|------------|------------|
| **Click** | Standard interaction feedback |
| **Double Click** | Confirming action |
| **Heavy Click** | Significant action completion |
| **Tick** | Moving through incremental values |
| **Reject** | Action denied or failed |

### Haptic Best Practices

1. **Be purposeful** — Don't add haptics to every interaction; they lose meaning
2. **Match intensity to action** — Light tap for minor, heavy for significant
3. **Respect system settings** — Honor system haptic preferences
4. **Complement visual feedback** — Haptics supplement but don't replace visual cues
5. **Test on real devices** — Haptics can't be tested in simulators
6. **Avoid continuous vibration** — Use discrete pulses, not sustained buzzing

---

## Gesture Discoverability

Gestures are powerful but hidden. Strategies to help users discover them:

### Onboarding Techniques

| Technique | Description | When |
|-----------|------------|------|
| **Coach marks** | Animated overlay showing gesture | First-time use |
| **Tooltip hints** | Small text hints near swipeable items | First encounter |
| **Animation peek** | Briefly animate to reveal hidden actions | First time on screen |
| **Contextual tip** | "Tip: Swipe left to delete" message | After related action |
| **Empty state** | Instructions in empty lists | When content is empty |

### Progressive Disclosure
```
1. User sees list item (tap is obvious)
2. User long-presses → Context menu appears with "Swipe for quick actions" hint
3. User swipes → Actions revealed with labels
4. Subsequent items: user knows to swipe (labels can be hidden)
```

---

## Gesture Accessibility

| Requirement | Implementation |
|-------------|----------------|
| **Alternative input** | Every gesture action must have a tap alternative |
| **Switch control** | Support iOS Switch Control / Android Switch Access |
| **Voice control** | Ensure gesture actions can be triggered by voice commands |
| **Custom gestures** | Support AssistiveTouch custom gestures (iOS) |
| **Motion sensitivity** | Avoid shake-to-undo; provide button alternative |
| **Timeout** | Don't require time-sensitive gestures |

### WCAG Gesture Requirements

- **2.5.1 Pointer Gestures** — Multi-point (pinch) and path-based (swipe) gestures must have single-pointer alternatives
- **2.5.2 Pointer Cancellation** — Actions must fire on finger up (not down), allowing cancellation by dragging away
- **2.5.4 Motion Actuation** — Shake/tilt actions must have UI alternatives and be disableable

---

## Gesture Anti-Patterns

1. **Gesture-only features** — No visible alternative for critical actions
2. **Conflicting gestures** — Horizontal swipe on a horizontally scrollable page
3. **Overloaded gestures** — Same gesture doing different things in different contexts
4. **Missing feedback** — No visual or haptic response to gesture input
5. **Tiny targets** — Touch targets smaller than 44pt/48dp
6. **No undo** — Destructive gesture actions without recovery path
7. **Custom over standard** — Redefining standard gestures (e.g., swipe right doesn't go back)
8. **Complex gestures** — Requiring 3+ finger gestures for common actions
