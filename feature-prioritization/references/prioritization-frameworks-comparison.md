# Prioritization Frameworks Comparison

Side-by-side evaluation of feature prioritization methodologies to guide framework selection.

---

## Framework Overview

| Framework | Dimensions | Best For | Complexity | Team Size |
|-----------|-----------|----------|-----------|-----------|
| RICE | Reach, Impact, Confidence, Effort | Growth teams, data-driven orgs | Medium | Any |
| ICE | Impact, Confidence, Ease | Quick scoring, early-stage | Low | Small |
| MoSCoW | Must, Should, Could, Won't | Release planning, stakeholder alignment | Low | Any |
| Kano | Must-Be, Performance, Attractive | Customer satisfaction analysis | High | Medium+ |
| Value vs. Effort | Business value, Development effort | Visual prioritization, workshops | Low | Any |
| WSJF | Cost of Delay, Job Size | SAFe/Lean, continuous flow | Medium | Large |
| Opportunity Scoring | Importance, Satisfaction | Jobs-to-be-Done alignment | Medium | Medium+ |
| Story Mapping | User journey position | MVP definition, release planning | Medium | Any |

## Detailed Comparisons

### RICE vs. ICE

Both use numerical scoring, but RICE includes Reach as a separate dimension:

| Aspect | RICE | ICE |
|--------|------|-----|
| Formula | (Reach × Impact × Confidence) / Effort | Impact × Confidence × Ease |
| Reach component | Explicit (how many users affected) | Implicit in Impact |
| Confidence | 100% / 80% / 50% levels | 1-10 scale |
| Effort unit | Person-months | 1-10 inverse scale |
| Objectivity | Higher (Reach is measurable) | Lower (more subjective) |
| Speed | Moderate (requires Reach data) | Fast (quick estimates) |

**Use RICE** when you have data on feature reach and need defensible prioritization. **Use ICE** for fast, lightweight scoring in early-stage or small-team contexts.

### MoSCoW vs. Value/Effort Matrix

| Aspect | MoSCoW | Value vs. Effort |
|--------|--------|-----------------|
| Output | Categorical buckets | 2×2 matrix placement |
| Granularity | 4 categories | Continuous (placement on axes) |
| Stakeholder buy-in | High (intuitive labels) | High (visual) |
| Quantitative rigor | Low (subjective categorization) | Medium (estimated scores) |
| Best output | Scope agreement for a release | Quick wins identification |

### WSJF vs. RICE

| Aspect | WSJF | RICE |
|--------|------|------|
| Core concept | Cost of Delay ÷ Job Size | (Reach × Impact × Confidence) ÷ Effort |
| Time sensitivity | Explicit (urgency and risk reduction) | Not explicit |
| Framework context | SAFe, Lean, PI Planning | General product management |
| Data requirements | Relative sizing | Absolute estimates for Reach |

## Combining Frameworks

No single framework is perfect. Effective teams often combine:

1. **Kano + RICE**: Use Kano to classify feature type (Must-Be, Performance, Attractive), then RICE to prioritize within each category
2. **MoSCoW + Story Mapping**: Use MoSCoW for release scope, then Story Mapping to sequence features within the release
3. **Value/Effort + ICE**: Quick Value/Effort matrix to identify quick wins, then ICE scoring for the remaining ambiguous items

## Common Pitfalls

| Pitfall | Description | Mitigation |
|---------|-------------|-----------|
| Gaming scores | Teams inflate scores for pet features | Calibrate with cross-team reviews |
| False precision | Treating 3.7 vs. 3.8 as meaningful | Use score ranges, not exact ranks |
| Ignoring dependencies | Prioritizing a feature that depends on unbuilt infrastructure | Map dependencies before scoring |
| Static prioritization | Scoring once and never revisiting | Re-score quarterly as data changes |
| Framework fatigue | Applying every framework to every decision | Match framework complexity to decision stakes |
