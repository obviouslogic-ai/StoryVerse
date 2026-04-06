# Phase 5: Testing and Pre-Release (Per Release)

## Goal

Comprehensive testing and validation before each significant release.

## Duration

1–3 days per release cycle

## Active Agents

| Agent | Role in Phase 5 |
|-------|-----------------|
| Test Architect (ATADA) | Comprehensive test execution |
| Security Agent (STMA) | Security review and abuse case testing |
| Release Readiness Agent (RRA) | Final GO / HOLD / BLOCK |
| Compliance Gate | Full compliance verification |
| Human Approval Authority (HAA) | Final sign-off (if required) |

## Testing Sequence

### 1. Full Test Suite Execution

- Unit tests — all passing
- Integration tests — all passing
- End-to-end tests — all passing
- Compliance tests — all manifest rules verified
- **Owner**: ATADA

### 2. Security Review

- Threat model updated for new features
- Abuse case testing for user-facing changes
- Dependency vulnerability scan (npm audit / pip audit)
- Auth flow verification
- **Owner**: STMA

### 3. Compliance Verification

- All active manifest rules checked
- Policy-gate-checklist filled out
- Any new policy domains scoped and manifested
- Audit trail complete
- **Owner**: Compliance Gate, STMA

### 4. Performance Validation

- Load testing (if applicable)
- Latency checks against baselines
- Bundle size verification
- Database query performance review
- **Owner**: CEA, ATADA

### 5. Reliability and Resilience Validation

- Idempotency duplicate tests pass for side-effecting flows
- Retry policy confirms no blind retry on permanent classes
- Reconciliation job run validates orphan repair success
- Failover/degrade-mode drill evidence attached (for outage-sensitive systems)
- **Owner**: ATADA, ORFA, RRA

### 6. Documentation Review

- All docs current with implementation
- Changelog complete for this release
- API documentation updated
- Runbooks updated for new operational concerns
- **Owner**: DMA

### 7. Release Readiness Assessment

- RRA evaluates all signals from steps 1–5
- Collects agent reports
- Generates release readiness report
- Issues verdict
- **Owner**: RRA

## Release Readiness Evaluation

RRA collects signals from all agents:

| Signal | Source | Threshold |
|--------|--------|-----------|
| Testing | ATADA | All tests pass, coverage above thresholds |
| Security | STMA | No open high/critical findings |
| Compliance | Compliance Gate | All manifest rules verified |
| Reliability | Reliability Gate | Dedupe/retry/reconciliation checks pass |
| Resilience | ORFA/RRA | Latest failover drill evidence within policy window |
| Quality | QMSA | No F-graded domains |
| Documentation | DMA | All docs current |
| Dependencies | CEA | No critical vulnerabilities |

## Verdicts

- **GO**: All signals green → merge and deploy
- **HOLD**: Issues identified but resolvable → remediation list provided, return when resolved
- **BLOCK**: Unacceptable risk → requires HAA to override (rarely appropriate)

## Post-Deploy

After deployment:
1. Observability Agent (ORFA) monitors production impact for 24 hours
2. Error rates, latency, and user-facing metrics compared to baseline
3. Rollback triggered if error budget is consumed
4. Linear issue updated with deployment status

## Phase 5 Checklist (Per Release)

- [ ] Full test suite passes
- [ ] Security review complete
- [ ] Compliance verification complete
- [ ] Performance acceptable
- [ ] Reliability and resilience validation complete
- [ ] Documentation current
- [ ] Release readiness report generated
- [ ] RRA verdict: GO / HOLD / BLOCK
- [ ] HAA approval (if required)
- [ ] Deployed to production
- [ ] Post-deploy monitoring active

## Cross-References

- Retrospective process: `lifecycle/phase-6-retrospective.md`
- Quality management: `lifecycle/phase-4-quality-entropy.md`
- Development loop: `lifecycle/development-loop.md`
- Feature development: `lifecycle/phase-3-feature-dev.md`
- Pilot and hardening runbook: `reference/operations/pilot-and-hardening-runbook.md`
