# HELIos Resource Locking Standard

## Use Cases

Apply to resources requiring serialized writes:
- physical printers
- shared ledger writers
- single-commit external APIs with ordering constraints

## Lease Model

- Acquire lease per resource key before write.
- Lease has bounded TTL and owner token.
- Renew only by current owner token.
- Release lease after completion or failure finalization.

## Behavioral Guarantees

1. Parallelism allowed across different resource keys.
2. No parallel writes within the same resource key.
3. FIFO queueing per resource key where order matters.
4. Stale lease recovery via TTL expiry and fencing token checks.

## Suggested Schema

- `resource_key`
- `lease_owner`
- `lease_token`
- `lease_expires_at`
- `last_heartbeat_at`

## Failure Handling

- If lease acquisition fails, classify as `local.resource_lock` and retry with short jittered delay.
- If lease owner crashes, next worker acquires after TTL and validates no duplicate side effect is produced.
- If ordering is violated, mark queue as degraded and require operator acknowledgement.
