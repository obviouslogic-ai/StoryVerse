# HELIos Error Taxonomy for Workflow Automation

## Purpose

Define deterministic handling by error class so agents do not guess retry behavior.

## Canonical Classes

| Class | Examples | Retry? | Action |
|------|----------|--------|--------|
| `transient.rate_limit` | HTTP 429, quota burst | Yes | Exponential backoff with jitter |
| `transient.upstream` | HTTP 5xx, timeout, network reset | Yes | Exponential backoff with jitter |
| `permanent.validation` | HTTP 400/422 schema/business errors | No | Park for correction, attach reason |
| `permanent.authz` | HTTP 401/403 permission failure | No | Escalate config/credential remediation |
| `conflict.duplicate` | HTTP 409 duplicate create/purchase | Conditional | Reconcile existing record linkage |
| `local.resource_lock` | Lease not acquired | Yes | Short retry within bounded lock window |
| `unknown` | Unmapped/novel errors | No automatic retry | Escalate and classify before resume |

## Workflow State Model

Use explicit parent and per-item state to support partial success.

### Parent Job States

`queued` -> `running` -> (`completed` | `completed_with_errors` | `failed`)

### Item States

`pending` -> `attempting` -> (`succeeded` | `retry_scheduled` | `blocked_permanent` | `reconcile_required`)

## Purchase/Irreversible Action Rule

Before making irreversible external calls:
1. Persist attempt record.
2. Persist idempotency key and desired action metadata.
3. Execute external call.
4. Persist result and any external reference.

If step 4 fails after step 3 succeeds, reconciliation must recover linkage before another attempt.

## Retry Envelope Defaults

- Base delay: 500ms
- Jitter: full jitter
- Max delay cap: 30s
- Max attempts: 6
- Retryable classes: `transient.*`, `local.resource_lock`

## Operator Surface

Every failure event must include:
- error class
- retry eligibility
- next action
- correlation ID
- idempotency key
