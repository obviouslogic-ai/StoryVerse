# Compliance Test Vectors

Template for expanding enforcement manifest `check_description` fields into executable test implementations.

## Purpose

Each enforceable rule in a manifest has a `check_description` field. This document templates how to turn those descriptions into actual tests that run in CI. The Test Architect agent reads manifests and generates test vectors for `ci_checkable` rules during Phase 1.

## Template Per Rule

Use this structure when adding a new compliance test:

```markdown
### [RULE-ID]: [Rule Name]
- **Source manifest:** [domain].manifest.yml
- **Check description:** [from manifest]
- **Test type:** unit | integration | e2e | static analysis
- **Test location:** tests/compliance/[rule-id].test.ts
- **Implementation:**
  - [Step 1]
  - [Step 2]
- **Pass criteria:** [What constitutes a pass]
- **Failure action:** block-merge | require-review | warn
```

## Example Test Vectors

### AUTH-001: Minimum 12-character passwords with complexity

- **Check:** Password schema enforces min length and character classes
- **Test type:** unit
- **Implementation:** Test auth service password validation; reject < 12 chars; reject missing uppercase/lowercase/digit/special
- **Pass:** All boundary cases reject invalid passwords; valid passwords accepted
- **Failure action:** block-merge

### AUTH-002: No plaintext password storage

- **Check:** No plaintext password columns; hashing in auth module
- **Test type:** static analysis + integration
- **Implementation:** Grep for plaintext password patterns; verify auth module uses bcrypt/argon2/scrypt
- **Pass:** No plaintext patterns; hashing verified in auth flow
- **Failure action:** block-merge

### DC-001: AES-256 encryption at rest

- **Check:** Database encryption enabled; sensitive columns use application-level encryption
- **Test type:** integration
- **Implementation:** Verify Supabase encryption; test encrypted column read/write; raw values unreadable
- **Pass:** Encryption active; sensitive data not human-readable in DB
- **Failure action:** block-merge

### DC-002: TLS 1.2+ for data in transit

- **Check:** HTTPS enforced; TLS 1.2 minimum; HSTS enabled
- **Test type:** integration / config check
- **Implementation:** Verify API enforces HTTPS; TLS config rejects < 1.2; HSTS header present
- **Pass:** All endpoints HTTPS; TLS 1.2+; HSTS configured
- **Failure action:** block-merge

### LOG-001: 180-day log retention, structured format

- **Check:** Log retention >= 180 days; JSON format; required fields present
- **Test type:** configuration check + unit
- **Implementation:** Verify logging config retention; test log output includes timestamp, user_id, action, resource, result
- **Pass:** Retention >= 180 days; log format correct
- **Failure action:** block-merge

### LOG-002: Security events generate audit entries

- **Check:** Auth, access, admin events logged; audit logs immutable
- **Test type:** integration
- **Implementation:** Trigger each event type; verify log entry created; verify app cannot modify audit logs
- **Pass:** All mandatory events logged; audit integrity preserved
- **Failure action:** block-merge

### DEV-001: Peer review required

- **Check:** Branch protection requires 1+ approvals; author not sole approver
- **Test type:** configuration check
- **Implementation:** Verify GitHub branch protection rules; verify PR approval requirement
- **Pass:** Branch protection enforces review
- **Failure action:** block-merge

### DEV-003: No secrets in source control

- **Check:** No hardcoded keys, tokens, passwords; .env in .gitignore
- **Test type:** static analysis
- **Implementation:** Secret scan (gitleaks/trufflehog); verify .gitignore; grep for patterns
- **Pass:** No secrets detected; .env excluded
- **Failure action:** block-merge

### VULN-001: Dependency vulnerability scanning

- **Check:** npm audit / Snyk in CI; critical/high block merge; lockfile committed
- **Test type:** CI configuration check
- **Implementation:** Verify scanning step; verify blocking on critical/high; verify lockfile present
- **Pass:** Scanning configured; blocking on critical/high; lockfile committed
- **Failure action:** block-merge

### INFRA-001: TLS 1.2 minimum

- **Check:** TLS 1.0/1.1 disabled; AEAD ciphers only; HSTS enabled
- **Test type:** integration / config
- **Implementation:** Test SSL handshake with old protocols; verify cipher suite; verify HSTS header
- **Pass:** Old TLS rejected; ciphers correct; HSTS present
- **Failure action:** block-merge

### KM-001: Keys managed via KMS/vault

- **Check:** No hardcoded keys; env vars or KMS; rotation documented
- **Test type:** static analysis + config review
- **Implementation:** Grep for key patterns; verify key source; verify rotation schedule
- **Pass:** No hardcoded keys; KMS/env used; rotation documented
- **Failure action:** block-merge

---

## Generating Test Vectors

During Phase 1 (Knowledge Base), the Test Architect agent:

1. Reads all enforcement manifests
2. Identifies rules with `ci_checkable: true`
3. For each, generates a test vector using the `check_description` field
4. Writes tests to `tests/compliance/`
5. Ensures compliance-gate.yml runs these tests

Add new vectors as manifests are updated or new domains are added.
