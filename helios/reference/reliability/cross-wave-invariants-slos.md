# HELIos Cross-Wave Reliability Invariants and SLOs

## Purpose

This document defines reliability and resilience invariants that apply across Wave 1 (runtime reliability), Wave 2 (resilience operations), and Wave 3 (automation governance and telemetry).

If a project cannot satisfy these invariants, release readiness is **HOLD** or **BLOCK**.

## Non-Negotiable Invariants

1. **Idempotent side effects:** externally visible writes must be safe under at-least-once delivery.
2. **Deterministic failure handling:** retries are allowed only for transient classes; permanent classes are surfaced for correction.
3. **State before side effect:** attempt metadata is persisted before irreversible external calls.
4. **Single-writer semantics for serialized resources:** resources that cannot tolerate concurrent writes use explicit lock/lease controls.
5. **Reconciliation is mandatory:** asynchronous workflows must include background repair for missed/partial linkage.
6. **Degraded mode is explicit:** outage behavior is predefined (read-only, queue-only, or fail-closed).
7. **Release drift is gated:** platform/model/provider behavior changes trigger regression evaluation before promotion.
8. **Observability before autonomy:** automation paths must emit auditable traces and outcome metrics.

## Canonical SLO Set

| SLO ID | Metric | Target | Window | Notes |
|-------|--------|--------|--------|-------|
| REL-001 | Event processing success rate (post-retry) | >= 99.9% | 30 days | Excludes events parked for valid 4xx corrections |
| REL-002 | Duplicate side-effect rate | <= 0.05% | 30 days | Measured after dedupe + reconciliation |
| REL-003 | Dedupe precision | >= 99.5% | 30 days | Prevent false positives dropping legitimate events |
| REL-004 | Dedupe recall | >= 99.0% | 30 days | Prevent duplicate execution leaks |
| REL-005 | Mean time to reconcile orphan states | <= 15 min | rolling 7 days | Includes replay/orphan repair jobs |
| REL-006 | Failover decision to traffic-steered state | <= 10 min | per drill/incident | Includes degrade mode activation |
| REL-007 | Release-delta regression detection latency | <= 24 hours | per platform delta | From delta detection to eval verdict |
| REL-008 | Alert actionability rate | >= 95% | 30 days | Alert produced concrete action, not noise |

## Error Budget Policy

- For any SLO miss, open a reliability incident and block non-critical feature work until a remediation plan exists.
- Repeated miss in two consecutive windows escalates to HAA review with corrective controls.
- Manual override is allowed only with documented exception and expiration date.

## Required Evidence at Release Gate

1. Last 30-day SLO report with pass/fail status.
2. Retry policy map showing transient vs permanent classes.
3. Reconciliation backlog trend and max age.
4. Most recent failover or degrade-mode drill record.
5. Release-delta evaluation result for active model/provider versions.

## Implementation Hooks

- CI/workflow templates enforce required checks where automatable.
- Runtime services persist operation IDs and attempt lineage.
- Dashboards expose SLOs and error budget burn by domain.
- Release Readiness Agent consumes this file as authoritative reliability criteria.
