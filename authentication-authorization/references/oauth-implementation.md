# OAuth 2.0 Implementation Guide

Comprehensive guide to implementing OAuth 2.0 flows for secure third-party authentication and authorization.

---

## OAuth 2.0 Grant Types

### Authorization Code Flow (Recommended for Server-Side Apps)

The most secure flow for web applications with a backend server.

**Flow Steps:**
1. Redirect user to authorization server with `response_type=code`
2. User authenticates and consents
3. Authorization server redirects back with `code` parameter
4. Backend exchanges `code` for tokens via POST to token endpoint
5. Store tokens securely server-side

**Request Parameters:**
| Parameter | Required | Description |
|-----------|----------|-------------|
| `response_type` | Yes | Must be `code` |
| `client_id` | Yes | Application's client ID |
| `redirect_uri` | Yes | Must match registered URI exactly |
| `scope` | Yes | Space-separated list of permissions |
| `state` | Yes | CSRF protection token (random, unguessable) |
| `code_challenge` | Recommended | PKCE challenge for added security |

### Authorization Code Flow with PKCE

Required for public clients (SPAs, mobile apps) and recommended for all clients.

**PKCE Implementation:**
1. Generate `code_verifier`: 43-128 character random string
2. Compute `code_challenge`: Base64URL(SHA256(code_verifier))
3. Include `code_challenge` and `code_challenge_method=S256` in auth request
4. Include `code_verifier` in token exchange request

### Client Credentials Flow

For machine-to-machine communication without user context.

**Use Cases:** Service-to-service APIs, background jobs, microservice auth

**Token Request:**
```
POST /oauth/token
Content-Type: application/x-www-form-urlencoded

grant_type=client_credentials
&client_id=YOUR_CLIENT_ID
&client_secret=YOUR_CLIENT_SECRET
&scope=api:read api:write
```

### Device Authorization Flow

For devices with limited input (smart TVs, IoT devices, CLI tools).

**Flow:** Device shows code → User enters code on another device → Device polls for token

---

## Token Management

### Access Token Best Practices
- **Short expiry**: 15-60 minutes
- **Stateless validation**: Use JWT format for self-contained validation
- **Scope restriction**: Request minimum necessary scopes
- **Never expose in URLs**: Use Authorization header or POST body

### Refresh Token Security
- **Long-lived but rotatable**: 7-90 days depending on sensitivity
- **Rotation on use**: Issue new refresh token with each use, invalidate old one
- **Bind to client**: Validate client_id on refresh
- **Secure storage**: Server-side only, encrypted at rest
- **Revocation support**: Maintain revocation list or use reference tokens

### Token Storage by Client Type

| Client Type | Access Token | Refresh Token |
|-------------|-------------|---------------|
| Server-side app | Server memory/session | Encrypted database |
| SPA | Memory (JS variable) | HttpOnly secure cookie or avoid |
| Mobile app | Secure keychain/keystore | Secure keychain/keystore |
| CLI tool | OS credential manager | OS credential manager |

---

## Provider Integration

### Google OAuth 2.0
- Authorization endpoint: `https://accounts.google.com/o/oauth2/v2/auth`
- Token endpoint: `https://oauth2.googleapis.com/token`
- Scopes: `openid email profile` for basic identity
- Supports PKCE and incremental authorization

### GitHub OAuth
- Authorization: `https://github.com/login/oauth/authorize`
- Token: `https://github.com/login/oauth/access_token`
- Scopes: `repo`, `user`, `read:org` (granular)
- Note: Does not support PKCE natively

### Microsoft Identity Platform
- Authorization: `https://login.microsoftonline.com/{tenant}/oauth2/v2/authorize`
- Token: `https://login.microsoftonline.com/{tenant}/oauth2/v2/token`
- Supports PKCE, multi-tenant, and B2C scenarios

---

## Security Checklist

- [ ] Always validate `state` parameter to prevent CSRF
- [ ] Use PKCE for all public clients
- [ ] Validate redirect URIs exactly (no wildcards in production)
- [ ] Store client secrets securely (environment variables, vault)
- [ ] Implement token revocation endpoint
- [ ] Log all token exchanges for audit
- [ ] Use TLS for all OAuth endpoints
- [ ] Validate token audience (`aud`) and issuer (`iss`) claims
- [ ] Implement rate limiting on token endpoints
- [ ] Handle token errors gracefully with proper user messaging
