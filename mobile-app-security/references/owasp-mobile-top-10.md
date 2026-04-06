# OWASP Mobile Top 10

Detailed coverage of the OWASP Mobile Top 10 risks with platform-specific guidance for iOS and Android.

---

## M1: Improper Credential Usage

Applications that hardcode credentials, API keys, or secrets in the source code, configuration files, or binary resources.

**Risk**: Attackers decompile the app and extract credentials, gaining access to backend services, APIs, or databases.

**Mitigations**:
- Never store API keys or secrets in client-side code — use server-side proxies
- Use platform keystores (iOS Keychain, Android Keystore) for any credentials that must be stored on-device
- Implement certificate pinning to prevent MITM attacks on credential transmission
- Rotate keys and tokens regularly; design for remote revocation

## M2: Inadequate Supply Chain Security

Third-party libraries, SDKs, and frameworks introducing vulnerabilities or malicious code.

**Risk**: A compromised dependency exfiltrates data, injects ads, or creates backdoors. Supply chain attacks are increasing in frequency.

**Mitigations**:
- Audit all third-party dependencies before inclusion
- Use dependency scanning tools (Snyk, OWASP Dependency-Check, GitHub Dependabot)
- Pin dependency versions and review changelogs before upgrading
- Prefer libraries with active maintenance, security policies, and source availability
- Implement Software Bill of Materials (SBOM) for your app

## M3: Insecure Authentication/Authorization

Weak or missing authentication mechanisms that allow unauthorized access to app functionality or data.

**Risk**: Attackers bypass login, escalate privileges, or access other users' data through broken auth flows.

**Mitigations**:
- Enforce authentication server-side — never trust client-side auth checks alone
- Use proven auth protocols (OAuth 2.0 + PKCE for mobile)
- Implement proper session management with server-side session validation
- Require biometric or MFA for sensitive operations
- Validate authorization on every API call, not just the initial login

## M4: Insufficient Input/Output Validation

Failure to properly validate, filter, or sanitize data going into or coming out of the app.

**Risk**: Injection attacks (SQL, XSS, command injection), data corruption, or app crashes from malformed input.

**Mitigations**:
- Validate all input on the server side (client-side validation is a UX feature, not a security control)
- Use parameterized queries for all database operations
- Sanitize data before rendering in WebViews to prevent XSS
- Validate API responses before processing (schema validation)

## M5: Insecure Communication

Data transmitted without encryption or with improperly configured TLS.

**Risk**: Attackers intercept sensitive data (credentials, personal information, financial data) via network sniffing or MITM attacks.

**Mitigations**:
- Enforce TLS 1.2+ for all network communications
- Implement certificate pinning (pin to the leaf or intermediate certificate)
- Disable fallback to cleartext HTTP (iOS ATS, Android Network Security Config `cleartextTrafficPermitted=false`)
- Validate server certificates properly — do not override certificate validation in production

## M6-M10: Additional Risks

| Risk | Description | Key Mitigation |
|------|-------------|---------------|
| M6: Inadequate Privacy Controls | Excessive data collection, missing consent | Minimize data collection, implement privacy by design |
| M7: Insufficient Binary Protections | No obfuscation, easy reverse engineering | Code obfuscation, integrity checks, anti-tampering |
| M8: Security Misconfiguration | Debug enabled in production, default settings | Automated security config checks in CI/CD |
| M9: Insecure Data Storage | Sensitive data in plaintext files, logs, backups | Encrypt local data, exclude from backups, clear logs |
| M10: Insufficient Cryptography | Weak algorithms, hardcoded keys, improper implementation | Use platform crypto APIs, AES-256, RSA-2048+, no custom crypto |

## Risk Assessment Matrix

| Risk | Likelihood | Impact | Priority |
|------|-----------|--------|----------|
| M1: Credential Usage | High | Critical | Immediate |
| M2: Supply Chain | Medium | High | High |
| M3: Auth/Authz | High | Critical | Immediate |
| M4: Input Validation | Medium | High | High |
| M5: Communication | Medium | Critical | High |
| M6-M10 | Varies | High | Address systematically |
