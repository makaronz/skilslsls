# Session Security

Implement secure session management for web applications across distributed systems.

---

## Session Architecture

### Server-Side Sessions

Store session data on the server, send only a session ID to the client.

**Session Store Options:**
| Store | Speed | Scalability | Persistence | Use Case |
|-------|-------|-------------|-------------|----------|
| In-memory | Fastest | Single server only | None | Development |
| Redis | Very fast | Horizontal scaling | Optional | Production (recommended) |
| PostgreSQL | Moderate | Vertical | Durable | Compliance-heavy apps |
| DynamoDB | Fast | Unlimited | Durable | AWS-native apps |
| Memcached | Very fast | Horizontal | None | Ephemeral sessions |

**Redis Session Implementation:**
- Key format: `session:{session_id}`
- TTL: Match session expiry (e.g., 3600 seconds)
- Data: JSON-serialized session object
- Use Redis Cluster for high availability

### Stateless Sessions (JWT-Based)

Session state encoded in the token itself — no server-side store needed.

**Tradeoffs:**
| Factor | Server-Side | Stateless (JWT) |
|--------|-------------|-----------------|
| Scalability | Requires shared store | Inherently scalable |
| Revocation | Immediate (delete from store) | Difficult (requires blacklist) |
| Size | Small cookie (session ID) | Larger cookie/header |
| Server load | Read from store per request | CPU for signature verification |

---

## Cookie Security Configuration

### Essential Cookie Attributes

| Attribute | Value | Purpose |
|-----------|-------|---------|
| `HttpOnly` | `true` | Prevents JavaScript access (XSS protection) |
| `Secure` | `true` | Only sent over HTTPS |
| `SameSite` | `Lax` or `Strict` | CSRF protection |
| `Path` | `/` | Cookie scope |
| `Domain` | `.example.com` | Subdomain sharing if needed |
| `Max-Age` | `3600` | Expiry in seconds |

**Example Set-Cookie Header:**
```
Set-Cookie: session_id=abc123;
  HttpOnly;
  Secure;
  SameSite=Lax;
  Path=/;
  Max-Age=3600
```

### SameSite Policy Selection

| Value | Cross-Site Requests | CSRF Protection | Compatibility |
|-------|-------------------|-----------------|---------------|
| `Strict` | Never sent | Complete | May break OAuth redirects |
| `Lax` | Sent on top-level navigation | Good (recommended) | Wide support |
| `None` | Always sent (requires Secure) | None | Cross-origin embeds only |

---

## Session ID Security

### Generation Requirements
- **Length**: Minimum 128 bits of entropy
- **Source**: Cryptographically secure random number generator (CSPRNG)
- **Format**: Hex or Base64URL encoded
- **Unpredictable**: No sequential IDs, no user-derivable patterns

### Session Fixation Prevention
1. **Regenerate session ID after authentication**: Always create new session on login
2. **Invalidate old session**: Delete previous session from store
3. **Bind to user agent**: Store and verify User-Agent header
4. **Bind to IP** (optional): Strict but may break mobile users

---

## Session Lifecycle Management

### Login
1. Authenticate user credentials
2. Generate new session ID (CSPRNG)
3. Store session data with user info, roles, created_at
4. Set secure cookie with session ID
5. Log authentication event

### Activity
- Extend session TTL on each request (sliding expiration)
- Or use fixed expiration with absolute timeout
- Track last activity timestamp

### Logout
1. Delete session from server store
2. Clear session cookie (set Max-Age=0)
3. Invalidate any associated tokens
4. Log logout event

### Timeouts

| Timeout Type | Duration | Purpose |
|-------------|----------|---------|
| Idle timeout | 15-30 minutes | Inactivity protection |
| Absolute timeout | 8-24 hours | Maximum session lifetime |
| Privileged timeout | 5-15 minutes | Re-auth for sensitive actions |

---

## Distributed Session Management

### Session Replication Strategies

**Sticky Sessions (Session Affinity):**
- Load balancer routes user to same server
- Simple but limits scaling and fails on server restart

**Centralized Session Store (Recommended):**
- All servers read/write to shared Redis/database
- True horizontal scaling
- Add Redis Sentinel or Cluster for HA

**Session Replication:**
- Copy sessions across all servers
- High memory usage, complex synchronization
- Suitable only for small clusters

---

## Security Best Practices

- Always regenerate session ID after login and privilege changes
- Set HttpOnly, Secure, and SameSite on all session cookies
- Implement both idle and absolute session timeouts
- Use centralized session store for distributed apps
- Monitor for session anomalies (concurrent sessions, geographic jumps)
- Implement concurrent session limits per user
- Provide "sign out all devices" functionality
- Log all session lifecycle events for audit
- Never expose session IDs in URLs
- Rate limit session creation to prevent DoS
