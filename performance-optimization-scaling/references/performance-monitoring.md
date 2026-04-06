# Performance Monitoring

Implement comprehensive monitoring for web application performance, availability, and user experience.

---

## Monitoring Architecture

### The Three Pillars of Observability

| Pillar | Purpose | Tools |
|--------|---------|-------|
| Metrics | Numeric measurements over time | Prometheus, Datadog, CloudWatch |
| Logs | Detailed event records | ELK Stack, Loki, CloudWatch Logs |
| Traces | Request flow across services | Jaeger, Zipkin, Datadog APM |

### Monitoring Stack Options

| Stack | Components | Best For |
|-------|-----------|----------|
| Open Source | Prometheus + Grafana + Jaeger + ELK | Full control, cost-conscious |
| AWS Native | CloudWatch + X-Ray + OpenSearch | AWS-heavy infrastructure |
| Datadog | All-in-one SaaS | Ease of use, full-featured |
| New Relic | APM + Infrastructure + Logs | Application-focused |

---

## Application Performance Monitoring (APM)

### Key Metrics

| Metric | Description | Target | Alert |
|--------|-------------|--------|-------|
| Response time (p50) | Median latency | < 100ms | > 200ms |
| Response time (p95) | Tail latency | < 300ms | > 500ms |
| Response time (p99) | Worst case | < 1000ms | > 2000ms |
| Error rate | 5xx responses / total | < 0.1% | > 1% |
| Throughput | Requests per second | Baseline ± 20% | < 50% baseline |
| Apdex score | User satisfaction index | > 0.9 | < 0.7 |

### Apdex Score Calculation
```
Apdex = (Satisfied + Tolerating/2) / Total Samples

Where:
- Satisfied: Response < T (e.g., 500ms)
- Tolerating: Response < 4T (e.g., 2000ms)
- Frustrated: Response >= 4T
```

---

## Infrastructure Monitoring

### Server Metrics

| Resource | Metric | Warning | Critical |
|----------|--------|---------|----------|
| CPU | Utilization | > 70% for 5m | > 90% for 2m |
| Memory | Usage % | > 80% | > 95% |
| Disk | Usage % | > 75% | > 90% |
| Disk | I/O wait | > 20% | > 40% |
| Network | Bandwidth utilization | > 70% | > 90% |
| Network | Packet loss | > 0.1% | > 1% |

### Database Metrics

| Metric | Warning | Critical |
|--------|---------|----------|
| Active connections | > 70% max | > 85% max |
| Query latency (p95) | > 100ms | > 500ms |
| Replication lag | > 1 second | > 5 seconds |
| Lock wait time | > 100ms | > 1 second |
| Cache hit ratio | < 95% | < 90% |
| Disk IOPS | > 70% provisioned | > 90% provisioned |

---

## Real User Monitoring (RUM)

### Core Web Vitals

| Metric | Good | Needs Improvement | Poor |
|--------|------|-------------------|------|
| LCP (Largest Contentful Paint) | ≤ 2.5s | ≤ 4.0s | > 4.0s |
| INP (Interaction to Next Paint) | ≤ 200ms | ≤ 500ms | > 500ms |
| CLS (Cumulative Layout Shift) | ≤ 0.1 | ≤ 0.25 | > 0.25 |
| FCP (First Contentful Paint) | ≤ 1.8s | ≤ 3.0s | > 3.0s |
| TTFB (Time to First Byte) | ≤ 800ms | ≤ 1800ms | > 1800ms |

### RUM Implementation
```javascript
// Performance Observer for Web Vitals
new PerformanceObserver((entryList) => {
  for (const entry of entryList.getEntries()) {
    sendToAnalytics({
      metric: entry.name,
      value: entry.startTime,
      page: window.location.pathname,
      connection: navigator.connection?.effectiveType
    });
  }
}).observe({ type: 'largest-contentful-paint', buffered: true });
```

---

## Alerting Strategy

### Alert Severity Levels

| Severity | Response Time | Notification | Example |
|----------|-------------|-------------|---------|
| P1 Critical | < 15 minutes | Page on-call + Slack | Site down, data loss |
| P2 High | < 1 hour | Slack + email | Error rate > 5% |
| P3 Medium | < 4 hours | Slack | Latency degradation |
| P4 Low | Next business day | Email/ticket | Disk usage warning |

### Alert Best Practices
- **Alert on symptoms, not causes**: Alert on error rate, investigate the cause
- **Use multi-signal alerts**: Combine metrics to reduce false positives
- **Set appropriate windows**: 5-minute average, not instantaneous spikes
- **Implement alert routing**: Route to the right team automatically
- **Review and tune regularly**: Remove noisy alerts, adjust thresholds
- **Document runbooks**: Link each alert to resolution steps

---

## Dashboards

### SRE Dashboard Structure

1. **Service Overview**: Uptime, error rate, latency (Golden Signals)
2. **Infrastructure**: CPU, memory, disk, network per service
3. **Dependencies**: External API health, database metrics
4. **Business Metrics**: Signups, transactions, active users
5. **Deployments**: Recent deploys, feature flags, rollbacks

### Golden Signals (Google SRE)

| Signal | Question | Metric |
|--------|----------|--------|
| Latency | How fast? | Request duration percentiles |
| Traffic | How much? | Requests per second |
| Errors | How often failing? | Error rate (%) |
| Saturation | How full? | Resource utilization (%) |
