# Iteration Prioritization Frameworks

Prioritization methods, impact/effort analysis, roadmapping techniques, and decision frameworks for planning design iterations effectively.

---

## Core Prioritization Frameworks

### Impact/Effort Matrix (2×2)

The most common prioritization tool for design iteration. Plot each improvement on two axes:

```
                     HIGH IMPACT
                         |
     🟢 DO FIRST          |         🟡 SCHEDULE
     High Impact,        |         High Impact,
     Low Effort          |         High Effort
     (Quick wins that    |         (Worth the investment
      move the needle)   |          but plan carefully)
                         |
  LOW EFFORT  -----------+----------  HIGH EFFORT
                         |
     🟢 BATCH            |         🟠 DEFER
     Low Impact,         |         Low Impact,
     Low Effort          |         High Effort
     (Polish items,      |         (Not worth it now,
      do in spare time)  |          maybe never)
                         |
                     LOW IMPACT
```

**Scoring guide for design iterations:**

| Factor | How to Estimate |
|--------|----------------|
| **Impact** | How many points will this add to the DQI score? Impact on which dimension? |
| **Effort** | Hours required to design + implement the change |

| Impact Level | Score Improvement | Examples |
|-------------|-------------------|--------|
| High | +0.5 to +1.0 on a dimension | Fix broken user flow, add missing responsive layout, fix accessibility failures |
| Medium | +0.2 to +0.4 on a dimension | Improve typography hierarchy, standardize spacing, add hover states |
| Low | +0.1 or less on a dimension | Adjust shadow values, tweak border radius, fine-tune animations |

| Effort Level | Time Estimate | Examples |
|-------------|--------------|--------|
| Low | < 2 hours | Color adjustments, font size changes, padding updates |
| Medium | 2–8 hours | New component states, layout restructuring, focus state design |
| High | 8+ hours | Full responsive redesign, new interaction patterns, major flow changes |

### RICE Scoring for Design Changes

Adapted from product management for design iteration prioritization:

| Factor | Definition | Scale | Design Application |
|--------|-----------|-------|-----------------------|
| **Reach** | How many screens/components affected | 1–10 | Changes affecting all screens score higher |
| **Impact** | Score improvement expected | 0.25/0.5/1/2/3 | Based on gap analysis from scoring |
| **Confidence** | How sure are we this will improve quality | 0–100% | Higher for proven patterns, lower for experimental |
| **Effort** | Person-hours to implement | Hours | Design + development time |

```
RICE Score = (Reach × Impact × Confidence) / Effort

Example:
Change: "Standardize spacing to 8px grid"
  Reach: 8 (affects most screens)
  Impact: 1 (medium improvement to consistency)
  Confidence: 90%
  Effort: 4 hours
  RICE = (8 × 1 × 0.9) / 4 = 1.8

Change: "Add skeleton loaders to data-heavy pages"
  Reach: 4 (affects 4 key pages)
  Impact: 2 (significant UX improvement)
  Confidence: 80%
  Effort: 6 hours
  RICE = (4 × 2 × 0.8) / 6 = 1.07

Priority: Spacing standardization first (RICE 1.8 > 1.07)
```

### MoSCoW for Iteration Scoping

Categorize iteration items to define scope:

| Category | Definition | Iteration Application |
|----------|-----------|----------------------|
| **Must Have** | Iteration fails without these | Fixes to critical issues, accessibility failures, broken flows |
| **Should Have** | Important but iteration still works without them | Score improvements targeting weakest dimensions |
| **Could Have** | Nice to include if time allows | Polish items, micro-interactions, edge case handling |
| **Won't Have** | Explicitly out of scope this iteration | Deferred items, requires prerequisite work, low priority |

**Scoping rule of thumb:**
- Must Have: 60% of iteration capacity
- Should Have: 20% of iteration capacity
- Could Have: 20% of iteration capacity
- Won't Have: 0% (explicitly deferred)

---

## Score-Driven Prioritization

### Gap-Weighted Priority Calculation

Use design quality scores to mathematically prioritize improvements:

```
Priority Score = Gap × Weight × Feasibility

Where:
  Gap = Target Score - Current Score (per dimension)
  Weight = Dimension weight in the scoring rubric
  Feasibility = 1.0 (easy), 0.7 (moderate), 0.4 (hard)
```

**Example calculation:**

| Dimension | Current | Target | Gap | Weight | Feasibility | Priority |
|-----------|---------|--------|-----|--------|-------------|----------|
| Visual Design | 7.5 | 9.0 | 1.5 | 0.25 | 0.7 | 0.263 |
| User Experience | 7.0 | 9.0 | 2.0 | 0.25 | 0.7 | 0.350 |
| Consistency | 8.0 | 9.0 | 1.0 | 0.15 | 1.0 | 0.150 |
| Responsiveness | 6.5 | 9.0 | 2.5 | 0.15 | 0.4 | 0.150 |
| Accessibility | 6.0 | 9.0 | 3.0 | 0.10 | 0.7 | 0.210 |
| Brand & Polish | 8.0 | 9.0 | 1.0 | 0.10 | 1.0 | 0.100 |

**Priority order:** UX (0.350) > Visual (0.263) > Accessibility (0.210) > Consistency = Responsiveness (0.150) > Brand (0.100)

### Diminishing Returns Analysis

Recognize when further iteration on a dimension yields minimal improvement:

| Current Score | Expected Gain per Hour | Recommendation |
|--------------|----------------------|----------------|
| < 6.0 | +0.3 to +0.5 per hour | High ROI — invest heavily |
| 6.0–7.5 | +0.2 to +0.3 per hour | Good ROI — continue investing |
| 7.5–8.5 | +0.1 to +0.2 per hour | Moderate ROI — be selective |
| 8.5–9.0 | +0.05 to +0.1 per hour | Low ROI — only high-impact items |
| 9.0+ | < +0.05 per hour | Diminishing returns — ship it |

**Decision rule:** When all dimensions are above 8.5 and the composite DQI is ≥ 9.0, stop iterating and ship. Further polish has minimal user impact.

---

## Iteration Roadmapping

### Iteration Sequence Planning

Plan 3–4 iterations with clear goals and expected outcomes:

```markdown
## Iteration Roadmap: [Project Name]

### Iteration 1: Foundation Fixes (Target: 7.0 → 7.8)
Focus: Critical UX issues and accessibility failures
Capacity: [X] hours
Items:
- [Must] Fix keyboard navigation on modal components (+0.3 A11y)
- [Must] Add loading states to data-heavy pages (+0.3 UX)
- [Must] Fix contrast failures on secondary text (+0.2 A11y)
- [Should] Improve heading hierarchy (+0.2 Visual)

### Iteration 2: Quality Uplift (Target: 7.8 → 8.5)
Focus: Consistency and visual polish
Capacity: [X] hours
Items:
- [Must] Standardize spacing across all screens (+0.3 Consistency)
- [Must] Redesign mobile navigation (+0.4 Responsiveness)
- [Should] Add hover and focus states to all interactive elements (+0.2 Visual)
- [Could] Implement skeleton loaders (+0.1 UX)

### Iteration 3: Polish Pass (Target: 8.5 → 9.0)
Focus: Final refinement and edge cases
Capacity: [X] hours
Items:
- [Must] Design empty states for all data views (+0.2 UX)
- [Should] Add micro-interactions to key actions (+0.1 Brand)
- [Should] Audit and fix all remaining A11y issues (+0.2 A11y)
- [Could] Optimize animations for reduced motion (+0.1 A11y)
```

### Iteration Scope Control

**Scope guard rules:**
1. Each iteration should be 4–8 hours of design work maximum
2. No more than 8–10 changes per iteration
3. Focus on 2–3 dimensions per iteration (not all at once)
4. Every iteration must include re-scoring to validate progress
5. If score doesn't improve after an iteration, reassess approach

**Scope creep indicators:**
- Iteration takes more than 2× estimated hours
- New items being added mid-iteration
- No items being completed (too many in progress)
- Score improvements not matching estimates

---

## Decision Frameworks for Iteration Choices

### The "Fix vs. Ship" Decision

When deciding whether to iterate further or ship:

| Factor | Ship | Iterate |
|--------|------|---------|
| DQI Score | ≥ 9.0 | < 9.0 |
| Critical Issues | 0 remaining | Any remaining |
| Deadline Pressure | High — ship at 8.5+ | Low — iterate to 9.0 |
| User Impact | Score gaps are in low-impact areas | Score gaps affect primary flows |
| Stakeholder Approval | Approved | Concerns remain |
| Competitor Benchmark | Above competitors | Below competitors |

### The "Redesign vs. Refine" Decision

When a dimension scores very low, decide between incremental refinement and redesign:

| Signal | Refine | Redesign |
|--------|--------|---------|
| Score | 5.0–7.0 | < 5.0 |
| Issue type | Execution problems (spacing, color, sizing) | Structural problems (IA, flow, layout approach) |
| Fix count | < 10 specific fixes needed | > 15 fixes, all interconnected |
| User feedback | "Almost there, just needs polish" | "I'm confused about what to do" |
| Time available | Limited | Sufficient for rework |

### Tiebreaker Rules

When two improvements have equal priority scores:

1. **User-facing wins over internal.** Prefer changes visible to end users.
2. **Accessibility wins over aesthetics.** Compliance issues take precedence.
3. **Broader impact wins over narrow.** Changes affecting more screens win.
4. **Reversible wins over irreversible.** Prefer changes easy to undo if wrong.
5. **Foundation wins over decoration.** Spacing, structure, and flow before animation and delight.
