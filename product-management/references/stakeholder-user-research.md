# Stakeholder and User Research

Methods for planning user research, conducting interviews, managing stakeholders, and synthesizing findings.

---

## User Research Methods

### Method Selection Guide

| Method | Best For | Sample Size | Time | Cost |
|--------|---------|-------------|------|------|
| User Interviews | Deep understanding, discovery | 5-15 | 2-4 weeks | Low |
| Usability Testing | Evaluating designs and flows | 5-8 | 1-2 weeks | Low |
| Surveys | Quantifying attitudes, preferences | 100-1000+ | 1-2 weeks | Low-Medium |
| A/B Testing | Validating design decisions with data | 1000+ visitors | 2-4 weeks | Low |
| Card Sorting | Information architecture, navigation | 15-30 | 1-2 weeks | Low |
| Diary Studies | Longitudinal behavior, habits | 10-20 | 2-8 weeks | Medium |
| Analytics Review | Usage patterns, funnel analysis | All users | Days | Free |
| Competitive Analysis | Market positioning, feature gaps | 5-10 competitors | 1-2 weeks | Low |

### When to Use Each Method

| Product Stage | Primary Methods | Purpose |
|--------------|----------------|---------|
| Pre-product | Interviews, surveys, competitor analysis | Validate problem and market |
| MVP | Usability testing, interviews | Test core experience |
| Growth | A/B testing, analytics, surveys | Optimize conversion and engagement |
| Mature | Diary studies, interviews, analytics | Discover new opportunities |

## User Interview Guide

### Preparation

1. **Define the research question**: What specific thing do you want to learn?
2. **Write a discussion guide**: 8-12 open-ended questions organized by topic
3. **Recruit participants**: Target 5-8 participants from the relevant user segment
4. **Schedule logistics**: 30-60 minutes per session, recording consent, note-taker assigned

### Interview Question Templates

**Opening** (build rapport):
- "Tell me about your role and what a typical day looks like."
- "How long have you been doing [relevant activity]?"

**Problem exploration**:
- "Walk me through the last time you [relevant task]. What happened?"
- "What was the hardest part of that experience?"
- "How do you currently solve [problem]? What tools do you use?"

**Depth probing**:
- "You mentioned [specific thing]. Can you tell me more about that?"
- "Why is that important to you?"
- "What would happen if you couldn't do that?"

**Closing**:
- "If you had a magic wand, what one thing would you change about [process]?"
- "Is there anything I should have asked but didn't?"

### What NOT to Ask

| Bad Question | Problem | Better Alternative |
|-------------|---------|-------------------|
| "Would you use this feature?" | Hypothetical — people are bad at predicting | "How do you currently handle this?" |
| "Do you think this is easy to use?" | Leading — invites social desirability | "Show me how you would complete this task" |
| "Don't you think X is a problem?" | Leading — puts words in their mouth | "Tell me about challenges you face with X" |
| "How much would you pay?" | Unreliable without real purchasing context | "What do you currently spend on solving this?" |

## Research Synthesis

### Affinity Mapping

1. Write each observation on a sticky note (physical or digital — Miro, FigJam)
2. Group similar observations into clusters
3. Name each cluster with a theme statement
4. Identify the top 3-5 themes by frequency and impact
5. Write insight statements: "Users need [need] because [reason], which means [implication]"

### Insight-to-Action Framework

| Insight | User Need | Opportunity | Confidence | Next Step |
|---------|----------|-------------|-----------|-----------|
| Users spend 30 min daily copying data between tools | Automated data sync | Integration feature | High (8/8 mentioned) | Prototype |
| Users create workaround spreadsheets for reporting | Customizable dashboards | Report builder | Medium (5/8 mentioned) | More research |
| New users struggle to find key features | Guided onboarding | Setup wizard | High (observed in 6/6 tests) | Design sprint |

## Stakeholder Management

### RACI Matrix for Product Decisions

| Decision | Product (PM) | Engineering | Design | Leadership | Sales |
|----------|-------------|-------------|--------|-----------|-------|
| Feature prioritization | A | C | C | I | C |
| Technical architecture | C | A | I | I | — |
| UX design | C | C | A | I | I |
| Pricing | C | I | I | A | C |
| Go-to-market | C | I | C | I | A |

R = Responsible, A = Accountable, C = Consulted, I = Informed

### Stakeholder Communication Cadence

| Audience | Format | Frequency | Content |
|----------|--------|-----------|---------|
| Engineering | Sprint planning, standups | Weekly | Priorities, requirements, decisions |
| Design | Discovery sync, design reviews | Weekly | Research findings, design feedback |
| Leadership | Product review | Bi-weekly | OKR progress, roadmap updates, risks |
| Sales | Product update | Monthly | New features, positioning, objection handling |
| Customers | Release notes, webinars | Per release | New capabilities, migration guides |
