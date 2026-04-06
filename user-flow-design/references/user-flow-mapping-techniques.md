# User Flow Mapping Techniques

Comprehensive guide to flow diagram types, mapping methods, collaborative techniques, and tools for creating effective user flow documentation.

---

## Flow Diagram Types

Different diagram types serve different purposes. Select based on what you need to communicate and the level of detail required.

### Diagram Type Comparison

| Diagram Type | Complexity | Audience | Best For | Limitations |
|-------------|:----------:|---------|---------|-------------|
| **Task flow** | Low | Designers, PMs | Single user completing a single task; no branching | Too simple for complex logic |
| **User flow** | Medium | Design team, PMs | Complete user journeys with decisions and branches | Can become unwieldy for very complex flows |
| **Wireflow** | High | Designers, developers | Flow + screen layouts combined; shows UI at each step | Time-intensive to create and maintain |
| **Swimlane diagram** | Medium | Cross-functional teams | Multi-actor processes (user + system + admin) | Requires clear role boundaries |
| **Journey map** | Medium | All stakeholders | Emotional arc + touchpoints across entire experience | Less precise than flow diagrams |
| **Service blueprint** | High | Service design, ops | Frontstage + backstage processes; shows what user sees vs. system processes | Complex; requires deep system knowledge |
| **State diagram** | High | Developers, system designers | All possible states an object or screen can be in | Abstract; hard for non-technical audiences |

### Task Flow

The simplest flow type — a single user completing a single task with no decision points.

```
[Landing Page] → [Click Sign Up] → [Enter Email] → [Create Password] → [Dashboard]
```

**When to use:** Early design phase; documenting the ideal happy path; communicating simple sequences.

### User Flow

Shows the complete path including decision points, branches, and alternate paths.

```
                    ┌───────────────┐
                    │  Landing Page  │
                    └───────┬───────┘
                            │
                    ┌───────◇───────┐
                    │ Has Account?  │
                    └─┬───────────┬─┘
                 Yes│             │No
            ┌─────┴───┐  ┌────┴─────┐
            │  Log In   │  │  Sign Up  │
            └────┬─────┘  └────┬─────┘
                 │             │
                 └─────┬─────┘
                       │
               ┌───────┴───────┐
               │   Dashboard    │
               └───────────────┘
```

**When to use:** Detailed design phase; documenting all paths; planning screen inventory.

### Wireflow

Combines flow diagram logic with low-fidelity wireframe screens.

**When to use:** Communicating both flow logic and UI layout simultaneously; useful when flow and layout decisions are intertwined.

**Structure per step:**
```
┌───────────────────┐
│ [Screen Name]       │
│ ┌───────────────┐ │
│ │  Header       │ │
│ └───────────────┘ │
│ ┌───────────────┐ │
│ │  Content Area │ │    →  [Next Screen]
│ └───────────────┘ │
│ [ CTA Button  ]     │
└───────────────────┘
```

### Swimlane Diagram

Shows multiple actors interacting in parallel lanes.

```
┌─────────────┬─────────────┬─────────────┐
│    User      │   System     │    Admin     │
├─────────────┼─────────────┼─────────────┤
│ Submit form  │              │              │
│      │       │              │              │
│      └──────▶ Validate     │              │
│              │      │       │              │
│              │      └──────▶ Review       │
│              │              │      │       │
│ Notification ◀───────────────────┘       │
└─────────────┴─────────────┴─────────────┘
```

**When to use:** Multi-role processes; showing handoffs between user, system, and admin; service design.

---

## Flow Mapping Methods

### Method 1: Goal-First Mapping

Start from user goals and work backward to identify required screens and steps.

| Step | Activity | Output |
|------|----------|--------|
| 1 | List all user goals for the feature/product | Goal inventory |
| 2 | For each goal, define the success state | Completion criteria |
| 3 | Identify the minimum steps to reach success | Happy path steps |
| 4 | Add decision points where user behavior may branch | Branch logic |
| 5 | Map error states and recovery for each step | Error handling |
| 6 | Identify entry points (how users arrive at step 1) | Entry point inventory |
| 7 | Connect flows that share screens or states | Flow interconnections |

### Method 2: Screen-First Mapping

Start from known screens (redesign projects) and map connections between them.

| Step | Activity | Output |
|------|----------|--------|
| 1 | Inventory all existing screens/pages | Screen list |
| 2 | Map current navigation connections | As-is connection map |
| 3 | Identify user tasks each screen supports | Task-screen mapping |
| 4 | Mark dead ends and orphan screens | Problem areas |
| 5 | Redesign connections based on user tasks | To-be flow diagram |

### Method 3: Jobs-to-be-Done Flow Mapping

Map flows based on the jobs users are trying to accomplish.

```
## Flow: [Job to be Done]

### Job Statement
When [situation], I want to [motivation], so I can [expected outcome].

### Job Steps
| # | Job Step | User Action | Screen | System Response |
|---|---------|------------|--------|----------------|
| 1 | Define need | [What user does] | [Where] | [What happens] |
| 2 | Locate solution | [What user does] | [Where] | [What happens] |
| 3 | Execute solution | [What user does] | [Where] | [What happens] |
| 4 | Confirm result | [What user does] | [Where] | [What happens] |

### Friction Points
| Step | Friction | Current Impact | Design Opportunity |
|------|---------|---------------|-------------------|
| [#] | [What slows the user] | [Drop-off %, time added] | [How to reduce friction] |
```

---

## Collaborative Flow Mapping

### Workshop Format: Flow Mapping Session

| Time | Activity | Materials |
|------|----------|----------|
| 0:00–0:10 | Introduction: share personas and goals | Persona cards, project brief |
| 0:10–0:25 | Individual: sketch happy path on sticky notes | Sticky notes, markers |
| 0:25–0:45 | Group: combine and discuss; build shared flow on wall | Whiteboard or large paper |
| 0:45–1:00 | Add decision points and alternate paths | Different color sticky notes |
| 1:00–1:15 | Add error states (red stickies) | Red sticky notes |
| 1:15–1:30 | Review and prioritize: mark critical vs. nice-to-have paths | Dot stickers for voting |

### Remote Flow Mapping Tips

| Challenge | Solution |
|-----------|----------|
| Can't see body language or energy | Use frequent check-ins; thumbs up/down reactions |
| Hard to collaborate spatially | Use Miro/FigJam with clear zones and templates |
| Distractions and multitasking | Keep sessions under 90 min; use active facilitation |
| Different tool proficiency | Send a practice board 24 hours before |
| Time zone challenges | Record sessions; share async for review |

---

## Flow Notation Standards

### Standard Flow Symbols

| Symbol | Shape | Meaning | Example |
|--------|-------|---------|--------|
| **Start/End** | Rounded rectangle or oval | Entry or exit point of flow | "User arrives from marketing email" |
| **Screen/Page** | Rectangle | A view the user sees | "Dashboard," "Settings Page" |
| **Decision** | Diamond | Branch point based on condition | "Is user logged in?" |
| **Action** | Rectangle with double border | User or system action | "System sends email," "User clicks submit" |
| **Direction** | Arrow (solid) | Primary flow direction | Happy path progression |
| **Alternate path** | Arrow (dashed) | Optional or secondary path | "Skip" option, edge case |
| **Error** | Rectangle with ⚠️ | Error state | "Validation error," "Network failure" |
| **Connector** | Circle with number | Continues flow on another page | ① links to ① on next sheet |
| **Note/Annotation** | Callout or flag | Design notes, context | "Consider: 2FA requirement" |

### Color Coding Convention

| Color | Meaning | Use |
|-------|---------|-----|
| **Blue** | Normal screens and flow | Happy path |
| **Green** | Success states | Completion, confirmation |
| **Red** | Error states | Validation errors, failures |
| **Yellow** | Decision points | Branches and logic |
| **Gray** | Alternate/optional paths | Secondary flows |
| **Purple** | System actions (not visible to user) | Backend processing, emails sent |

---

## Flow Documentation Tools

### Tool Comparison

| Tool | Flow Diagrams | Wireflows | Collaboration | Dev Handoff | Free Tier |
|------|:----------:|:---------:|:------------:|:----------:|:---------:|
| **Figma / FigJam** | ✅ | ✅ | ✅ Real-time | ✅ | ✅ |
| **Miro** | ✅ | Basic | ✅ Real-time | ❌ | ✅ |
| **Whimsical** | ✅ | ✅ | ✅ Real-time | ❌ | ✅ |
| **Lucidchart** | ✅ | Basic | ✅ Real-time | ❌ | ✅ |
| **Overflow** | ✅ | ✅ | View-only | ✅ | Trial |
| **draw.io** | ✅ | Basic | Via file sharing | ❌ | ✅ |
| **Markdown / ASCII** | Basic | ❌ | Via Git | ❌ | ✅ |

### Tool Selection Guide

| Need | Recommended Tool |
|------|------------------|
| Quick flow sketching | FigJam, Whimsical, or Miro |
| Detailed wireflows | Figma with auto-layout |
| Developer handoff | Figma (flows embedded in design file) |
| Stakeholder presentation | Overflow or Lucidchart (polished exports) |
| Version-controlled flows | Markdown/ASCII in code repository |
| Workshop facilitation | Miro or FigJam (sticky notes + flow tools) |

---

## Flow Quality Checklist

### Before Finalizing Any Flow

- [ ] **Entry points defined** — All ways users can start this flow are documented
- [ ] **Happy path complete** — Ideal scenario is fully mapped start to finish
- [ ] **Decision points have clear criteria** — Each diamond specifies the condition
- [ ] **All branches terminate** — No paths lead to dead ends
- [ ] **Error states identified** — What can go wrong at each step is documented
- [ ] **Recovery paths exist** — Users can recover from every error state
- [ ] **Screen inventory derived** — List of all unique screens needed
- [ ] **Consistent notation** — Same symbols and colors used throughout
- [ ] **Persona labeled** — Which user segment this flow represents is noted
- [ ] **Metrics defined** — Success rate targets and monitoring points are specified
- [ ] **Edge cases covered** — Unusual but important scenarios are addressed
- [ ] **Re-entry points noted** — How users return to the flow if they leave

---

## Flow Versioning and Maintenance

Use version naming like `[feature]-flow-v[Major].[Minor]` (e.g., `onboarding-flow-v1.0`). Update flows when new features are added (minor version), usability tests reveal problems (minor/major), features are redesigned (major version), or flow metrics fall below targets.
