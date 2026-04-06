# Card Sorting & Tree Testing

Practical techniques for card sorting studies, tree testing validation, and IA research methods that ensure navigation structures match user mental models.

---

## Card Sorting Overview

Card sorting is a user research method where participants organize content items into groups that make sense to them. It directly reveals user mental models for information organization.

### Card Sorting Types

| Type | How It Works | When to Use | Output |
|------|-------------|------------|--------|
| **Open card sort** | Participants create their own groups and name them | Early exploration; no existing IA; discovering mental models | Category candidates and labels |
| **Closed card sort** | Participants sort items into predefined categories | Validating proposed IA; testing category labels | Category fit percentage per item |
| **Hybrid card sort** | Predefined categories, but participants can create new ones | Validating IA while discovering gaps | Category fit + new category suggestions |
| **Reverse card sort** (tree test) | Participants find items within an existing structure | Validating hierarchy; measuring findability | Task success rates and paths |

### When to Use Each Type

| Project Phase | Card Sort Type | Goal |
|--------------|---------------|------|
| Discovery (no IA exists) | Open | Learn how users naturally group content |
| Design (draft IA exists) | Closed or Hybrid | Validate proposed categories |
| Refinement (IA exists, issues reported) | Closed | Test specific problematic areas |
| Validation (IA finalized) | Tree test | Confirm findability before build |

---

## Running an Open Card Sort

### Planning

**Number of cards:** 30–60 items is ideal. Below 20 is too few for meaningful grouping; above 80 causes fatigue.

**Card content guidelines:**

| Do | Don't |
|----|-------|
| Use actual content titles or page names | Use internal jargon or code names |
| Keep card labels concise (2–5 words) | Write full sentences on cards |
| Include a mix of content types | Only include one type of content |
| Randomize card order for each participant | Present in alphabetical or structural order |
| Pilot test cards with 2–3 people first | Skip piloting |

**Participant requirements:**
- 15–30 participants for stable results
- Recruit from target user segments
- Include mix of expertise levels
- Remote or in-person both work well

### Facilitation Script

```
## Open Card Sort: Facilitator Guide

### Introduction (2 min)
"We're working on organizing [product/website] content. We'd like
your help figuring out how to group things in a way that makes
sense to you. There are no right or wrong answers — we want your
natural instinct."

### Task Instructions (1 min)
"You'll see [N] cards, each with a content item or page name.
Please:
1. Look through all the cards first
2. Group them in whatever way makes sense to you
3. Give each group a name that describes what's in it
4. It's OK to create an 'Unsure' pile for items you can't place"

### During the Sort (15–25 min)
- Observe silently; don't guide
- Note hesitations or out-loud reasoning
- Don't answer questions about where items "should" go

### Debrief (5–10 min)
"Walk me through your groups:
- Why did you group these together?
- Was anything hard to place? Why?
- Were any groups hard to name?
- Is there anything you would have split further?"
```

### Analyzing Open Card Sort Results

**Step 1: Create a similarity matrix**

Count how many participants placed each pair of items together:

| | Item A | Item B | Item C | Item D |
|---|:------:|:------:|:------:|:------:|
| Item A | — | 80% | 20% | 15% |
| Item B | 80% | — | 25% | 10% |
| Item C | 20% | 25% | — | 75% |
| Item D | 15% | 10% | 75% | — |

**Step 2: Identify clusters**

Items paired by ≥60% of participants should be in the same category. Items paired by 30–59% might belong in the same category. Items below 30% likely belong in different categories.

**Step 3: Analyze category labels**

| Proposed Category | Participant Labels Used | Consensus Level |
|------------------|----------------------|----------------|
| Account Settings | "Settings" (12), "My Account" (8), "Profile" (5) | High — "Settings" is the preferred label |
| Help Resources | "Help" (10), "Support" (7), "Learning" (5), "Resources" (3) | Medium — "Help" or "Support" both viable |
| Project Tools | "Projects" (6), "Work" (5), "Tools" (4), "Tasks" (4) | Low — no clear winner; test further |

---

## Running a Closed Card Sort

### Setup

Provide predefined category names and ask participants to place items.

```
## Categories Provided to Participants
1. Dashboard
2. Projects
3. Team
4. Reports
5. Settings
6. Help & Support

## Cards to Sort: [30–50 items]
```

### Success Criteria

| Metric | Target | What It Tells You |
|--------|--------|-------------------|
| **Agreement rate** | >70% of participants place item in same category | Strong category fit |
| **Disputed items** | <15% of items with no clear category winner | Categories cover content well |
| **Category balance** | No category gets >40% of all items | Categories are appropriately scoped |
| **"None of the above"** | <10% of placements | Categories are comprehensive enough |

### Interpreting Results

| Result Pattern | Meaning | Action |
|---------------|---------|--------|
| Item placed 80%+ in one category | Strong fit | Confirm placement |
| Item split 50/50 between two categories | Ambiguous — could belong in either | Cross-link; place in primary; add to secondary |
| Item spread across 3+ categories | Confusing item or missing category | Rewrite card label; consider new category |
| Category receives very few items | Category may be too narrow | Merge with related category |
| Category receives too many items | Category may be too broad | Split into subcategories |

---

## Tree Testing

Tree testing (also called reverse card sorting) validates whether users can find content within your proposed navigation hierarchy. It tests the IA structure independent of visual design.

### How Tree Testing Works

1. Create a text-only version of your navigation hierarchy (the "tree")
2. Write task scenarios that require users to find specific content
3. Participants navigate the tree to find where they'd expect each item
4. Measure success rate, directness, and time per task

### Creating the Tree

```
Home
├─ Dashboard
├─ Projects
│  ├─ Active Projects
│  ├─ Archived Projects
│  └─ Templates
├─ Team
│  ├─ Members
│  ├─ Roles & Permissions
│  └─ Invitations
├─ Reports
│  ├─ Project Reports
│  ├─ Time Reports
│  └─ Custom Reports
├─ Settings
│  ├─ Account
│  ├─ Billing
│  ├─ Notifications
│  └─ Integrations
└─ Help
   ├─ Getting Started
   ├─ Knowledge Base
   └─ Contact Support
```

**Tree design rules:**
- Maximum 3–4 levels of depth
- 5–7 top-level categories
- No category should have more than 10 children
- Use real labels (same words users will see in the product)

### Writing Tree Test Tasks

| Guideline | Bad Task | Good Task |
|-----------|---------|----------|
| Use realistic scenarios | "Find Notifications" | "You want to stop getting email alerts for project updates" |
| Don't use menu labels | "Go to Settings" | "You need to connect your Slack workspace" |
| One correct answer | "Find team info" (vague) | "You need to give a new hire access to the project" |
| Vary difficulty | All easy tasks | Mix of shallow (level 1–2) and deep (level 3–4) tasks |

### Tree Test Metrics

| Metric | Definition | Target | Interpretation |
|--------|-----------|--------|----------------|
| **Task success rate** | % of participants who found the correct answer | >80% | Below 60% = IA problem; needs restructuring |
| **Directness** | % who found the answer without backtracking | >60% | Low directness = confusing labels or structure |
| **Time to complete** | Average seconds per task | Varies by depth | Significantly longer than expected = IA friction |
| **First click correctness** | % who clicked the right top-level category first | >70% | Low = top-level labels are misleading |
| **Path analysis** | Common navigation paths taken | N/A | Reveals where users get lost or confused |

### Interpreting Tree Test Results

| Result | Diagnosis | Fix |
|--------|----------|-----|
| High success, high directness | IA works well for this task | No change needed |
| High success, low directness | Users found it but had to backtrack | Improve labels or cross-link |
| Low success, most fail at same point | Specific label or category is confusing | Rename category or restructure |
| Low success, failures scattered | Fundamental structural problem | Major IA restructure needed |
| Users consistently go to wrong category first | Label mismatch or mental model conflict | Rename; move content; or add alias/redirect |

---

## Tools for Card Sorting and Tree Testing

| Tool | Card Sorting | Tree Testing | Remote/In-Person | Free Tier |
|------|:----------:|:----------:|:----------------:|:---------:|
| **Optimal Workshop** | ✅ | ✅ | Remote | Limited |
| **UserZoom / UserTesting** | ✅ | ✅ | Remote | No |
| **Maze** | ✅ | ✅ | Remote | Limited |
| **UXtweak** | ✅ | ✅ | Remote | Yes |
| **Miro / FigJam** | ✅ (manual) | ❌ | Both | Yes |
| **Physical cards** | ✅ | ❌ | In-person | Yes |
| **Spreadsheet** | ✅ (analysis) | ❌ | N/A | Yes |

---

## Combining Card Sorting and Tree Testing

### Recommended Workflow

| Phase | Method | Purpose | Participants |
|-------|--------|---------|-------------|
| 1. Discovery | Open card sort | Learn user mental models | 20–30 |
| 2. Draft IA | (Design activity) | Create initial hierarchy from sort results | Design team |
| 3. Validate categories | Closed card sort | Confirm items fit proposed categories | 15–20 |
| 4. Refine IA | (Design activity) | Adjust based on closed sort results | Design team |
| 5. Validate findability | Tree test | Confirm users can find content in the hierarchy | 30–50 |
| 6. Iterate | Additional tree tests | Test refinements; compare before/after | 30–50 |

### Reporting Results to Stakeholders

```
## IA Validation Report: [Project Name]

### Method Summary
- Open card sort: [N] participants, [N] cards
- Tree test: [N] participants, [N] tasks

### Key Findings
1. [Finding about category structure]
2. [Finding about problematic labels]
3. [Finding about content placement]

### Recommendations
| Change | Evidence | Impact | Effort |
|--------|----------|--------|--------|
| [Rename X to Y] | [Sort/test data] | [High/Med/Low] | [Low] |
| [Move X under Y] | [Sort/test data] | [High/Med/Low] | [Med] |

### Before/After Comparison
| Task | Success Before | Success After | Change |
|------|:--------------:|:-------------:|:------:|
| [Task 1] | 45% | 82% | +37% |
| [Task 2] | 70% | 78% | +8% |
```

---

## Common Pitfalls

| Pitfall | Impact | Prevention |
|---------|--------|------------|
| Too few participants | Unstable results | 15+ for card sorts; 30+ for tree tests |
| Cards use internal jargon | Results reflect jargon confusion, not real mental models | Use user language; pilot test cards |
| Leading task wording | Inflated success rates that don't reflect real findability | Avoid using navigation labels in task descriptions |
| Only testing happy paths | Miss confusing edge cases | Include tasks for less common but important content |
| Not iterating | First draft IA ships with known problems | Always tree test → refine → re-test |
| Ignoring outlier data | Minority users may represent important segments | Analyze by segment; check if outliers share characteristics |
