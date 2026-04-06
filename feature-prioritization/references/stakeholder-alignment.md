# Stakeholder Alignment

Techniques for navigating conflicting priorities, communicating prioritization decisions, and building consensus across teams.

---

## Stakeholder Mapping

### Influence-Interest Matrix

Map stakeholders on two dimensions to determine engagement strategy:

| Quadrant | Influence | Interest | Strategy |
|----------|-----------|----------|----------|
| Manage Closely | High | High | Regular updates, involve in decisions |
| Keep Satisfied | High | Low | Periodic updates, escalate only major changes |
| Keep Informed | Low | High | Share decisions, welcome feedback |
| Monitor | Low | Low | Minimal engagement, general newsletters |

### Common Stakeholder Personas in Prioritization

| Persona | Typical Ask | Underlying Need | Engagement Approach |
|---------|-----------|-----------------|-------------------|
| CEO / Founder | "We need this feature to win the deal" | Revenue and competitive pressure | Show how the prioritized roadmap maximizes overall revenue, not just one deal |
| VP Sales | "Customers keep asking for X" | Pipeline conversion, quota attainment | Quantify the demand (how many customers, how much revenue), score via framework |
| VP Engineering | "We need to address tech debt" | Platform stability, developer velocity | Frame tech debt as investment: show how it accelerates future feature delivery |
| Customer Success | "We'll lose this account without Y" | Retention, health scores | Evaluate churn risk vs. cost of building Y, compare with other retention levers |
| Design | "The UX needs a fundamental redesign" | User experience quality | Quantify UX impact on conversion/retention metrics |

## Communication Frameworks

### The Prioritization Narrative

When sharing prioritization decisions, structure the message:

1. **Context**: Remind stakeholders of the team's goals and constraints (OKRs, headcount, timeline)
2. **Framework**: Briefly explain how features were scored (RICE, MoSCoW, etc.)
3. **Decisions**: Present what is prioritized AND what is not, with brief rationale for each
4. **Tradeoffs**: Acknowledge what you are giving up and why the chosen path is better
5. **Next Steps**: When the deprioritized items will be reconsidered

### Saying No Constructively

| Instead of... | Say... |
|--------------|--------|
| "That's not a priority" | "That scored lower on our framework because [reason]. Here's when we'll revisit it." |
| "We don't have resources" | "Given our current capacity, choosing this means deferring [specific item]. Is that the right tradeoff?" |
| "The data doesn't support it" | "Here's what the data shows [share specifics]. What data would change our assessment?" |
| "Engineering says it's too hard" | "The effort estimate is X person-months. Here's what we could build instead in that time." |

## Conflict Resolution Techniques

### Buy-a-Feature Exercise

Give stakeholders a fixed budget of virtual currency and ask them to "buy" the features they want most. Features are priced proportional to their effort. This forces explicit tradeoffs:

1. List 15-20 candidate features with effort-based prices
2. Give each stakeholder $100 in virtual currency
3. Stakeholders allocate their budget across features (they can pool money for expensive items)
4. Tally the results — the market has spoken

### Disagree and Commit

When consensus cannot be reached:
1. Ensure all perspectives have been heard and documented
2. The decision owner (typically the PM) makes the call with stated rationale
3. Dissenters acknowledge the decision and commit to supporting execution
4. Set a review date to evaluate the outcome with data
5. If the data proves the dissenter right, adjust course without blame

### Escalation Protocol

When a stakeholder disagrees with prioritization:
1. **Level 1**: PM explains the scoring and tradeoff rationale
2. **Level 2**: Joint session to re-score with additional data from both sides
3. **Level 3**: Escalate to product leadership with both perspectives documented
4. **Level 4**: Executive tiebreaker with the understanding that the decision will be data-reviewed in 90 days

## Building Long-Term Trust

- **Transparency**: Share the full prioritization spreadsheet, not just the results
- **Predictability**: Follow the same process every cycle so stakeholders know what to expect
- **Follow-through**: When you commit to revisiting a deprioritized item, actually do it
- **Celebrate wins**: When a prioritized feature delivers results, share the data with the stakeholders who supported the decision
- **Acknowledge misses**: When a prioritization call was wrong, own it and explain what you learned
