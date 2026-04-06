# Research Reporting & Insights Communication

Guide to structuring research reports, communicating findings to diverse stakeholders, and translating insights into actionable design decisions.

---

## Report Formats by Audience

Different stakeholders need different levels of detail. Choose the right format based on who will consume the findings.

### Format Selection Guide

| Format | Audience | Length | Detail Level | When to Use |
|--------|----------|--------|-------------|-------------|
| **Executive Summary** | C-suite, sponsors | 1 page | Key findings + recommendations only | Steering committees, stakeholder updates |
| **Research Deck** | Product team, design leads | 10–20 slides | Findings, themes, evidence, recommendations | Sprint planning, design reviews |
| **Full Report** | Research team, documentation | 10–30 pages | Complete methodology, data, analysis | Research repository, compliance |
| **Insight Cards** | Designers, engineers | 1 card per insight | Single insight with evidence + action | Kanban boards, design sprints |
| **Video Highlights** | All stakeholders | 3–5 min | Curated participant clips | Empathy building, kickoff meetings |
| **Research Nuggets** | Slack/Teams channels | 1–2 sentences | Single compelling finding | Ongoing awareness, culture building |

---

## Executive Summary Structure

The one-page format that busy stakeholders actually read:

```
## Research Summary: [Project Name]
### [Date] | [Method] | [N] Participants

### Why We Did This Research
[1–2 sentences on the business question that prompted this study]

### What We Found
1. **[Finding 1 headline]**: [One sentence with key data point]
2. **[Finding 2 headline]**: [One sentence with key data point]
3. **[Finding 3 headline]**: [One sentence with key data point]

### What This Means
[2–3 sentences interpreting findings in business context — impact on
revenue, retention, user satisfaction, or competitive position]

### What We Recommend
| Priority | Recommendation | Expected Impact |
|----------|---------------|-----------------|
| Do Now | [Action item] | [Measurable outcome] |
| Do Next | [Action item] | [Measurable outcome] |
| Explore | [Action item] | [Measurable outcome] |

### Confidence Level
[High/Medium/Low] — Based on [sample size, method rigor, data consistency]
```

---

## Research Deck Framework

The 15-slide research presentation that tells a complete story:

| Slide # | Content | Purpose | Time |
|---------|---------|---------|------|
| 1 | Title + key stat | Hook attention | 30s |
| 2 | Research objectives and questions | Set context | 1 min |
| 3 | Methodology and participants | Build credibility | 1 min |
| 4 | Participant snapshot (demographics, segments) | Humanize the data | 1 min |
| 5–6 | Theme 1: Finding + evidence (quotes, data) | Core finding | 2 min |
| 7–8 | Theme 2: Finding + evidence | Core finding | 2 min |
| 9–10 | Theme 3: Finding + evidence | Core finding | 2 min |
| 11 | Surprise finding or contradiction | Provoke thinking | 1 min |
| 12 | Insight summary with severity | Crystallize meaning | 1 min |
| 13 | Recommendations with prioritization | Drive action | 2 min |
| 14 | Open questions and next steps | Set follow-up | 1 min |
| 15 | Appendix: detailed data, methodology notes | Reference (skip in live presentation) | — |

### Slide Design Principles for Research Decks

- **One finding per slide** — avoid information overload
- **Lead with the insight, support with data** — don't make stakeholders interpret raw data
- **Use direct participant quotes** — builds empathy and credibility
- **Include participant video clips** — 10–30 second clips are more powerful than any chart
- **Show severity/frequency** — "3 of 12 participants" is better than "some users"
- **Use before/after or comparison layouts** — for usability testing findings

---

## Stakeholder Communication Strategies

### Tailoring the Message

| Stakeholder | They Care About | Lead With | Avoid |
|-------------|----------------|----------|-------|
| **Executives** | Business impact, ROI, risk | Revenue/retention impact, competitive advantage | Methodology details, jargon |
| **Product Managers** | Priorities, roadmap impact, user needs | Actionable insights with severity ranking | Open-ended findings without direction |
| **Designers** | User behavior, pain points, opportunities | Specific UX issues with context | Abstract statistics without user stories |
| **Engineers** | Feasibility, edge cases, technical requirements | Clear requirements, error states, data needs | Vague "make it better" recommendations |
| **Marketing** | User language, motivations, personas | Quotes, segments, messaging insights | Technical usability findings |
| **Customer Support** | Pain points, workarounds, FAQ implications | Common issues with frequency data | Strategic recommendations |

### Presenting Negative Findings

Research often reveals problems. Frame them constructively:

| Instead of... | Say... |
|--------------|--------|
| "The design failed" | "We identified 3 specific opportunities to improve task completion" |
| "Users hated the navigation" | "Users expect to find [feature] under [location], creating an opportunity to restructure" |
| "Nobody could complete the task" | "Task completion was 20% — we've identified the two specific steps where users need more guidance" |
| "The feature is useless" | "Current usage is low because users don't discover the feature — awareness is the bottleneck" |

### Handling Stakeholder Pushback

| Pushback | Response Strategy |
|----------|------------------|
| "That's just 8 people" | Explain qualitative research validity: patterns from 5+ users are reliable for identifying issues; reference Nielsen's research |
| "Our users are different" | Describe screening criteria and how participants were selected to match the user base |
| "We already knew that" | Reframe: "This confirms the hypothesis with evidence — now we can quantify the severity and prioritize" |
| "We can't change that" | Separate insight (what we learned) from recommendation (what to do); offer alternative solutions |
| "What about [edge case]?" | Acknowledge scope limitations; add to research backlog if it's important |

---

## Actionable Insights Framework

### Converting Findings to Action

Every insight should map to a concrete next step:

| Finding Type | Insight Format | Action Type | Example |
|-------------|---------------|------------|--------|
| **Usability issue** | Users fail to [task] because [reason] | Design fix with severity | Redesign form layout to show progress |
| **Unmet need** | Users need [capability] to [goal] | Feature opportunity | Add bulk export functionality |
| **Mental model mismatch** | Users expect [X] but encounter [Y] | Information architecture change | Rename "Workspace" to "Projects" |
| **Workflow gap** | Users work around [limitation] by [method] | Process/feature improvement | Enable cross-project file linking |
| **Emotional pain** | Users feel [emotion] when [situation] | Experience redesign | Add confirmation + undo instead of warning dialogs |

### Insight-to-Backlog Pipeline

```
Insight → Design Opportunity → User Story → Backlog Item → Sprint
```

| Stage | Responsible | Output |
|-------|------------|--------|
| Insight documented | Researcher | Insight card with evidence |
| Design opportunity defined | Researcher + Designer | HMW statement, opportunity brief |
| User story written | Product Manager | Story with acceptance criteria |
| Backlog item created | Product Manager | Sized, prioritized ticket |
| Sprint planned | Team | Work committed to sprint |

### Severity Classification for Usability Findings

| Severity | Definition | Action Required | Timeline |
|----------|-----------|-----------------|----------|
| **Critical (S1)** | User cannot complete core task; data loss risk | Immediate fix | This sprint |
| **Major (S2)** | User can complete task but with significant difficulty | High priority | Next 1–2 sprints |
| **Minor (S3)** | User is slowed or annoyed but can complete task | Normal priority | Backlog |
| **Enhancement (S4)** | Opportunity for improvement; not a current pain | Low priority | Future consideration |

---

## Research Repository Management

### Why Maintain a Repository

- **Avoid duplicate research** — check what's already been studied
- **Build institutional knowledge** — insights compound over time
- **Track insight lifecycle** — from discovery to implementation
- **Enable cross-project patterns** — find themes across multiple studies

### Repository Structure

```
Research Repository/
├── Studies/
│   ├── [YYYY-MM] Study Name/
│   │   ├── Research Brief
│   │   ├── Raw Data (tagged, transcribed)
│   │   ├── Analysis (affinity maps, themes)
│   │   ├── Report (summary + full)
│   │   └── Insight Cards
├── Insights/
│   ├── Active Insights (unaddressed)
│   ├── In Progress (being designed/built)
│   └── Resolved (implemented and validated)
├── Personas/
│   └── [Current persona documents]
├── Journey Maps/
│   └── [Current journey maps]
└── Templates/
    ├── Research Brief Template
    ├── Interview Guide Template
    ├── Insight Card Template
    └── Report Template
```

### Insight Card Template

```
## Insight: [Short descriptive title]

### Statement
[User segment] needs [need] because [motivation], but currently
[barrier] which results in [consequence].

### Evidence
- [Quote or observation] — P3, P7, P11
- [Data point] — Analytics, Survey
- Frequency: [X of Y participants]

### Severity: [Critical / Major / Minor / Enhancement]

### Design Opportunity
[HMW statement or specific recommendation]

### Status: [New / In Discussion / In Design / Shipped / Validated]

### Source Study
[Study name, date, researcher]
```

---

## Measuring Research Impact

### Research Effectiveness Metrics

| Metric | How to Measure | Target |
|--------|---------------|--------|
| **Insight activation rate** | % of insights that lead to product changes | >60% |
| **Time to action** | Days from insight to backlog item | <14 days |
| **Stakeholder satisfaction** | Post-presentation survey (1–5) | >4.0 |
| **Research utilization** | % of sprints informed by research | >70% |
| **Repeat request rate** | Stakeholders requesting more research | Increasing trend |
| **Decision confidence** | Team confidence in direction (survey) | >4.0/5.0 |

### Demonstrating ROI of Research

Connect research outcomes to business metrics:

| Research Input | Design Change | Business Outcome |
|---------------|--------------|------------------|
| Usability test revealed checkout confusion | Simplified 5-step checkout to 3 steps | Cart abandonment reduced 18% |
| Interviews found users need bulk actions | Added multi-select and bulk operations | Support tickets for manual requests dropped 40% |
| Survey showed feature discovery problem | Added contextual tooltips and onboarding | Feature adoption increased 25% in 30 days |

---

## Reporting Anti-Patterns to Avoid

| Anti-Pattern | Problem | Better Approach |
|-------------|---------|----------------|
| **Data dump** | 50-page report nobody reads | Layered reporting: 1-page summary → deck → full report |
| **No recommendations** | Findings without direction | Every insight maps to at least one recommendation |
| **Delayed reporting** | Report arrives weeks after research | Share preliminary findings within 48 hours |
| **Jargon-heavy** | "Heuristic evaluation revealed poor affordance signifiers" | "Users couldn't tell which elements were clickable" |
| **Missing evidence** | Claims without supporting data | Every finding includes frequency + example quotes |
| **One-time artifact** | Report is created and forgotten | Living repository with tracked insight status |
