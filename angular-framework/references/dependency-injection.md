# Dependency Injection

Dependency Injection for Angular Framework — comprehensive strategies, implementation details, and best practices.

---

## Introduction

This reference provides detailed, actionable guidance on dependency injection within the context of Angular Framework. Use this document as a deep-dive resource when implementing the strategies outlined in the main SKILL.md file.

## Angular Dependency Injection

### Understanding Angular DI

Angular's dependency injection system is hierarchical and provides:

- **Singleton services**: `providedIn: 'root'` for app-wide singletons
- **Component-level providers**: New instance per component tree
- **Module-level providers**: Scoped to lazy-loaded modules

### Injection Tokens

```typescript
// Create an injection token for configuration
export const API_CONFIG = new InjectionToken<ApiConfig>('api.config');

// Provide in module
@NgModule({
  providers: [{ provide: API_CONFIG, useValue: { baseUrl: '/api' } }]
})
export class AppModule {}

// Inject in component or service
constructor(@Inject(API_CONFIG) private config: ApiConfig) {}
```

### Provider Types

| Provider | Syntax | Use Case |
|----------|--------|----------|
| useClass | `{ provide: X, useClass: Y }` | Substitute implementation |
| useValue | `{ provide: X, useValue: val }` | Configuration objects |
| useFactory | `{ provide: X, useFactory: fn }` | Dynamic creation |
| useExisting | `{ provide: X, useExisting: Y }` | Alias to another provider |

### Advanced Patterns

- **Multi providers**: `multi: true` for extensible provider lists
- **Optional injection**: `@Optional()` decorator for optional dependencies
- **Self/SkipSelf**: Control injector hierarchy traversal
- **Tree-shakable providers**: Use `providedIn` for automatic tree-shaking


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
