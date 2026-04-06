# Implementation Best Practices

Setting up prioritization processes, templates, and cadences for effective feature prioritization.

---

## Setting Up the Process

### Step 1: Define Scoring Criteria

Before scoring any feature, align the team on what each dimension means:

| Dimension | Definition | Scale | Evidence Required |
|-----------|-----------|-------|------------------|
| Reach | Number of users/accounts affected in a quarter | Actual number or estimate | Analytics data, market sizing |
| Impact | Contribution to the target metric per user | 3 = massive, 2 = high, 1 = medium, 0.5 = low, 0.25 = minimal | User research, A/B test data, analogies |
| Confidence | How certain are we in the estimates? | 100% = high, 80% = medium, 50% = low | Data availability, research depth |
| Effort | Person-months to ship | Estimated by engineering | Technical assessment, historical velocity |

### Step 2: Create the Scoring Template

Build a shared spreadsheet or tool with these columns:

| Column | Type | Description |
|--------|------|-------------|
| Feature Name | Text | Clear, concise feature description |
| Problem Statement | Text | The user problem this solves |
| Reach | Number | Users affected per quarter |
| Impact | Number | 0.25 to 3 scale |
| Confidence | Percentage | 50%, 80%, or 100% |
| Effort | Number | Person-months |
| RICE Score | Formula | (Reach × Impact × Confidence) / Effort |
| Category | Dropdown | Must-Have, Growth, Delight, Debt |
| Status | Dropdown | Proposed, Scored, Committed, Shipped |
| Owner | Text | PM or squad responsible |

### Step 3: Establish the Cadence

| Activity | Frequency | Participants | Output |
|----------|-----------|-------------|--------|
| Feature intake | Continuous | Anyone (via form) | Backlog additions |
| Scoring session | Bi-weekly | PM, Eng Lead, Design Lead | Scored features |
| Prioritization review | Monthly | Product leadership | Ranked backlog |
| Roadmap alignment | Quarterly | Cross-functional leadership | Committed quarterly plan |
| Retrospective | Quarterly | Product team | Process improvements |

## Scoring Best Practices

### Collaborative Scoring

- Score in groups of 3-5 (PM, engineering lead, design lead, data analyst)
- Use blind scoring first (everyone submits independently), then discuss outliers
- Focus discussion time on features where scores diverge > 30%
- Document the rationale for each score — future-you will forget why

### Handling Bias

| Bias | Symptom | Countermeasure |
|------|---------|---------------|
| Recency | Latest customer complaint gets top priority | Require data showing frequency, not just recency |
| HiPPO | Executive opinion overrides data | Require all features go through the same scoring |
| Sunk Cost | "We already built half of it" | Score remaining value vs. remaining effort only |
| Anchoring | First score influences all subsequent | Use blind scoring before discussion |
| Confirmation | Cherry-picking data to support a preferred feature | Assign a devil's advocate role in scoring sessions |

## Backlog Management

### Backlog Hygiene Practices

1. **Groom weekly**: Review the top 20 items to ensure they are ready for development
2. **Archive quarterly**: Move items untouched for 2+ quarters to an archive — if nobody missed them, they are not important
3. **Limit WIP**: Cap the "In Progress" column to prevent feature sprawl
4. **Tag dependencies**: Mark items that block or are blocked by other items
5. **Link to research**: Every feature in the backlog should link to the user research, data, or strategy that justifies it

### When to Re-Prioritize

Trigger a re-prioritization when:
- A major competitor launches a similar feature
- Customer churn data reveals a new top reason for leaving
- A strategic pivot changes the North Star metric
- Engineering estimates change significantly (>50% variance)
- New market data becomes available (industry report, user survey)
