# OWASP Top 10 Detailed Guide

In-depth coverage of each OWASP Top 10:2025 vulnerability with examples and remediation.

---

## A01: Broken Access Control

The most critical web application vulnerability — 94% of applications tested had some form of broken access control.

### Common Vulnerabilities

| Vulnerability | Example | Impact |
|---------------|---------|--------|
| IDOR | `/api/users/123` → change to `/api/users/456` | Data exposure |
| Missing function-level access | Regular user accesses `/admin/users` | Privilege escalation |
| CORS misconfiguration | `Access-Control-Allow-Origin: *` | Cross-origin data theft |
| Path traversal | `../../../etc/passwd` in file parameter | System compromise |
| JWT manipulation | Modify role claim without re-signing | Authorization bypass |

### Prevention Strategies
- Implement server-side access control checks on every request
- Default deny: require explicit grants for all resources
- Validate object ownership before returning data
- Use indirect reference maps (UUID → internal ID)
- Disable directory listing and ensure metadata files aren't served
- Log and alert on access control failures
- Rate limit API access to minimize automated attacks

---

## A02: Cryptographic Failures

### Common Mistakes

| Mistake | Risk | Correct Approach |
|---------|------|-----------------|
| MD5/SHA1 for passwords | Rainbow table attacks | bcrypt, scrypt, or Argon2 |
| ECB mode encryption | Pattern leakage | AES-GCM or ChaCha20-Poly1305 |
| Hardcoded keys | Key compromise | Key management service (KMS) |
| HTTP for sensitive data | Eavesdropping | TLS 1.2+ everywhere |
| Weak random generation | Predictable tokens | CSPRNG (os.urandom, crypto.randomBytes) |

### Data Classification
- **Public**: No encryption needed
- **Internal**: Encrypt in transit (TLS)
- **Confidential**: Encrypt in transit and at rest
- **Restricted**: Encrypt everywhere, strict key management, access logging

---

## A03: Injection

### SQL Injection Prevention

```python
# VULNERABLE
query = f"SELECT * FROM users WHERE email = '{user_input}'"

# SAFE: Parameterized query
cursor.execute("SELECT * FROM users WHERE email = %s", (user_input,))

# SAFE: ORM
User.objects.filter(email=user_input)
```

### XSS Prevention

| Context | Encoding | Example |
|---------|----------|---------|
| HTML body | HTML entity encode | `&lt;script&gt;` |
| HTML attribute | Attribute encode + quote | `value="encoded"` |
| JavaScript | JS encode | `\x3cscript\x3e` |
| URL | URL encode | `%3Cscript%3E` |
| CSS | CSS encode | `\003Cscript\003E` |

### Command Injection Prevention
- Avoid system calls with user input entirely
- Use language-native libraries instead of shell commands
- If unavoidable: whitelist allowed characters, use parameterized APIs

---

## A04: Insecure Design

### Threat Modeling Process
1. **Decompose**: Identify assets, entry points, trust boundaries
2. **Identify threats**: Use STRIDE (Spoofing, Tampering, Repudiation, Info Disclosure, DoS, Elevation)
3. **Rate risks**: Impact × Likelihood
4. **Mitigate**: Design controls for high-risk threats
5. **Validate**: Security testing against threat model

### Secure Design Patterns
- Defense in depth (multiple security layers)
- Fail securely (errors don't bypass security)
- Least privilege (minimum necessary access)
- Separation of concerns (isolate security-critical components)
- Complete mediation (check access on every request)

---

## A05-A10: Additional Vulnerabilities

### A05: Security Misconfiguration
- Remove default credentials and accounts
- Disable unnecessary features and services
- Keep frameworks and dependencies updated
- Implement proper error handling (no stack traces in production)
- Set security headers on all responses

### A06: Vulnerable Components
- Maintain software bill of materials (SBOM)
- Monitor CVE databases for dependencies
- Automate dependency scanning (Dependabot, Snyk, OWASP Dependency-Check)
- Remove unused dependencies

### A07: Authentication Failures
- Implement MFA for all accounts
- Use strong password policies (length > complexity)
- Rate limit and lock accounts after failed attempts
- Use secure session management

### A08: Software and Data Integrity Failures
- Verify software integrity with checksums and signatures
- Secure CI/CD pipelines (signed commits, protected branches)
- Validate serialized data before processing

### A09: Security Logging and Monitoring Failures
- Log authentication events, access control failures, input validation failures
- Implement alerting for suspicious patterns
- Ensure logs are tamper-proof and centralized

### A10: Server-Side Request Forgery (SSRF)
- Validate and sanitize all user-supplied URLs
- Use allowlists for permitted external services
- Disable unnecessary URL schemes (file://, gopher://)
- Implement network segmentation
