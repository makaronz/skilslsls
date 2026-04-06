# Story Mapping Fundamentals

Theoretical foundation and core concepts of Jeff Patton's user story mapping methodology.

---

## What Is a Story Map

A story map is a two-dimensional visualization of a product's functionality organized by user activities (horizontal) and priority/detail (vertical). Unlike a flat backlog, a story map preserves the user's journey context, making it easier to plan releases that deliver complete, meaningful experiences.

### Story Map Anatomy

```
                    Activities (User's Big Goals)
                ┌──────────┬──────────┬──────────┐
Backbone →      │ Sign Up  │ Set Up   │ Use Core │
                │          │ Profile  │ Feature  │
                ├──────────┼──────────┼──────────┤
Tasks →         │ Enter    │ Add      │ Create   │
(Steps under    │ Email    │ Photo    │ Widget   │
 each activity) │ Set PWD  │ Add Bio  │ Edit     │
                │ Verify   │ Connect  │ Share    │
                ├──────────┼──────────┼──────────┤
                │ OAuth    │ Import   │ Template │
Body →          │ Login    │ From     │ Library  │
(Detail         │          │ LinkedIn │          │
 stories)       │ Magic    │ Skills   │ Advanced │
                │ Link     │ Tags     │ Editor   │
                └──────────┴──────────┴──────────┘
                ← Low Priority ——————→ High Priority ↑
                              (read left to right,
                               top to bottom)
```

### Key Components

| Component | Description | Position |
|-----------|-------------|----------|
| **Activities** | Large user goals or workflow phases | Top row (backbone) |
| **Tasks** | Steps a user takes within each activity | Second row (backbone) |
| **User Stories** | Specific implementations of each task | Below the backbone (body) |
| **Walking Skeleton** | Thinnest possible end-to-end implementation | Top stories across all activities |
| **Release Slices** | Horizontal lines grouping stories into releases | Drawn across the body |

## The Backbone

The backbone is the top row(s) of the story map. It represents the user's journey through the product at the highest level.

### Building the Backbone

1. **Identify the user persona**: Who is the primary user of this journey?
2. **List activities**: What major goals does the user accomplish? (e.g., "Discover Products," "Make a Purchase," "Track Order")
3. **Order left to right**: Arrange activities in the sequence the user would naturally perform them
4. **Add tasks under each activity**: What specific steps does the user take? (e.g., under "Make a Purchase": Browse, Add to Cart, Enter Payment, Confirm Order)

### Backbone Rules

- Read the backbone left to right — it should tell a coherent story of the user's experience
- Activities should be verbs or verb phrases
- Keep the backbone at the right level of abstraction — not too detailed, not too vague
- The backbone should be stable; the body changes frequently as you learn more

## The Body

The body contains the user stories that flesh out each task. Stories are arranged vertically by priority (most important at the top, least at the bottom).

### Story Arrangement Principles

- **Top stories** across all activities form the walking skeleton — the minimal viable flow
- **Middle stories** add essential functionality that makes the experience good
- **Bottom stories** add delight, edge cases, and advanced features

### Writing Stories for the Map

Stories on the map are typically short (card-sized). Full acceptance criteria and technical details live in the backlog tool, not on the map. The map is a planning and communication artifact.

Format: "As a [user], I can [action] so that [value]"

## Narrative Flow

The most important principle of story mapping is narrative flow. When you read across the top of the map (the backbone), you should be able to narrate the user's complete journey:

"First, the user signs up by entering their email and setting a password. Then they set up their profile by adding a photo and bio. Then they use the core feature by creating a widget, editing it, and sharing it."

This narrative test ensures:
- No critical activities are missing
- Activities are in a logical sequence
- The map covers the end-to-end experience, not just one feature

## Common Mistakes

| Mistake | Problem | Fix |
|---------|---------|-----|
| Backbone too detailed | Map becomes overwhelming, hard to see the big picture | Consolidate tasks, use sub-maps for complex areas |
| No persona focus | Stories are generic, not grounded in user needs | Start every mapping session by naming the persona |
| Missing activities | Map covers product features but not the full user journey | Include pre-product and post-product activities |
| Stories not prioritized | All stories at the same level, no release slicing possible | Force vertical ordering, draw release lines |
| Map created once, never updated | Becomes stale and unused | Review and update the map every sprint or planning cycle |
