# Scoring Implementation & Calibration

Processes for implementing scoring systems, calibrating scores across reviewers, and maintaining scoring consistency over time.

---

## Implementing a Scoring Process

### Scoring Workflow Overview

```
1. Select Rubric → 2. Prepare Artifacts → 3. Individual Scoring → 4. Calibration
→ 5. Consensus Score → 6. Gap Analysis → 7. Action Plan → 8. Archive
```

### Step 1: Rubric Selection

Choose the appropriate rubric based on context:

| Context | Recommended Rubric | Time Required |
|---------|-------------------|---------------|
| Quick design check-in | Quick Assessment (5 dimensions) | 5–10 minutes |
| Sprint review | Standard Rubric (6 dimensions) | 15–25 minutes |
| Milestone review | Comprehensive Rubric (6 dimensions, sub-scores) | 30–45 minutes |
| Client presentation gate | Full Rubric + Stakeholder Criteria | 45–60 minutes |
| Final delivery validation | Full Rubric + Compliance Checklist | 60–90 minutes |

### Step 2: Artifact Preparation

Before scoring, ensure all necessary materials are assembled:

**Required Artifacts:**
- All screens/pages in the current design version
- Component library or design system reference
- User flow diagrams
- Previous iteration scores (if applicable)
- Project-specific requirements or constraints

**Artifact Presentation Standards:**
- Screens organized by flow or section
- Labeled with screen name and state
- Responsive variants grouped together
- Interactive prototypes accessible (if available)
- Design system tokens documented

### Step 3: Individual Scoring Protocol

**Scoring Environment:**
- Review designs on a calibrated display
- View at actual device sizes when possible (not just zoomed in Figma)
- Review without distractions for consistent attention
- Score one dimension at a time across all screens (not one screen at a time)

**Scoring Discipline:**
1. Score the dimension, not the designer — evaluate the artifact objectively
2. Write evidence before assigning a number — the rationale should drive the score
3. Use the full scale — avoid clustering everything at 7–8
4. Score against the rubric criteria, not personal preference
5. Flag items where you have low confidence

---

## Calibration Methods

### Why Calibration Matters

Without calibration, the same design can receive vastly different scores from different reviewers. Calibration ensures:
- Scores are meaningful and comparable across time
- Different reviewers produce similar scores for similar quality
- The scoring system produces actionable, trustworthy results
- Progress tracking is accurate across iterations

### Calibration Technique 1: Anchor Example Scoring

Establish reference designs at known quality levels:

| Quality Level | Score Range | Anchor Description |
|--------------|-------------|--------------------|
| Exemplary | 9.0–10.0 | Award-winning designs, Dribbble top picks, Apple HIG exemplars |
| Professional | 7.5–8.9 | Well-designed production apps (Stripe, Linear, Notion) |
| Acceptable | 6.0–7.4 | Functional apps with decent design (typical SaaS products) |
| Below Standard | 4.0–5.9 | Dated or inconsistent designs (legacy enterprise tools) |
| Poor | 1.0–3.9 | Broken layouts, accessibility failures, no design system |

**Anchor Calibration Process:**
1. Collect 5–10 example designs at different quality levels
2. Score each example as a group, discussing rationale
3. Establish consensus scores as reference points
4. Before each scoring session, review 2–3 anchors to recalibrate
5. When in doubt during scoring, compare to the nearest anchor

### Calibration Technique 2: Blind Dual Scoring

Two reviewers score the same design independently, then compare:

```
Reviewer A scores: Visual 8, UX 7, Consistency 8, Responsive 6, A11y 7, Brand 8
Reviewer B scores: Visual 7, UX 8, Consistency 7, Responsive 7, A11y 6, Brand 7

Delta analysis:
- Visual: Δ1 (within tolerance)
- UX: Δ1 (within tolerance)
- Consistency: Δ1 (within tolerance)
- Responsive: Δ1 (within tolerance)
- A11y: Δ1 (within tolerance)
- Brand: Δ1 (within tolerance)

Acceptable delta: ≤ 1.5 points per dimension
Calibration needed: > 1.5 points on any dimension
```

**When Scores Diverge:**
1. Each reviewer shares their evidence and rationale
2. Identify whether the disagreement is about criteria interpretation or evidence evaluation
3. Revisit the rubric definition for the dimension in question
4. Agree on the evidence, then re-score independently
5. If still divergent, take the average and document the discussion

### Calibration Technique 3: Score Distribution Analysis

Periodically analyze scoring patterns to detect bias:

**Common Scoring Biases:**

| Bias | Description | Detection | Correction |
|------|-------------|-----------|------------|
| Central Tendency | Scores cluster around 6–7 | Standard deviation < 1.0 | Practice using full scale, review anchors |
| Leniency Bias | Scores consistently high | Mean > 8.0 across projects | Recalibrate against anchor examples |
| Severity Bias | Scores consistently low | Mean < 5.0 across projects | Recognize good work, adjust expectations |
| Halo Effect | One strong area inflates all scores | High correlation between all dimensions | Score each dimension independently |
| Recency Bias | Recent work scores higher than older | Trend analysis shows upward drift | Re-score older work periodically |
| Anchoring Bias | First score influences subsequent | First dimension scored always highest | Randomize dimension scoring order |

### Calibration Technique 4: Historical Trend Validation

Compare scores against outcomes to validate accuracy:

```
If a design scored 9.0 → Did it perform well in production? (user metrics, stakeholder feedback)
If a design scored 6.0 → Were the predicted issues actually problematic?
If scores improved V1→V3 → Did the identified improvements match what was done?
```

This feedback loop ensures scoring predicts actual quality, not just perceived quality.

---

## Maintaining Consistency Over Time

### Scoring Session Protocol

Follow this protocol for every scoring session to maintain consistency:

**Before Session:**
1. Review the rubric definitions (even if familiar)
2. Glance at 1–2 anchor examples for calibration
3. Review previous iteration scores (if applicable)
4. Clear your mental state — don't carry frustration or excitement from other work

**During Session:**
1. Score all screens for one dimension before moving to the next
2. Take breaks between dimensions (avoid fatigue-driven score drift)
3. Write rationale before committing to a number
4. Flag low-confidence scores for discussion
5. Don't revise early scores based on later impressions (score forward)

**After Session:**
1. Review all scores holistically — do they tell a coherent story?
2. Check for obvious inconsistencies (e.g., high consistency score but noted inconsistencies in evidence)
3. Calculate composite score and compare to quality gate
4. Document the scoring session metadata (date, scorer, version, time spent)

### Version-to-Version Consistency

When scoring iterations of the same design:

**Do:**
- Review previous scores and evidence before starting
- Use the same rubric and weights
- Score the current version on its own merits first, then compare
- Document what changed and its impact on scores

**Don't:**
- Copy-paste previous scores and modify — start fresh
- Let improvement bias inflate scores ("it's better so it must be 9")
- Forget to check for regressions in previously strong areas
- Change rubric weights between iterations without documenting why

### Score Normalization

When comparing scores across different projects or time periods:

**Z-Score Normalization:**
```
Normalized Score = (Raw Score - Mean Score) / Standard Deviation

This tells you how many standard deviations a score is from average.
Positive = above average, Negative = below average.
```

**Percentile Ranking:**
```
Rank all scored designs by DQI.
A score of 8.5 might be 85th percentile across all projects.
Useful for benchmarking: "This design is better than 85% of what we've scored."
```

---

## Scoring Automation and Tools

### Automated Scoring Components

Some criteria can be scored automatically or semi-automatically:

| Criterion | Automation Potential | Tool/Method |
|-----------|---------------------|-------------|
| Color contrast ratios | Fully automatable | axe, Stark, WebAIM API |
| Touch target sizes | Fully automatable | Figma plugin measurement |
| Font size compliance | Fully automatable | Design token audit |
| Spacing consistency | Semi-automatable | Design token audit + visual check |
| Component reuse | Semi-automatable | Figma component analytics |
| Heading hierarchy | Semi-automatable | HTML structure analysis |
| Responsive breakpoints | Manual with tool assist | Browser DevTools, Responsively |
| Visual harmony | Manual | Human evaluation required |
| Emotional design | Manual | Human evaluation required |
| Brand alignment | Manual | Human evaluation required |

### Scoring Tracking Dashboard

Track scores over time with this structure:

```markdown
## Design Quality Tracker

| Project | Version | Date | Visual | UX | Consistency | Responsive | A11y | Brand | DQI | Gate |
|---------|---------|------|--------|-----|-------------|------------|------|-------|-----|------|
| TaskFlow | V1 | Jan 15 | 6.5 | 6.0 | 5.5 | 5.0 | 4.5 | 6.0 | 5.73 | Fail |
| TaskFlow | V2 | Jan 22 | 7.5 | 7.0 | 7.0 | 6.5 | 6.0 | 7.0 | 6.93 | Fail |
| TaskFlow | V3 | Jan 29 | 8.5 | 8.0 | 8.0 | 7.5 | 7.5 | 8.0 | 8.00 | Pass |
| TaskFlow | V4 | Feb 5 | 9.0 | 9.0 | 8.5 | 8.5 | 8.5 | 8.5 | 8.75 | Pass |
```

### Score Reporting Template

```markdown
## Score Report: [Project] [Version]

Date: [Date]
Scorer: [Name/AI]
Rubric: [Quick/Standard/Comprehensive]

### Summary
- **DQI**: [Score]/10 ([+/-X] from previous)
- **Quality Gate**: [Pass/Fail] (threshold: [X])
- **Verdict**: [Ship / Iterate / Rework]

### Dimension Breakdown
| Dimension | Score | Δ Previous | Confidence | Top Issue |
|-----------|-------|-----------|------------|----------|
| [Each] | _/10 | +/- _ | H/M/L | [Issue] |

### Key Findings
1. **Strongest**: [Dimension] at [score] — [why]
2. **Weakest**: [Dimension] at [score] — [why]
3. **Most Improved**: [Dimension] [+X] — [what changed]

### Recommended Actions
1. [Action] — Expected impact: +[X] on [Dimension]
2. [Action] — Expected impact: +[X] on [Dimension]
3. [Action] — Expected impact: +[X] on [Dimension]

### Calibration Notes
- Scoring confidence: [Overall H/M/L]
- Calibration method used: [Anchor/Dual/Self]
- Known biases to note: [Any]
```

---

## Common Scoring Pitfalls

### Pitfall 1: Scoring Without Evidence
**Problem:** Assigning a number based on gut feeling without documenting why.
**Solution:** Always write the rationale before the score. If you can't articulate evidence, you can't justify the score.

### Pitfall 2: Inconsistent Granularity
**Problem:** Scoring one dimension in great detail and others superficially.
**Solution:** Spend equal time on each dimension. Use a timer if needed.

### Pitfall 3: Ignoring Context
**Problem:** Scoring an internal tool against consumer app standards.
**Solution:** Select appropriate weight distributions and anchor examples for the project type.

### Pitfall 4: Score Inflation Over Iterations
**Problem:** Each iteration scores higher simply because "it improved" even if absolute quality is mediocre.
**Solution:** Always score against the rubric, not against the previous version. Improvement is good but doesn't guarantee the score threshold.

### Pitfall 5: Not Acting on Scores
**Problem:** Scoring becomes a ritual without driving improvement.
**Solution:** Every scoring session must produce a prioritized action list. If scores don't drive changes, the process is wasteful.
