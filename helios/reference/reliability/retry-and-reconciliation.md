# HELIos Retry and Reconciliation Standard

## Retry Strategy

Retries are for transient conditions only. Permanent failures are routed to remediation, not repeated blindly.

## Backoff Algorithm

Use exponential backoff with full jitter:

- `delay = random(0, min(cap, base * 2^attempt))`
- base = 500ms
- cap = 30s
- max attempts = 6

## Retry Eligibility Matrix

| Signal | Eligible | Notes |
|-------|----------|------|
| 429 | Yes | Respect `Retry-After` when provided |
| 5xx | Yes | Include network timeout/reset classes |
| 4xx validation | No | Requires payload or business correction |
| 401/403 | No | Requires credential/permission correction |
| 409 duplicate | Conditional | Resolve via reconciliation path first |
| Lock contention | Yes | Bounded retry until lease timeout |

## Reconciliation Worker Requirements

1. Scan for orphan attempts where external action may have completed but linkage is missing.
2. Query external system for authoritative state using idempotency key or reference hints.
3. Backfill local linkage and mark item state as recovered.
4. Emit reconciliation outcome metrics and alerts for unresolved cases.

## Minimum SLO-Linked Metrics

- `retry_attempts_total` by class and domain
- `retry_exhausted_total`
- `reconcile_candidates_total`
- `reconcile_success_total`
- `reconcile_age_seconds_max`

## Safety Rules

- Never execute a second irreversible action while an earlier attempt is `reconcile_required`.
- Reconciliation workers are idempotent and reentrant.
- Reconciliation output is auditable and trace-linked to original attempt.
