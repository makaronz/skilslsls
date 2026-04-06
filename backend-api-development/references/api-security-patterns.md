# API Security Patterns

Protect APIs against common attacks with authentication, rate limiting, input validation, and monitoring.

---

## Authentication Patterns

### API Key Authentication
- Simple, suitable for server-to-server communication
- Pass in header: `X-API-Key: your_key_here`
- Hash keys in database (never store plaintext)
- Support key rotation with multiple active keys
- Scope keys to specific endpoints and rate limits

### Bearer Token (OAuth 2.0 / JWT)
- Standard for user-context APIs
- Header: `Authorization: Bearer <token>`
- Validate token signature, expiry, audience on every request
- Use short-lived access tokens (15-60 min)

### Mutual TLS (mTLS)
- Both client and server present certificates
- Use for high-security service-to-service communication
- Managed via service mesh (Istio, Linkerd) in Kubernetes

### HMAC Request Signing
- Client signs request body/params with shared secret
- Server recomputes and verifies signature
- Prevents tampering and replay attacks
- Include timestamp in signed payload (reject old requests)

---

## Input Validation

### Validation Layers

| Layer | What to Validate | Tools |
|-------|-----------------|-------|
| Schema | Data types, required fields, formats | JSON Schema, Joi, Zod, Pydantic |
| Business logic | Value ranges, relationships, state transitions | Custom validators |
| Database | Constraints, uniqueness, foreign keys | DB constraints, ORM validators |

### Common Injection Attacks

| Attack | Vector | Prevention |
|--------|--------|------------|
| SQL Injection | User input in queries | Parameterized queries, ORM |
| NoSQL Injection | JSON operators in input | Input type validation, sanitize |
| XSS | User content in responses | Output encoding, CSP headers |
| Command Injection | User input in shell commands | Avoid shell execution, whitelist |
| Path Traversal | `../` in file paths | Canonicalize paths, whitelist |
| SSRF | User-controlled URLs | URL allowlist, disable redirects |

### Request Size Limits

| Content Type | Recommended Max | Purpose |
|-------------|----------------|---------|
| JSON body | 1-10 MB | Prevent memory exhaustion |
| File upload | 50-500 MB | Match business requirements |
| URL length | 2,048 characters | Browser/proxy compatibility |
| Header size | 8-16 KB | Prevent header injection |
| Query params | 2,048 characters | Prevent URL overflow |

---

## Rate Limiting

### Multi-Tier Rate Limiting

| Tier | Scope | Limit Example | Purpose |
|------|-------|--------------|---------|
| Global | All requests | 10,000/min | Infrastructure protection |
| Per-user | Authenticated user | 1,000/min | Fair usage |
| Per-endpoint | Specific route | 100/min on POST | Prevent abuse |
| Per-IP | Unauthenticated | 60/min | Brute force prevention |

### Implementation with Redis
```
Key: ratelimit:{user_id}:{window}
Value: request count
TTL: window duration
```

Use sliding window algorithm for smoother rate limiting.

---

## Security Headers

| Header | Value | Purpose |
|--------|-------|---------|
| `Strict-Transport-Security` | `max-age=31536000; includeSubDomains` | Force HTTPS |
| `Content-Security-Policy` | `default-src 'self'` | Prevent XSS |
| `X-Content-Type-Options` | `nosniff` | Prevent MIME sniffing |
| `X-Frame-Options` | `DENY` | Prevent clickjacking |
| `X-Request-ID` | `uuid` | Request tracing |
| `Cache-Control` | `no-store` for sensitive data | Prevent caching secrets |

---

## CORS Configuration

```javascript
// Production CORS
{
  origin: ['https://app.example.com', 'https://admin.example.com'],
  methods: ['GET', 'POST', 'PUT', 'PATCH', 'DELETE'],
  allowedHeaders: ['Authorization', 'Content-Type', 'X-Request-ID'],
  credentials: true,
  maxAge: 86400  // Cache preflight for 24 hours
}
```

**Rules:**
- Never use `origin: '*'` with `credentials: true`
- Whitelist specific origins in production
- Validate `Origin` header server-side
- Set appropriate `maxAge` to reduce preflight requests

---

## API Security Checklist

- [ ] All endpoints require authentication (except public ones explicitly marked)
- [ ] Input validation on all parameters (type, format, length, range)
- [ ] Rate limiting at multiple tiers
- [ ] HTTPS enforced with HSTS header
- [ ] Security headers on all responses
- [ ] Request/response logging with PII masking
- [ ] Error responses do not leak internal details
- [ ] CORS properly configured for known origins
- [ ] Dependency scanning for known vulnerabilities
- [ ] Regular penetration testing and security audits
