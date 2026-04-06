# RXJS Patterns

RXJS Patterns for Angular Framework — comprehensive strategies, implementation details, and best practices.

---

## Introduction

This reference provides detailed, actionable guidance on rxjs patterns within the context of Angular Framework. Use this document as a deep-dive resource when implementing the strategies outlined in the main SKILL.md file.

## Angular RXJS Patterns

### Core RxJS Concepts in Angular

Angular heavily relies on RxJS for reactive programming:

### Essential Operators

| Operator | Category | Use Case |
|----------|----------|----------|
| `map` | Transform | Transform emitted values |
| `filter` | Filter | Conditionally pass values |
| `switchMap` | Higher-order | Cancel previous, switch to new |
| `mergeMap` | Higher-order | Run in parallel |
| `concatMap` | Higher-order | Queue sequentially |
| `exhaustMap` | Higher-order | Ignore while processing |
| `debounceTime` | Rate | Wait for pause in emissions |
| `distinctUntilChanged` | Filter | Skip duplicate values |
| `takeUntil` | Complete | Unsubscribe on signal |
| `catchError` | Error | Handle errors in stream |
| `retry` | Error | Retry failed operations |
| `shareReplay` | Multicasting | Share and cache |

### Common Patterns

```typescript
// Search with debounce
this.searchControl.valueChanges.pipe(
  debounceTime(300),
  distinctUntilChanged(),
  switchMap(term => this.searchService.search(term)),
  catchError(err => of([]))
).subscribe(results => this.results = results);

// Auto-unsubscribe pattern
private destroy$ = new Subject<void>();
ngOnDestroy() { this.destroy$.next(); this.destroy$.complete(); }

ngOnInit() {
  this.data$.pipe(takeUntil(this.destroy$)).subscribe(...);
}
```

### Subjects

| Subject Type | Behavior | Use Case |
|-------------|----------|----------|
| Subject | No initial value, multicast | Event bus |
| BehaviorSubject | Has current value | State management |
| ReplaySubject | Replays N values to new subscribers | Cached data |
| AsyncSubject | Emits last value on complete | One-time results |

### Memory Leak Prevention

- Always unsubscribe from manual subscriptions
- Use `async` pipe in templates when possible (auto-unsubscribes)
- Use `takeUntil` with a destroy subject for component subscriptions
- Avoid subscribing inside `subscribe` (use higher-order operators instead)


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
