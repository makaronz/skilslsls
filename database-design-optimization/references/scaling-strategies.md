# Database Scaling Strategies

Scale databases horizontally and vertically for high-traffic production workloads.

---

## Scaling Approaches

### Vertical Scaling (Scale Up)
- Add more CPU, RAM, storage to existing server
- Simple but has upper limits
- Suitable for: Read-heavy workloads under 10TB
- Diminishing returns past certain thresholds

### Horizontal Scaling (Scale Out)
- Distribute data across multiple servers
- Complex but virtually unlimited
- Required for: Write-heavy workloads, massive datasets

---

## Read Replicas

### Architecture
```
Writes → Primary Database
              ↓ (async replication)
         Read Replica 1
         Read Replica 2
         Read Replica 3
              ↑
Reads → Load Balancer → Replicas
```

### Implementation Considerations

| Factor | Detail |
|--------|--------|
| Replication lag | Typically 10-100ms; plan for eventual consistency |
| Read-after-write | Route to primary immediately after writes |
| Failover | Promote replica to primary on failure |
| Load distribution | 80-90% reads to replicas, all writes to primary |
| Replica count | 2-5 replicas typical; more adds replication overhead |

### Application-Level Routing
```python
def get_connection(operation):
    if operation == 'write':
        return primary_pool.getconn()
    elif requires_fresh_data:
        return primary_pool.getconn()
    else:
        return replica_pool.getconn()
```

---

## Partitioning (Sharding)

### Sharding Strategies

| Strategy | Method | Pros | Cons |
|----------|--------|------|------|
| Hash-based | `shard = hash(key) % num_shards` | Even distribution | Difficult to add shards |
| Range-based | Date ranges, ID ranges | Easy range queries | Hot spots possible |
| Directory-based | Lookup table maps key → shard | Flexible | Lookup overhead |
| Geographic | Region-based placement | Data locality | Uneven distribution |

### Shard Key Selection

**Good Shard Keys:**
- High cardinality (many unique values)
- Even distribution across shards
- Frequently used in queries (avoid cross-shard queries)
- Examples: user_id, tenant_id, order_id

**Bad Shard Keys:**
- Low cardinality (status, country)
- Monotonically increasing (timestamp, auto-increment)
- Rarely used in queries

### Cross-Shard Query Patterns
- **Scatter-gather**: Query all shards, merge results (expensive)
- **Global tables**: Replicate small reference tables to all shards
- **Denormalization**: Store related data together on same shard

---

## Connection Management

### Pool Configuration

| App Type | Min Connections | Max Connections | Idle Timeout |
|----------|----------------|-----------------|-------------|
| Web API (per instance) | 5 | 20 | 300s |
| Background worker | 2 | 10 | 600s |
| Batch processing | 10 | 50 | 60s |

### Connection Proxies
- **PgBouncer**: PostgreSQL connection pooling
- **ProxySQL**: MySQL connection pooling and query routing
- **Amazon RDS Proxy**: Managed proxy for AWS databases

---

## Caching Layers

### Multi-Level Cache Architecture

```
Client → CDN Cache → Application Cache (Redis) → Read Replica → Primary DB
```

| Cache Level | TTL | Hit Rate Target | Use Case |
|-------------|-----|----------------|----------|
| Application memory | 1-5 min | 50-80% | Hot objects, config |
| Redis/Memcached | 5-60 min | 80-95% | Session, API responses |
| Database query cache | Auto | Varies | Repeated identical queries |

### Cache Invalidation Strategies
- **TTL-based**: Simple, eventual consistency
- **Event-driven**: Invalidate on write (pub/sub)
- **Version-based**: Append version to cache key
- **Tag-based**: Group related cache entries, invalidate by tag

---

## Monitoring and Capacity Planning

### Key Metrics

| Metric | Warning | Critical | Action |
|--------|---------|----------|--------|
| CPU utilization | > 70% | > 85% | Scale up or optimize queries |
| Memory usage | > 80% | > 90% | Add RAM or optimize |
| Disk I/O | > 70% capacity | > 85% | Move to faster storage |
| Connection count | > 70% max | > 85% max | Add pooling or scale |
| Replication lag | > 1 second | > 5 seconds | Check replica capacity |
| Query time p99 | > 500ms | > 2000ms | Optimize or index |
