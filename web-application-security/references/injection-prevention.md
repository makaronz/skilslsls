# Injection Prevention Guide

Comprehensive strategies for preventing SQL, NoSQL, XSS, CSRF, and other injection attacks.

---

## SQL Injection

### Attack Vectors

| Vector | Example Input | Impact |
|--------|--------------|--------|
| Classic injection | `' OR 1=1 --` | Authentication bypass |
| Union-based | `' UNION SELECT password FROM users --` | Data extraction |
| Blind boolean | `' AND 1=1 --` vs `' AND 1=2 --` | Data inference |
| Time-based blind | `' AND SLEEP(5) --` | Database fingerprinting |
| Second-order | Stored payload executed later | Delayed exploitation |
| Batch injection | `'; DROP TABLE users; --` | Data destruction |

### Prevention by Layer

**Layer 1 — Parameterized Queries (Primary Defense):**
```python
# Python (psycopg2)
cursor.execute("SELECT * FROM users WHERE id = %s AND status = %s", (user_id, status))

# Node.js (pg)
client.query('SELECT * FROM users WHERE id = $1', [userId])

# Java (PreparedStatement)
PreparedStatement ps = conn.prepareStatement("SELECT * FROM users WHERE id = ?");
ps.setInt(1, userId);
```

**Layer 2 — ORM Usage:**
```python
# Django ORM - inherently parameterized
User.objects.filter(email=user_input, status='active')

# SQLAlchemy
session.query(User).filter(User.email == user_input).all()
```

**Layer 3 — Input Validation:**
- Validate data types (integer for IDs, email format for emails)
- Whitelist allowed values for enums and status fields
- Reject unexpected characters in structured fields

**Layer 4 — Least Privilege:**
- Application database user has only SELECT, INSERT, UPDATE, DELETE
- No CREATE, DROP, ALTER, or GRANT permissions
- Separate credentials for migrations vs application

---

## Cross-Site Scripting (XSS)

### XSS Types

| Type | Delivery | Persistence | Example |
|------|----------|-------------|---------|
| Reflected | URL parameter | None | Search query displayed in results |
| Stored | Database field | Persistent | Comment with script tag |
| DOM-based | Client-side code | None | `document.write(location.hash)` |
| Mutation | Browser parser quirks | Varies | Malformed HTML bypassing filters |

### Prevention Strategy

**1. Context-Aware Output Encoding:**
- Use framework auto-escaping (React, Angular, Django, Rails)
- Manually encode when inserting into non-HTML contexts

**2. Content Security Policy:**
```
Content-Security-Policy: 
  script-src 'self' 'nonce-{random}';
  object-src 'none';
  base-uri 'self'
```

**3. Sanitize User HTML (when HTML input is required):**
- Use allowlist-based sanitizers (DOMPurify, Bleach)
- Never use regex-based HTML cleaning
- Strip all event handlers and JavaScript URIs

**4. Additional Headers:**
```
X-Content-Type-Options: nosniff
X-XSS-Protection: 0  (deprecated, use CSP instead)
```

---

## Cross-Site Request Forgery (CSRF)

### Prevention Methods

| Method | Implementation | Effectiveness |
|--------|---------------|--------------|
| CSRF tokens | Unique token per session/form | High |
| SameSite cookies | `SameSite=Lax` or `Strict` | High |
| Double-submit cookie | Token in cookie + request body | Medium-High |
| Custom headers | `X-Requested-With` check | Medium |
| Origin validation | Check `Origin`/`Referer` headers | Medium |

### CSRF Token Implementation
1. Generate random token per session
2. Include token in forms as hidden field
3. Include token in AJAX via custom header
4. Validate token on every state-changing request
5. Regenerate token periodically

---

## NoSQL Injection

### MongoDB Injection
```javascript
// VULNERABLE: User can pass {"$gt": ""} to bypass
db.users.find({username: req.body.username, password: req.body.password})

// SAFE: Type checking and sanitization
const username = String(req.body.username);
const password = String(req.body.password);
db.users.find({username, password})
```

### Prevention
- Validate input types strictly (reject objects when expecting strings)
- Use parameterized queries where available
- Sanitize operators (`$gt`, `$ne`, `$regex`) from user input
- Use ODM libraries (Mongoose) with schema validation

---

## Server-Side Request Forgery (SSRF)

### Attack Scenarios
- Fetch internal metadata: `http://169.254.169.254/latest/meta-data/`
- Port scanning: `http://internal-server:22/`
- Access internal APIs: `http://internal-api:8080/admin`

### Prevention
- Validate URLs against allowlist of permitted domains
- Block private IP ranges (10.x, 172.16-31.x, 192.168.x, 127.x, 169.254.x)
- Disable HTTP redirects or re-validate after redirect
- Use network segmentation (application cannot reach metadata services)
- Implement URL parsing to detect bypass attempts (decimal IPs, IPv6)
