# Violation Classifications

How compliance violations are classified and what actions are taken.

## Classification Levels

### Critical (block-merge)
The violation exposes the system to immediate, severe risk. The PR cannot proceed under any circumstances without Human Approval Authority override and documented exception.

Examples:
- Plaintext password storage
- PHI/PII exposed in logs or error messages
- Missing authentication on sensitive endpoints
- Disabled encryption
- Hardcoded secrets in source code

### High (block-merge)
The violation represents a significant gap in compliance posture. The PR cannot proceed without remediation.

Examples:
- Password complexity below policy minimum
- Missing RLS on tables containing user data
- Audit logging absent for auth/data events
- HTTPS not enforced
- Missing input validation on API endpoints

### Medium (require-review)
The violation is a gap that should be addressed but may have legitimate exceptions. Requires human review and sign-off.

Examples:
- Log retention below policy minimum but above regulatory minimum
- Access control configured but not role-based
- Encryption using acceptable but not preferred algorithm
- Missing documentation for security decisions

### Low (warn)
The violation is a best-practice gap. Logged for tracking and addressed during entropy management.

Examples:
- Missing security headers (non-critical)
- Test coverage below threshold for compliance tests
- Documentation not up to date for minor policy changes
- Naming conventions not followed for security-related code

### Informational (log)
Not a violation but a data point for compliance posture tracking.

Examples:
- New dependency added (needs supply chain review)
- Configuration change in auth/data domain
- New API endpoint created (needs security review)
- Schema migration applied

## Actions

| Classification | CI Action | PR Status | Escalation |
|---------------|-----------|-----------|------------|
| Critical | Block merge | Cannot proceed | RRA + HAA |
| High | Block merge | Cannot proceed | RRA |
| Medium | Flag for review | Requires human approval | STMA review |
| Low | Warning in CI output | Can proceed | Tracked in backlog |
| Informational | Logged | Can proceed | None |

## Exception Process
1. Developer identifies that a rule cannot be satisfied for legitimate reasons
2. Developer requests exception via PR comment referencing rule ID
3. Security Agent (STMA) reviews and provides assessment
4. Human Approval Authority approves or rejects
5. If approved: exception documented in exception register with expiration date
6. Exception reviewed at next quarterly retro

## Exception Register Format
| Rule ID | Exception Reason | Approved By | Date | Expiration | Status |
|---------|-----------------|-------------|------|------------|--------|
| [RULE-ID] | [Why this rule cannot be satisfied] | [HAA name] | [date] | [date] | Active/Expired |
