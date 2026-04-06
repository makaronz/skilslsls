# Security Testing Guide

Comprehensive security testing strategies including SAST, DAST, penetration testing, and bug bounties.

---

## Testing Types

| Type | When | What It Finds | Tools |
|------|------|--------------|-------|
| SAST | During development | Code-level vulnerabilities | Semgrep, SonarQube, CodeQL |
| DAST | Against running app | Runtime vulnerabilities | OWASP ZAP, Burp Suite |
| SCA | CI/CD pipeline | Vulnerable dependencies | Snyk, Dependabot, Trivy |
| Penetration testing | Quarterly/annually | Complex attack chains | Manual + tools |
| Bug bounty | Ongoing | Unknown vulnerabilities | HackerOne, Bugcrowd |

---

## Static Application Security Testing (SAST)

### Tool Comparison

| Tool | Languages | Free Tier | CI Integration | Accuracy |
|------|-----------|-----------|---------------|----------|
| Semgrep | 30+ languages | Yes (OSS) | GitHub, GitLab | High (low FP) |
| SonarQube | 25+ languages | Community edition | Jenkins, GitHub | Good |
| CodeQL | JS, Python, Java, C++ | Free for OSS | GitHub Actions | Very high |
| Bandit | Python only | Yes (OSS) | Any CI | Good |
| ESLint (security plugins) | JavaScript/TS | Yes | Any CI | Moderate |

### SAST Integration in CI/CD
```yaml
# GitHub Actions example
- name: Run Semgrep
  uses: returntocorp/semgrep-action@v1
  with:
    config: >-
      p/security-audit
      p/owasp-top-ten
      p/secrets
```

### Custom Rules
Write project-specific rules for your security requirements:
- Enforce parameterized queries
- Detect hardcoded credentials
- Flag unsafe deserialization
- Require authentication decorators on endpoints

---

## Dynamic Application Security Testing (DAST)

### OWASP ZAP Workflow

1. **Spider**: Crawl application to discover all endpoints
2. **Ajax Spider**: Crawl JavaScript-heavy SPAs
3. **Active Scan**: Test each endpoint for vulnerabilities
4. **Manual Testing**: Explore areas the scanner missed

### Common DAST Findings

| Finding | Severity | False Positive Rate |
|---------|----------|-------------------|
| Missing security headers | Low-Medium | Very low |
| SQL injection | Critical | Low |
| XSS (reflected) | High | Medium |
| Open redirects | Medium | Medium |
| Information disclosure | Low-Medium | Low |
| CSRF vulnerability | Medium | Medium |

### DAST in CI/CD
- Run baseline scan on every PR (fast, passive only)
- Run full scan weekly or on release branches
- Gate deployments on critical/high findings
- Maintain false positive suppression list

---

## Penetration Testing

### Scope Definition

| Area | Include | Exclude |
|------|---------|---------|
| Web application | All endpoints, authentication, authorization | Third-party services |
| API | All API versions, authentication | Rate limit testing (coordinate) |
| Infrastructure | Cloud config, network segmentation | Physical security |
| Mobile | App logic, API communication | App store review |

### Testing Methodology (OWASP Testing Guide)

1. **Information Gathering**: Technology stack, endpoints, error messages
2. **Configuration Testing**: Security headers, TLS configuration, error handling
3. **Authentication Testing**: Brute force, credential stuffing, session management
4. **Authorization Testing**: IDOR, privilege escalation, function-level access
5. **Input Validation**: Injection, XSS, file upload, parameter manipulation
6. **Business Logic**: Workflow bypass, race conditions, abuse cases
7. **API Testing**: Authentication, rate limiting, data exposure

### Reporting Template

| Field | Content |
|-------|---------|
| Title | Clear, descriptive vulnerability name |
| Severity | Critical/High/Medium/Low (CVSS score) |
| Description | Technical details of the vulnerability |
| Steps to Reproduce | Exact steps to recreate the issue |
| Impact | What an attacker could achieve |
| Evidence | Screenshots, request/response logs |
| Remediation | Specific fix recommendations |
| References | CVE, CWE, OWASP references |

---

## Software Composition Analysis (SCA)

### Dependency Risk Assessment

| Risk Factor | Weight | Assessment |
|-------------|--------|-----------|
| Known CVEs | High | Auto-scan with Snyk/Dependabot |
| Maintenance status | Medium | Last commit, open issues, maintainers |
| License compliance | Medium | Auto-detect with license checkers |
| Transitive dependencies | Medium | Full dependency tree analysis |
| Download popularity | Low | npm downloads, GitHub stars |

### Vulnerability Response SLAs

| Severity | Patch SLA | Workaround SLA |
|----------|----------|---------------|
| Critical (CVSS 9.0+) | 24 hours | Immediate |
| High (CVSS 7.0-8.9) | 1 week | 48 hours |
| Medium (CVSS 4.0-6.9) | 1 month | 1 week |
| Low (CVSS 0.1-3.9) | Next release | N/A |

---

## Security Testing Automation

### Recommended Pipeline

```
Code Commit → SAST Scan → SCA Scan → Build → DAST Baseline
  → Deploy Staging → DAST Full Scan → Manual Review → Deploy Production
```

### Metrics to Track
- **Mean Time to Remediate (MTTR)** by severity
- **Vulnerability density** (findings per 1000 LOC)
- **False positive rate** (tune scanners regularly)
- **Coverage** (% of codebase scanned, % of endpoints tested)
- **Recurrence rate** (same vulnerability type found again)
