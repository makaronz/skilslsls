# Security Testing Guide

Methodologies, tools, and checklists for testing mobile application security on iOS and Android.

---

## Testing Methodology

### OWASP Mobile Security Testing Guide (MSTG)

The MSTG provides a comprehensive framework organized by test area:

| Area | Focus | Key Tests |
|------|-------|-----------|
| Data Storage | Files, databases, logs, clipboard, backups | Check for sensitive data in plaintext storage |
| Cryptography | Algorithm strength, key management, implementation | Verify proper crypto implementation |
| Authentication | Login, session management, biometrics | Test for bypass, token leakage, brute force |
| Network | TLS configuration, certificate pinning, data in transit | Intercept traffic, test pin bypass |
| Platform | OS integration, WebView, IPC, permissions | Test deep links, content providers, intent handling |
| Code Quality | Obfuscation, anti-tampering, reverse engineering | Decompile and analyze binary |

## Static Analysis (SAST)

### Tools

| Tool | Platform | Type | Key Features |
|------|----------|------|-------------|
| MobSF | iOS + Android | Open source | Automated static + dynamic analysis, API scanning |
| Semgrep | Both | Open source | Custom rule-based code scanning, CI/CD integration |
| Checkmarx | Both | Commercial | Enterprise SAST with mobile-specific rules |
| SonarQube | Both | Open source + Commercial | Code quality + security scanning |
| Snyk | Both | Commercial | Dependency vulnerability scanning |

### What to Scan For

| Category | Pattern | Severity |
|----------|---------|----------|
| Hardcoded secrets | API keys, passwords, tokens in source | Critical |
| Insecure storage | `SharedPreferences` (unencrypted), `NSUserDefaults` for sensitive data | High |
| Weak crypto | MD5, SHA1 for security, DES, ECB mode | High |
| Insecure network | HTTP URLs, disabled certificate validation | High |
| SQL injection | String concatenation in queries | High |
| Logging sensitive data | Tokens or PII in log statements | Medium |
| Debug configuration | `android:debuggable="true"`, disabled ATS | Medium |

## Dynamic Analysis (DAST)

### Proxy-Based Testing

Intercept and modify app traffic using a proxy:

1. **Setup**: Install Burp Suite or mitmproxy, configure device to use proxy
2. **Install CA cert**: Add the proxy's CA certificate to the device trust store
3. **Bypass pinning** (for testing): Use Frida or objection to disable certificate pinning at runtime
4. **Intercept**: Capture all API requests and responses
5. **Test**: Modify requests to test for IDOR, auth bypass, input validation failures

### Runtime Analysis with Frida

Frida enables dynamic instrumentation of running apps:

```javascript
// Hook a function to inspect arguments
Java.perform(function() {
    var LoginActivity = Java.use("com.example.app.LoginActivity");
    LoginActivity.authenticate.implementation = function(username, password) {
        console.log("Username: " + username);
        console.log("Password: " + password);
        return this.authenticate(username, password);
    };
});
```

Use Frida to:
- Bypass root/jailbreak detection
- Disable certificate pinning
- Inspect encrypted storage at runtime
- Hook crypto functions to capture keys and plaintext

## Penetration Testing Checklist

### Pre-Test Setup

- [ ] Install app on rooted/jailbroken device
- [ ] Configure proxy and install CA certificate
- [ ] Set up Frida server on device
- [ ] Decompile APK (jadx) or decrypt IPA (frida-ios-dump)

### Data Storage Tests

- [ ] Check filesystem for plaintext sensitive data
- [ ] Inspect SQLite databases for unencrypted data
- [ ] Review app logs for sensitive information
- [ ] Check clipboard for leaked data
- [ ] Verify backup exclusion of sensitive files

### Network Tests

- [ ] Verify TLS version (must be 1.2+)
- [ ] Test certificate pinning implementation
- [ ] Check for sensitive data in URL parameters
- [ ] Verify API authentication on all endpoints
- [ ] Test for IDOR (change user IDs in requests)

### Authentication Tests

- [ ] Test login with invalid credentials (brute force protection)
- [ ] Verify session timeout implementation
- [ ] Test token refresh and revocation
- [ ] Attempt to reuse expired tokens
- [ ] Test biometric bypass (if applicable)

### Binary Tests

- [ ] Check for code obfuscation
- [ ] Test root/jailbreak detection and bypass
- [ ] Verify anti-tampering mechanisms
- [ ] Check for debug symbols in production binary
