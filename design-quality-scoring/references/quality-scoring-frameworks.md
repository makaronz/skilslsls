# Quality Scoring Frameworks

Comprehensive scoring rubrics, evaluation frameworks, and quality metrics for objectively measuring design quality across multiple dimensions.

---

## Scoring Rubric Architecture

### Multi-Dimensional Rubric Design

Effective design scoring requires rubrics that capture quality across interconnected dimensions rather than isolated criteria. A well-structured rubric balances breadth of coverage with depth of evaluation.

**Rubric Structure Hierarchy:**

| Level | Description | Example |
|-------|-------------|---------|
| Dimension | Major quality area | Visual Design, UX, Accessibility |
| Category | Specific focus within dimension | Typography, Color, Layout |
| Criterion | Individual measurable item | Line height ratio, Contrast ratio |
| Indicator | Observable evidence | Body text uses 1.5–1.7 line height |

### Weight Distribution Models

**Equal Weight Model** — Every dimension counts equally. Simple to implement but may not reflect project priorities.

**Stakeholder-Aligned Model** — Weights reflect business priorities:

| Dimension | Consumer App | Enterprise SaaS | Marketing Site | Internal Tool |
|-----------|-------------|-----------------|----------------|---------------|
| Visual Design | 30% | 15% | 35% | 10% |
| User Experience | 25% | 30% | 20% | 35% |
| Consistency | 10% | 20% | 10% | 20% |
| Responsiveness | 15% | 15% | 20% | 10% |
| Accessibility | 10% | 15% | 5% | 20% |
| Brand & Polish | 10% | 5% | 10% | 5% |

**Maturity-Based Model** — Weights shift as the design matures:
- Early iterations: UX and Visual Design weighted higher (focus on foundations)
- Later iterations: Consistency, Accessibility, and Polish weighted higher (focus on refinement)

---

## Scoring Scale Systems

### 10-Point Continuous Scale

The most common design scoring scale. Provides granularity while remaining intuitive.

| Score | Label | Definition | Observable Evidence |
|-------|-------|------------|--------------------|
| 10 | Exceptional | Industry-leading quality, innovative | Wins design awards, sets new patterns |
| 9 | Excellent | Professional, polished, delightful | Ready for premium product launch |
| 8 | Very Good | Strong quality, minor improvements possible | Production-ready with light polish |
| 7 | Good | Solid foundation, noticeable gaps | Needs focused iteration on 2–3 areas |
| 6 | Adequate | Meets basic requirements, lacks refinement | Functional but not impressive |
| 5 | Mediocre | Significant quality gaps | Needs substantial improvement |
| 4 | Below Average | Multiple issues affecting usability | Major revision required |
| 3 | Poor | Fundamental problems throughout | Rethink approach needed |
| 2 | Very Poor | Barely functional, major issues | Near-complete redesign required |
| 1 | Unacceptable | Does not meet minimum standards | Start over |

### Likert-Based Categorical Scale

Useful for quick assessments or when numeric precision is unnecessary:

| Rating | Meaning | When to Use |
|--------|---------|-------------|
| Strongly Exceeds | Far beyond expectations | Rare — reserved for exceptional work |
| Exceeds | Above expected quality | Solid professional work |
| Meets | Satisfactory quality | Acceptable for the context |
| Partially Meets | Some gaps present | Needs specific improvements |
| Does Not Meet | Below expectations | Requires significant rework |

### Binary Pass/Fail Criteria

For compliance-oriented items where partial credit is inappropriate:

- Color contrast meets WCAG AA: **Pass / Fail**
- Touch targets ≥ 44px: **Pass / Fail**
- All interactive elements have focus states: **Pass / Fail**
- Content readable at 200% zoom: **Pass / Fail**

---

## Framework Comparisons

### Nielsen's Heuristic Evaluation Framework

Adapted for design scoring with quantifiable criteria:

| Heuristic | Scoring Criteria | Weight |
|-----------|-----------------|--------|
| Visibility of system status | Loading states, progress indicators, feedback | 10% |
| Match between system and real world | Familiar language, intuitive metaphors | 10% |
| User control and freedom | Undo, back navigation, cancel options | 10% |
| Consistency and standards | Pattern adherence, platform conventions | 15% |
| Error prevention | Validation, confirmation dialogs, constraints | 10% |
| Recognition over recall | Visible options, contextual help, breadcrumbs | 10% |
| Flexibility and efficiency | Shortcuts, customization, progressive disclosure | 10% |
| Aesthetic and minimalist design | Signal-to-noise ratio, visual clarity | 10% |
| Error recovery | Helpful messages, clear recovery paths | 10% |
| Help and documentation | Onboarding, tooltips, contextual guidance | 5% |

### Google HEART Framework (Adapted for Design)

| Metric | Design Scoring Application | Measurement Method |
|--------|---------------------------|--------------------|
| Happiness | Visual appeal, emotional response, delight | Subjective rating + peer review |
| Engagement | Interaction design quality, call-to-action clarity | Task analysis scoring |
| Adoption | Onboarding clarity, learnability of interface | First-use walkthrough scoring |
| Retention | Consistency, memorability, navigation ease | Cross-screen evaluation |
| Task Success | Flow completeness, error handling, feedback | Task completion scoring |

### Dieter Rams' Design Principles Scoring

Apply the ten principles as a scoring framework for digital design:

| Principle | Digital Application | Scoring Focus |
|-----------|--------------------|--------------|
| Innovative | Novel interaction patterns, creative solutions | Does the design advance the craft? |
| Useful | Functional completeness, user value | Does every element serve a purpose? |
| Aesthetic | Visual harmony, proportion, beauty | Is the design visually pleasing? |
| Understandable | Intuitive interface, clear affordances | Can users immediately understand it? |
| Unobtrusive | Minimal chrome, content-focused | Does the UI get out of the way? |
| Honest | Authentic representation, no dark patterns | Are interactions transparent? |
| Long-lasting | Timeless design choices, no fads | Will this design age well? |
| Thorough | Edge cases, states, responsive design | Is every detail considered? |
| Environmentally Friendly | Performance, accessibility, inclusivity | Does it serve all users well? |
| Minimal | Essential elements only, no excess | Is anything unnecessary? |

---

## Quality Metrics and KPIs

### Design Quality Index (DQI)

A composite metric that tracks overall design quality over time:

```
DQI = Σ (Dimension Score × Dimension Weight) / Total Weight

Example:
DQI = (Visual 8.5 × 0.25) + (UX 7.8 × 0.25) + (Consistency 8.0 × 0.15)
    + (Responsive 7.5 × 0.15) + (A11y 6.5 × 0.10) + (Brand 8.0 × 0.10)
    = 2.125 + 1.95 + 1.20 + 1.125 + 0.65 + 0.80
    = 7.85 / 10
```

### Score Velocity

Track improvement rate across iterations:

```
Score Velocity = (Current Score - Previous Score) / Days Between Iterations

Healthy velocity: +0.3 to +0.8 points per iteration
Stalling: < +0.1 points per iteration (review approach)
Diminishing returns threshold: Score > 9.0 (expect slower gains)
```

### Category Gap Analysis

Identify the categories dragging overall scores down:

```
Category Gap = Target Score - Category Score
Weighted Gap = Category Gap × Category Weight

Prioritize categories with highest Weighted Gap for maximum score improvement.
```

### Quality Gate Thresholds

Define minimum scores required to proceed through design phases:

| Phase Gate | Minimum DQI | Critical Criteria |
|------------|-------------|-------------------|
| Concept → Wireframe | 5.0 | UX score ≥ 5.0 |
| Wireframe → Visual | 6.5 | UX ≥ 7.0, Consistency ≥ 6.0 |
| Visual → Prototype | 7.5 | All dimensions ≥ 6.0 |
| Prototype → Handoff | 8.5 | Accessibility ≥ 8.0, all ≥ 7.0 |
| Final Delivery | 9.0 | No dimension below 8.0 |

---

## Rubric Template Library

### Quick Assessment Rubric (5-Minute Review)

| Area | Score | Key Evidence |
|------|-------|--------------|
| First Impression | _/10 | What grabs attention first? Positive or negative? |
| Clarity | _/10 | Can you immediately tell the page purpose? |
| Navigation | _/10 | Can you find what you need quickly? |
| Visual Appeal | _/10 | Does it feel professional and polished? |
| Completeness | _/10 | Are all states and scenarios covered? |
| **Quick Score** | **_/10** | Average of above |

### Comprehensive Scoring Template

Use for formal reviews where detailed scoring is required:

```markdown
## Scoring Record

Project: [Name]
Version: [X.X]
Scorer: [Name/AI]
Date: [Date]

### Dimension Scores
| Dimension | Sub-Score 1 | Sub-Score 2 | Sub-Score 3 | Dimension Avg | Weight | Weighted |
|-----------|------------|------------|------------|--------------|--------|----------|
| Visual | Color: _ | Type: _ | Layout: _ | _ | 0.25 | _ |
| UX | Flows: _ | Clarity: _ | Errors: _ | _ | 0.25 | _ |
| Consistency | Components: _ | Patterns: _ | Spacing: _ | _ | 0.15 | _ |
| Responsive | Mobile: _ | Tablet: _ | Desktop: _ | _ | 0.15 | _ |
| Accessibility | Contrast: _ | Focus: _ | Targets: _ | _ | 0.10 | _ |
| Brand | Alignment: _ | Emotion: _ | Polish: _ | _ | 0.10 | _ |

### Final DQI: _/10
### Quality Gate: [Pass/Fail]
### Verdict: [Ready / Iterate / Rework]
```

---

## Implementing Scoring in Practice

### Pre-Scoring Preparation

1. Confirm which rubric model to use (quick vs. comprehensive)
2. Verify weight distribution matches project type
3. Gather all design artifacts (screens, flows, component specs)
4. Review previous scores if iterating (for comparison)
5. Identify any custom criteria for this project

### During Scoring

1. Score each dimension independently before calculating composite
2. Write evidence for each score (not just the number)
3. Flag any "automatic fail" items (accessibility violations, broken flows)
4. Note scoring confidence level (high/medium/low per dimension)
5. Identify top 3 strengths and top 3 improvement areas

### Post-Scoring Actions

1. Calculate DQI and compare against quality gate
2. Generate gap analysis with prioritized improvements
3. Estimate effort to close each gap
4. Create iteration plan based on highest-impact improvements
5. Archive score for trend tracking
