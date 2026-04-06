# Advanced Commands

Advanced Commands for Git Version Control — comprehensive strategies, implementation details, and best practices.

---

## Introduction

This reference provides detailed, actionable guidance on advanced commands within the context of Git Version Control. Use this document as a deep-dive resource when implementing the strategies outlined in the main SKILL.md file.

## Git Advanced Commands

### Interactive Rebase

```bash
# Rewrite last 5 commits
git rebase -i HEAD~5

# Commands: pick, reword, edit, squash, fixup, drop
# pick = use commit
# reword = use commit, edit message
# squash = meld into previous commit
# fixup = like squash but discard message
# drop = remove commit
```

### Cherry-Pick

```bash
# Apply specific commit to current branch
git cherry-pick <commit-hash>

# Cherry-pick without committing
git cherry-pick --no-commit <commit-hash>

# Cherry-pick range
git cherry-pick A..B
```

### Stash Operations

```bash
git stash push -m "description"   # Stash with message
git stash list                      # View stash list
git stash pop                       # Apply and remove
git stash apply stash@{2}           # Apply specific stash
git stash branch <branch> stash@{0} # Create branch from stash
```

### Bisect (Binary Search for Bugs)

```bash
git bisect start
git bisect bad              # Current commit is broken
git bisect good <commit>    # Known good commit
# Git checks out middle commit — test and mark good/bad
git bisect good/bad
git bisect reset            # Return to original state
```

### Reflog (Recovery)

```bash
git reflog                  # View all HEAD movements
git checkout HEAD@{5}       # Go to specific reflog entry
git branch recovery HEAD@{3} # Create branch at reflog point
```


## Implementation Checklist

Use this checklist to ensure complete implementation:

- [ ] Review current state and identify gaps
- [ ] Define clear objectives and success metrics
- [ ] Create implementation plan with timeline
- [ ] Set up necessary tools and integrations
- [ ] Configure tracking and measurement
- [ ] Document processes and playbooks
- [ ] Train team members on new processes
- [ ] Launch pilot and gather feedback
- [ ] Iterate based on initial results
- [ ] Scale successful approaches across organization
- [ ] Establish regular review cadence
- [ ] Create reporting dashboard for stakeholders


## Common Pitfalls and How to Avoid Them

| Pitfall | Why It Happens | How to Avoid |
|---------|---------------|---------------|
| Analysis paralysis | Too much data, not enough action | Set decision deadlines, use frameworks |
| Premature scaling | Scaling before validating | Prove ROI at small scale first |
| Ignoring data | Relying on gut feelings | Build data review into process |
| Tool overload | Adding tools without strategy | Audit tool stack quarterly |
| Siloed execution | Teams working independently | Regular cross-functional syncs |
| Inconsistent measurement | Different teams, different metrics | Standardize KPI definitions |
| Set-and-forget | Launching without ongoing optimization | Schedule regular optimization reviews |


## Key Metrics and KPIs

Track these metrics to measure success:

| Metric | Description | Measurement Frequency | Target |
|--------|------------|----------------------|--------|
| Efficiency | Output per resource invested | Weekly | Improving trend |
| Quality | Error rate or satisfaction score | Weekly | >95% |
| Velocity | Speed of execution or delivery | Sprint/Weekly | Stable or improving |
| Impact | Business outcome achieved | Monthly | Meeting objectives |
| ROI | Return on investment | Quarterly | Positive and growing |


## Additional Resources and References

### Recommended Learning Path

1. **Beginner**: Understand core concepts and terminology
2. **Intermediate**: Apply frameworks to real scenarios
3. **Advanced**: Optimize and scale proven approaches
4. **Expert**: Innovate and develop custom methodologies

### Industry Standards and Frameworks

- Follow established industry frameworks as starting points
- Adapt frameworks to your specific context and constraints
- Stay current with industry publications and thought leaders
- Participate in professional communities for peer learning
- Document your own best practices and share with team

### Continuous Improvement

- Schedule quarterly strategy reviews
- Maintain a backlog of improvement ideas
- Allocate time for experimentation (10-20%)
- Benchmark against competitors and industry leaders
- Invest in team development and training
