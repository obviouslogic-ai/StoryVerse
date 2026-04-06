# Policy Gate Checklist

Pre-release compliance checklist. Every manifest rule must be verified before Release Readiness Agent can issue GO.

## Instructions

1. Before each release, populate status for each rule from active enforcement manifests
2. For each rule, verify compliance and record status (GREEN = pass, RED = fail)
3. All `block-merge` and `require-review` rules must be GREEN
4. Submit completed checklist to Release Readiness Agent as compliance signal

---

## Access Control Domain

| Rule ID | Rule | Status | Verified By | Date | Notes |
|---------|------|--------|-------------|------|-------|
| AUTH-001 | Min 12-char passwords with complexity | [ ] GREEN / [ ] RED | | | |
| AUTH-002 | No plaintext password storage | [ ] GREEN / [ ] RED | | | |
| AC-001 | RBAC enforcement on all resources | [ ] GREEN / [ ] RED | | | |
| AUTH-003 | MFA available for all accounts | [ ] GREEN / [ ] RED | | | |
| SESS-001 | Session timeouts and secure token handling | [ ] GREEN / [ ] RED | | | |
| PAM-001 | Privileged access reviewed quarterly | [ ] GREEN / [ ] RED | | | |

---

## Data Protection Domain

| Rule ID | Rule | Status | Verified By | Date | Notes |
|---------|------|--------|-------------|------|-------|
| DC-001 | AES-256 encryption at rest | [ ] GREEN / [ ] RED | | | |
| DC-002 | TLS 1.2+ for data in transit | [ ] GREEN / [ ] RED | | | |
| DC-003 | Data classified and handled per level | [ ] GREEN / [ ] RED | | | |
| PHI-001 | No PHI/PII in logs or errors | [ ] GREEN / [ ] RED | | | |
| DR-001 | Data retention and disposal policy | [ ] GREEN / [ ] RED | | | |
| DC-004 | No production data in non-prod | [ ] GREEN / [ ] RED | | | |

---

## Development & Change Domain

| Rule ID | Rule | Status | Verified By | Date | Notes |
|---------|------|--------|-------------|------|-------|
| DEV-001 | All code changes peer reviewed | [ ] GREEN / [ ] RED | | | |
| DEV-002 | No direct commits to main | [ ] GREEN / [ ] RED | | | |
| SEC-001 | OWASP Top 10 / secure coding | [ ] GREEN / [ ] RED | | | |
| API-001 | API input validation and sanitization | [ ] GREEN / [ ] RED | | | |
| DEV-003 | No secrets in source control | [ ] GREEN / [ ] RED | | | |

---

## Security Operations Domain

| Rule ID | Rule | Status | Verified By | Date | Notes |
|---------|------|--------|-------------|------|-------|
| LOG-001 | Structured logging, 180-day retention | [ ] GREEN / [ ] RED | | | |
| LOG-002 | Security events generate audit entries | [ ] GREEN / [ ] RED | | | |
| IR-001 | Incident response plan documented | [ ] GREEN / [ ] RED | | | |
| VULN-001 | Dependency vulnerability scanning | [ ] GREEN / [ ] RED | | | |
| AUDIT-001 | Audit trail tamper-evident | [ ] GREEN / [ ] RED | | | |

---

## Infrastructure & Configuration Domain

| Rule ID | Rule | Status | Verified By | Date | Notes |
|---------|------|--------|-------------|------|-------|
| INFRA-001 | TLS 1.2 minimum, 1.3 preferred | [ ] GREEN / [ ] RED | | | |
| KM-001 | Keys managed via KMS/vault | [ ] GREEN / [ ] RED | | | |
| NET-001 | Network least-privilege, segmentation | [ ] GREEN / [ ] RED | | | |
| CM-001 | Config version-controlled, reproducible | [ ] GREEN / [ ] RED | | | |
| ENV-001 | Dev/staging/prod strictly separated | [ ] GREEN / [ ] RED | | | |

---

## Business Continuity Domain

| Rule ID | Rule | Status | Verified By | Date | Notes |
|---------|------|--------|-------------|------|-------|
| BC-001 | Daily backups, verified restoration | [ ] GREEN / [ ] RED | | | |
| BC-002 | DR plan tested annually | [ ] GREEN / [ ] RED | | | |
| BC-003 | RTO/RPO defined and achievable | [ ] GREEN / [ ] RED | | | |
| BC-004 | Availability monitored, alerting | [ ] GREEN / [ ] RED | | | |

---

## Client Overrides (if applicable)

| Rule ID | Rule | Status | Verified By | Date | Notes |
|---------|------|--------|-------------|------|-------|
| [Add from client-overrides.manifest.yml] | | | | | |

---

## Summary

| Metric | Count |
|--------|-------|
| Total rules | ___ |
| GREEN | ___ |
| RED | ___ |
| Exceptions (in exception register) | ___ |

## Verdict

- **PASS:** All `block-merge` and `require-review` rules GREEN
- **FAIL (BLOCK):** Any `block-merge` rule RED
- **HOLD:** Any `require-review` rule RED (needs human sign-off)
