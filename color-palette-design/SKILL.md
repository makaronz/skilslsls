---
name: color-palette-design
description: "Create harmonious color systems with proper contrast ratios, semantic meaning, and consistent application across UI components. Use for: building brand color palettes, defining primary and accent colors, ensuring WCAG contrast compliance, creating dark mode variants, and establishing systematic color tokens for design systems."
---

# Color Palettes

Create harmonious color systems with proper contrast ratios, semantic meaning, and consistent application across UI components.

# Skill: Color Palettes

## Overview
| Attribute | Value |
|-----------|-------|
| **Skill Name** | Color Palettes |
| **Category** | Visual Design |
| **Phase** | 3 - Visual Design |
| **Estimated Time** | 30-45 minutes |
| **Dependencies** | `inspiration_gathering.md`, `competitive_analysis.md` |
| **Outputs** | Complete color system with primary, secondary, neutral, and semantic colors |

## Description
Color Palettes skill creates harmonious, accessible, and purposeful color systems that support brand identity, establish visual hierarchy, and ensure usability across all design contexts.

## When to Use
- Starting visual design phase
- Establishing brand identity
- Creating design system foundations
- When existing colors need refinement
- Ensuring accessibility compliance

---

## Instructions for AI Agents
### Step 1: Define Color Strategy

**Prompt to establish direction:**
```
Based on this project context:
- Brand personality: [PERSONALITY TRAITS]
- Target audience: [AUDIENCE]
- Industry: [INDUSTRY]
- Competitive colors to avoid: [COMPETITOR COLORS]
- Mood to convey: [MOOD]

Recommend:
1. Primary color direction (hue family)
2. Overall palette mood (warm/cool/neutral)
3. Saturation level (vibrant/muted/mixed)
4. Contrast approach (high/medium/subtle)
```

### Step 2: Build Color System

**Complete color system structure:**

```markdown

## Color System: [Project Name]
### Primary Colors
| Name | Hex | RGB | Usage |
|------|-----|-----|-------|
| Primary-500 | #3B82F6 | rgb(59,130,246) | Main brand color, primary CTAs |
| Primary-400 | #60A5FA | rgb(96,165,250) | Hover states |
| Primary-600 | #2563EB | rgb(37,99,235) | Active/pressed states |
| Primary-100 | #DBEAFE | rgb(219,234,254) | Light backgrounds |
| Primary-900 | #1E3A8A | rgb(30,58,138) | Dark text on light primary |

### Secondary Colors
| Name | Hex | RGB | Usage |
|------|-----|-----|-------|
| Secondary-500 | #8B5CF6 | rgb(139,92,246) | Accent, secondary actions |
| Secondary-400 | #A78BFA | rgb(167,139,250) | Hover |
| Secondary-600 | #7C3AED | rgb(124,58,237) | Active |

### Neutral Colors
| Name | Hex | RGB | Usage |
|------|-----|-----|-------|
| Gray-900 | #111827 | | Primary text |
| Gray-700 | #374151 | | Secondary text |
| Gray-500 | #6B7280 | | Placeholder, disabled |
| Gray-300 | #D1D5DB | | Borders |
| Gray-100 | #F3F4F6 | | Backgrounds, hover |
| Gray-50 | #F9FAFB | | Page background |
| White | #FFFFFF | | Cards, inputs |

### Semantic Colors
| Name | Hex | Usage |
|------|-----|-------|
| Success | #10B981 | Success messages, confirmations |
| Success-light | #D1FAE5 | Success backgrounds |
| Warning | #F59E0B | Warnings, cautions |
| Warning-light | #FEF3C7 | Warning backgrounds |
| Error | #EF4444 | Errors, destructive actions |
| Error-light | #FEE2E2 | Error backgrounds |
| Info | #3B82F6 | Information, tips |
| Info-light | #DBEAFE | Info backgrounds |
```

### Step 3: Generate Color Scale

**Prompt for scale generation:**
```
Given primary color #3B82F6, generate a complete scale:

50:  [Very light, almost white tint]
100: [Light tint for backgrounds]
200: [Lighter shade]
300: [Light]
400: [Slightly lighter than base]
500: [BASE COLOR]
600: [Slightly darker]
700: [Darker shade]
800: [Dark]
900: [Very dark, almost black shade]

Ensure:
- Perceptually even steps
- 500 is the provided base color
- Good contrast ratios throughout
```

### Step 4: Verify Accessibility

**WCAG contrast requirements:**

| Use Case | Minimum Ratio | Level |
|----------|---------------|-------|
| Body text | 4.5:1 | AA |
| Large text (18px+ bold, 24px+) | 3:1 | AA |
| UI components, graphics | 3:1 | AA |
| Enhanced body text | 7:1 | AAA |

**Contrast check prompt:**
```
Verify these color combinations meet WCAG AA:

| Foreground | Background | Use | Ratio | Pass? |
|------------|------------|-----|-------|-------|
| [Text color] | [Bg color] | Body text | [Ratio] | [Y/N] |
| [Button text] | [Button bg] | Button | [Ratio] | [Y/N] |
| [Link color] | [Page bg] | Links | [Ratio] | [Y/N] |

For any failures, suggest alternatives.
```

### Step 5: Define Usage Guidelines

**Color application rules:**

```markdown
### Color Usage Guidelines

#### Do
- Use Primary-500 for main CTAs and key actions
- Use Gray-900 for headings and body text
- Use semantic colors for status indicators
- Apply Primary-100 for highlighted sections

#### Don't
- Don't use Primary on Primary (no contrast)
- Don't use Error color for non-error purposes
- Don't use more than 3 colors in one component
- Don't rely on color alone for meaning

#### Hierarchy
1. **Primary CTA**: Primary-500 background, white text
2. **Secondary CTA**: White background, Primary-500 text, Primary-500 border
3. **Tertiary CTA**: Transparent, Primary-500 text
```

---

## Example Input/Output
### Example Input

```markdown
**Project**: TaskFlow - SaaS project management
**Personality**: Modern, professional, approachable, creative
**Audience**: Creative agencies
**Competitors using**: Blue (Asana, Monday), Black (Notion)
**Desired mood**: Warm but professional, premium but friendly
```

### Example Output

```markdown

## Prompts Library
### Quick Palette Generation
```
Create a color palette for [PROJECT TYPE] with:
- Primary: [COLOR DIRECTION or specific hue]
- Mood: [MOOD]
- Avoid: [COLORS TO AVOID]

Provide:
1. Primary color (hex)
2. Secondary accent (hex)
3. 3 neutral grays (hex)
4. Success/Error/Warning colors
```

### Color Scale from Single Color
```
Given #3B82F6 as the base (500), generate:
- Lighter variations: 50, 100, 200, 300, 400
- Darker variations: 600, 700, 800, 900

Format as table with hex values.
```

### Accessibility Fix
```
This color combination fails WCAG:
Foreground: #111827
Background: #FFFFFF
Current ratio: [RATIO]
Required: 4.5:1

Suggest alternatives that:
1. Maintain the same hue
2. Meet the contrast requirement
3. Look visually similar
```

---

## Resources
### Color Tools
| Tool | URL | Use Case |
|------|-----|----------|
| Coolors | coolors.co | Palette generation |
| Realtime Colors | realtimecolors.com | Preview in context |
| Adobe Color | color.adobe.com | Color wheel, extract |
| Contrast Checker | webaim.org/resources/contrastchecker | WCAG verification |
| Colorable | colorable.jxnblk.com | Contrast combinations |
| Huemint | huemint.com | AI palettes |

### Color Theory Reference
- **Complementary**: Colors opposite on wheel (high contrast)
- **Analogous**: Colors adjacent on wheel (harmonious)
- **Triadic**: Three colors evenly spaced (vibrant)
- **Split-complementary**: Base + two adjacent to complement (balanced)

---

## Success Criteria
### Minimum Requirements
- [ ] Primary color with 5+ shades
- [ ] Secondary/accent color
- [ ] Full neutral scale (50-900)
- [ ] Semantic colors (success, warning, error, info)
- [ ] All text/background combos pass WCAG AA

### Quality Indicators
- [ ] Colors support brand personality
- [ ] Clear hierarchy through color
- [ ] Differentiated from competitors
- [ ] Works for colorblind users
- [ ] Dark mode consideration (if needed)

---

## Related Skills
- **Previous**: `inspiration_gathering.md` - Color direction from inspiration
- **Next**: `typography.md` - Type system to complement colors
- **Related**: `accessibility_review.md` - Full accessibility verification

## Using the Reference Files

### When to Read Each Reference

**`/references/color-theory-psychology.md`** — Read when you need to understand color theory fundamentals, color harmony systems (complementary, analogous, triadic), the psychology of color and emotional impact, cultural color associations, or the 60-30-10 rule for palette distribution.

**`/references/accessibility-contrast-wcag.md`** — Read when you need to verify WCAG contrast ratios, design for color vision deficiencies, build accessible palettes with proper neutral scales, implement dark mode accessibility, or select contrast testing tools and workflows.

**`/references/color-system-implementation.md`** — Read when you need to implement design tokens for color (primitive, semantic, component tiers), define naming conventions, set up CSS custom properties or Tailwind config, use Style Dictionary for multi-platform output, or generate perceptually uniform color scales with OKLCH.

**`/references/color-system-taskflow.md`** — Read when you need detailed guidance on color system taskflow aspects of this skill.
