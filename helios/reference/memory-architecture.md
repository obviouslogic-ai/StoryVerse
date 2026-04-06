# HELIos Memory Architecture

> Governance standard formalizing agentic memory tiers per *Agentic Design Patterns* (Gulli, 2025).

---

## Overview

HELIos agents operate across three memory tiers. Each tier has a defined scope, lifetime, storage mechanism, and access contract. No agent may read or write memory outside its declared `memory_contract`.

---

## 1. Short-Term Memory (Session Scope)

| Property | Value |
|---|---|
| **Scope** | Single execution plan run |
| **Storage** | In-context (LLM context window) |
| **Lifetime** | Created at plan start, discarded at plan completion |
| **Max Size** | 80K tokens |

### Contents

- Active execution plan (current SOP, phase, step)
- `plan_graph` (dependency DAG for the current sprint plan)
- Intermediate agent outputs not yet classified for persistence
- Tool call results pending evaluation

### Access Rules

| Role | Agents | Permission |
|---|---|---|
| **Writer** | PPMA | Constructs and updates the active plan and plan_graph |
| **Reader** | CEA, ARA, ABE | Read current plan state to execute assigned tasks |

### Constraints

- Short-term memory is **never persisted** without explicit classification by the writing agent.
- If context approaches the 80K token limit, PPMA must summarize or offload to Working State before continuing.
- ORFA monitors context utilization and flags plans exceeding 60K tokens as `memory_pressure: warning`.

---

## 2. Working State (Sprint Scope)

| Property | Value |
|---|---|
| **Scope** | Current sprint |
| **Storage** | Supabase (PostgreSQL) |
| **Lifetime** | Created at sprint start, archived at sprint close |
| **Tables** | `helios_quality_scores`, `helios_violations` |

### Contents

| Data | Table | Description |
|---|---|---|
| Quality grade | `helios_quality_scores` | Current OPT scores per agent, per phase |
| Open violations | `helios_violations` | Active SOP violations awaiting resolution |
| Active tech debt | `helios_violations` | Items tagged `category: tech_debt` with `status: open` |
| Current ROI actuals | `helios_quality_scores` | Sprint-to-date ROI measurements vs. targets |

### Access Rules

| Role | Agents | Permission |
|---|---|---|
| **Writer** | QMSA | Writes quality scores, updates violation status |
| **Reader** | PPMA | Reads at plan time to inform sprint planning decisions |

### Schema Reference

```sql
-- helios_quality_scores
CREATE TABLE helios_quality_scores (
  id            UUID PRIMARY KEY DEFAULT gen_random_uuid(),
  sprint_id     TEXT NOT NULL,
  agent_id      TEXT NOT NULL,
  phase         TEXT NOT NULL,
  outcome_score NUMERIC(4,2),
  process_score NUMERIC(4,2),
  trajectory_score NUMERIC(4,2),
  opt_aggregate NUMERIC(4,2),
  roi_actual    NUMERIC(10,2),
  recorded_at   TIMESTAMPTZ DEFAULT now()
);

-- helios_violations
CREATE TABLE helios_violations (
  id            UUID PRIMARY KEY DEFAULT gen_random_uuid(),
  sprint_id     TEXT NOT NULL,
  agent_id      TEXT NOT NULL,
  category      TEXT NOT NULL,  -- 'sop_violation' | 'tech_debt' | 'security' | 'quality'
  severity      TEXT NOT NULL,  -- 'critical' | 'major' | 'minor'
  description   TEXT NOT NULL,
  status        TEXT NOT NULL DEFAULT 'open',  -- 'open' | 'resolved' | 'deferred'
  created_at    TIMESTAMPTZ DEFAULT now(),
  resolved_at   TIMESTAMPTZ
);
```

---

## 3. Long-Term Memory (Cross-Sprint, Semantic)

| Property | Value |
|---|---|
| **Scope** | Cross-sprint, organization-wide |
| **Storage** | Supabase with pgvector extension |
| **Lifetime** | Persistent until explicit archival or deletion |
| **Tables** | `helios_knowledge_items`, `helios_roi_events`, `helios_audit_trail` |

### Contents

| Table | Description |
|---|---|
| `helios_knowledge_items` | Lessons learned, pattern records, architectural decisions -- each with a vector embedding for semantic retrieval |
| `helios_roi_events` | Discrete ROI-impacting events (time saved, bugs prevented, rework avoided) |
| `helios_audit_trail` | Immutable log of all agent actions, gate decisions, and escalations |

### Access Rules

| Role | Agents | Tables | Notes |
|---|---|---|---|
| **Writer** | QMSA | `helios_knowledge_items`, `helios_roi_events` | Quality insights and ROI events |
| **Writer** | STMA | `helios_knowledge_items`, `helios_audit_trail` | Threat patterns and security decisions |
| **Writer** | ABE | `helios_knowledge_items` | Bug patterns and resolution strategies |
| **Writer** | AGA | `helios_audit_trail` | Gate pass/fail decisions |
| **Writer** | DMA | `helios_knowledge_items` | Documentation patterns |
| **Reader** | PPMA | All tables | Full read access for planning |
| **Reader** | ABE | `helios_knowledge_items` | Bug pattern lookups |
| **Reader** | STMA | `helios_knowledge_items` | Threat history lookups |
| **Reader** | ARA | `helios_knowledge_items` | Tech debt and refactor patterns |

### Semantic Query via pgvector

```sql
-- Example: find knowledge items similar to a query embedding
SELECT id, title, content, category,
       1 - (embedding <=> $1::vector) AS similarity
FROM helios_knowledge_items
WHERE 1 - (embedding <=> $1::vector) > 0.75
ORDER BY similarity DESC
LIMIT 10;
```

### Schema Reference

```sql
-- Requires: CREATE EXTENSION IF NOT EXISTS vector;

CREATE TABLE helios_knowledge_items (
  id            UUID PRIMARY KEY DEFAULT gen_random_uuid(),
  sprint_id     TEXT,
  agent_id      TEXT NOT NULL,
  category      TEXT NOT NULL,  -- 'bug_pattern' | 'threat_pattern' | 'arch_decision' | 'lesson_learned' | 'doc_pattern'
  title         TEXT NOT NULL,
  content       TEXT NOT NULL,
  embedding     vector(1536),
  created_at    TIMESTAMPTZ DEFAULT now()
);

CREATE TABLE helios_roi_events (
  id            UUID PRIMARY KEY DEFAULT gen_random_uuid(),
  sprint_id     TEXT NOT NULL,
  event_type    TEXT NOT NULL,  -- 'time_saved' | 'bug_prevented' | 'rework_avoided' | 'security_hardened'
  agent_id      TEXT NOT NULL,
  value_usd     NUMERIC(10,2),
  description   TEXT,
  created_at    TIMESTAMPTZ DEFAULT now()
);

CREATE TABLE helios_audit_trail (
  id            UUID PRIMARY KEY DEFAULT gen_random_uuid(),
  sprint_id     TEXT,
  agent_id      TEXT NOT NULL,
  action        TEXT NOT NULL,
  input_hash    TEXT,
  output_hash   TEXT,
  decision      TEXT,            -- 'pass' | 'fail' | 'escalate' | 'defer'
  metadata      JSONB,
  created_at    TIMESTAMPTZ DEFAULT now()
);
```

---

## 4. Memory Access Rules

These rules apply across all three tiers and are enforced by ORFA (Observability & Runtime Feedback Agent).

| Rule | Description | Enforcement |
|---|---|---|
| **No read without contract** | No agent may read any memory tier without a declared `memory_contract` in its agent configuration. | ORFA rejects unauthorized read attempts and logs a violation. |
| **No write without plan authorization** | No agent may write to Working State or Long-Term Memory unless the current execution plan grants write permission. | PPMA validates write authorization at plan construction. |
| **No unclassified persistence** | Short-term memory contents must never be persisted to Working State or Long-Term Memory without explicit classification (`category`, `agent_id`, `sprint_id`). | QMSA validates classification before accepting writes. |
| **Memory pattern monitoring** | ORFA continuously monitors memory access patterns for anomalies (excessive reads, unauthorized write attempts, context bloat). | ORFA flags anomalies as `helios_violations` with `category: memory_access`. |

### Memory Contract Declaration

Each agent's configuration must include a `memory_contract` block:

```yaml
# Example: ABE agent memory contract
agent: ABE
memory_contract:
  short_term:
    read: true
    write: false
  working_state:
    read: false
    write: false
  long_term:
    read:
      - helios_knowledge_items  # bug patterns only
    write:
      - helios_knowledge_items  # bug patterns and resolutions
```

---

## References

- Gulli, A. (2025). *Agentic Design Patterns*. Memory architecture patterns (Ch. 4).
- HELIos Agent Communication Protocol: `HELIos/reference/agent-communication-protocol.md`
- HELIos SOP Execution Data Model: `HELIos/reference/sop-execution-data-model.md`
