# API Testing and Deployment

Comprehensive testing strategies and production deployment patterns for backend APIs.

---

## Testing Pyramid

### Unit Tests (70% of tests)

Test individual functions, validators, and business logic in isolation.

**What to Test:**
- Input validation logic
- Business rule calculations
- Data transformation functions
- Error handling paths
- Edge cases (null, empty, boundary values)

**Best Practices:**
- Mock external dependencies (database, APIs, file system)
- Test both success and failure paths
- Use descriptive test names: `test_create_user_rejects_duplicate_email`
- Aim for >80% code coverage on business logic

### Integration Tests (20% of tests)

Test API endpoints with real database and middleware.

**What to Test:**
- Full request/response cycle
- Authentication and authorization flows
- Database queries and transactions
- Error response format and status codes
- Pagination, filtering, sorting

**Example Structure:**
```python
def test_create_user_success(client, db):
    response = client.post("/api/v1/users", json={
        "email": "test@example.com",
        "name": "Test User",
        "role": "editor"
    })
    assert response.status_code == 201
    assert response.json()["data"]["email"] == "test@example.com"
    assert db.users.count() == 1

def test_create_user_duplicate_email(client, db, existing_user):
    response = client.post("/api/v1/users", json={
        "email": existing_user.email,
        "name": "Another User",
        "role": "viewer"
    })
    assert response.status_code == 409
    assert response.json()["error"]["code"] == "DUPLICATE_RESOURCE"
```

### End-to-End Tests (10% of tests)

Test critical user workflows across multiple endpoints.

**What to Test:**
- User registration → login → create resource → verify
- Payment flow: create order → process payment → confirm
- Admin workflows: create → approve → publish

---

## Load Testing

### Tools Comparison

| Tool | Language | Distributed | Real Browser | Best For |
|------|----------|-------------|-------------|----------|
| k6 | JavaScript | Yes | No | API load testing |
| Locust | Python | Yes | No | Python teams |
| Artillery | YAML/JS | Yes | No | Quick setup |
| JMeter | Java | Yes | No | Complex scenarios |
| Gatling | Scala | Yes | No | High performance |

### Performance Benchmarks

| Metric | Target | Critical |
|--------|--------|----------|
| p50 latency | < 100ms | < 200ms |
| p95 latency | < 300ms | < 500ms |
| p99 latency | < 500ms | < 1000ms |
| Error rate | < 0.1% | < 1% |
| Throughput | Baseline + 50% | Baseline |

---

## CI/CD Pipeline

### Pipeline Stages

```
Code Push → Lint & Format → Unit Tests → Build → Integration Tests
  → Security Scan → Deploy Staging → Smoke Tests → Deploy Production
  → Health Check → Monitor
```

### Deployment Strategies

| Strategy | Downtime | Risk | Complexity | Rollback |
|----------|----------|------|------------|----------|
| Rolling | None | Low-Medium | Low | Reverse rolling |
| Blue-Green | None | Low | Medium | Switch traffic |
| Canary | None | Very Low | High | Route to stable |
| Feature Flags | None | Very Low | Medium | Toggle off |

### Blue-Green Deployment
1. Deploy new version to idle (green) environment
2. Run smoke tests against green
3. Switch load balancer from blue to green
4. Monitor error rates and latency
5. Keep blue running for instant rollback
6. Decommission blue after confidence period

### Canary Deployment
1. Deploy new version to small subset (1-5% of traffic)
2. Compare error rates, latency, business metrics
3. Gradually increase traffic (5% → 25% → 50% → 100%)
4. Automated rollback if metrics degrade

---

## Database Migrations

### Migration Best Practices
- Always make migrations backward-compatible
- Deploy schema changes before code changes
- Use expand-contract pattern for breaking changes
- Test migrations against production-size data
- Include both up and down migration scripts
- Run migrations in transactions where possible

### Expand-Contract Pattern
1. **Expand**: Add new column/table (old code still works)
2. **Migrate**: Backfill data, deploy new code that writes to both
3. **Contract**: Remove old column/table after full migration

---

## Production Monitoring

### Key Metrics to Track

| Category | Metrics | Alert Threshold |
|----------|---------|-----------------|
| Availability | Uptime, health check | < 99.9% |
| Latency | p50, p95, p99 response time | p95 > 500ms |
| Errors | 5xx rate, 4xx rate | 5xx > 1% |
| Throughput | Requests/second | > 80% capacity |
| Resources | CPU, memory, disk, connections | > 80% utilization |

### Health Check Endpoint
```json
GET /health

{
  "status": "healthy",
  "version": "1.2.3",
  "uptime": "72h15m",
  "checks": {
    "database": "healthy",
    "redis": "healthy",
    "external_api": "degraded"
  }
}
```
