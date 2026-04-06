# Feedback Collection & Synthesis

Methods for collecting design feedback, synthesis techniques for organizing input, and frameworks for converting feedback into prioritized action items.

---

## Feedback Collection Methods

### Synchronous Collection Methods

| Method | Best For | Participants | Setup Effort | Depth |
|--------|---------|-------------|-------------|-------|
| **Live critique session** | Team alignment, broad feedback | 3–8 designers | Medium | High |
| **Pair design review** | Quick focused feedback | 2 people | Low | Medium |
| **Stakeholder presentation** | Business alignment, approval | 2–6 stakeholders | High | Medium |
| **Usability testing** | Real user validation | 5–8 users per round | High | Very High |
| **Design sprint review** | Sprint-level check-in | Sprint team | Low | Medium |

### Asynchronous Collection Methods

| Method | Best For | Response Rate | Depth | Tools |
|--------|---------|-------------|-------|-------|
| **Figma comments** | Contextual, screen-specific feedback | High (easy to use) | Medium | Figma |
| **Loom walkthroughs** | Detailed design explanations before async review | Medium | High | Loom + comments |
| **Structured survey** | Gathering specific ratings across many reviewers | Medium | Varies | Google Forms, Typeform |
| **Annotation boards** | Collecting visual feedback on specific screens | High | Medium | Miro, FigJam |
| **Slack/Teams thread** | Quick reactions, informal feedback | High | Low | Slack, Teams |
| **Email review** | Formal stakeholder feedback | Low | Medium | Email + document |

### Feedback Collection Templates

**Structured Review Survey:**

```markdown
## Design Feedback Form

Design: [Name] | Version: [X] | Review deadline: [Date]

### Overall Impression
- Rate the overall quality (1–10): ___
- First word that comes to mind: ___
- Would this design meet user needs? (Yes / Partially / No)

### Specific Dimensions
Rate each 1–10 and provide one comment:

1. Visual Design: ___ 
   Comment: ___

2. Usability / UX: ___
   Comment: ___

3. Consistency: ___
   Comment: ___

4. Responsiveness: ___
   Comment: ___

5. Accessibility: ___
   Comment: ___

### Open Feedback
- What works best about this design?
- What needs the most improvement?
- Any concerns about feasibility or implementation?
- Additional comments:
```

**Figma Comment Protocol:**

To ensure Figma comments are useful, establish conventions:

| Prefix | Meaning | Example |
|--------|---------|--------|
| 🟢 STRENGTH | Something that works well | "🟢 STRENGTH: Great visual hierarchy on this card" |
| 🔴 ISSUE | Something that needs fixing | "🔴 ISSUE: Contrast ratio on this text is only 3.1:1" |
| 🟡 QUESTION | Clarification needed | "🟡 QUESTION: What happens when the list is empty?" |
| 🟣 SUGGESTION | Alternative approach | "🟣 SUGGESTION: Consider a stepper instead of tabs here" |
| ⚪ NITPICK | Minor polish item | "⚪ NITPICK: 2px misalignment on the right edge" |

---

## Feedback Synthesis Techniques

### Affinity Mapping

Organize raw feedback into meaningful groups:

**Process:**
1. Collect all feedback items as individual notes (sticky notes or cards)
2. Spread all notes visible on a board
3. Silently group similar items together (no talking during grouping)
4. Name each group with a theme label
5. Identify the largest and most critical groups
6. Prioritize themes by frequency and severity

**Example grouping:**

```
Theme: "Navigation Confusion" (7 items)
  - "Can't find settings"
  - "Back button behavior unexpected"
  - "Breadcrumbs would help"
  - "Nav labels are ambiguous"
  - "Mobile menu is hard to discover"
  - "Too many clicks to reach profile"
  - "Search should be more prominent"

Theme: "Typography Issues" (4 items)
  - "Body text feels small on desktop"
  - "Heading levels not differentiated enough"
  - "Line length too wide on large screens"
  - "Caption text hard to read on dark backgrounds"
```

### Feedback Impact Matrix

Map each feedback item on two axes to determine priority:

```
                    HIGH FREQUENCY
                         |
    Critical Issues      |      Common Polish
    (Fix immediately)    |      (Batch and fix)
                         |
  HIGH SEVERITY ---------+--------- LOW SEVERITY
                         |
    Rare but Serious     |      Minor Nitpicks
    (Schedule fix)       |      (Fix if time allows)
                         |
                    LOW FREQUENCY
```

| Quadrant | Action | Timeline |
|----------|--------|----------|
| High Severity + High Frequency | Fix immediately — these block users | Current iteration |
| High Severity + Low Frequency | Schedule for next iteration — serious but rare | Next iteration |
| Low Severity + High Frequency | Batch and fix — polish items many people notice | This or next iteration |
| Low Severity + Low Frequency | Backlog — fix if time allows | Future iteration |

### Contradiction Resolution

When feedback conflicts (common with multiple reviewers):

| Conflict Type | Resolution Strategy | Example |
|--------------|--------------------|---------|
| **Preference vs. Preference** | Use data or testing to decide | "Make the CTA blue" vs. "Make it green" → A/B test |
| **Preference vs. Best Practice** | Follow best practice, explain rationale | "Remove the focus ring" vs. WCAG requires focus indicators → Keep focus ring |
| **Expert vs. Expert** | Defer to domain expert or test with users | UX says simplify, PM says add features → User test both approaches |
| **Stakeholder vs. User Data** | Present data, let stakeholder decide with context | Exec wants hero image, data shows users skip it → Present data, propose compromise |

**Resolution framework:**
1. Identify the conflict explicitly
2. Gather evidence for each position
3. Check against project goals and user needs
4. If still unresolved, propose a test or experiment
5. Document the decision and rationale

### Feedback Weighting

Not all feedback is equal. Weight feedback based on source credibility:

| Source | Weight | Rationale |
|--------|--------|-----------|
| User testing findings | ★★★★★ | Direct evidence of real user behavior |
| Analytics / data | ★★★★★ | Objective, large-sample evidence |
| Accessibility audit | ★★★★ | Compliance-driven, legal implications |
| Domain expert review | ★★★★ | Deep expertise in specific area |
| Peer designer critique | ★★★ | Professional perspective, may have bias |
| Product manager input | ★★★ | Business context, but may lack design expertise |
| Engineering feasibility | ★★★ | Implementation reality, but may default to "hard" |
| Stakeholder opinion | ★★ | Important for alignment, but may not represent users |
| Individual preference | ★ | Personal taste, lowest weight unless backed by evidence |

---

## Converting Feedback to Action Items

### Feedback-to-Action Pipeline

```
Raw Feedback → Categorize → Synthesize → Prioritize → Action Items → Iteration Plan
```

**Step 1: Categorize** each feedback item:

| Category | Examples |
|----------|--------|
| Visual Design | Color, typography, layout, imagery, polish |
| UX / Interaction | Flows, navigation, feedback, errors, states |
| Content | Copy, labels, microcopy, help text |
| Accessibility | Contrast, keyboard, screen reader, targets |
| Technical | Performance, responsive, animation, feasibility |
| Business | Alignment, requirements, stakeholder concerns |

**Step 2: Synthesize** into themes (use affinity mapping above)

**Step 3: Prioritize** using the Impact/Effort matrix:

| Priority | Impact | Effort | Action |
|----------|--------|--------|--------|
| P0 — Critical | Blocks users or fails compliance | Any | Fix immediately |
| P1 — High | Significantly improves quality | Low–Medium | Current iteration |
| P2 — Medium | Noticeable improvement | Medium | Next iteration |
| P3 — Low | Polish and refinement | Low | Batch with other items |
| P4 — Backlog | Nice to have | High | Future consideration |

**Step 4: Write action items** with clear specifications:

```markdown
## Action Item Template

### [Action Title]
- **Source**: [Which feedback/theme this addresses]
- **Category**: [Visual / UX / Accessibility / Content / Technical]
- **Priority**: [P0–P4]
- **Current State**: [What exists now — be specific]
- **Target State**: [What it should be — be specific]
- **Acceptance Criteria**: [How to verify the fix is correct]
- **Estimated Effort**: [Hours]
- **Owner**: [Who will implement]
- **Deadline**: [When it should be done]
```

### Action Item Examples

```markdown
### Increase body text size
- **Source**: 4 reviewers noted body text feels small; typography theme
- **Category**: Visual Design / Typography
- **Priority**: P1
- **Current State**: Body text is 14px/1.4 line height
- **Target State**: Body text 16px/1.6 line height
- **Acceptance Criteria**: All body text updated, no layout breakage, readable on mobile
- **Estimated Effort**: 2 hours
- **Owner**: Designer
- **Deadline**: Sprint 12

### Add inline error messages to form
- **Source**: Usability testing — 3/5 users missed error summary at page top
- **Category**: UX / Accessibility
- **Priority**: P0
- **Current State**: Errors shown in summary banner at page top
- **Target State**: Inline errors next to each field + summary retained
- **Acceptance Criteria**: Each invalid field shows error below it, aria-describedby links error to field
- **Estimated Effort**: 4 hours
- **Owner**: Designer + Developer
- **Deadline**: This sprint
```

---

## Feedback Tracking Systems

### Feedback Log Template

Maintain a running log across all reviews:

```markdown
## Feedback Log: [Project Name]

| # | Date | Source | Screen | Feedback | Category | Priority | Status | Action Taken |
|---|------|--------|--------|----------|----------|----------|--------|--------------|
| 1 | Mar 1 | Team critique | Dashboard | Cards need more breathing room | Visual | P2 | Done | Increased padding 16→24px |
| 2 | Mar 1 | Team critique | Dashboard | Loading state missing | UX | P1 | In Progress | Designing skeleton loader |
| 3 | Mar 5 | Stakeholder | Nav | Add search to top bar | UX | P2 | Planned | Sprint 13 |
| 4 | Mar 8 | A11y audit | Forms | Labels missing on 3 fields | A11y | P0 | Done | Labels added |
```

### Feedback Metrics

Track feedback patterns over time:

| Metric | What It Tells You | Healthy Range |
|--------|-------------------|---------------|
| Issues per review | Design maturity and review thoroughness | 5–15 (fewer over time) |
| P0 issues per review | Critical quality gaps | 0–2 (should be 0 by handoff) |
| Feedback implementation rate | Team responsiveness | > 80% of P0–P2 items addressed |
| Repeat issues across reviews | Whether fixes are holding | < 10% repeat rate |
| Time from feedback to fix | Iteration speed | < 1 sprint for P0–P1 |
| Feedback source diversity | Review coverage breadth | Input from 3+ sources |
