# HELIos Escalation and Meeting-to-Task Automation Recipes

## Design Principle

Prefer deterministic extraction first, then optional LLM enrichment with confidence thresholds.

## Recipe A: VIP Email Escalation

### Trigger

- inbound message tagged with `vip` label/category

### Flow

1. Ingest message metadata and thread ID.
2. Compute upsert key: `email:threadId:eventType`.
3. Upsert incident/task record in Notion or ticket store.
4. Post escalation summary to Teams/Slack channel.
5. Suppress duplicates via idempotency key and TTL window.

### Safety Controls

- ignore events with `origin=helios-automation` where applicable
- throttle repeated alerts per thread within cooldown window
- attach source permalink and trace ID for auditability

## Recipe B: Meeting Notes to Action Items

### Trigger

- new meeting transcript/notes page updated

### Flow

1. Run deterministic action extractor (owner, due date, action verb).
2. Validate required fields and confidence threshold.
3. Upsert tasks using key: `meetingId:lineItemHash`.
4. Optional LLM refinement for summary tone and grouping.
5. Publish digest to team channel.

### Quality Controls

- no task creation when owner or due date is missing
- unresolved actions stay in review queue
- maintain correction feedback set for extractor improvement

## Recipe C: SLA Breach Escalation

### Trigger

- metric store indicates SLA breach beyond threshold duration

### Flow

1. Compute breach key from service + SLO + time bucket.
2. Upsert incident and notify escalation channel.
3. Open follow-up task with remediation owner.
4. Auto-close when breach clears for stable window.

### Controls

- one active incident per breach key
- suppress alert storms with escalating cooldowns
- require post-incident note before closure
