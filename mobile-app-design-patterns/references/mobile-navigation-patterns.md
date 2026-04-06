# Mobile Navigation Patterns

Comprehensive guide to mobile navigation patterns including tab bars, hamburger menus, bottom sheets, drawer navigation, and strategies for organizing mobile app information architecture.

---

## Navigation Pattern Selection

Choosing the right navigation pattern depends on the number of top-level destinations, content depth, and user task frequency.

### Decision Framework

```
How many top-level destinations?
│
├─ 2–5 destinations (frequently accessed)
│  └─→ BOTTOM TAB BAR
│
├─ 6+ destinations (varied frequency)
│  └─→ NAVIGATION DRAWER
│
├─ 3–5 destinations (content-focused, swipeable)
│  └─→ TOP TABS (scrollable)
│
├─ Deep hierarchy (settings, account)
│  └─→ NESTED LIST NAVIGATION
│
└─ Single primary task with sub-actions
   └─→ CONTEXTUAL NAVIGATION (bottom sheet, FAB)
```

### Pattern Comparison

| Pattern | Max Items | Visibility | Switching Cost | Best For |
|---------|-----------|-----------|---------------|----------|
| **Bottom Tab Bar** | 5 | Always visible | Very low (1 tap) | Core app sections |
| **Navigation Drawer** | Unlimited | Hidden (on demand) | Medium (2 taps) | Many destinations |
| **Top Tabs** | 5–7 (scrollable) | Always visible | Low (1 tap/swipe) | Content categories |
| **Bottom Sheet Nav** | 10+ | Hidden (on demand) | Medium (2 taps) | Contextual actions |
| **Hub & Spoke** | Varies | On hub screen | High (back + select) | Utility/tool apps |

---

## Bottom Tab Bar

The most common and recommended primary navigation pattern for mobile apps.

### Anatomy

```
┌─────────────────────────────────────┐
│                                     │
│         Screen Content               │
│                                     │
├─────────────────────────────────────┤
│  ●        ○        ○        ○       │
│ Home    Search    Cart    Profile   │
└─────────────────────────────────────┘
```

### Design Guidelines

| Rule | Guideline |
|------|----------|
| **Number of items** | 3–5 tabs (never more than 5) |
| **Labels** | Always show text labels with icons |
| **Icon + label** | Icon above label, centered in tab area |
| **Active state** | Clearly distinguished (color, fill, size) |
| **Inactive state** | Muted but still legible |
| **Badge notifications** | Small dot or number badge on icon |
| **Tap behavior** | Tapping active tab scrolls to top / resets |
| **Position** | Fixed at bottom, always visible |
| **Height** | ~56–83dp (including safe area on iOS) |

### Tab Bar Patterns

**Standard Tab Bar (Equal Width):**
```
│  Home  │  Search │  Orders │  Account │
```

**Tab Bar with Prominent Action:**
```
│  Home  │  Search │  [+]  │  Inbox  │  Profile │
                     ▲
              Raised FAB or
              prominent action
```

**Scrollable Tab Bar (Top):**
```
│  For You  │  Trending  │  Following  │  Sports  │  Tech  │ ...
```

### Tab Bar Anti-Patterns
- ❌ More than 5 tabs (use drawer for 6+ destinations)
- ❌ Icons without labels (users can't guess meaning)
- ❌ Hiding the tab bar on scroll (breaks muscle memory)
- ❌ Using tabs for sequential flow (tabs are non-linear)
- ❌ Different tab sets on different screens (breaks consistency)

---

## Navigation Drawer (Hamburger Menu)

A side panel that slides in from the left edge, containing navigation destinations.

### Anatomy

```
┌───────────────┬────────────────────┐
│ ┌───────────┐ │                    │
│ │ [Avatar]  │ │                    │
│ │ User Name │ │     Content        │
│ │ email@... │ │     (dimmed)       │
│ └───────────┘ │                    │
├───────────────┤                    │
│ ● Home         │                    │
│ ○ Messages     │                    │
│ ○ Favorites    │                    │
│ ○ Downloads    │                    │
├───────────────┤                    │
│ ○ Settings     │                    │
│ ○ Help         │                    │
└───────────────┴────────────────────┘
```

### When to Use
- 6+ top-level destinations
- Destinations with varied access frequency
- Complex apps with many sections
- When tab bar can't accommodate all destinations

### When to Avoid
- Fewer than 6 destinations (use tab bar instead)
- Frequently-accessed core features (hidden = forgotten)
- iOS apps (not a native iOS pattern)

### Drawer Design Guidelines

| Element | Specification |
|---------|---------------|
| Width | 256–320dp (or 85% of screen width, max 400dp) |
| Header | Optional: User profile, app branding |
| Items | Icon + label, grouped with dividers |
| Active item | Highlighted background, primary color |
| Scrim | Semi-transparent overlay behind drawer |
| Dismissal | Tap scrim, swipe left, or back gesture |
| Animation | Slide from left, 250ms ease-in-out |

### The Hamburger Menu Debate

**Arguments against:**
- Low discoverability (hidden behind icon)
- Adds interaction cost (tap to open, then tap destination)
- Users engage less with hidden navigation
- Data shows lower engagement vs visible navigation

**When it's still appropriate:**
- Secondary navigation alongside a visible primary nav
- Admin/settings sections accessed infrequently
- Apps with many destinations that can't fit in a tab bar
- Android apps where it's a platform convention

---

## Bottom Sheet Navigation

Modal surfaces that slide up from the bottom, used for contextual navigation and actions.

### Types of Bottom Sheets

**Standard (Modal):**
```
┌───────────────────────────┐
│       ─────               │
│                           │
│  ○  Share to...            │
│  ○  Copy link              │
│  ○  Save to collection     │
│  ○  Report                 │
│                           │
└───────────────────────────┘
```

**Expandable (Persistent):**
```
Collapsed (peek):         Expanded (half):          Expanded (full):
┌──────────────┐      ┌──────────────┐      ┌──────────────┐
│              │      │   Content    │      │   Header     │
│              │      │   Area       │      ├──────────────┤
│  Content     │      ├──────────────┤      │              │
│              │      │    ────      │      │   Full       │
├──────────────┤      │  Sheet       │      │   Content    │
│    ────      │      │  Content     │      │   Area       │
│ Summary info │      │              │      │              │
└──────────────┘      └──────────────┘      └──────────────┘
```

### Bottom Sheet Guidelines

| Rule | Guideline |
|------|----------|
| Drag handle | Always show a drag indicator at the top |
| Snap points | Define 2–3 height positions (peek, half, full) |
| Scrolling | Internal scroll when content exceeds sheet height |
| Scrim | Use semi-transparent backdrop for modal sheets |
| Dismiss | Swipe down to collapse or dismiss |
| Keyboard | Sheet should move above keyboard when input is focused |
| Max height | Don't cover the entire screen (leave ~40dp top margin) |

### Use Cases
- Map applications (location details, directions)
- Music/media players (now playing, queue)
- Contextual actions (share, save, report)
- Filter and sort controls
- Quick composition (message, note, task)

---

## Floating Action Button (FAB)

A prominent button for the primary action of a screen.

### FAB Guidelines

```
                              ┌─────┐
                              │  +  │  ← FAB (56dp)
                              └─────┘
┌──────┬──────┬──────┬──────┐
│ Home │ Srch │ Chat │ Prof │  ← Tab Bar
└──────┴──────┴──────┴──────┘
```

| Rule | Guideline |
|------|----------|
| Count | One FAB per screen maximum |
| Action | Most important action on the screen |
| Position | Bottom-right (default) or bottom-center |
| Size | Regular (56dp), Small (40dp), Large (96dp) |
| Behavior | Scroll down: hide FAB. Scroll up: show FAB |
| Extended FAB | Icon + text label for clarity |
| Platform | Primarily Android (Material Design). Not standard iOS. |

### FAB vs Inline Button Decision

| Scenario | Use FAB | Use Inline Button |
|----------|---------|-------------------|
| Create new item (universal) | ✅ | |
| Submit form | | ✅ |
| Context-specific action | | ✅ |
| Multiple primary actions | | ✅ (use no FAB) |
| Action needs explanation | | ✅ (with text label) |

---

## Search Navigation

### Search Entry Patterns

**Persistent Search Bar:**
```
┌────────────────────────────┐
│ 🔍  Search products...     │
└────────────────────────────┘
```
**Best for:** Search-primary apps (e-commerce, maps, content discovery).

**Expandable Search (Icon → Bar):**
```
Collapsed:           Expanded:
[🔍]                ← [🔍 Search...        ✕]
```
**Best for:** Apps where search is secondary to browsing.

**Full-Screen Search:**
```
┌────────────────────────────┐
│ ←  Search...          ✕   │
├────────────────────────────┤
│ Recent Searches:           │
│  ○  Running shoes           │
│  ○  Blue jacket             │
│  ○  Wireless headphones     │
├────────────────────────────┤
│ Trending:                  │
│  ○  Summer sale             │
│  ○  New arrivals            │
└────────────────────────────┘
```
**Best for:** Complex search with filters, suggestions, and history.

---

## Contextual Navigation

### Segmented Control (iOS) / Toggle Button Group (Android)

```
┌──────────┬──────────┬──────────┐
│ [█ Day  ] │   Week   │  Month   │
└──────────┴──────────┴──────────┘
```

**Use for:** Switching between views of the same content (e.g., list/grid, day/week/month, map/list).

### Breadcrumbs (Mobile Adaptation)

On mobile, simplify breadcrumbs to show only the parent:

```
← Category Name
```

Instead of full path: Home > Products > Category > Subcategory

---

## Navigation Accessibility

| Requirement | Implementation |
|-------------|----------------|
| Focus management | Move focus to new content when navigating |
| Screen reader labels | Announce current section name |
| Back navigation | System back must work predictably |
| Skip navigation | Allow jumping past repeated nav elements |
| Active state | Current tab/section must be announced |
| Drawer announce | Screen reader must announce drawer open/close state |
| Touch targets | All nav items minimum 44x44pt (iOS) / 48x48dp (Android) |

---

## Navigation Pattern Selection by App Type

| App Type | Recommended Primary Nav | Secondary Nav |
|----------|------------------------|----------------|
| Social media | Bottom tab bar | Top tabs for content feeds |
| E-commerce | Bottom tab bar | Category drawer, filters |
| Messaging | Bottom tab bar | Conversation list → thread |
| News/content | Bottom tab bar + top tabs | Category filters |
| Productivity | Bottom tab bar or drawer | Contextual menus |
| Maps/travel | Bottom tab bar | Expandable bottom sheet |
| Settings/admin | Nested list | Section grouping |
| Single-purpose tool | Minimal (back button only) | Bottom sheet for options |
