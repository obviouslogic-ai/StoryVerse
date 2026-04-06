---
document_title: "Agent Communication Protocol"
document_type: "Standard"
document_category: "Reference"
applies_to: "All agents, all projects"
process_owner: "Daniel DeZago"
status: "Active"
effective_date: "2026-03-01"
last_reviewed: "2026-03-01"
next_review_due: "2027-03-01"
---

# Agent Communication Protocol

> Standard specification for inter-agent communication in the HELIos pipeline. Defines message envelopes, orchestration patterns, conflict resolution, retry semantics, and data classification tagging. All agent-to-agent interactions must conform to this protocol.

---

## Purpose

As the HELIos agent population grows (20 agents across 5 tiers), interactions between agents require a formal communication contract. Without it, agents risk duplicate side effects, lost handoffs, untracked escalations, and data classification leakage.

This protocol defines:
1. **What** every inter-agent message must contain (envelope specification)
2. **How** multi-agent workflows are orchestrated (saga model)
3. **Who wins** when agents disagree (conflict resolution)
4. **What happens** when messages fail (retry and idempotency)
5. **How sensitive data is tagged** in transit (classification tagging)

---

## Scope

All agent-to-agent interactions in the HELIos pipeline, including:
- Direct handoffs (e.g., REA → PPMA, CEA → ATADA)
- Escalations (any agent → PPMA/HAA/ORFA)
- Evidence submissions (any agent → ARA, PGA)
- Metric emissions (any agent → QMSA)
- Requirement traces (REA ↔ CEA/ATADA)
- SLO checks (SOA ↔ ORFA/RRA)
- Data classification enforcement (PDA → all agents)

This protocol does NOT define:
- Human-to-agent communication (that is governed by HAA override procedures)
- Platform API contracts (those are defined in the Integration Matrix)
- UI-facing messaging (that is a product concern)

---

## 1. Message Envelope Specification

Every inter-agent communication must include a message envelope with the following fields:

| Field | Type | Required | Description |
|-------|------|----------|-------------|
| `correlation_id` | UUID | Yes | Unique identifier linking all messages in a single workflow instance. Generated at workflow initiation, propagated through all downstream messages. |
| `idempotency_key` | UUID | Yes | Unique identifier for this specific message. Prevents duplicate processing if the message is retried. |
| `message_id` | UUID | Yes | Unique identifier for this message instance (distinct from idempotency_key — a retry produces a new message_id with the same idempotency_key). |
| `sender` | String | Yes | Agent abbreviation of the sending agent (e.g., `CEA`, `PPMA`). |
| `sender_tier` | Integer | Yes | Authority tier of the sending agent (0-3 or `Support`). |
| `recipient` | String | Yes | Agent abbreviation of the intended recipient. |
| `intent` | Enum | Yes | The purpose of the message. Valid values: `HANDOFF`, `ESCALATION`, `EVIDENCE`, `METRIC`, `QUERY`, `RESPONSE`, `NOTIFICATION`, `OVERRIDE`. |
| `trigger` | String | Yes | What caused this message to be sent (e.g., `ticket_validated`, `gate_check_failed`, `slo_breach_detected`). |
| `payload` | Object | Yes | The structured data being transferred. Schema varies by intent. |
| `data_classification` | Enum | Yes | Sensitivity level of the payload. Valid values: `PUBLIC`, `INTERNAL`, `CONFIDENTIAL`, `RESTRICTED`. See Section 6. |
| `timestamp` | ISO 8601 | Yes | When the message was created. |
| `workflow_phase` | String | No | The lifecycle phase this message relates to (e.g., `Phase 0`, `Phase 3`). |
| `ttl_seconds` | Integer | No | Time-to-live for the message. After TTL, unprocessed messages are dead-lettered. Default: 3600 (1 hour). |

### Envelope Example

```json
{
  "correlation_id": "a1b2c3d4-e5f6-7890-abcd-ef1234567890",
  "idempotency_key": "f9e8d7c6-b5a4-3210-fedc-ba0987654321",
  "message_id": "11223344-5566-7788-99aa-bbccddeeff00",
  "sender": "REA",
  "sender_tier": 2,
  "recipient": "PPMA",
  "intent": "HANDOFF",
  "trigger": "requirement_normalized",
  "payload": {
    "requirement_id": "REQ-2026-00142",
    "normalization_status": "VALIDATED",
    "normalization_duration_ms": 1200,
    "metadata_snapshot": { }
  },
  "data_classification": "INTERNAL",
  "timestamp": "2026-02-25T14:30:00Z",
  "workflow_phase": "Phase 1",
  "ttl_seconds": 3600
}
```

---

## 2. Orchestration Pattern — Orchestrated Saga Model

HELIos uses an **orchestrated saga model** for multi-agent workflows. This means:

1. **Workflows are sequences of agent actions**, not parallel free-for-alls
2. **HAA + the governance runtime** define the valid sequences
3. **Each agent emits state transitions and evidence** as it completes its step
4. **Compensation actions** are defined for rollback when a step fails

### Workflow Sequencing Rules

| Rule | Description |
|------|-------------|
| **Sequential handoff** | Agent A completes its step and sends a HANDOFF to Agent B. Agent B does not begin until it receives the HANDOFF. |
| **Gate enforcement** | Gate transitions require evidence objects from specific agents before the transition is allowed. The governance runtime validates evidence completeness. |
| **Parallel allowed** | Agents may operate in parallel ONLY when their actions have no data dependencies. The governance runtime must explicitly authorize parallel execution. |
| **Compensation on failure** | If Agent B fails after Agent A succeeded, Agent B must emit a failure event. The governance runtime determines whether to retry, compensate, or escalate. |

### Standard Workflow Pattern

```
Initiator → Agent A (step 1) → emit state + evidence
                                    ↓
                              Agent B (step 2) → emit state + evidence
                                    ↓
                              Gate check (evidence validation)
                                    ↓
                              Agent C (step 3) → emit state + evidence
                                    ↓
                              Workflow complete → archive correlation
```

### Example: Requirement-to-Implementation Workflow

```
Requirement submitted → REA (normalize) → HANDOFF → PPMA (scope assessment)
                                                          ↓
                                                    [In scope]    → CEA (implement)
                                                    [Out of scope] → Deferred
                                                          ↓
                                                    ATADA (test validation) → Gate check
```

All messages in this workflow share the same `correlation_id`, enabling end-to-end tracing.

---

## 3. Conflict Resolution Policy

When agents disagree or produce contradictory outputs, the following resolution rules apply:

### Tier-Based Resolution

| Scenario | Resolution Rule |
|----------|----------------|
| Higher-tier agent contradicts lower-tier agent | Higher-tier output prevails. Lower-tier agent's output is logged but overridden. |
| Equal-tier agents disagree | Escalate to HAA (Tier 0) for authoritative resolution. Both outputs are preserved for HAA review. |
| Support-tier agent contradicts any other tier | Support agent's output is advisory. The other agent's output prevails unless the support agent's domain is directly involved (e.g., UIBGA on UI matters). |
| HAA issues an override | HAA's decision is final. All agents must comply. The override is logged with HAA's justification. |

### Conflict Logging Requirements

Every conflict resolution must produce a conflict record containing:
- `correlation_id` of the workflow
- Agents involved
- Nature of the disagreement
- Resolution applied (which output prevailed)
- Authority basis for the resolution (tier rule, HAA override, domain precedence)
- Timestamp

Conflict records are governance artifacts and must be retained for audit purposes.

---

## 4. Retry Semantics and Idempotency

### Idempotency Contract

Every agent must guarantee idempotent processing of messages:
- **Same `idempotency_key`** → Same result, no duplicate side effects
- Agents must check the `idempotency_key` before processing. If a message with the same key was already processed, return the cached result without re-executing the action.
- Idempotency keys must be retained for at least the TTL of the message (default: 1 hour) plus a buffer period (recommended: 24 hours).

### Retry Strategy

When message delivery or processing fails:

| Attempt | Delay | Action |
|---------|-------|--------|
| 1 (initial) | Immediate | Process the message |
| 2 (retry 1) | 30 seconds | Retry with same idempotency_key |
| 3 (retry 2) | 60 seconds | Retry with same idempotency_key |
| 4 (retry 3) | 120 seconds | Retry with same idempotency_key |
| 5 (retry 4) | 240 seconds | Final retry with same idempotency_key |
| Dead-letter | N/A | Move to dead-letter queue, alert ORFA |

### Compensation Actions

When an agent's step fails and cannot be retried:
1. The failing agent emits a `FAILURE` event with the `correlation_id`
2. The governance runtime evaluates whether upstream actions need compensation
3. If compensation is required, the runtime sends `COMPENSATE` messages to upstream agents
4. Compensation actions must also be idempotent

---

## 5. Intent Definitions

| Intent | Description | Expected Recipient Action |
|--------|-------------|--------------------------|
| `HANDOFF` | Sender has completed its step and is passing work to the recipient | Recipient begins its step |
| `ESCALATION` | Sender cannot handle the situation and needs a higher authority | Recipient evaluates and either resolves or escalates further |
| `EVIDENCE` | Sender is submitting evidence artifacts for a gate check | Recipient validates evidence and records it |
| `METRIC` | Sender is emitting an operational metric | Recipient records the metric (QMSA/KPI framework) |
| `QUERY` | Sender is requesting information from the recipient | Recipient responds with a RESPONSE message |
| `RESPONSE` | Sender is answering a previous QUERY | Recipient processes the answer |
| `NOTIFICATION` | Sender is informing the recipient of an event (no action required) | Recipient logs the notification |
| `OVERRIDE` | Sender (must be HAA or higher-tier) is overriding a previous decision | Recipient complies and logs the override |

---

## 6. Data Classification Tagging

Every message must declare the sensitivity level of its payload. Agents must handle payloads according to their classification level.

| Classification | Definition | Handling Rules |
|---------------|------------|----------------|
| `PUBLIC` | Information that can be freely shared externally | No restrictions on logging or transmission |
| `INTERNAL` | Standard operational data, not for external distribution | May be logged in full. Do not expose to external APIs without PDA review. |
| `CONFIDENTIAL` | Customer data, PHI-adjacent data, compliance evidence | Must be encrypted in transit. Logged with redaction. Access restricted to authorized agents. |
| `RESTRICTED` | Credentials, API keys, security configurations, breach data | Must not be included in message payloads. Use secure reference pointers instead. |

### Classification Enforcement

- PDA (Privacy & Data Protection Agent) governs classification standards
- All agents must tag outgoing messages with the appropriate classification
- Agents receiving `CONFIDENTIAL` or `RESTRICTED` messages must not forward them without PDA-compliant handling
- Misclassification (tagging sensitive data as `INTERNAL` or `PUBLIC`) is a compliance violation flagged by PGA audit

---

## 7. Observability Requirements

All message exchanges must be observable:

| Requirement | Implementation |
|-------------|---------------|
| **Trace ID propagation** | `correlation_id` propagates through all messages in a workflow |
| **Span creation** | Each agent creates a span for its processing step |
| **Metric emission** | Processing time, success/failure, retry count emitted per message |
| **Log correlation** | All log entries include `correlation_id` and `message_id` |
| **Dead-letter monitoring** | ORFA monitors dead-letter queue depth and age |

---

## Related Documents

- Constitution: `../agents/00-constitution.md`
- Agent Registry: `../agents/00-agent-registry.md`
- Integration Matrix: `integration-matrix.md`
- Escalation Protocols: `escalation-protocols.md`
- PDA Agent Definition: `../agents/tier-2-privacy-data-protection.md`
- SOA Agent Definition: `../agents/support-slo-observability.md`
