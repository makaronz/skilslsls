# Troubleshooting

Troubleshooting for NPM Package Management — comprehensive strategies, implementation details, and best practices.

---

## Introduction

This reference provides detailed, actionable guidance on troubleshooting within the context of NPM Package Management. Use this document as a deep-dive resource when implementing the strategies outlined in the main SKILL.md file.

## npm Troubleshooting

### Common npm Issues

| Problem | Solution |
|---------|----------|
| `ERESOLVE` dependency conflicts | `npm install --legacy-peer-deps` or resolve conflicts |
| Stale cache | `npm cache clean --force` |
| Permission errors | Fix npm prefix or use nvm |
| Module not found | Delete `node_modules` and reinstall |
| Peer dependency warnings | Install required peer deps manually |
| Publish fails | Check npm login, package name availability |

### Nuclear Reset

```bash
rm -rf node_modules package-lock.json
npm cache clean --force
npm install
```

### Debugging Dependency Trees

```bash
npm ls                      # View full dependency tree
npm ls <package>            # Find where a package is installed
npm explain <package>       # Explain why a package is installed
npm outdated                # List outdated packages
```

### Performance

- Use `npm ci` in CI (faster, uses lock file exactly)
- Consider `node_modules` caching in CI pipelines
- Reduce install time with `--ignore-scripts` when safe


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
