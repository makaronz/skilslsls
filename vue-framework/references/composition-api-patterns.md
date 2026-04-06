# Composition API Patterns

Composition API Patterns for Vue Framework — comprehensive strategies, implementation details, and best practices.

---

## Introduction

This reference provides detailed, actionable guidance on composition api patterns within the context of Vue Framework. Use this document as a deep-dive resource when implementing the strategies outlined in the main SKILL.md file.

## Vue.js Composition API Patterns

### Composition API Fundamentals

```typescript
import { ref, computed, watch, onMounted } from 'vue';

export default defineComponent({
  setup() {
    const count = ref(0);
    const doubled = computed(() => count.value * 2);

    watch(count, (newVal, oldVal) => {
      console.log(`Count changed: ${oldVal} → ${newVal}`);
    });

    onMounted(() => { console.log('Component mounted'); });

    return { count, doubled };
  }
});
```

### Composables (Custom Hooks)

Extract reusable logic into composable functions:

```typescript
// useFetch.ts
export function useFetch<T>(url: string) {
  const data = ref<T | null>(null);
  const error = ref<Error | null>(null);
  const loading = ref(true);

  fetch(url)
    .then(res => res.json())
    .then(json => { data.value = json; })
    .catch(err => { error.value = err; })
    .finally(() => { loading.value = false; });

  return { data, error, loading };
}
```

### Reactivity Deep Dive

| API | Use Case | Unwrap Behavior |
|-----|----------|----------------|
| `ref` | Primitive values | Auto-unwrap in templates |
| `reactive` | Objects | No `.value` needed |
| `computed` | Derived state | Cached, lazy |
| `shallowRef` | Large objects | Only top-level reactive |
| `toRefs` | Destructure reactive | Maintain reactivity |

### Provide/Inject

- Use `provide`/`inject` for deep component tree communication
- Define injection keys with `InjectionKey<T>` for type safety
- Prefer props for parent-child; provide/inject for deeply nested


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
