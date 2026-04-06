# JWT Authentication Patterns

Comprehensive guide to JSON Web Token implementation, security, and lifecycle management.

---

## JWT Structure

A JWT consists of three Base64URL-encoded parts separated by dots: `header.payload.signature`

### Header
```json
{
  "alg": "RS256",
  "typ": "JWT",
  "kid": "key-2024-01"
}
```
- **alg**: Signing algorithm (RS256 recommended for production)
- **kid**: Key ID for key rotation support

### Payload (Claims)

**Registered Claims:**
| Claim | Name | Purpose | Example |
|-------|------|---------|---------|
| `iss` | Issuer | Who created the token | `https://auth.example.com` |
| `sub` | Subject | User identifier | `user_abc123` |
| `aud` | Audience | Intended recipient | `https://api.example.com` |
| `exp` | Expiration | Token expiry (Unix timestamp) | `1700000000` |
| `iat` | Issued At | When token was created | `1699996400` |
| `nbf` | Not Before | Token not valid before | `1699996400` |
| `jti` | JWT ID | Unique token identifier | `uuid-v4` |

**Custom Claims:**
```json
{
  "sub": "user_abc123",
  "email": "user@example.com",
  "roles": ["admin", "editor"],
  "org_id": "org_456",
  "permissions": ["read:users", "write:posts"]
}
```

---

## Signing Algorithms

### Algorithm Selection

| Algorithm | Type | Key | Use Case | Security |
|-----------|------|-----|----------|----------|
| **RS256** | Asymmetric | RSA 2048+ | Production APIs, microservices | High |
| **ES256** | Asymmetric | ECDSA P-256 | Mobile, performance-sensitive | High |
| **HS256** | Symmetric | Shared secret | Simple apps, internal services | Medium |
| **EdDSA** | Asymmetric | Ed25519 | Modern systems, compact | High |

**Recommendation:** Use RS256 or ES256 for production. Asymmetric algorithms allow verification without exposing the signing key.

### Key Rotation Strategy
1. Generate new key pair with unique `kid`
2. Add new public key to JWKS endpoint
3. Start signing new tokens with new key
4. Keep old public key available for validation (overlap period)
5. Remove old public key after all old tokens expire

---

## Token Lifecycle

### Access Token Pattern
- **Duration**: 15-60 minutes
- **Content**: User identity + permissions
- **Storage**: Memory only (never localStorage)
- **Validation**: Verify signature, expiry, audience, issuer

### Refresh Token Pattern
- **Duration**: 7-30 days
- **Content**: Opaque reference (not JWT) or minimal JWT
- **Storage**: HttpOnly secure cookie or server-side
- **Rotation**: Issue new refresh token on each use

### Silent Refresh (SPA Pattern)
1. Access token expires
2. Use hidden iframe or background fetch to authorization server
3. If session still valid, receive new tokens
4. If session expired, redirect to login

---

## Validation Checklist

Every JWT must be validated before trusting its claims:

1. **Parse**: Decode Base64URL, verify three parts exist
2. **Algorithm**: Verify `alg` matches expected (prevent `alg: none` attack)
3. **Signature**: Verify using appropriate public key or secret
4. **Expiration**: Check `exp` > current time (allow small clock skew ~30s)
5. **Not Before**: Check `nbf` <= current time if present
6. **Issuer**: Verify `iss` matches expected issuer
7. **Audience**: Verify `aud` includes your service
8. **Custom claims**: Validate roles, permissions, org_id as needed

---

## Common Vulnerabilities and Mitigations

| Vulnerability | Attack | Mitigation |
|---------------|--------|------------|
| Algorithm confusion | Attacker changes `alg` to `none` | Whitelist allowed algorithms |
| Key confusion | RS256 → HS256 with public key as secret | Enforce asymmetric validation |
| Token theft (XSS) | Steal token from localStorage | Store in memory only, use HttpOnly cookies |
| Replay attacks | Reuse stolen token | Short expiry, token binding, jti tracking |
| Privilege escalation | Modify claims | Always verify signature before reading claims |
| Information leakage | Sensitive data in payload | Never put secrets in JWT; payload is Base64, not encrypted |

---

## Production Best Practices

- Use asymmetric signing (RS256/ES256) for distributed systems
- Keep tokens small — minimize custom claims
- Implement JWKS endpoint for public key distribution
- Set appropriate `exp` based on sensitivity (15min for financial, 1hr for general)
- Never store JWTs in localStorage (XSS vulnerable)
- Implement token revocation for logout (blacklist or short-lived tokens)
- Use `jti` claim for replay protection on sensitive operations
- Monitor for anomalous token usage patterns
