# Secure Coding Practices Guide

Language-agnostic secure coding practices for building resilient web applications.

---

## Input Validation

### Validation Strategy

**Always validate on the server side** — client-side validation is for UX only.

| Validation Type | Description | Example |
|----------------|-------------|---------|
| Type checking | Ensure correct data type | Integer, string, boolean |
| Length limits | Min/max length constraints | Username: 3-50 characters |
| Format validation | Regex or format matching | Email, phone, date |
| Range checking | Numeric boundaries | Age: 0-150, price: 0.01-999999 |
| Allowlist | Accept only known-good values | Country codes, status enums |
| Canonicalization | Normalize before validation | URL decode, Unicode normalize |

### Validation Patterns

```python
# Pydantic model (Python)
from pydantic import BaseModel, Field, EmailStr

class CreateUserRequest(BaseModel):
    name: str = Field(min_length=1, max_length=100)
    email: EmailStr
    age: int = Field(ge=13, le=150)
    role: Literal["viewer", "editor", "admin"]
```

---

## Output Encoding

### Context-Aware Encoding

Always encode output based on where it appears:

| Context | Encoding Function | Framework Support |
|---------|------------------|-------------------|
| HTML body | HTML entity encode | React JSX (auto), Django `{{ var }}` |
| HTML attributes | Attribute encode | Most frameworks auto-encode |
| JavaScript | JS string encode | Never inject user data into `<script>` |
| URL parameters | URL encode | `encodeURIComponent()` |
| CSS values | CSS encode | Avoid user input in CSS |
| JSON | JSON serialize | `JSON.stringify()` |

### Content Security Policy (CSP)

```
Content-Security-Policy:
  default-src 'self';
  script-src 'self' 'nonce-abc123';
  style-src 'self' 'unsafe-inline';
  img-src 'self' data: https:;
  font-src 'self';
  connect-src 'self' https://api.example.com;
  frame-ancestors 'none';
  base-uri 'self';
  form-action 'self'
```

---

## Authentication Security

### Password Storage
- Use Argon2id (preferred), bcrypt, or scrypt
- Never use MD5, SHA-1, or SHA-256 alone for passwords
- Salt is generated automatically by modern hashing libraries
- Set appropriate work factors (bcrypt: cost 12+, Argon2: 64MB memory, 3 iterations)

### Session Security
- Generate session IDs with CSPRNG (128+ bits entropy)
- Regenerate session ID after login
- Set HttpOnly, Secure, SameSite flags on cookies
- Implement idle and absolute timeouts
- Invalidate sessions on logout server-side

---

## Error Handling

### Secure Error Responses

**In Production:**
```json
{
  "error": {
    "code": "INTERNAL_ERROR",
    "message": "An unexpected error occurred. Please try again.",
    "request_id": "req_abc123"
  }
}
```

**Never Expose:**
- Stack traces
- Database query details
- Internal file paths
- Framework versions
- Server configuration

### Exception Handling Pattern
```python
try:
    result = process_request(data)
except ValidationError as e:
    return error_response(400, "VALIDATION_ERROR", str(e))
except PermissionError:
    return error_response(403, "FORBIDDEN", "Insufficient permissions")
except Exception as e:
    logger.error(f"Unexpected error: {e}", exc_info=True)
    return error_response(500, "INTERNAL_ERROR", "An unexpected error occurred")
```

---

## File Upload Security

### Validation Checklist

| Check | Implementation |
|-------|---------------|
| File type | Verify magic bytes (not just extension) |
| File size | Enforce server-side limits (e.g., 10MB) |
| Filename | Sanitize, replace with UUID |
| Content scanning | Antivirus scan for user uploads |
| Storage location | Outside web root, separate domain |
| Access control | Signed URLs with expiry |

### Secure Upload Flow
1. Validate file type by magic bytes
2. Rename to UUID with safe extension
3. Scan for malware
4. Store in isolated storage (S3, separate domain)
5. Serve through signed URLs or proxy with security headers

---

## Dependency Management

### Security Practices
- Pin dependency versions in lock files
- Enable automated vulnerability scanning (Dependabot, Snyk, Renovate)
- Review dependency updates before merging
- Monitor for newly disclosed CVEs
- Remove unused dependencies
- Prefer well-maintained packages with active security response
- Audit transitive dependencies

---

## Logging and Monitoring

### Security Events to Log
- Authentication successes and failures
- Authorization failures
- Input validation failures
- Application errors and exceptions
- Administrative actions
- Data access patterns

### PII in Logs
- Never log passwords, tokens, or secrets
- Mask credit card numbers, SSNs
- Hash or truncate email addresses in logs
- Use structured logging with redaction filters
