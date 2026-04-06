# HELIos Agent Evaluation Framework

> Governance standard formalizing agent evaluation per *Agentic Design Patterns* (Gulli, 2025).

---

## Overview

Every HELIos agent action is evaluated across three dimensions: **Outcome**, **Process**, and **Trajectory** (OPT). These dimensions provide a complete picture of agent effectiveness -- not just whether the agent succeeded, but whether it succeeded efficiently and reliably.

---

## 1. Three Evaluation Dimensions

### 1.1 Outcome (O) -- "Did the agent achieve its goal?"

| Rating | Definition |
|---|---|
| **Pass** | Agent fully satisfied all acceptance criteria for the assigned task. |
| **Partial** | Agent satisfied some but not all criteria, or achieved the goal with caveats. |
| **Fail** | Agent did not satisfy the primary acceptance criteria. |

**Measured by:** Gate results (AGA), task completion status, test pass rates, deliverable checklist.

**Score range:** 0--10

| Score | Meaning |
|---|---|
| 10 | All criteria met, no rework needed |
| 7--9 | All criteria met, minor polish needed |
| 4--6 | Partial completion, some criteria unmet |
| 1--3 | Significant criteria failures |
| 0 | Complete failure or no output produced |

### 1.2 Process (P) -- "Was the reasoning logical and efficient?"

Evaluates whether the agent's reasoning path was sound, efficient, and well-informed.

**Measured by:** ORFA trajectory logs + QMSA aggregation.

**Score range:** 0--10

| Score | Meaning |
|---|---|
| 10 | Optimal reasoning path, no wasted steps |
| 7--9 | Sound reasoning, minor inefficiencies |
| 4--6 | Reasoning reached correct outcome but with notable waste |
| 1--3 | Flawed reasoning that happened to produce partial results |
| 0 | Incoherent or circular reasoning |

### 1.3 Trajectory (T) -- "Was the execution log consistent and recoverable?"

Evaluates whether the agent's execution trace was well-structured, bounded, and could be replayed or audited.

**Captured by:** ORFA (Observability & Reliability Feedback Agent).

**Score range:** 0--10

| Score | Meaning |
|---|---|
| 10 | Clean execution trace, all actions logged, fully recoverable |
| 7--9 | Minor logging gaps, execution was bounded and orderly |
| 4--6 | Some unlogged actions or recovery would require manual intervention |
| 1--3 | Significant logging gaps, execution was erratic |
| 0 | Execution trace is unrecoverable or agent entered undefined state |

---

## 2. Red Flags

Red flags are specific anti-patterns that indicate agent malfunction or misconfiguration. Each dimension has its own set of red flags that trigger investigation.

### 2.1 Outcome Red Flags

| Red Flag | Description | Severity |
|---|---|---|
| **Gate failure** | Agent output fails AGA gate evaluation | Critical |
| **Incomplete criteria** | Agent marks task complete but acceptance criteria remain unmet | Major |
| **Silent failure** | Agent reports success but downstream agents detect errors | Critical |
| **Regression** | Agent's output breaks previously passing tests or functionality | Critical |

### 2.2 Process Red Flags

| Red Flag | Description | Severity |
|---|---|---|
| **Unnecessary tool calls (>2)** | Agent invokes tools that do not contribute to the outcome | Major |
| **Contradictory reasoning** | Agent's reasoning steps contradict each other within the same execution | Critical |
| **Ignoring memory data** | Agent has relevant data in Working State or Long-Term Memory but fails to query it | Major |
| **Reasoning loop** | Agent repeats the same reasoning step without new information | Major |
| **Premature conclusion** | Agent skips reasoning steps and jumps to a conclusion without sufficient evidence | Major |

### 2.3 Trajectory Red Flags

| Red Flag | Description | Severity |
|---|---|---|
| **Infinite loop** | Agent exceeds max iteration count for its reasoning pattern | Critical |
| **Scope creep** | Agent performs actions outside its declared `memory_contract` or task scope | Critical |
| **Skipping stop conditions** | Agent ignores defined termination criteria and continues executing | Critical |
| **Self-authorization** | Agent grants itself permissions or approvals that require HAA or another agent | Critical |
| **Unlogged actions** | Agent performs tool calls or state changes without audit trail entries | Major |

---

## 3. Evaluation Ownership

Evaluation is a distributed responsibility across multiple HELIos agents, with clear ownership at each stage.

```
ORFA ──collects──> Trajectory Logs
  |
  v
QMSA ──aggregates──> Outcome + Process Scores
  |
  v
PGA ──flags──> SOP Violations
  |
  v
Phase 6 Retrospective ──feeds──> SOP Deltas
```

### Ownership Matrix

| Responsibility | Owner | Description |
|---|---|---|
| **Trajectory log collection** | ORFA | Records every agent action, tool call, reasoning step, and state transition. Logs are immutable and written to `helios_audit_trail`. |
| **Outcome + Process scoring** | QMSA | Aggregates gate results, task completion data, and ORFA trajectory analysis into O and P scores. Writes to `helios_quality_scores`. |
| **SOP violation detection** | PGA | Reviews agent behavior against declared SOPs. Flags deviations as `helios_violations` with `category: sop_violation`. |
| **Retrospective feedback** | Phase 6 (Sprint Close) | Analyzes OPT score trends across the sprint. Produces SOP delta recommendations that are reviewed by HAA before adoption. |

### Data Flow

| Source | Destination | Data |
|---|---|---|
| Agent execution | ORFA | Raw trajectory logs (actions, tool calls, reasoning traces) |
| ORFA | `helios_audit_trail` | Structured, immutable audit entries |
| ORFA | QMSA | Trajectory analysis summary |
| AGA | QMSA | Gate pass/fail results per agent per phase |
| QMSA | `helios_quality_scores` | OPT scores per agent per sprint |
| PGA | `helios_violations` | SOP violation records |
| QMSA | Phase 6 Retrospective | Sprint OPT aggregates and trend data |

---

## 4. OPT Scoring

### 4.1 Per-Action Scoring

Every scorable agent action receives three independent scores:

| Dimension | Symbol | Range | Evaluator |
|---|---|---|---|
| Outcome | O | 0--10 | QMSA (from gate results + task completion) |
| Process | P | 0--10 | QMSA (from ORFA trajectory analysis) |
| Trajectory | T | 0--10 | ORFA (from execution log analysis) |

### 4.2 Sprint Aggregate Formula

```
OPT = O x 0.5 + P x 0.3 + T x 0.2
```

| Component | Weight | Rationale |
|---|---|---|
| Outcome (O) | 50% | Results matter most -- did the agent deliver? |
| Process (P) | 30% | Efficient reasoning reduces cost and latency |
| Trajectory (T) | 20% | Clean execution enables auditability and recovery |

### 4.3 Example Calculation

```
Agent: CEA
Sprint: 2026-S12

  Outcome:    8.5 (all gates passed, one minor rework)
  Process:    7.0 (two unnecessary file reads)
  Trajectory: 9.0 (clean logs, all actions bounded)

  OPT = 8.5 x 0.5 + 7.0 x 0.3 + 9.0 x 0.2
      = 4.25 + 2.10 + 1.80
      = 8.15
```

### 4.4 SOP Review Threshold

```
IF agent.opt_aggregate < 7.0 FOR 2 consecutive sprints:
  THEN trigger SOP review for that agent
```

| Threshold | Action |
|---|---|
| OPT >= 8.0 | Agent performing well. No action needed. |
| 7.0 <= OPT < 8.0 | Monitor. QMSA flags for attention in retrospective. |
| OPT < 7.0 (1 sprint) | Warning. PGA reviews agent SOP for potential issues. |
| OPT < 7.0 (2 consecutive sprints) | **SOP review triggered.** PGA + HAA conduct formal review. SOP deltas are drafted, tested, and adopted. |
| OPT < 5.0 (any sprint) | **Immediate intervention.** Agent is suspended from autonomous operation. HAA must approve all actions until OPT recovers above 7.0. |

### 4.5 Scoring Storage

OPT scores are stored in `helios_quality_scores` (Working State) and archived to Long-Term Memory at sprint close:

```sql
-- Record an OPT score
INSERT INTO helios_quality_scores (
  sprint_id, agent_id, phase,
  outcome_score, process_score, trajectory_score,
  opt_aggregate
) VALUES (
  '2026-S12', 'CEA', 'phase-3-build',
  8.5, 7.0, 9.0,
  8.15
);

-- Query agents below threshold for 2 consecutive sprints
SELECT a.agent_id
FROM helios_quality_scores a
JOIN helios_quality_scores b
  ON a.agent_id = b.agent_id
WHERE a.sprint_id = '2026-S12'
  AND b.sprint_id = '2026-S11'
  AND a.opt_aggregate < 7.0
  AND b.opt_aggregate < 7.0;
```

---

## 5. Evaluation Cadence

| When | What | Who |
|---|---|---|
| **Per action** | O, P, T scores recorded | ORFA + QMSA |
| **Per phase gate** | Phase-level OPT aggregate calculated | QMSA |
| **Per sprint close** | Sprint OPT aggregate calculated, trends analyzed | QMSA + Phase 6 Retrospective |
| **Per 2-sprint window** | SOP review threshold check | PGA |
| **On red flag detection** | Immediate investigation triggered | ORFA (detection) + PGA (investigation) |

---

## References

- Gulli, A. (2025). *Agentic Design Patterns*. Agent evaluation patterns (Ch. 6).
- HELIos Quality Metrics: `HELIos/reference/roi-measurement-protocol.md`
- HELIos Memory Architecture: `HELIos/reference/memory-architecture.md`
- HELIos Reasoning Model Guide: `HELIos/reference/reasoning-model-guide.md`
