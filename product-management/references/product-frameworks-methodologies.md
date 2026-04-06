# Product Frameworks and Methodologies

Comprehensive reference for selecting and applying product development frameworks.

---

## Framework Comparison

| Framework | Philosophy | Best For | Cadence | Team Size |
|-----------|-----------|----------|---------|-----------|
| Lean Startup | Build-Measure-Learn | Early-stage, high uncertainty | Continuous | Small |
| Design Thinking | Empathize-Define-Ideate-Prototype-Test | UX-focused, complex problems | Project-based | Any |
| Jobs-to-be-Done | Customers hire products for jobs | Feature design, positioning | Ongoing research | Any |
| Dual Track Agile | Discovery + Delivery in parallel | Established product teams | Sprint-based | Medium |
| Shape Up | Appetite-based, 6-week cycles | Opinionated teams, autonomy | 6-week cycles | Small-medium |
| SAFe | Scaled Agile, PI Planning | Large enterprises, compliance | 8-12 week increments | Large |

## Lean Startup

### Build-Measure-Learn Loop

1. **Build**: Create the minimum viable product (MVP) that tests a specific hypothesis
2. **Measure**: Collect data on the key metric that validates or invalidates the hypothesis
3. **Learn**: Analyze results and decide to persevere, pivot, or kill

### Hypothesis Template

```
We believe that [specific user segment]
will [expected behavior]
because [underlying reason].
We will know this is true when [measurable signal].
```

### MVP Types

| MVP Type | Purpose | Effort | Example |
|----------|---------|--------|---------|
| Landing Page | Gauge demand before building | Days | Product page with waitlist signup |
| Concierge | Manually deliver the experience | Days-weeks | Do the task by hand for early users |
| Wizard of Oz | Appear automated, human behind the scenes | Weeks | Chatbot with human operator |
| Single Feature | Test one core value prop | Weeks | One feature in production |
| Piecemeal | Combine existing tools to simulate the product | Days | Google Forms + Zapier + Sheets |

## Jobs-to-be-Done (JTBD)

### Job Statement Format

```
When [situation], I want to [motivation], so I can [expected outcome].
```

Examples:
- "When I'm commuting, I want to catch up on news, so I can feel informed at work."
- "When onboarding a new client, I want to set up their account quickly, so I can demonstrate value in the first meeting."

### Outcome-Driven Innovation

Map customer jobs and desired outcomes:

| Job Step | Desired Outcome | Importance | Satisfaction | Opportunity Score |
|---------|----------------|-----------|-------------|------------------|
| Find relevant content | Minimize time spent searching | 9 | 4 | 14 (9 + (9-4)) |
| Compare options | Minimize effort to understand differences | 8 | 6 | 10 |
| Make decision | Increase confidence in choice | 9 | 7 | 11 |

Opportunity Score = Importance + (Importance − Satisfaction). Scores > 12 indicate underserved outcomes.

## Dual Track Agile

### Discovery Track

Runs continuously alongside delivery:
- **Weekly**: Customer interviews (minimum 2 per week)
- **Bi-weekly**: Prototype testing sessions
- **Continuous**: Data analysis of product usage
- **Output**: Validated ideas ready for delivery

### Delivery Track

Standard Agile sprints:
- **Input**: Validated ideas from Discovery
- **Process**: Sprint planning → Development → Testing → Release
- **Output**: Shipped features

### Integration Points

| Activity | Discovery | Delivery | Frequency |
|----------|----------|----------|-----------|
| Sprint Planning | Present validated opportunities | Estimate and commit | Every sprint |
| Retrospective | Share research insights | Share delivery learnings | Every sprint |
| Roadmap Review | Update opportunity backlog | Update delivery backlog | Monthly |

## Shape Up (Basecamp)

### Core Concepts

| Concept | Description |
|---------|-------------|
| **Appetite** | Fixed time budget (2 or 6 weeks) for a project, not an estimate |
| **Pitch** | Shaped problem + solution, presented to leadership for betting |
| **Bet** | Leadership decides which pitches to bet on for the next cycle |
| **Hill Chart** | Visual progress indicator (uphill = figuring out, downhill = executing) |
| **Cooldown** | 2-week period between cycles for bug fixes, exploration, and free work |

### Shaping Process

1. **Set the appetite**: "We're willing to spend 6 weeks on this"
2. **Narrow the problem**: Define the specific problem, not just the feature request
3. **Sketch the solution**: Fat-marker sketches, not detailed mockups — leave room for the team
4. **Identify rabbit holes**: Call out risks and mark what is NOT included
5. **Write the pitch**: Problem, appetite, solution sketch, rabbit holes, no-gos
