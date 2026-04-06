# REST API Design Patterns

Comprehensive guide to designing and implementing production-ready RESTful APIs.

---

## Resource Design

### URL Structure

Follow consistent naming conventions:
```
GET    /api/v1/users              # List users
POST   /api/v1/users              # Create user
GET    /api/v1/users/{id}         # Get user
PUT    /api/v1/users/{id}         # Replace user
PATCH  /api/v1/users/{id}         # Partial update
DELETE /api/v1/users/{id}         # Delete user
GET    /api/v1/users/{id}/posts   # User's posts (sub-resource)
```

**Naming Rules:**
- Use plural nouns for collections: `/users` not `/user`
- Use kebab-case: `/user-profiles` not `/userProfiles`
- Avoid verbs in URLs: `/users/{id}/activate` → `PATCH /users/{id}` with `{"status": "active"}`
- Nest sub-resources max 2 levels deep

### HTTP Methods and Status Codes

| Method | Action | Success Code | Error Codes |
|--------|--------|-------------|-------------|
| GET | Read | 200 OK | 404 Not Found |
| POST | Create | 201 Created | 400 Bad Request, 409 Conflict |
| PUT | Replace | 200 OK | 400, 404 |
| PATCH | Partial Update | 200 OK | 400, 404, 422 Unprocessable |
| DELETE | Remove | 204 No Content | 404 |

---

## Pagination

### Cursor-Based Pagination (Recommended)

```json
GET /api/v1/users?limit=20&cursor=eyJpZCI6MTAwfQ

{
  "data": [...],
  "pagination": {
    "next_cursor": "eyJpZCI6MTIwfQ",
    "has_more": true,
    "limit": 20
  }
}
```
- Stable with real-time data changes
- Efficient for large datasets (no OFFSET scan)
- Encode cursor as opaque Base64 string

### Offset-Based Pagination

```json
GET /api/v1/users?page=3&per_page=20

{
  "data": [...],
  "pagination": {
    "page": 3,
    "per_page": 20,
    "total": 245,
    "total_pages": 13
  }
}
```
- Simple but inconsistent with concurrent writes
- Suitable for admin UIs and small datasets

---

## Filtering, Sorting, and Search

### Filtering
```
GET /api/v1/users?status=active&role=admin&created_after=2024-01-01
GET /api/v1/products?price_min=10&price_max=100&category=electronics
```

### Sorting
```
GET /api/v1/users?sort=created_at&order=desc
GET /api/v1/products?sort=-price,name    # - prefix for descending
```

### Full-Text Search
```
GET /api/v1/users?q=john+smith
GET /api/v1/products?search=wireless+headphones
```

---

## Error Handling

### Standard Error Response Format

```json
{
  "error": {
    "code": "VALIDATION_ERROR",
    "message": "Request validation failed",
    "details": [
      {
        "field": "email",
        "message": "Must be a valid email address",
        "code": "INVALID_FORMAT"
      }
    ],
    "request_id": "req_abc123",
    "documentation_url": "https://api.example.com/docs/errors#VALIDATION_ERROR"
  }
}
```

### Error Code Categories

| HTTP Status | Error Type | When to Use |
|-------------|-----------|-------------|
| 400 | Bad Request | Malformed syntax, missing required fields |
| 401 | Unauthorized | Missing or invalid authentication |
| 403 | Forbidden | Authenticated but insufficient permissions |
| 404 | Not Found | Resource does not exist |
| 409 | Conflict | Duplicate resource, version conflict |
| 422 | Unprocessable | Valid syntax but semantic errors |
| 429 | Too Many Requests | Rate limit exceeded |
| 500 | Internal Error | Unexpected server failure |

---

## Versioning Strategies

| Strategy | Example | Pros | Cons |
|----------|---------|------|------|
| URL path | `/api/v1/users` | Clear, easy routing | URL changes |
| Header | `Accept: application/vnd.api+json;version=1` | Clean URLs | Hidden, harder to test |
| Query param | `/api/users?version=1` | Easy to test | Cluttered URL |

**Recommendation:** URL path versioning (`/v1/`, `/v2/`) for public APIs. Header versioning for internal APIs.

---

## Rate Limiting

### Response Headers
```
X-RateLimit-Limit: 1000
X-RateLimit-Remaining: 950
X-RateLimit-Reset: 1699999999
Retry-After: 30
```

### Rate Limit Strategies
- **Fixed window**: Simple, reset at interval boundaries
- **Sliding window**: Smoother, more accurate
- **Token bucket**: Allows bursts, configurable refill rate
- **Per-endpoint limits**: Different limits for read vs write operations
