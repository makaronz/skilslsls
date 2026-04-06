# OKR Tracking and Scoring

Methods for monitoring OKR progress, scoring results, and conducting effective retrospectives.

---

## Tracking Methods

### Weekly Check-In Format

Run a 15-minute weekly OKR check-in with each team:

| Agenda Item | Duration | Purpose |
|------------|----------|---------|
| KR Progress Update | 5 min | Each KR owner reports current value and trajectory |
| Confidence Rating | 3 min | Rate each KR: On Track (green), At Risk (yellow), Off Track (red) |
| Blockers | 5 min | Identify and assign blockers to owners |
| Priorities This Week | 2 min | Name the 1-2 actions that will most move KRs forward |

### Progress Tracking Dashboard

Build a simple dashboard showing:

| KR | Baseline | Current | Target | % Progress | Confidence | Trend |
|----|----------|---------|--------|-----------|-----------|-------|
| NPS score | 32 | 38 | 50 | 33% | 🟡 At Risk | ↗ Improving |
| API latency (p95) | 800ms | 450ms | 200ms | 58% | 🟢 On Track | ↗ Improving |
| New ARR | $1.8M | $2.0M | $3.0M | 17% | 🔴 Off Track | → Flat |

### Confidence Scoring System

At each check-in, rate confidence that the KR will be achieved by end of quarter:

| Confidence Level | Definition | Action |
|-----------------|-----------|--------|
| 🟢 On Track | High confidence of achieving target | Continue current approach |
| 🟡 At Risk | Possible but requires intervention or luck | Identify specific actions to get back on track |
| 🔴 Off Track | Unlikely to achieve without significant change | Escalate, reprioritize resources, or adjust target |

Track confidence over time — consistent 🟡 or 🔴 without action indicates process failure, not just goal failure.

## Scoring Methodology

### The 0.0 to 1.0 Scale

At end of quarter, score each Key Result:

| Score | Meaning | Color |
|-------|---------|-------|
| 0.0-0.3 | Failed to make meaningful progress | Red |
| 0.4-0.6 | Made progress but fell significantly short | Yellow |
| 0.7 | Achieved what we expected (sweet spot for stretch goals) | Green |
| 0.8-0.9 | Exceeded expectations | Green |
| 1.0 | Fully achieved or exceeded — may indicate sandbagging | Blue |

### Scoring Formula for Quantitative KRs

```
Score = (Actual - Baseline) / (Target - Baseline)
```

Example: NPS from 32 (baseline) to 50 (target), actual = 41
```
Score = (41 - 32) / (50 - 32) = 9 / 18 = 0.50
```

### Objective Score

Average the KR scores under each Objective:

```
Objective Score = Average of all KR scores
```

For company-level reporting, average all Objective scores. The ideal company-wide average is 0.6-0.7 (indicates appropriate stretch).

## Scoring Patterns and What They Mean

| Pattern | Interpretation | Action |
|---------|---------------|--------|
| All KRs score 1.0 | Goals were too easy (sandbagging) | Set more ambitious targets next quarter |
| All KRs score < 0.3 | Goals were unrealistic or execution failed | Analyze root cause — was it bad goals or bad execution? |
| Mixed scores (0.3-0.8) | Healthy — some stretch achieved, some fell short | Normal and expected |
| One KR at 1.0, others < 0.3 | Team over-focused on one metric | Rebalance effort allocation next quarter |
| Consistent 0.5 across quarters | Team is plateauing | Reassess strategy, not just tactics |

## Quarterly Retrospective

### Retrospective Agenda (60 minutes)

| Section | Duration | Questions |
|---------|----------|-----------|
| Score Review | 15 min | What did we achieve? What did we miss? |
| Learning | 20 min | Why did we succeed or fail on each KR? What surprised us? |
| Process | 15 min | Did the OKR process work well? What would we change? |
| Forward Look | 10 min | What should next quarter's OKRs focus on based on what we learned? |

### Key Retrospective Questions

- **For high-scoring KRs**: What made this successful? Was the target ambitious enough? Can we raise the bar?
- **For low-scoring KRs**: Was the target reasonable? What blocked progress? Was this the right thing to measure?
- **For the process**: Did weekly check-ins happen consistently? Were KRs clearly defined with baselines? Did we have the right data to track progress?

### Documenting Learnings

Create a one-page summary per team per quarter:
1. **Objective and KR scores** (table)
2. **Top 3 wins** with quantified impact
3. **Top 3 misses** with root cause analysis
4. **Key learnings** that should inform next quarter's OKRs
5. **Process improvements** for the OKR methodology itself
