# Caching Strategies

Implement multi-layer caching for optimal web application performance.

---

## Caching Architecture

### Multi-Layer Cache

```
Client (Browser Cache) → CDN (Edge Cache) → Application Cache (Redis)
  → Database Query Cache → Database
```

| Layer | TTL | Hit Rate Target | Latency |
|-------|-----|----------------|---------|
| Browser | 1h-1yr (static) | 60-90% | 0ms |
| CDN | 5min-24h | 85-95% | 5-50ms |
| Application (Redis) | 1min-1h | 80-95% | 1-5ms |
| DB query cache | Auto | 30-60% | Varies |

---

## Application-Level Caching (Redis)

### Caching Patterns

**Cache-Aside (Lazy Loading):**
```python
def get_user(user_id):
    # Check cache first
    cached = redis.get(f"user:{user_id}")
    if cached:
        return json.loads(cached)
    
    # Cache miss: query database
    user = db.query("SELECT * FROM users WHERE id = %s", user_id)
    
    # Store in cache with TTL
    redis.setex(f"user:{user_id}", 3600, json.dumps(user))
    return user
```

**Write-Through:**
```python
def update_user(user_id, data):
    # Update database
    db.execute("UPDATE users SET ... WHERE id = %s", user_id)
    
    # Update cache immediately
    user = db.query("SELECT * FROM users WHERE id = %s", user_id)
    redis.setex(f"user:{user_id}", 3600, json.dumps(user))
    return user
```

**Write-Behind (Write-Back):**
- Write to cache immediately, return to client
- Background worker syncs cache → database asynchronously
- Risk: data loss if cache fails before sync
- Use case: High-write scenarios where slight delay is acceptable

### Cache Key Design

| Pattern | Example | Use Case |
|---------|---------|----------|
| Entity | `user:123` | Single object lookup |
| Query | `users:active:page1:limit20` | Paginated lists |
| Computed | `dashboard:org_456:daily` | Expensive computations |
| Fragment | `nav:v3:premium` | UI component fragments |

**Key Rules:**
- Include version or hash for cache busting
- Use namespaces for easy invalidation
- Keep keys short but descriptive
- Include relevant query parameters

---

## Cache Invalidation

### Strategies

| Strategy | Consistency | Complexity | Best For |
|----------|------------|------------|----------|
| TTL expiry | Eventual | Low | Read-heavy, tolerance for staleness |
| Event-driven | Near-real-time | Medium | Write-after-read patterns |
| Tag-based | Near-real-time | Medium | Related cache entries |
| Version-based | Immediate | Low | Static assets, API responses |
| Pub/Sub | Near-real-time | High | Distributed cache clusters |

### Event-Driven Invalidation
```python
def update_user(user_id, data):
    db.execute("UPDATE users SET ...", data)
    
    # Invalidate all related cache entries
    redis.delete(f"user:{user_id}")
    redis.delete(f"user:{user_id}:posts")
    redis.delete(f"org:{user.org_id}:members")
    
    # Publish event for other services
    redis.publish("cache:invalidate", json.dumps({
        "type": "user", "id": user_id
    }))
```

---

## HTTP Caching

### Cache-Control Headers

| Directive | Effect | Use Case |
|-----------|--------|----------|
| `public, max-age=31536000` | CDN + browser cache for 1 year | Versioned static assets |
| `private, max-age=0, must-revalidate` | Browser only, always validate | User-specific pages |
| `no-store` | Never cache | Sensitive data, auth endpoints |
| `stale-while-revalidate=60` | Serve stale while refreshing | API responses |

### ETag/Conditional Requests
```
# Server response
ETag: "abc123"

# Client subsequent request
If-None-Match: "abc123"

# Server response if unchanged
304 Not Modified
```

---

## Cache Warming

### Strategies
- **Startup warming**: Pre-populate cache on deployment
- **Scheduled warming**: Refresh popular items before TTL expiry
- **Predictive warming**: Pre-cache based on usage patterns
- **Lazy warming with thundering herd protection**: Lock mechanism for cache misses

### Thundering Herd Prevention
```python
def get_with_lock(key, compute_fn, ttl=3600):
    value = redis.get(key)
    if value:
        return json.loads(value)
    
    # Acquire lock to prevent multiple simultaneous computations
    lock_key = f"lock:{key}"
    if redis.set(lock_key, 1, ex=30, nx=True):
        try:
            value = compute_fn()
            redis.setex(key, ttl, json.dumps(value))
            return value
        finally:
            redis.delete(lock_key)
    else:
        # Another process is computing; wait and retry
        time.sleep(0.5)
        return get_with_lock(key, compute_fn, ttl)
```

---

## Monitoring

### Key Cache Metrics
| Metric | Healthy | Action If Unhealthy |
|--------|---------|-------------------|
| Hit rate | > 80% | Review TTL, warming strategy |
| Eviction rate | Low | Increase memory or reduce stored data |
| Memory usage | < 80% | Scale or evict low-value keys |
| Latency (p99) | < 5ms | Check network, connection pool |
| Key count growth | Stable | Review TTL, add expiry to all keys |
