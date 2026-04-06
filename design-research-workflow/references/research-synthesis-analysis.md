# Research Synthesis & Analysis

Methods for transforming raw research data into structured insights using affinity mapping, thematic analysis, and systematic extraction techniques.

---

## From Raw Data to Actionable Insights

Research synthesis bridges the gap between collected data and design decisions. The goal is to move from individual observations to patterns, and from patterns to actionable insights that drive design.

### The Synthesis Pipeline

```
Raw Data → Organized Data → Codes → Themes → Insights → Recommendations
```

| Stage | Input | Activity | Output |
|-------|-------|----------|--------|
| **Capture** | Interview recordings, notes | Transcribe, tag, timestamp | Clean transcripts, observation logs |
| **Organize** | Transcripts, observations | Affinity mapping, clustering | Grouped data points |
| **Code** | Grouped data | Label patterns, tag behaviors | Code book with categories |
| **Theme** | Coded data | Identify recurring themes | 5–8 major themes |
| **Insight** | Themes | Extract meaning, find tensions | Insight statements |
| **Recommend** | Insights | Connect to design opportunities | Prioritized recommendations |

---

## Affinity Mapping

Affinity mapping (also called affinity diagramming or KJ Method) is the primary technique for organizing qualitative research data into meaningful groups.

### Process Steps

1. **Extract observations** — Write each distinct observation, quote, or data point on a sticky note (physical or digital). One idea per note.
2. **Spread everything out** — Make all notes visible simultaneously. Do not pre-categorize.
3. **Silent grouping** — Team members silently move notes into clusters that feel related. No discussion during this phase.
4. **Name the groups** — Once clusters stabilize, give each group a descriptive label that captures the theme.
5. **Create hierarchy** — Group related clusters into super-categories if needed.
6. **Document** — Photograph or screenshot the final arrangement.

### Affinity Mapping Best Practices

| Practice | Why It Matters |
|----------|---------------|
| Use participant quotes, not interpretations | Keeps data grounded in reality |
| One observation per sticky note | Allows flexible regrouping |
| Include participant ID on each note | Enables tracing back to source |
| Do silent sorting before discussion | Prevents groupthink |
| Aim for 5–10 top-level groups | More than 10 means insufficient abstraction |
| Allow "outlier" group for unclassifiable items | Some data doesn't fit — that's OK |
| Re-sort if groups feel wrong | Iteration improves quality |

### Affinity Mapping Template

```
## Affinity Map: [Research Project Name]

### Group 1: [Theme Label]
- "[Direct quote]" — P3
- [Observation from contextual inquiry] — P1
- [Behavioral pattern noted] — P5, P7

### Group 2: [Theme Label]
- "[Direct quote]" — P2
- [Observation] — P4
- [Pattern] — P1, P6

### Outliers (Ungrouped)
- [Interesting but doesn't fit current groups]
```

**Recommended tools:** Miro (remote workshops, real-time collaboration), FigJam (design team synthesis), Dovetail (ongoing research programs with auto-tagging), Notion (smaller teams), or a physical wall (co-located teams).

---

## Thematic Analysis

Thematic analysis is a systematic method for identifying, analyzing, and reporting patterns (themes) within qualitative data. It works with any qualitative data source — interviews, diary studies, open-ended survey responses, observation notes.

### Six-Phase Thematic Analysis (Braun & Clarke)

| Phase | Activity | Output |
|-------|----------|--------|
| 1. Familiarization | Read and re-read all data, note initial ideas | Annotations, initial impressions |
| 2. Generating Codes | Systematically code interesting features across dataset | Code list with data extracts |
| 3. Searching for Themes | Collate codes into potential themes | Theme candidates with supporting codes |
| 4. Reviewing Themes | Check themes against coded data and full dataset | Refined theme map |
| 5. Defining Themes | Name and define each theme clearly | Theme definitions and scope |
| 6. Reporting | Select compelling examples, write narrative | Final analysis report |

### Coding Techniques

**Descriptive Coding** — Summarize the topic of a passage in a word or short phrase.
- Example: "I always forget where the export button is" → Code: `navigation-confusion`

**In-Vivo Coding** — Use the participant's exact words as the code.
- Example: "It feels like a maze" → Code: `feels-like-a-maze`

**Process Coding** — Use gerunds (-ing words) to capture actions.
- Example: User switching between three apps to complete task → Code: `context-switching`

**Emotion Coding** — Capture the emotional dimension.
- Example: User sighs heavily when form resets → Code: `frustration-data-loss`

### Code Book Template

| Code | Definition | Example Data | Frequency |
|------|------------|-------------|----------|
| `navigation-confusion` | User cannot locate a feature or page | "I never know where settings are" — P3 | 7/12 participants |
| `time-pressure` | User feels rushed or constrained by workflow | "I don't have time to figure this out" — P8 | 5/12 participants |
| `workaround-created` | User developed non-standard method to accomplish task | P2 uses spreadsheet instead of built-in reporting | 4/12 participants |

### Theme Quality Criteria

A good theme should:

- **Capture something meaningful** about the data in relation to your research questions
- **Be supported by multiple data points** (not just one participant's view)
- **Have clear boundaries** — distinguishable from other themes
- **Be internally coherent** — data within the theme should be consistent
- **Tell a story** — contribute to a narrative about user experience

---

## Insight Extraction

Insights are the bridge between research findings and design action. A good insight reframes observed behavior into an opportunity.

### Insight Statement Formula

```
[User segment] needs [need/goal] because [motivation/reason],
but currently [barrier/pain point], which results in [consequence].
```

**Example:**
> Freelance designers need to quickly find past project assets because they reuse elements across client work, but currently they rely on manual folder searching across multiple cloud storage apps, which results in 15–30 minutes of wasted time per project.

### Insight Quality Framework

| Criterion | Weak Insight | Strong Insight |
|-----------|-------------|----------------|
| **Specificity** | "Users want it to be easier" | "Users abandon the export flow at the format selection step because they don't understand the difference between PNG and SVG" |
| **Evidence-based** | "We think users prefer dark mode" | "7 of 12 participants used dark mode; 3 cited reduced eye strain during evening work" |
| **Actionable** | "The onboarding is confusing" | "New users skip the tutorial because it launches immediately on first login before they have context for the features" |
| **Surprising** | "Users want fast load times" | "Power users intentionally slow down to review each step, contradicting our speed-optimization hypothesis" |
| **Connected** | Isolated data point | Links user behavior to business metric (e.g., drop-off rate, support tickets) |

### Insight Prioritization Matrix

| Insight | User Impact | Business Impact | Frequency | Feasibility | Priority Score |
|---------|-----------|----------------|-----------|-------------|---------------|
| [Insight 1] | High (3) | High (3) | 8/12 users | Medium (2) | 8 |
| [Insight 2] | Medium (2) | High (3) | 5/12 users | High (3) | 8 |
| [Insight 3] | High (3) | Medium (2) | 10/12 users | Low (1) | 6 |

Score = User Impact + Business Impact + Feasibility (each 1–3)

---

## Pattern Recognition Techniques

### Cross-Participant Analysis

Look for patterns that appear across multiple participants:

| Pattern Type | What to Look For | Example |
|-------------|-----------------|--------|
| **Behavioral** | Same action taken by multiple users | 6/8 users right-click to find export |
| **Mental model** | Shared expectation of how something should work | Users expect drag-and-drop in the file manager |
| **Emotional** | Consistent emotional response to same stimulus | Frustration at multi-step confirmation dialogs |
| **Workaround** | Same problem solved with non-standard method | Multiple users use browser bookmarks instead of app navigation |
| **Vocabulary** | Consistent terminology users employ | Users say "board" not "project view" |

### Contradiction Analysis

Look for contradictions \u2014 they're often the most valuable findings. Watch for: say vs. do gaps (users want feature X but never use it), segment differences (power users love complexity that frustrates beginners), and context shifts (different behavior on mobile vs. desktop).

---

## Synthesis Workshop Facilitation

### Workshop Agenda (Half-Day)

| Time | Activity | Purpose |
|------|----------|--------|
| 0:00–0:15 | Research overview and ground rules | Align the team |
| 0:15–0:45 | Individual data review (silent reading) | Familiarization |
| 0:45–1:30 | Affinity mapping (silent sort, then discuss) | Pattern identification |
| 1:30–1:45 | Break | — |
| 1:45–2:30 | Theme naming and insight generation | Move from data to meaning |
| 2:30–3:15 | "How might we" brainstorm from insights | Bridge to design opportunities |
| 3:15–3:30 | Prioritization dot-voting | Focus on highest-impact insights |
| 3:30–4:00 | Document and assign next steps | Ensure action |

### "How Might We" (HMW) Conversion

Convert insights to design opportunities using the format: "How might we [verb] [user need]?"

| Insight | HMW Statement |
|---------|---------------|
| Users lose context when switching between views | HMW help users maintain context across navigation? |
| New members don't know which templates to use | HMW guide new users toward the right starting template? |

---

## Synthesis Output Artifacts

### Key Findings Summary Template

```
## Research Findings: [Project Name]
### Date: [Date] | Method: [Method] | Participants: [N]

### Top Findings
1. **[Finding title]**: [1–2 sentence summary with data support]
2. **[Finding title]**: [1–2 sentence summary with data support]
3. **[Finding title]**: [1–2 sentence summary with data support]

### Themes
| Theme | Description | Supporting Evidence | Participant Count |
|-------|-------------|--------------------|-----------------|
| [Theme 1] | [What this theme captures] | [Key quotes/observations] | [N/total] |

### Insights
| # | Insight Statement | Severity | Opportunity |
|---|------------------|----------|-------------|
| 1 | [Full insight statement] | High/Med/Low | [Design opportunity] |

### Recommended Actions
| Priority | Action | Insight Link | Owner | Timeline |
|----------|--------|-------------|-------|----------|
| P0 | [Immediate fix] | Insight #1 | [Who] | [When] |
| P1 | [Design change] | Insight #2 | [Who] | [When] |
```

---

## Common Synthesis Pitfalls

| Pitfall | Description | Prevention |
|---------|-------------|------------|
| **Cherry-picking** | Only selecting data that supports a hypothesis | Review all data before forming conclusions |
| **Over-generalization** | "All users want..." based on small sample | Use precise language: "7 of 12 participants..." |
| **Premature solutions** | Jumping to design fixes during analysis | Separate analysis from ideation phases |
| **Lost context** | Extracting quotes without surrounding context | Include participant context with every data point |
| **Recency bias** | Last interview dominates memory | Use structured notes; weight all sessions equally |
| **Theme inflation** | Creating too many themes | Aim for 5–8 themes; merge overlapping ones |
