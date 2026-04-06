# Kanban Metrics and Analytics

Key performance indicators, charts, and analytical techniques for measuring and improving Kanban system performance.

---

## Core Kanban Metrics

### Lead Time

The total time from when a work item is requested to when it is delivered.

```
Lead Time = Delivery Date − Request Date
```

Includes all wait time (in queues, blocked) plus active work time. This is the metric customers care about.

### Cycle Time

The time from when active work begins on an item to when it is complete.

```
Cycle Time = Completion Date − Start Date
```

Cycle time excludes backlog wait time. It measures how long your system takes to process work once started.

### Throughput

The number of work items completed per unit of time.

```
Throughput = Items Completed / Time Period
```

Track weekly throughput to measure team capacity and identify trends. Use it for forecasting delivery dates.

### Work in Progress (WIP)

The count of items currently in active work columns (between "started" and "done").

Little's Law connects these three metrics:
```
Average Cycle Time = Average WIP / Average Throughput
```

This means reducing WIP directly reduces cycle time (assuming throughput stays constant or improves).

## Charts and Visualizations

### Cumulative Flow Diagram (CFD)

The CFD is the most powerful Kanban analytics tool. It plots the cumulative count of items in each workflow state over time as stacked area bands.

**Reading the CFD**:
- **Band width** (vertical distance) = WIP in that state
- **Horizontal distance between bands** = approximate lead/cycle time
- **Slope of the "Done" band** = throughput rate
- **Widening band** = items accumulating (bottleneck forming)
- **Parallel bands** = stable, healthy flow

**Warning signs**:
- A band that keeps getting wider over time → items are entering faster than leaving (WIP growing)
- Flat "Done" line → no items completing (systemic blocker)
- Steps / staircase in "Done" line → batch delivery instead of continuous flow

### Cycle Time Scatter Plot

Plot each completed item as a point: x-axis = completion date, y-axis = cycle time. Add percentile lines:
- **50th percentile**: Median cycle time — "half our items finish in X days or less"
- **85th percentile**: Realistic commitment — "85% of items finish in X days or less"
- **95th percentile**: Near-worst case — use for SLA commitments

### Throughput Histogram

Plot the distribution of weekly throughput values. This shows:
- Most likely throughput (mode)
- Range of outcomes (spread)
- Whether throughput is stable or highly variable

## Forecasting with Monte Carlo Simulation

Use historical throughput data to probabilistically forecast future delivery:

1. Sample random weekly throughput values from historical data (with replacement)
2. Simulate how many items would complete in each future week
3. Run 10,000 simulations
4. Report confidence intervals: "There is an 85% chance we will complete 20 items by March 15"

Monte Carlo is more realistic than single-point estimates because it accounts for natural variability.

## Flow Efficiency

```
Flow Efficiency = Active Work Time / Total Lead Time × 100
```

Typical flow efficiency in knowledge work is 15-40%. The rest is wait time. Improving flow efficiency (reducing wait time) is often more impactful than speeding up active work.

| Efficiency Range | Assessment | Action |
|-----------------|------------|--------|
| < 15% | Poor — mostly waiting | Reduce handoffs, lower WIP, address blockers |
| 15-40% | Typical | Identify largest wait states, reduce queues |
| 40-60% | Good | Fine-tune, maintain discipline |
| > 60% | Excellent | Sustain and share practices |

## Blocker Analysis

Track blockers to identify systemic issues:

| Metric | Description | Target |
|--------|-------------|--------|
| Blocker frequency | How often items become blocked | < 10% of items |
| Blocker duration | Average time an item stays blocked | < 1 day |
| Blocker categories | External dependency, unclear requirements, environment issue | Pareto the top 3 |
| Blocker resolution | Who resolves and how quickly | Named owner, < 4 hours |

Run a monthly blocker review: cluster blocked items by root cause and address the top category systemically.
