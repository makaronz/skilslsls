# WIP Limits Optimization

Strategies for setting, adjusting, and enforcing Work-in-Progress limits to maximize flow and minimize cycle time.

---

## Why WIP Limits Matter

WIP limits are the core mechanism that transforms a task board into a Kanban system. Without WIP limits, you have a visual board; with them, you have a pull system.

### Effects of Excessive WIP

| Symptom | Cause | Impact |
|---------|-------|--------|
| Long cycle times | Context switching, items waiting in queues | Delayed delivery, missed deadlines |
| Low quality | Rushing between tasks, insufficient focus | More bugs, rework |
| Hidden bottlenecks | Everything appears "in progress" | Cannot identify constraints |
| Unpredictable delivery | High variability in cycle time | Cannot make reliable commitments |
| Team burnout | Constant multitasking, no sense of completion | Decreased morale and productivity |

## Setting Initial WIP Limits

### Rule of Thumb Approaches

| Method | Formula | Example (5-person team) |
|--------|---------|------------------------|
| N+1 | Team size + 1 buffer | WIP = 6 |
| N×1.5 | Team size × 1.5 | WIP = 7-8 |
| Historical | Average observed WIP | Measure current WIP for 2 weeks, start there |
| Stretch | Current WIP × 0.8 | If current average is 12, set WIP = 10 |

Start with a WIP limit that is slightly uncomfortable but not paralyzing. The goal is to create tension that surfaces problems without stopping all work.

### Per-Column WIP Limits

Set limits for each active work column:

| Column | Suggested Limit | Rationale |
|--------|----------------|-----------|
| Development | 2 per developer | Allow one active + one context switch |
| Code Review | Team size | Each developer can review one item |
| QA | 2-3 | Prevent QA from becoming bottleneck |
| Deployment | 1-2 | Encourage frequent, small deploys |

### System-Level WIP Limit

Also set a total WIP limit across all active columns:
```
System WIP = Sum of column limits (or lower)
```

The system-level limit prevents work from simply shifting between columns while total WIP stays high.

## Adjusting WIP Limits

### When to Lower WIP Limits

- Cycle time is stable but you want to reduce it further
- Team reports feeling comfortable (limits should create productive tension)
- Bottleneck analysis shows wait time in queues between stages
- Quality metrics are declining (lower WIP → more focus → better quality)

### When to Raise WIP Limits

- Items are frequently blocked by external dependencies (team has nothing to pull)
- Throughput is declining because team members are idle
- A new team member joins (adjust proportionally)
- After a process change reduces cycle time, giving capacity for more parallel work

### Adjustment Process

1. Propose a change in the team retrospective with data (cycle time charts, blocker frequency)
2. Adjust by 1-2 items (never make large jumps)
3. Run with the new limit for 2-4 weeks
4. Measure the impact on cycle time, throughput, and quality
5. Decide whether to keep, adjust further, or revert

## Enforcement Strategies

### Soft Limits vs. Hard Limits

| Approach | Behavior | Best For |
|----------|----------|---------|
| Soft limit | Exceeding is allowed but must be justified and visible | Teams new to Kanban, discovery phase |
| Hard limit | Cannot exceed — tool prevents it or team agreement prohibits it | Mature teams, bottleneck-sensitive processes |

### What to Do When a Column Is at Limit

1. **Help finish**: Swarm on items in the at-limit column to move them forward
2. **Wait**: Do not start new work; instead, improve the process (refactor, document, mentor)
3. **Escalate blockers**: If items are stuck, the WIP limit makes the problem visible and urgent
4. **Pull from upstream**: Help with items in the previous column that are ready to advance

### Common Violations and Responses

| Violation | Root Cause | Response |
|-----------|-----------|----------|
| "I'll just start one more" | Discomfort with waiting | Coach: "What can you do to help finish current items?" |
| Expedite lane overuse | Everything feels urgent | Limit expedite to 1 item max; require VP-level approval |
| Items split to stay within limits | Gaming the metric | Track original item, not sub-tasks, against WIP |
| Blocked items counted separately | Misunderstanding WIP definition | Blocked items count toward WIP — they consume capacity |
