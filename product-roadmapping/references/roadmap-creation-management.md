# Roadmap Creation and Management

Practical guide for building product roadmaps, choosing formats, and establishing review cadences.

---

## Roadmap Formats

### Now / Next / Later

The most flexible and communication-friendly format:

| Column | Timeframe | Commitment Level | Detail Level |
|--------|-----------|-----------------|-------------|
| Now | Current quarter | High (in progress or committed) | Specific features and initiatives |
| Next | Next quarter | Medium (planned, may shift) | Themes and initiatives |
| Later | 2+ quarters out | Low (directional) | Strategic themes only |

**Advantages**: Avoids false precision, adapts to change, focuses conversation on priorities not dates. **Best for**: Product teams, stakeholder communication, Agile environments.

### Quarterly Theme-Based

Organize by quarter with 2-3 themes per quarter:

| Quarter | Theme | Key Initiatives |
|---------|-------|----------------|
| Q1 | Onboarding Excellence | Setup wizard, video tutorials, health score v1 |
| Q2 | Enterprise Readiness | SSO, RBAC, audit logging, SOC 2 compliance |
| Q3 | Platform Expansion | API v2, webhooks, marketplace foundation |
| Q4 | Growth & Retention | Referral program, advanced analytics, mobile app |

**Advantages**: Provides strategic narrative, easy for leadership to understand. **Best for**: Board presentations, annual planning, go-to-market coordination.

### Timeline Roadmap

Traditional Gantt-style with date ranges:

**Advantages**: Clear delivery expectations, useful for coordinating cross-team dependencies. **Best for**: Teams with hard deadlines, hardware coordination, regulatory compliance. **Risks**: Creates false precision, roadmap becomes a commitment document rather than a strategy tool.

## Building the Roadmap

### Step-by-Step Process

1. **Review strategy**: Revisit the product strategy, annual objectives, and OKRs
2. **Gather inputs**: Collect feature requests, customer feedback, competitive intelligence, and technical debt items
3. **Score and prioritize**: Apply a prioritization framework (RICE, MoSCoW, WSJF)
4. **Group into themes**: Cluster related initiatives into coherent themes
5. **Sequence**: Order themes by dependency, strategic priority, and resource availability
6. **Validate capacity**: Ensure the roadmap does not exceed available engineering capacity
7. **Draft and review**: Create the first draft and review with engineering, design, and leadership
8. **Communicate**: Share appropriate views with each audience

### Roadmap Views by Audience

| Audience | Format | Detail Level | Frequency |
|----------|--------|-------------|-----------|
| Board / Investors | Quarterly themes | Strategic, outcome-focused | Quarterly |
| Executive Team | Now/Next/Later with OKR alignment | Strategic + key initiatives | Monthly |
| Product & Engineering | Detailed feature roadmap | Feature-level with dependencies | Bi-weekly |
| Sales & Customer Success | Customer-facing roadmap | Features by customer need | Monthly |
| Customers | High-level public roadmap | Themes only, no dates | Quarterly |

## Managing the Roadmap

### Review Cadence

| Review | Frequency | Purpose | Participants |
|--------|-----------|---------|-------------|
| Sprint Review | Bi-weekly | Progress on current roadmap items | Product team |
| Roadmap Sync | Monthly | Review priorities, adjust based on learnings | Product + Engineering leads |
| Quarterly Planning | Quarterly | Set next quarter's roadmap, review annual themes | Cross-functional leadership |
| Annual Planning | Annually | Set annual strategy and themes | Executive team |

### Handling Roadmap Changes

When new information requires a roadmap change:

1. **Assess impact**: What gets displaced if we add this? What is the opportunity cost?
2. **Quantify the case**: Score the new item through your prioritization framework
3. **Propose the swap**: Present "If we do X, we must defer Y" — never just add scope
4. **Get alignment**: Review with affected stakeholders before changing
5. **Communicate the change**: Update all roadmap views and notify relevant teams

### Common Anti-Patterns

| Anti-Pattern | Problem | Fix |
|-------------|---------|-----|
| Feature factory roadmap | Lists features without strategic narrative | Group features under outcome-based themes |
| Date-driven roadmap | Every item has a deadline, creating false commitments | Use Now/Next/Later or quarterly themes |
| Never-changing roadmap | Roadmap set once and never updated | Monthly review cadence with explicit change process |
| Everything is priority 1 | No real prioritization, team is overloaded | Force-rank everything; apply MoSCoW or RICE |
| No customer input | Roadmap driven by internal opinions | Integrate user research, NPS feedback, and support data |
