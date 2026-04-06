# Kanban Board Design Guide

Patterns and best practices for designing Kanban boards that visualize workflow, surface bottlenecks, and drive continuous improvement.

---

## Board Structure Fundamentals

### Column Design

Map columns to the actual workflow steps your team follows, not an idealized process:

| Column Type | Examples | Purpose |
|-------------|---------|---------|
| Queue / Backlog | To Do, Ready | Items waiting to be pulled |
| Active Work | In Progress, Development, Review | Items being actively worked on |
| Buffer / Wait | Waiting for Review, Blocked | Items paused between active stages |
| Done | Done, Deployed, Released | Completed items |

### Split Columns

Split active columns into "Doing" and "Done" sub-columns to make handoffs visible:

```
| Development      | Code Review      | QA              |
| Doing  |  Done   | Doing  |  Done   | Doing  | Done  |
```

When a developer finishes coding, they move the card to "Development: Done." The reviewer pulls it into "Code Review: Doing." This makes wait time between stages visible.

## Board Types by Team

### Software Development Board

```
Backlog → Ready → Development [Doing | Done] → Code Review [Doing | Done] → QA → Deploy → Done
```

- WIP limit on Development: 2× team size
- WIP limit on Code Review: team size
- Expedite lane for production incidents

### Marketing / Content Board

```
Ideas → Research → Drafting → Review → Design → Scheduled → Published
```

- WIP limit on Drafting: 3 (prevent content pile-up)
- Use card types to distinguish blog posts, social, email campaigns

### Support / IT Operations Board

```
Incoming → Triage → In Progress → Waiting on Customer → Resolved → Closed
```

- SLA markers on cards (red border if approaching breach)
- Priority swim lanes (Critical, High, Normal)

## Swim Lanes

Horizontal lanes that segment the board by a secondary dimension:

| Lane Type | Use Case | Example |
|-----------|----------|---------|
| Priority | Separate urgent from standard work | Expedite, Standard, Low Priority |
| Work type | Distinguish different work categories | Feature, Bug, Tech Debt |
| Team / Person | Track individual assignments | Team A, Team B |
| Customer / Project | Multi-project visibility | Project Alpha, Project Beta |

## Card Design

Each card should display at a glance:

| Element | Purpose | Placement |
|---------|---------|-----------|
| Title | What is this work item? | Top, bold |
| Card type indicator | Feature, bug, task, spike | Color strip or icon |
| Assignee | Who is working on it? | Avatar or initials |
| Age indicator | How long has this card been in progress? | Days counter or color aging |
| Blocked flag | Is this item stuck? | Red indicator or emoji |
| Size / Points | Relative effort | Small badge |
| Due date | When is this expected | Date or SLA tag |

### Card Aging

Color cards based on time spent in the current column:
- **0-2 days**: Normal (no highlight)
- **3-5 days**: Yellow (approaching typical cycle time)
- **6+ days**: Red (exceeding cycle time, likely blocked)

## Board Policies

Document explicit policies for each column. Display them on the board (physical or digital):

| Column | Policy |
|--------|--------|
| Ready | Item has acceptance criteria, is estimated, and has no blockers |
| Development: Doing | Developer has pulled the item (not assigned/pushed) |
| Code Review: Doing | PR submitted, reviewer assigned within 4 hours |
| QA: Done | All acceptance criteria verified, no critical bugs |
| Deploy | Deployment window is Tuesday and Thursday at 10am |

Explicit policies eliminate ambiguity about when work can move between stages.
