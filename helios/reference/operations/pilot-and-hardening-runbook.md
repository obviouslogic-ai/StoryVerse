# Pilot and Hardening Runbook

## Goal

Validate HELIos reliability, resilience, and automation capabilities in a pilot repo before broad rollout.

## Pilot Scope

- one representative repository
- at least one side-effecting workflow
- at least one webhook or queue consumer
- one escalation automation path

## Entry Criteria

- reliability and resilience gates installed
- idempotency/retry/reconciliation primitives implemented
- failover and release-delta runbooks present
- telemetry KPI strip configured

## Pilot Steps

1. **Baseline capture**
   - collect current duplicate rate, failure rate, and operator intervention hours
2. **Controlled enablement**
   - enable reliability controls first
   - then enable resilience controls
   - then enable automation recipes
3. **Observation window**
   - run for minimum 2 weeks
   - review alerts and incidents daily
4. **Gate review**
   - confirm reliability and resilience gates detect seeded violations
5. **Exit review**
   - compare baseline vs pilot outcomes
   - list unresolved risks and mitigation owners

## Chaos and Drill Suite

Run and record outcomes for:

1. duplicate webhook burst test
2. transient upstream outage simulation
3. permanent 4xx error injection
4. lock contention on serialized resource
5. degraded-mode and failover drill with replay
6. release-delta regression simulation

## Hardening Checklist

- dedupe precision and recall meet SLO
- no blind 4xx retries observed
- reconciliation backlog max age within threshold
- failover and rollback drills completed with evidence
- alert actionability >= 95%
- docs and runbooks updated from pilot learnings

## Rollout Decision

- **GO**: all hardening checks pass and residual risks accepted
- **HOLD**: partial pass with bounded remediation plan
- **BLOCK**: major invariants not met

## First Target Rule

Before broad rollout, the first target repository must complete:

- `setup/deploy-helios-first-target-rollout.md`
- evidence bundle under `docs/helios/deploy-sessions/<session_id>/first-target-evidence/`
- final hardening verdict of `GO`
