# Supabase Failover and Degrade-Mode Playbook

## Purpose

Provide deterministic response when Supabase primary region or dependent services degrade.

## Failure Modes Covered

- primary region database unavailable
- auth endpoint instability
- storage or edge function regional degradation
- elevated latency causing SLO breach

## Control Modes

1. **Normal mode**: read/write against primary.
2. **Degraded read-only mode**: writes paused or queued, reads continue where safe.
3. **Failover mode**: traffic switched to warm read replica and supported read paths.
4. **Recovery mode**: replay queued writes, reconcile records, restore primary.

## Required Preconditions

- Warm replica configured in secondary region.
- Health checks for `db`, `auth`, `storage`, and `functions`.
- Write-ahead event log for replay after incident.
- Reconciliation worker available and tested.

## Detection and Trigger Thresholds

- Trigger degrade mode when one of:
  - primary health check fails for 2 consecutive intervals
  - p95 latency exceeds threshold for 10 minutes
  - error-rate breaches error budget burn policy
- Trigger failover after degrade mode if primary remains unhealthy beyond configured timeout.

## Runbook Steps

### A. Enter Degraded Mode

1. Set feature flag `HELIOS_DEGRADE_READ_ONLY=true`.
2. Route write endpoints to queue-only or fail-fast with user-safe messaging.
3. Announce incident status and expected mode behavior.

### B. Evaluate Failover

1. Validate replica health and read consistency checks.
2. Confirm auth/session behavior for supported paths.
3. Execute traffic steering command using environment-driven switch.

### C. Recovery and Replay

1. Restore primary availability and validate consistency lag is acceptable.
2. Replay durable event log in bounded batches.
3. Run reconciliation to repair orphaned or partial linkages.
4. Compare pre-incident and post-replay counts; investigate drift.

### D. Return to Normal

1. Disable degrade flag.
2. Move writes back to primary.
3. Capture incident evidence and postmortem actions.

## Drill Cadence and Evidence

- Monthly: degrade-mode drill.
- Quarterly: full failover + replay + reconciliation drill.
- Evidence required:
  - timestamps for mode transitions
  - replay totals and reconciliation results
  - unresolved exception count and owner
