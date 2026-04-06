# HELIos Pipeline Risk Matrix

## Purpose
Identifies risks to the pipeline's operation, their likelihood, impact, and mitigations.

## Risk Scoring
- Likelihood: 1 (Rare) to 5 (Almost Certain)
- Impact: 1 (Negligible) to 5 (Critical)
- Risk Score = Likelihood × Impact
- Categories: Low (1-6), Medium (7-12), High (13-19), Critical (20-25)

## Risk Register

### Agent Risks
| ID | Risk | L | I | Score | Mitigation |
|----|------|---|---|-------|------------|
| A-01 | Agent produces incorrect code that passes tests | 3 | 4 | 12 | Structural tests, compliance gate, human review for high-risk paths |
| A-02 | Agent drifts from architectural intent over time | 3 | 4 | 12 | Architecture Guardian reviews, ARCHITECTURE.md as canonical source |
| A-03 | Agent makes unauthorized decisions (scope creep) | 2 | 4 | 8 | Constitution enforcement, stop-on-ambiguity rule |
| A-04 | Agent hallucinates dependencies or APIs | 3 | 3 | 9 | Self-review loop, CI build verification |
| A-05 | Conflicting agent directives cause deadlock | 2 | 3 | 6 | Authority hierarchy, conflict resolution protocol |

### Platform Risks
| ID | Risk | L | I | Score | Mitigation |
|----|------|---|---|-------|------------|
| P-01 | Supabase outage blocks development | 3 | 4 | 12 | Degrade-mode runbook, warm replica strategy, replay/reconcile drill cadence |
| P-02 | MCP server disconnection during session | 3 | 2 | 6 | Verify MCP before sessions, manual fallback procedures |
| P-03 | GitHub Actions CI becomes slow (>15 min) | 3 | 2 | 6 | DX Agent monitors, optimize workflows quarterly |
| P-04 | Codex access revoked or API changes | 2 | 4 | 8 | AGENTS.md works with any LLM, document migration path |
| P-05 | Vercel deployment failure | 2 | 4 | 8 | Preview deployments catch issues, rollback capability |

### Compliance Risks
| ID | Risk | L | I | Score | Mitigation |
|----|------|---|---|-------|------------|
| C-01 | Agent generates code violating compliance policy | 3 | 5 | 15 | Compliance manifests, inline enforcement, CI gate, RRA block |
| C-02 | Enforcement manifest out of sync with policies | 2 | 4 | 8 | Doc gardening catches drift, manifest generation in Phase 1 |
| C-03 | Client policy conflicts with baseline | 2 | 3 | 6 | Merge rules: client adds/strengthens only, never weakens |
| C-04 | Compliance exception granted without documentation | 2 | 5 | 10 | HAA-only exceptions, documented in exception register |
| C-05 | PHI/PII exposure through logging or errors | 3 | 5 | 15 | Compliance manifests, structured logging enforcement, CI scanning |

### Process Risks
| ID | Risk | L | I | Score | Mitigation |
|----|------|---|---|-------|------------|
| R-01 | Documentation drifts from implementation | 3 | 3 | 9 | Doc Manager gardening, weekly sync, CI structural checks |
| R-02 | Knowledge base incomplete, agents underperform | 3 | 4 | 12 | Phase 1 mandatory, Architecture Guardian reviews |
| R-03 | Human becomes bottleneck on approvals | 3 | 3 | 9 | Minimize HAA triggers, expand agent autonomy where safe |
| R-04 | Technical debt accumulates faster than reduction | 3 | 3 | 9 | Weekly entropy management, ARA recurring tasks |
| R-05 | Duplicate webhook/event deliveries trigger repeated side effects | 4 | 4 | 16 | Idempotency keys, dedupe store TTL, reconciliation worker |
| R-06 | Retry loops amplify incidents and cost | 3 | 5 | 15 | Error taxonomy, transient-only retry policy, jittered backoff caps |
| R-07 | Automation writeback loops trigger alert/task storms | 3 | 4 | 12 | Origin tagging, anti-loop counters, circuit breaker controls |

### Reliability SLO Risks
| ID | Risk | L | I | Score | Mitigation |
|----|------|---|---|-------|------------|
| S-01 | Dedupe precision too low suppresses valid work | 2 | 4 | 8 | Precision SLO, canary rollout, false-positive audits |
| S-02 | Dedupe recall too low allows duplicate side effects | 3 | 5 | 15 | Replay tests, duplicate simulation suite, reconciliation checks |
| S-03 | Release-delta drift causes silent quality regression | 3 | 4 | 12 | Release-delta eval gate before production promotion |

## Review Cadence
- Monthly: review risk scores, update mitigations
- Quarterly: full risk reassessment
