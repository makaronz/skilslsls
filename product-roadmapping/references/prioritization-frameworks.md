# Prioritization Frameworks for Roadmapping

Applying scoring methods to rank features and initiatives for inclusion on the product roadmap.

---

## RICE Scoring

### Components

| Component | Definition | Scale | Source |
|-----------|-----------|-------|--------|
| Reach | How many users will this impact per quarter? | Actual number | Analytics, market sizing |
| Impact | How much will this move the target metric per user? | 3=massive, 2=high, 1=medium, 0.5=low, 0.25=minimal | User research, judgment |
| Confidence | How certain are we about Reach and Impact? | 100%=high, 80%=medium, 50%=low | Evidence quality |
| Effort | How many person-months to build? | Person-months | Engineering estimate |

### Formula

```
RICE Score = (Reach × Impact × Confidence) / Effort
```

### Worked Example

| Initiative | Reach | Impact | Confidence | Effort | RICE |
|-----------|-------|--------|-----------|--------|------|
| Onboarding wizard | 5,000 | 2 | 80% | 3 | 2,667 |
| API v2 | 500 | 3 | 100% | 6 | 250 |
| Dark mode | 8,000 | 0.5 | 100% | 1 | 4,000 |
| Enterprise SSO | 200 | 3 | 80% | 4 | 120 |

Dark mode scores highest due to massive reach and low effort. But RICE alone does not capture strategic importance — SSO may be a prerequisite for enterprise deals. Use RICE as input, not the final answer.

## MoSCoW Method

Categorize features into four buckets for a specific release:

| Category | Definition | Rule of Thumb |
|----------|-----------|---------------|
| **Must Have** | Without this, the release is a failure | Non-negotiable requirements |
| **Should Have** | Important but not critical for this release | Significant value, can wait if needed |
| **Could Have** | Nice to have, included only if capacity allows | Included only if low effort |
| **Won't Have** | Explicitly out of scope for this release | Agreed exclusions to prevent scope creep |

### Applying MoSCoW

1. List all candidate features for the release
2. Start by identifying Must Haves — these are non-negotiable
3. Must Haves should not exceed 60% of available capacity
4. Fill Should Haves up to 80% of capacity
5. Add Could Haves if any capacity remains
6. Explicitly list Won't Haves to set expectations

## Value vs. Effort Matrix

### 2×2 Matrix

Plot features on a two-dimensional chart:

| Quadrant | Value | Effort | Strategy |
|----------|-------|--------|----------|
| Quick Wins | High | Low | Do first — highest ROI |
| Strategic Bets | High | High | Plan carefully, commit resources |
| Fill-Ins | Low | Low | Do if capacity allows |
| Money Pits | Low | High | Avoid unless strategically required |

### Facilitating the Exercise

1. Give each participant sticky notes with feature names
2. Draw a large 2×2 grid on a whiteboard or Miro board
3. Have each person place their features independently
4. Discuss items where placements disagree — these are the most valuable conversations
5. Move items to consensus positions
6. Prioritize: Quick Wins → Strategic Bets → Fill-Ins → Money Pits

## Weighted Shortest Job First (WSJF)

Used in SAFe environments to prioritize by cost of delay:

```
WSJF = Cost of Delay / Job Size
```

Cost of Delay includes:
- **User/Business Value**: How much value does this deliver?
- **Time Criticality**: How much does value decrease with delay?
- **Risk Reduction/Opportunity Enablement**: Does this reduce risk or enable future value?

Score each factor relatively (Fibonacci: 1, 2, 3, 5, 8, 13) against other items in the backlog. Higher WSJF items should be done first.

## Framework Selection Guide

| Situation | Recommended Framework |
|-----------|---------------------|
| Data-rich environment with analytics | RICE |
| Stakeholder alignment for a release | MoSCoW |
| Workshop with cross-functional team | Value vs. Effort |
| SAFe / Lean enterprise | WSJF |
| Customer-centric product discovery | Kano Model |
| Quick team exercise | ICE or Dot Voting |
