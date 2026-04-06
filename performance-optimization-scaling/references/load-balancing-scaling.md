# Load Balancing and Scaling Strategies

Implement horizontal scaling, auto-scaling, and load balancing for high-traffic applications.

---

## Load Balancing

### Algorithm Selection

| Algorithm | Description | Best For | Drawback |
|-----------|-------------|----------|----------|
| Round Robin | Rotate through servers | Equal-capacity servers | Ignores server load |
| Weighted Round Robin | Rotate with weights | Mixed-capacity servers | Static weights |
| Least Connections | Route to least busy | Variable request duration | Overhead tracking |
| IP Hash | Hash client IP to server | Session affinity | Uneven distribution |
| Least Response Time | Route to fastest | Latency-sensitive apps | Measurement overhead |
| Random | Random selection | Large server pools | Simple but uneven |

### Layer 4 vs Layer 7 Load Balancing

| Feature | Layer 4 (TCP/UDP) | Layer 7 (HTTP/HTTPS) |
|---------|-------------------|---------------------|
| Speed | Very fast | Moderate |
| Routing | IP + port | URL, headers, cookies |
| SSL termination | No | Yes |
| Content-based routing | No | Yes |
| WebSocket support | Pass-through | Full |
| Health checks | TCP ping | HTTP request/response |
| Use case | High throughput | Intelligent routing |

### Health Check Configuration

```nginx
# Nginx upstream health check
upstream backend {
    server 10.0.1.1:8080 max_fails=3 fail_timeout=30s;
    server 10.0.1.2:8080 max_fails=3 fail_timeout=30s;
    server 10.0.1.3:8080 max_fails=3 fail_timeout=30s backup;
}
```

| Parameter | Recommended | Purpose |
|-----------|------------|---------|
| Interval | 10-30 seconds | Check frequency |
| Timeout | 5 seconds | Max wait for response |
| Threshold | 3 consecutive failures | Remove from pool |
| Recovery | 2 consecutive successes | Add back to pool |

---

## Horizontal Scaling

### Stateless Application Design

Requirements for horizontal scaling:
- No local file storage (use S3/object storage)
- No in-memory sessions (use Redis/database)
- No local caches that must be consistent (use shared cache)
- Externalize configuration (environment variables, config service)
- Handle database connections through pooling

### Auto-Scaling Policies

| Metric | Scale Up Threshold | Scale Down Threshold | Cooldown |
|--------|-------------------|---------------------|----------|
| CPU utilization | > 70% for 3 min | < 30% for 10 min | 5 min |
| Memory | > 80% for 5 min | < 40% for 10 min | 5 min |
| Request count | > 1000 rps | < 200 rps | 3 min |
| Response time (p95) | > 500ms for 5 min | < 100ms for 10 min | 5 min |
| Queue depth | > 100 messages | < 10 messages | 3 min |

### Scaling Strategies

**Reactive Scaling:**
- Scale based on current metrics
- Simple but always playing catch-up
- Good for: Gradual traffic changes

**Predictive Scaling:**
- Use historical patterns to pre-scale
- Better for known traffic patterns
- Good for: Daily/weekly cycles, events

**Scheduled Scaling:**
- Set capacity for known events
- Most reliable for predictable spikes
- Good for: Sales events, launches, peak hours

---

## Container Orchestration Scaling

### Kubernetes HPA (Horizontal Pod Autoscaler)

```yaml
apiVersion: autoscaling/v2
kind: HorizontalPodAutoscaler
metadata:
  name: api-hpa
spec:
  scaleTargetRef:
    apiVersion: apps/v1
    kind: Deployment
    name: api
  minReplicas: 3
  maxReplicas: 50
  metrics:
  - type: Resource
    resource:
      name: cpu
      target:
        type: Utilization
        averageUtilization: 70
  - type: Resource
    resource:
      name: memory
      target:
        type: Utilization
        averageUtilization: 80
  behavior:
    scaleUp:
      stabilizationWindowSeconds: 60
      policies:
      - type: Percent
        value: 50
        periodSeconds: 60
    scaleDown:
      stabilizationWindowSeconds: 300
```

---

## Database Scaling for High Traffic

| Strategy | Read Scaling | Write Scaling | Complexity |
|----------|-------------|---------------|-----------|
| Read replicas | Yes | No | Low |
| Connection pooling | Both (reduces overhead) | Both | Low |
| Caching layer (Redis) | Yes | Indirect | Medium |
| Sharding | Yes | Yes | High |
| CQRS | Yes | Yes | High |

---

## Capacity Planning

### Traffic Estimation

```
Peak daily users × Actions per session × Avg requests per action
= Peak requests per minute

Example:
100,000 users × 20 actions × 3 requests = 6,000,000 requests
Concentrated in 4 peak hours: 6M / 240 min = 25,000 rpm
Peak factor (2-3x): 50,000-75,000 rpm
```

### Server Sizing
```
Servers needed = Peak RPM / (Requests per server per minute × 0.7 utilization target)

Example:
75,000 / (5,000 × 0.7) = 21.4 → 22 servers minimum
Add 20% buffer → 27 servers
```
