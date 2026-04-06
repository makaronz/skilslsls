# Persona Templates & Formats

Comprehensive guide to persona formats, structural templates, presentation styles, and practical examples for creating personas that drive design decisions.

---

## Persona Format Overview

Different persona formats serve different audiences and purposes. Choose the format that best fits your team's needs and the decisions the persona needs to support.

### Format Comparison

| Format | Best For | Detail Level | Time to Create | Shelf Life |
|--------|---------|-------------|---------------|------------|
| **Lean Persona** | Agile teams, early-stage | Low | 1–2 hours | 1–3 months |
| **Standard Persona** | Product teams, design | Medium | 4–8 hours | 6–12 months |
| **Comprehensive Persona** | Enterprise, long-term strategy | High | 2–5 days | 12–24 months |
| **Proto-Persona** | Hypothesis validation | Minimal | 30 min | Until research validates |
| **Jobs-to-be-Done Persona** | Innovation, feature design | Medium | 4–6 hours | 6–12 months |
| **Data-Driven Persona** | Analytics-heavy orgs | High | 1–2 weeks | 6–12 months |

---

## Proto-Persona Template

Proto-personas are assumption-based personas created collaboratively before research. They serve as hypotheses to be validated through user research.

### When to Use
- Project kickoff with no existing research
- Workshop activity to align team assumptions
- Basis for planning research recruitment

### Template

```markdown
## Proto-Persona: [Name]

### Quick Sketch
[Hand-drawn or simple avatar]

### Demographics (Assumed)
- Role: [Job title]
- Age range: [Range]
- Technical skill: [Low / Medium / High]

### Goals (Top 3)
1. [Primary goal]
2. [Secondary goal]
3. [Tertiary goal]

### Pain Points (Top 3)
1. [Primary frustration]
2. [Secondary frustration]
3. [Tertiary frustration]

### Behaviors (Assumed)
- [How they currently solve the problem]
- [Tools they use]
- [Frequency of task]

### Open Questions
- [What we need to validate through research]
- [Assumptions we're least confident about]
```

**Critical rule:** Proto-personas must be clearly labeled as assumption-based and scheduled for validation.

---

## Lean Persona Template

Lean personas focus on actionable attributes — the minimum information needed to make design decisions.

### Template

```markdown
## [Persona Name] — [One-Line Role Description]

**Segment:** [User segment this persona represents]
**Data Source:** [Research methods used]

### Context
[2–3 sentences: Who is this person? What is their situation?]

### Goals
| Priority | Goal | Success Metric |
|----------|------|----------------|
| P1 | [Primary goal] | [How they measure success] |
| P2 | [Secondary goal] | [How they measure success] |
| P3 | [Tertiary goal] | [How they measure success] |

### Frustrations
1. **[Frustration]** — [Impact on their work/life]
2. **[Frustration]** — [Impact on their work/life]
3. **[Frustration]** — [Impact on their work/life]

### Key Behaviors
- [Behavior pattern with frequency]
- [Tool/channel preference]
- [Decision-making pattern]

### Design Implications
- [What this means for our product]
- [Feature/UX decisions this persona drives]
```

---

## Standard Persona Template

The most commonly used format. Balances depth with readability.

### Template

```markdown
## [Full Name]
**[Job Title] at [Company Type]**

> "[A direct quote from research that captures their essence]"

### Demographics
| Attribute | Value |
|-----------|-------|
| Age | [Age or range] |
| Location | [City/Region] |
| Education | [Degree/Level] |
| Experience | [Years in role] |
| Company Size | [Range] |
| Industry | [Primary industry] |
| Tech Savviness | [████░ 4/5] |

### Bio
[3–4 paragraph narrative describing this person's professional life,
how they approach their work, what motivates them, and what their
typical day looks like. Written in third person, present tense.
Ground in research findings but make it human and relatable.]

### Goals
1. **[Primary Goal]** — [Why this matters to them]
2. **[Secondary Goal]** — [Why this matters to them]
3. **[Tertiary Goal]** — [Why this matters to them]

### Pain Points
1. **[Pain Point]** (Severity: High)
   - [Detailed description of the frustration]
   - [Current workaround, if any]
2. **[Pain Point]** (Severity: Medium)
   - [Description]
   - [Workaround]
3. **[Pain Point]** (Severity: Low)
   - [Description]

### Behaviors & Patterns
- **Workflow:** [How they approach their primary task]
- **Tools:** [Software, platforms, devices they use regularly]
- **Information Sources:** [Where they go for answers]
- **Decision Process:** [How they evaluate options and make choices]
- **Collaboration:** [Who they work with, how they communicate]

### Motivations
- [What drives them professionally]
- [What they value in tools/products]
- [What would make them recommend a product]

### Scenario
[A specific, realistic scenario where this persona encounters your
product or the problem your product solves. Include context, trigger,
action, and outcome. 3–5 sentences.]

### Influence on Design
| Design Decision | Persona Need | Priority |
|----------------|-------------|----------|
| [Feature/UX choice] | [What need it addresses] | High |
| [Feature/UX choice] | [What need it addresses] | Medium |
| [Feature/UX choice] | [What need it addresses] | Low |
```

---

## Comprehensive Persona Template

For enterprise products, long-term strategy, or when multiple teams reference the same personas.

### Template Structure

```markdown
## [Full Name]
**Archetype: [The Efficient Manager / The Technical Explorer / etc.]**

### Identity
| Attribute | Detail |
|-----------|--------|
| Full Name | [Name] |
| Age | [Age] |
| Location | [City, Country] |
| Job Title | [Title] |
| Company | [Type/Size description] |
| Reports To | [Role] |
| Team Size | [Number] |
| Income Range | [Range] |
| Education | [Degree, Institution type] |

### Quote
> "[Research-based quote that captures their core attitude]"

### Narrative Bio
[4–6 paragraphs covering their background, career path, current role,
daily challenges, personal motivations, and relationship with technology.
This should read like a character study grounded in research data.]

### A Day in the Life
| Time | Activity | Tools | Pain Points |
|------|----------|-------|-------------|
| 8:00 AM | Check email, triage tasks | Gmail, Slack | Information overload |
| 9:00 AM | Team standup | Zoom | Meetings eat into productive time |
| 10:00 AM | [Primary task] | [Tool] | [Specific frustration] |
| ... | ... | ... | ... |

### Goals & Motivations

**Professional Goals:**
1. [Goal with measurable outcome]
2. [Goal with measurable outcome]

**Personal Motivations:**
1. [What drives them beyond work metrics]
2. [Values and professional identity]

**Anti-Goals (What They Want to Avoid):**
1. [What they actively try to prevent]
2. [Outcomes they fear]

### Pain Points & Frustrations

| Pain Point | Severity | Frequency | Current Workaround | Opportunity |
|-----------|----------|-----------|-------------------|-------------|
| [Pain] | Critical | Daily | [Workaround] | [How we solve it] |
| [Pain] | High | Weekly | [Workaround] | [How we solve it] |
| [Pain] | Medium | Monthly | [Workaround] | [How we solve it] |

### Technology Profile
- **Devices:** [Primary and secondary devices]
- **Operating System:** [OS preference]
- **Browser:** [Primary browser]
- **Key Software:** [Top 5 tools they use daily]
- **Adoption Style:** [Early adopter / Mainstream / Late majority]
- **Learning Preference:** [Self-taught / Training / Documentation]

### Decision-Making Process

```
Awareness → Research → Evaluation → Decision → Adoption
[Trigger]   [Sources]  [Criteria]   [Approvers] [Onboarding]
```

**Key Decision Criteria:**
1. [Most important factor in product selection]
2. [Second most important]
3. [Third most important]

**Influencers:**
- [Who influences their decisions]
- [What content they consume]
- [Communities they participate in]

### Scenarios

**Scenario 1: [Primary Use Case]**
[Detailed scenario with context, trigger, steps, and desired outcome]

**Scenario 2: [Secondary Use Case]**
[Detailed scenario]

**Scenario 3: [Edge Case]**
[Detailed scenario]

### Design Principles for This Persona
1. [Principle derived from persona needs]
2. [Principle derived from persona needs]
3. [Principle derived from persona needs]

### Metrics That Matter to This Persona
| Metric | Target | Why It Matters |
|--------|--------|----------------|
| [Metric] | [Target] | [Reason] |
| [Metric] | [Target] | [Reason] |
```

---

## Jobs-to-be-Done (JTBD) Persona Format

Focuses on the jobs users hire your product to do, rather than demographic attributes.

### Template

```markdown
## Job Performer: [Name]

### Core Job
**When** [situation/trigger],
**I want to** [job/action],
**So I can** [desired outcome].

### Job Map
| Step | Functional Job | Emotional Job | Social Job |
|------|---------------|---------------|------------|
| 1. Define | [What they do] | [How they want to feel] | [How they want to appear] |
| 2. Locate | [What they do] | [How they want to feel] | [How they want to appear] |
| 3. Prepare | [What they do] | [How they want to feel] | [How they want to appear] |
| 4. Execute | [What they do] | [How they want to feel] | [How they want to appear] |
| 5. Monitor | [What they do] | [How they want to feel] | [How they want to appear] |
| 6. Resolve | [What they do] | [How they want to feel] | [How they want to appear] |

### Hiring Criteria
What makes this persona "hire" a solution:
1. [Criterion] — Importance: [High/Med/Low], Current satisfaction: [High/Med/Low]
2. [Criterion] — Importance: [High/Med/Low], Current satisfaction: [High/Med/Low]
3. [Criterion] — Importance: [High/Med/Low], Current satisfaction: [High/Med/Low]

### Switching Triggers
- [What would make them switch from current solution]
- [Threshold of dissatisfaction that triggers search]

### Competing Solutions
| Solution | Strengths | Weaknesses | When Chosen |
|----------|----------|------------|-------------|
| [Competitor/Alternative] | [Strength] | [Weakness] | [Situation] |
| [DIY / Manual] | [Strength] | [Weakness] | [Situation] |
| [Do Nothing] | [Strength] | [Weakness] | [Situation] |
```

---

## Persona Presentation Formats

### One-Page Poster
Best for printing and posting in team workspaces.

**Layout:**
```
┌────────────────────────────────────────┐
│ [Photo]  NAME, Title           Quote  │
├──────────┬───────────────┬─────────────┤
│ BIO      │ GOALS           │ PAIN POINTS │
│          │ 1.              │ 1.          │
│          │ 2.              │ 2.          │
│          │ 3.              │ 3.          │
├──────────┴───────────────┴─────────────┤
│ BEHAVIORS        │ DESIGN IMPLICATIONS       │
│ • ...            │ • ...                     │
│ • ...            │ • ...                     │
└──────────────────┴──────────────────────┘
```

### Persona Card (Quick Reference)
For sprint boards and quick design reviews.

```markdown
## [Name] — [Archetype Label]
🎯 Goal: [Primary goal in one sentence]
🔥 Pain: [Primary frustration in one sentence]
💡 Insight: [Key behavioral insight]
→ Design Implication: [What to build/prioritize]
```

### Empathy Map Format
Helps teams internalize persona perspectives.

```
          THINKS                    FEELS
     [Thoughts, beliefs,       [Emotions, concerns,
      considerations]           anxieties, hopes]
              \                    /
               \                  /
        ┌──────────────────┐
        │   [PERSONA NAME]  │
        └──────────────────┘
               /                  \
              /                    \
          SAYS                    DOES
     [Quotes, statements,      [Actions, behaviors,
      expressed needs]          observable patterns]

              PAINS                  GAINS
     [Frustrations, fears,     [Wants, needs, goals,
      obstacles, risks]         measures of success]
```

---

## Persona Maintenance & Governance

### Keeping Personas Current

| Activity | Frequency | Owner |
|----------|-----------|-------|
| Review analytics for behavioral shifts | Monthly | Product/UX |
| Validate with 2–3 user interviews | Quarterly | UX Research |
| Full persona refresh (new research) | Annually | UX Research |
| Update after major product changes | As needed | Product |
| Retire personas that no longer apply | As needed | Product |

### Persona Governance Checklist
- [ ] Each persona has a designated owner
- [ ] Personas are stored in a shared, accessible location
- [ ] Last-validated date is displayed on each persona
- [ ] Research evidence is linked or referenced
- [ ] Retired personas are archived, not deleted
- [ ] New team members receive persona onboarding
- [ ] Design reviews reference specific persona needs

### Signs Your Personas Need Updating
- User feedback contradicts persona assumptions
- Analytics show new behavioral segments not represented
- Product has pivoted to serve different market
- Conversion or retention patterns have shifted significantly
- Team members no longer reference personas in decisions
- More than 12 months since last validation

---

## Anti-Patterns to Avoid

1. **Persona as decoration** — Beautiful documents that nobody reads. Fix: Link personas to specific design decisions.
2. **Too many personas** — More than 5 primary personas dilutes focus. Fix: Limit to 3–5 primary, 1–2 secondary.
3. **Demographic-only personas** — Descriptions without behavioral insights. Fix: Lead with goals and behaviors.
4. **Assumption-based "research"** — Personas built from stakeholder opinions. Fix: Ground in actual user data.
5. **Static personas** — Created once, never updated. Fix: Schedule quarterly reviews.
6. **Generic personas** — So broad they describe everyone (and thus no one). Fix: Include specific, differentiating details.
7. **Missing negative personas** — Not defining who you're NOT designing for. Fix: Create at least one exclusion persona.
