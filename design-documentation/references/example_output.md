# Example Output — Design Documentation

A complete example of a design document demonstrating proper structure, content depth, and formatting conventions.

---

## Example: User Authentication Service — Design Document

### 1. Overview

This document describes the design for a centralized user authentication service that handles login, registration, session management, and multi-factor authentication (MFA) for all client applications.

**Problem Statement**: The current system has authentication logic duplicated across three services, leading to inconsistent security policies and a fragmented user experience.

**Goals**:
- Consolidate authentication into a single service with a unified API
- Support email/password, OAuth (Google, GitHub), and MFA (TOTP, SMS)
- Achieve 99.99% uptime with sub-200ms p95 login latency
- Comply with SOC 2 and GDPR requirements

**Non-Goals**:
- User profile management (handled by the User Service)
- Authorization / permissions (handled by the Policy Service)

### 2. Architecture

```
┌─────────────┐     ┌──────────────────┐     ┌──────────────┐
│  Web Client  │────▶│  API Gateway     │────▶│  Auth Service │
│  Mobile App  │     │  (rate limiting) │     │  (this doc)  │
└─────────────┘     └──────────────────┘     └──────┬───────┘
                                                     │
                              ┌───────────┬──────────┼──────────┐
                              ▼           ▼          ▼          ▼
                         PostgreSQL   Redis Cache  OAuth      SMS
                         (users,     (sessions,   Provider   Gateway
                          creds)     rate limits)  (Google)   (Twilio)
```

### 3. API Design

| Endpoint | Method | Description | Auth Required |
|----------|--------|-------------|--------------|
| `/auth/register` | POST | Create new account | No |
| `/auth/login` | POST | Authenticate and receive tokens | No |
| `/auth/refresh` | POST | Exchange refresh token for new access token | Refresh token |
| `/auth/logout` | POST | Invalidate session | Access token |
| `/auth/mfa/setup` | POST | Generate TOTP secret and QR code | Access token |
| `/auth/mfa/verify` | POST | Verify TOTP code | Access token |

### 4. Data Model

```sql
CREATE TABLE users (
    id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
    email VARCHAR(255) UNIQUE NOT NULL,
    password_hash VARCHAR(255),
    mfa_enabled BOOLEAN DEFAULT FALSE,
    mfa_secret VARCHAR(255),
    created_at TIMESTAMPTZ DEFAULT NOW(),
    updated_at TIMESTAMPTZ DEFAULT NOW()
);

CREATE TABLE sessions (
    id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
    user_id UUID REFERENCES users(id),
    refresh_token_hash VARCHAR(255) NOT NULL,
    expires_at TIMESTAMPTZ NOT NULL,
    created_at TIMESTAMPTZ DEFAULT NOW()
);
```

### 5. Security Considerations

- **Password hashing**: bcrypt with cost factor 12 (min 100ms hash time)
- **Token format**: JWT with RS256 signing, 15-minute access token TTL, 7-day refresh token TTL
- **Rate limiting**: 5 failed login attempts per account per 15 minutes, then 30-minute lockout
- **TOTP**: 6-digit codes, 30-second window, SHA-1 per RFC 6238
- **Audit logging**: All authentication events logged with IP, user agent, and outcome

### 6. Tradeoffs and Alternatives Considered

| Decision | Chosen | Alternative | Rationale |
|----------|--------|-------------|-----------|
| Token format | JWT | Opaque tokens | JWTs allow stateless verification by downstream services |
| Session store | Redis | PostgreSQL | Sub-millisecond lookups for session validation |
| Password hash | bcrypt | Argon2id | Broader library support; Argon2id considered for future migration |
| MFA method | TOTP | WebAuthn | Simpler initial implementation; WebAuthn planned for Phase 2 |

### 7. Rollout Plan

- **Phase 1** (Week 1-2): Deploy service with email/password login, shadow mode alongside existing auth
- **Phase 2** (Week 3-4): Enable OAuth providers, migrate web client to new service
- **Phase 3** (Week 5-6): Add MFA support, migrate mobile apps
- **Phase 4** (Week 7-8): Decommission legacy auth endpoints, full cutover

### 8. Success Metrics

| Metric | Target | Measurement |
|--------|--------|-------------|
| Login p95 latency | < 200ms | Datadog APM |
| Uptime | 99.99% | Uptime monitor |
| MFA adoption | > 30% of active users within 6 months | Analytics dashboard |
| Failed login rate | < 5% of attempts | Auth service logs |

---

This example demonstrates the expected depth, structure, and level of technical detail for design documentation. Adapt section headings and depth to the complexity of the system being designed.
