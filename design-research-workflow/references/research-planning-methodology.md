# Research Planning & Methodology

Comprehensive guide to selecting research types, building planning frameworks, and designing rigorous studies for design projects.

---

## Research Type Selection

Choose the right research method based on project phase, timeline, and what you need to learn.

### Qualitative vs. Quantitative Research

| Dimension | Qualitative | Quantitative |
|-----------|------------|---------------|
| **Purpose** | Understand *why* and *how* | Measure *what* and *how much* |
| **Data Type** | Words, observations, themes | Numbers, statistics, metrics |
| **Sample Size** | 5–15 participants | 30–1,000+ respondents |
| **Analysis** | Thematic, interpretive | Statistical, computational |
| **Timeline** | 1–4 weeks per round | 1–2 weeks for survey; ongoing for analytics |
| **Best For** | Discovery, exploration, concept validation | Validation, benchmarking, prioritization |
| **Limitations** | Not statistically generalizable | Misses context, nuance, emotion |

### Research Method Quick-Reference

| Method | Type | Best Phase | Time Required | Participants | Output |
|--------|------|-----------|---------------|-------------|--------|
| User Interviews | Qualitative | Discovery | 2–3 weeks | 5–12 | Needs, motivations, pain points |
| Contextual Inquiry | Qualitative | Discovery | 2–4 weeks | 4–8 | Workflow insights, environment context |
| Diary Studies | Qualitative | Discovery/Validation | 1–4 weeks | 8–15 | Longitudinal behavior patterns |
| Surveys | Quantitative | Any | 1–2 weeks | 50–500+ | Preferences, satisfaction, demographics |
| Card Sorting | Mixed | Design | 1–2 weeks | 15–30 | Information architecture validation |
| Usability Testing | Mixed | Validation | 1–3 weeks | 5–8 per round | Task success, friction points |
| A/B Testing | Quantitative | Optimization | 2–6 weeks | 1,000+ | Statistical preference data |
| Analytics Review | Quantitative | Any | 1–3 days | N/A (behavioral data) | Usage patterns, drop-off points |
| Heuristic Evaluation | Qualitative | Audit | 3–5 days | 3–5 evaluators | Usability issues ranked by severity |
| Competitive Benchmarking | Mixed | Discovery | 1–2 weeks | N/A | Market standards, gap analysis |

### Decision Tree for Method Selection

1. **What do you need to learn?**
   - Understanding user needs → User Interviews, Contextual Inquiry
   - Validating a concept → Usability Testing, Surveys
   - Measuring existing performance → Analytics, A/B Testing
   - Exploring new territory → Diary Studies, Ethnography

2. **What stage is the project?**
   - Pre-design discovery → Interviews, Contextual Inquiry, Competitive Analysis
   - During design → Card Sorting, Tree Testing, Concept Testing
   - Post-launch → Usability Testing, Analytics, Surveys

3. **What are the constraints?**
   - Limited budget → Guerrilla Usability, Unmoderated Remote Testing, Surveys
   - Limited time → Heuristic Evaluation, Analytics Review, 5-Second Test
   - Limited access to users → Competitor Analysis, Expert Review, Secondary Research

---

## Research Planning Frameworks

### The Research Brief Template

Every research project starts with a brief that aligns stakeholders:

```
## Research Brief: [Project Name]

### Background
- What is the product/feature?
- What prompted this research?
- What existing knowledge do we have?

### Research Objectives
1. [Primary objective — the must-answer question]
2. [Secondary objective]
3. [Tertiary objective]

### Research Questions
- RQ1: [Specific, answerable question]
- RQ2: [Specific, answerable question]
- RQ3: [Specific, answerable question]

### Methodology
- Method: [Selected method with rationale]
- Participants: [Number, criteria, recruitment plan]
- Timeline: [Key dates and milestones]
- Tools: [Software, equipment needed]

### Deliverables
- [What will be produced: report, personas, journey map, etc.]
- Delivery date: [Target date]

### Stakeholders
- Sponsor: [Who approved this research]
- Consumers: [Who will use the findings]
```

### SMART Research Objectives

Frame objectives using SMART criteria:

| Criterion | Bad Example | Good Example |
|-----------|-------------|---------------|
| **Specific** | Learn about users | Understand how freelancers track project hours |
| **Measurable** | Find usability issues | Identify task completion rates for 5 core workflows |
| **Achievable** | Interview 100 users this week | Conduct 8 interviews over 2 weeks |
| **Relevant** | Study competitor pricing | Study how users navigate between projects |
| **Time-bound** | Do research soon | Complete discovery research by March 15 |

### Research Roadmap Planning

Organize research activities across a project timeline:

| Phase | Research Activities | Duration | Outputs |
|-------|-------------------|----------|--------|
| **Week 1–2: Discovery** | Stakeholder interviews, analytics review, competitive audit | 2 weeks | Research brief, initial hypotheses |
| **Week 3–4: Exploration** | User interviews, contextual inquiry | 2 weeks | Interview transcripts, affinity map |
| **Week 5: Synthesis** | Analysis, persona creation, journey mapping | 1 week | Personas, journey maps, key findings |
| **Week 6–7: Concept Testing** | Prototype testing, card sorting | 2 weeks | Validated concepts, IA structure |
| **Week 8: Validation** | Usability testing with refined prototypes | 1 week | Usability report, design recommendations |

---

## Study Design Principles

### Participant Recruitment

**Screening Criteria Framework:**

| Criterion Type | Examples | Purpose |
|---------------|----------|--------|
| **Must-have** | Uses the product category, age 25–45, specific role | Ensures relevance |
| **Nice-to-have** | Mix of experience levels, geographic diversity | Adds richness |
| **Exclude** | Works in UX/design, competitors' employees | Reduces bias |
| **Demographic mix** | Gender balance, accessibility needs represented | Ensures inclusivity |

**Sample Size Guidelines:**

- Usability testing: 5 per user segment (catches ~85% of issues)
- Interviews: 8–12 for saturation (stop when themes repeat)
- Surveys: 100+ for reliable quantitative data
- Card sorting: 15–30 for stable groupings
- A/B testing: Calculate based on effect size and statistical power

### Interview Guide Structure

Build semi-structured interview guides with this skeleton:

1. **Warm-up** (5 min): Introductions, explain process, get consent
2. **Context questions** (10 min): Role, daily workflow, tools used
3. **Core topic questions** (20 min): Deep dive into research questions
4. **Scenario/task questions** (10 min): Walk through specific situations
5. **Reflection** (5 min): What would improve, anything we missed
6. **Wrap-up** (5 min): Thank, next steps, incentive

**Question Types to Use:**

| Type | Example | When to Use |
|------|---------|------------|
| Open-ended | "Tell me about your last experience with..." | Exploration, discovery |
| Probing | "Can you say more about that?" | Deepening understanding |
| Hypothetical | "If you could change one thing..." | Uncovering latent needs |
| Comparative | "How does this compare to..." | Understanding mental models |
| Task-based | "Walk me through how you would..." | Understanding real behavior |

**Questions to Avoid:**
- Leading: "Don't you think this is easier?" → "How would you describe this experience?"
- Binary: "Is this useful?" → "In what situations would you use this?"
- Future prediction: "Would you use this?" → "Tell me about the last time you needed something like this."

### Usability Test Plan Components

```
## Usability Test Plan: [Feature/Product]

### Objectives
- Measure task completion rate for [core tasks]
- Identify navigation confusion points
- Assess learnability for new users

### Participants
- Number: [5–8 per segment]
- Segments: [Novice / Experienced / Power user]
- Recruitment: [Source and screening criteria]

### Tasks
| # | Task Description | Success Criteria | Time Limit |
|---|-----------------|------------------|------------|
| 1 | [Realistic scenario] | [What counts as success] | [Minutes] |
| 2 | [Realistic scenario] | [What counts as success] | [Minutes] |

### Metrics
- Task success rate (binary: complete/incomplete)
- Time on task
- Error count per task
- System Usability Scale (SUS) score
- Single Ease Question (SEQ) per task

### Environment
- Remote/In-person: [Selection]
- Tools: [Screen sharing, recording, prototype platform]
- Device: [Desktop / Mobile / Both]
```

---

## Ethical Research Practices

### Informed Consent Checklist

- [ ] Purpose of the study explained in plain language
- [ ] Participant understands what they will be asked to do
- [ ] Recording permissions explicitly obtained
- [ ] Right to withdraw at any time without consequence
- [ ] Data handling and privacy policy explained
- [ ] Incentive terms clearly stated
- [ ] Contact information for follow-up questions provided

### Bias Mitigation Strategies

| Bias Type | Description | Mitigation |
|-----------|-------------|------------|
| **Confirmation bias** | Seeking data that supports hypothesis | Use neutral questions; have second researcher review |
| **Sampling bias** | Non-representative participants | Screen carefully; recruit from diverse channels |
| **Social desirability** | Participants say what they think you want | Emphasize no wrong answers; use indirect questions |
| **Observer effect** | Behavior changes when watched | Build rapport; use natural task scenarios |
| **Recency bias** | Over-weighting recent data | Review all data systematically before drawing conclusions |
| **Anchoring** | First data point skews interpretation | Randomize participant order; delay synthesis |

---

## Research Tools and Platforms

| Category | Tools | Use Case |
|----------|-------|----------|
| **Remote Testing** | UserTesting, Maze, Lookback, dscout | Unmoderated/moderated remote sessions |
| **Survey** | Typeform, Google Forms, SurveyMonkey, Qualtrics | Quantitative data collection |
| **Interview** | Zoom, Teams, Google Meet (with recording) | Remote interview sessions |
| **Analysis** | Dovetail, Reframer, Miro, FigJam | Tagging, affinity mapping, synthesis |
| **Recruitment** | User Interviews, Respondent, Ethnio | Finding qualified participants |
| **Prototype Testing** | Figma, Maze, UsabilityHub, Optimal Workshop | Click-through prototype testing |
| **Analytics** | Google Analytics, Mixpanel, Hotjar, FullStory | Behavioral data and heatmaps |

---

## Research Planning Checklist

- [ ] Research objectives defined and aligned with stakeholders
- [ ] Appropriate methodology selected with clear rationale
- [ ] Participant criteria and recruitment plan established
- [ ] Interview guide or test script drafted and piloted
- [ ] Consent forms and ethics considerations addressed
- [ ] Recording and note-taking logistics arranged
- [ ] Analysis approach planned before data collection
- [ ] Deliverables and timeline communicated to stakeholders
- [ ] Budget approved (incentives, tools, recruiting fees)
