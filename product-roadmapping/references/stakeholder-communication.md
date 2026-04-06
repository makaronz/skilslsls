# Stakeholder Communication for Roadmaps

Strategies for presenting roadmaps, managing expectations, and handling stakeholder requests.

---

## Audience-Specific Communication

### Executive Audience

Executives care about strategic alignment, business impact, and resource allocation — not feature details.

**Presentation format**:
- Start with business context (market trends, competitive moves, customer insights)
- Connect roadmap themes to company OKRs
- Show expected business outcomes (revenue impact, retention improvement)
- Present resource allocation across themes
- End with risks and tradeoffs

**Tips**:
- Use outcome language: "This will increase retention by 5%" not "We're building a notification system"
- Present 3-5 themes, not 20 features
- Always include what you are NOT doing and why
- Prepare for "what about X?" questions with a prioritization rationale

### Sales Audience

Sales teams need to know what is coming, when, and how to position it with prospects.

**Presentation format**:
- Organize by customer pain points, not product areas
- Include competitive positioning for new capabilities
- Provide estimated availability (quarter, not specific date)
- Include talk tracks and objection-handling guidance

**Tips**:
- Never share exact dates — say "Q3" not "August 15"
- Create a "customer-safe" version with no internal details
- Highlight features that directly address common lost-deal reasons
- Include a feedback loop for deal-critical feature requests

### Engineering Audience

Engineers need technical detail, dependencies, and capacity planning information.

**Presentation format**:
- Feature-level detail with technical context
- Dependency map (which features depend on which infrastructure work)
- Capacity allocation (percentage of sprint time per theme)
- Technical debt allocation (recommend 15-25% of capacity)

## Managing Expectations

### Setting Expectations Upfront

Establish these norms when presenting any roadmap:

| Expectation | Statement |
|------------|-----------|
| Roadmap ≠ Promise | "This represents our current best thinking on priorities. It will change as we learn more." |
| Timeframes are estimates | "Quarters are directional, not commitments. We'll update monthly." |
| Tradeoffs are explicit | "Choosing to do X means we cannot do Y in the same period." |
| Feedback is welcome | "If you see something missing or mis-prioritized, here's how to provide input." |

### Handling "When Will Feature X Ship?"

This is the most common stakeholder question. Handle it with:

1. **Acknowledge**: "That's an important feature. Let me share where it sits."
2. **Context**: "Here's how we prioritize..." (brief framework explanation)
3. **Status**: "It's currently in the [Now/Next/Later] column because..."
4. **Next step**: "If you have new data that changes the priority, share it with me and we'll re-evaluate."

Never answer with a date unless the feature is actively in development with a high-confidence delivery timeline.

### Managing Feature Requests

Create a structured intake process:

| Field | Purpose |
|-------|---------|
| Requester | Who is asking? |
| Customer(s) | Which customers need this? Revenue at stake? |
| Problem Statement | What problem does this solve? (Not the solution, the problem) |
| Business Impact | Revenue, retention, efficiency impact |
| Urgency | Why now? What happens if we delay? |
| Alternatives | Can the need be met with current functionality? |

Route requests through the prioritization framework rather than directly onto the roadmap.

## Communication Cadence

| Communication | Audience | Frequency | Format |
|--------------|----------|-----------|--------|
| Roadmap update email | All stakeholders | Monthly | Written summary with changelog |
| Product review meeting | Leadership | Bi-weekly | Presentation with Q&A |
| Release notes | All employees + customers | Per release | Written (internal and external versions) |
| Product newsletter | Sales, CS, Support | Monthly | Email with upcoming features and positioning |
| Annual strategy | All company | Annually | All-hands presentation |

## Handling Disagreements

When a stakeholder strongly disagrees with prioritization:

1. **Listen fully**: Understand their concern without defending the roadmap
2. **Validate**: "I understand why this is important to you and your customers"
3. **Share the tradeoff**: "Here's what we'd need to defer to accommodate this"
4. **Seek data**: "What data do you have that would change our assessment?"
5. **Offer alternatives**: "Here's a lighter version we could deliver sooner"
6. **Escalate if needed**: "If we can't agree, let's bring this to [decision-maker] with both perspectives documented"

Never change the roadmap in the meeting. Take the input, evaluate it through the process, and follow up with a decision.
