# Review Process & Facilitation

Design review types, facilitation techniques, meeting structures, and best practices for running effective design reviews.

---

## Design Review Types

### Review Type Selection Guide

| Review Type | Purpose | Participants | Duration | When to Use |
|-------------|---------|-------------|----------|-------------|
| **Self-Review** | Designer checks own work against rubric | Solo | 15–30 min | Before any peer review |
| **Pair Review** | Quick feedback from one peer | 2 designers | 20–30 min | During active iteration |
| **Team Critique** | Broad feedback from design team | 3–8 designers | 45–60 min | After completing a design phase |
| **Cross-Functional Review** | Input from engineering, PM, QA | 4–10 mixed roles | 30–60 min | Before development handoff |
| **Stakeholder Review** | Alignment with business goals | Designer + stakeholders | 30–45 min | At milestones or decision points |
| **Expert Review** | Deep evaluation by specialist | 1–2 specialists | 30–60 min | For accessibility, performance, brand |
| **Heuristic Evaluation** | Systematic usability inspection | 3–5 evaluators | 1–2 hours each | After major design completion |

### Review Cadence Recommendations

| Project Phase | Recommended Reviews | Frequency |
|--------------|--------------------|-----------|
| Discovery / Exploration | Pair reviews, informal team share | 2–3× per week |
| Wireframing | Team critique (structure focus) | End of each sprint |
| Visual Design | Pair reviews + team critique | Weekly |
| Prototyping | Cross-functional review | Bi-weekly |
| Pre-Handoff | Full team critique + stakeholder review | Once before handoff |
| Post-Launch | Expert review + heuristic evaluation | Within 2 weeks of launch |

---

## Facilitation Techniques

### The "I Like, I Wish, What If" Method

A structured feedback framework that encourages balanced critique:

| Category | Purpose | Example |
|----------|---------|--------|
| **I Like** | Identify strengths to preserve | "I like how the card hierarchy guides the eye from image to title to CTA" |
| **I Wish** | Express desired improvements | "I wish the error states were more prominent — the red text is easy to miss" |
| **What If** | Propose creative alternatives | "What if we used progressive disclosure for the advanced settings?" |

**Facilitation steps:**
1. Present the design with context (2–3 minutes)
2. Silent observation period (2 minutes)
3. Each participant writes I Like / I Wish / What If notes (5 minutes)
4. Share and discuss, one category at a time (20–30 minutes)
5. Facilitator synthesizes themes and action items (5 minutes)

### The "Red Team / Blue Team" Method

Assign opposing roles for thorough evaluation:

| Role | Focus | Mindset |
|------|-------|---------|
| **Blue Team** (Defenders) | Identify and articulate design strengths and rationale | "This works because..." |
| **Red Team** (Challengers) | Find weaknesses, edge cases, and potential failures | "This breaks when..." |

**Process:**
1. Divide participants into two groups
2. Blue Team presents design strengths (5 minutes)
3. Red Team presents challenges and concerns (5 minutes)
4. Open discussion to resolve identified issues (15–20 minutes)
5. Agree on which Red Team findings require action

### Silent Critique (Dot Voting)

Reduces groupthink and ensures equal participation:

1. Display design screens on wall or shared board
2. Each participant places colored dots silently:
   - 🟢 Green dot = This works well
   - 🟡 Yellow dot = I have a question about this
   - 🔴 Red dot = This needs improvement
3. Add sticky notes with brief comments next to dots
4. After silent phase, discuss areas with most red/yellow dots first
5. Green-heavy areas are noted as strengths to preserve

**Benefits:** Prevents anchoring bias, ensures quieter team members contribute equally.

### Structured Question Framework

Guide reviews with specific questions rather than open-ended "what do you think?":

**First Impression Questions:**
- What is the purpose of this screen?
- What action would you take first?
- What draws your attention?
- How does this make you feel?

**Usability Questions:**
- Can you identify how to complete [specific task]?
- Is there anything confusing about this layout?
- What would you expect to happen when you click [element]?
- Where would you look for [specific information]?

**Quality Questions:**
- Does the typography create a clear reading hierarchy?
- Is the spacing consistent and intentional?
- Are all interactive elements clearly identifiable?
- Does this feel complete, or does something seem missing?

**Comparison Questions (for iterations):**
- What improved from the previous version?
- Did anything get worse?
- Does this address the issues from the last review?
- Are we closer to our quality target?

---

## Meeting Structure Templates

### Team Design Critique (45–60 minutes)

```
[0:00–0:05] Setup & Context
  - Facilitator sets ground rules
  - Designer provides context: goals, constraints, target user
  - State what feedback is needed (broad vs. specific)

[0:05–0:10] Silent Observation
  - Participants review designs without discussion
  - Take individual notes

[0:10–0:40] Structured Feedback
  - Walk through screen by screen
  - Use chosen framework (I Like/I Wish/What If, etc.)
  - Facilitator captures themes on shared board
  - Keep feedback specific and actionable

[0:40–0:50] Prioritization
  - Group feedback into themes
  - Dot-vote on most impactful issues
  - Identify must-fix vs. nice-to-fix

[0:50–1:00] Action Items & Next Steps
  - Document agreed-upon changes
  - Assign owners and deadlines
  - Schedule follow-up review if needed
```

### Cross-Functional Review (30–45 minutes)

```
[0:00–0:05] Context Setting
  - Designer presents design goals and user stories being addressed
  - Identify key decisions that need input

[0:05–0:15] Design Walkthrough
  - Walk through primary user flows
  - Highlight interaction specifications
  - Show responsive behavior

[0:15–0:30] Role-Specific Feedback
  - Engineering: feasibility, performance concerns, component reuse
  - Product: alignment with requirements, edge cases, business logic
  - QA: testability, state coverage, error scenarios
  - Each role asks clarifying questions

[0:30–0:40] Decision Making
  - List open questions and decisions
  - Make decisions where possible
  - Document deferred decisions with owners

[0:40–0:45] Next Steps
  - Agree on design changes before handoff
  - Set handoff date
  - Identify any follow-up discussions needed
```

### Quick Pair Review (20–30 minutes)

```
[0:00–0:03] Context
  - What are you solving? What feedback do you need?

[0:03–0:10] Walkthrough
  - Show the design, explain key decisions

[0:10–0:25] Discussion
  - Reviewer asks questions and provides feedback
  - Focus on specific areas requested

[0:25–0:30] Summary
  - Agree on top 3 takeaways
  - Decide if further review is needed
```

---

## Facilitation Best Practices

### Ground Rules for Productive Reviews

1. **Critique the design, not the designer.** Frame feedback about the work, not personal ability.
2. **Be specific.** "The 12px body text is hard to read" is better than "the text is too small."
3. **Explain why.** "The contrast fails AA because it's 3.2:1" rather than just "fix the contrast."
4. **Offer alternatives.** Don't just point out problems — suggest a direction for improvement.
5. **Stay in scope.** Address what was asked for feedback on. Save out-of-scope thoughts for later.
6. **Assume good intent.** Every design decision was made for a reason — ask about it before criticizing.
7. **Equal voice.** Junior and senior opinions are equally valuable in critique.

### Common Facilitation Pitfalls

| Pitfall | Symptoms | Prevention |
|---------|----------|------------|
| **HiPPO effect** | Highest-paid person's opinion dominates | Use silent critique first, then discuss |
| **Design by committee** | Trying to incorporate every opinion | Facilitator synthesizes, designer decides |
| **Solutioning too early** | Jumping to solutions before understanding issues | Ask "what's the problem?" before "what's the fix?" |
| **Scope creep** | Review expands to unrelated areas | Set scope at the start, park off-topic items |
| **Vague feedback** | "It doesn't feel right" without specifics | Require evidence: "What specifically isn't working?" |
| **Negativity spiral** | Focus only on problems, ignoring strengths | Always start with what's working well |

### Remote Review Facilitation

**Tools for remote reviews:**
- Figma comments for async feedback
- Miro/FigJam for collaborative critique boards
- Loom for recorded design walkthroughs (async)
- Zoom/Meet for synchronous critique sessions

**Remote-specific tips:**
- Share designs in advance (15+ minutes before meeting)
- Use screen sharing with presenter control
- Chat channel for parallel comments
- Record sessions for absent team members
- Use timer-boxed activities to maintain energy
- Round-robin feedback to ensure everyone speaks

---

## Review Documentation

### Capturing Review Outcomes

Every review should produce a documented outcome:

```markdown
## Review Record

Date: [Date]
Type: [Team Critique / Cross-Functional / Pair]
Design: [Name, Version]
Participants: [Names and Roles]
Facilitator: [Name]

### Context
- Design goal: [What problem is this solving?]
- Feedback requested: [Specific areas or broad review]

### Key Feedback Themes
1. [Theme]: [Summary of feedback] | Priority: [High/Med/Low]
2. [Theme]: [Summary of feedback] | Priority: [High/Med/Low]
3. [Theme]: [Summary of feedback] | Priority: [High/Med/Low]

### Strengths to Preserve
- [Strength 1]
- [Strength 2]

### Decisions Made
- [Decision 1]: [Rationale]
- [Decision 2]: [Rationale]

### Action Items
| Action | Owner | Deadline | Priority |
|--------|-------|----------|----------|
| [Action] | [Name] | [Date] | [H/M/L] |

### Follow-Up
- Next review date: [Date]
- Open questions: [List]
```
