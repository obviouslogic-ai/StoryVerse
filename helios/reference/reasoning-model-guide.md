# HELIos Reasoning Model Guide

> Governance standard formalizing reasoning patterns per *Agentic Design Patterns* (Gulli, 2025).

---

## Overview

HELIos agents select from five reasoning patterns based on task requirements. Each pattern defines a structured approach to problem-solving with explicit loop bounds, escalation triggers, and agent assignments.

---

## 1. ReAct (Reason + Act)

### Pattern

```
Loop:
  1. Thought   -- Agent reasons about current state and next action
  2. Action    -- Agent invokes a tool or external system
  3. Observation -- Agent processes tool output
  Repeat until goal met or max iterations reached.
```

### When to Use

- Agent must interact with external tools (file system, APIs, databases, test runners).
- Task requires iterative exploration where each step depends on the previous result.
- Output cannot be determined without real-world feedback.

### Assigned Agents

| Agent | Typical ReAct Use |
|---|---|
| **CEA** (Coding Execution Agent) | Write code, run tests, observe results, iterate |
| **ABE** (AI Bug Evaluation Agent) | Reproduce bug, apply fix, verify fix, iterate |
| **ORFA** (Observability & Runtime Feedback Agent) | Check metrics, identify anomaly, drill down, report |
| **DSCA** (Dependency & Supply Chain Agent) | Scan dependencies, evaluate CVEs, apply patches |
| **PIA** (Platform Intelligence Agent) | Configure integration, test connection, verify |

### Defaults

| Parameter | Value |
|---|---|
| Max iterations | 5 |
| Escalation trigger | 3 consecutive failed tool calls |
| Escalation target | HAA (Human Approval Authority) |

### Example Trace

```
[CEA] Thought: Unit test for parseConfig is failing. I need to read the test file.
[CEA] Action: read_file("src/utils/parseConfig.test.ts")
[CEA] Observation: Test expects { timeout: 30 } but function returns { timeout: "30" }.
[CEA] Thought: The function is not parsing the string to a number. I'll fix the parser.
[CEA] Action: edit_file("src/utils/parseConfig.ts", ...)
[CEA] Observation: File updated.
[CEA] Action: run_tests("src/utils/parseConfig.test.ts")
[CEA] Observation: All tests pass. Goal met.
```

---

## 2. Chain-of-Thought (CoT)

### Pattern

```
1. Break problem into discrete reasoning steps
2. Reason through each step explicitly
3. Synthesize conclusion
4. Self-check: review reasoning for logical errors
```

### When to Use

- Complex evaluation that requires structured reasoning before rendering a verdict.
- No tool interaction needed -- the agent already has sufficient context.
- Decision requires weighing multiple factors with clear trade-offs.

### Assigned Agents

| Agent | Typical CoT Use |
|---|---|
| **AGA** (Architecture Guardian Agent) | Evaluate gate criteria against collected evidence |
| **STMA** (Security & Threat Modeling Agent) | Assess threat model completeness |
| **REA** (Requirements Engineering Agent) | Evaluate fault tolerance and recovery strategies |
| **RRA** (Regulatory & Risk Agent) | Assess compliance posture |
| **ATADA** (Automated Test Adequacy & Design Agent) | Evaluate test coverage sufficiency |
| **DMA** (Documentation Agent) | Assess documentation completeness and accuracy |
| **DXA** (Developer Experience Agent) | Evaluate developer workflow friction |
| **PGA** (Process Governance Agent) | Evaluate SOP adherence |
| **PDA** (Privacy & Data Protection Agent) | Assess performance benchmarks |
| **UIBGA** (UI/Brand Governance Agent) | Evaluate design system compliance |

### Defaults

| Parameter | Value |
|---|---|
| Passes | 1 reasoning pass + 1 self-check |
| Escalation trigger | Self-check contradicts initial conclusion |
| Escalation target | Chain of Debates (CoD) |

---

## 3. Tree-of-Thought (ToT)

### Pattern

```
1. Generate N candidate solutions
2. Evaluate each candidate against defined criteria
3. Score and rank candidates
4. Select the best viable candidate
5. If fewer than threshold viable, escalate
```

### When to Use

- High-stakes decisions where multiple valid approaches exist.
- The cost of choosing the wrong approach is significant (security, architecture, major refactors).
- Agent needs to explore the solution space before committing.

### Assigned Agents

| Agent | Typical ToT Use |
|---|---|
| **STMA** (Security & Threat Modeling Agent) | Evaluate multiple threat mitigation strategies |
| **ABE** (AI Bug Evaluation Agent) | Compare multiple bug fix approaches for side-effect risk |
| **ARA** (Automated Refactoring Agent) | Evaluate refactoring strategies for complexity vs. risk |

### Defaults

| Parameter | Value |
|---|---|
| Candidates (N) | 3 |
| Minimum viable candidates | 2 |
| Escalation trigger | Fewer than 2 viable candidates |
| Escalation target | Chain of Debates (CoD) |

### Evaluation Criteria Template

```yaml
candidate_evaluation:
  - criterion: correctness
    weight: 0.4
  - criterion: risk_of_side_effects
    weight: 0.3
  - criterion: implementation_complexity
    weight: 0.2
  - criterion: maintainability
    weight: 0.1
```

---

## 4. Chain of Debates (CoD)

### Pattern

```
Round 1:
  Agent A argues position → structured response
  Agent B argues counter-position → structured response
  (Optional: Agent C, Agent D)
Round 2:
  Agents respond to each other's arguments
  Attempt consensus
If no consensus after max rounds:
  HAA (Human Approval Authority) is tiebreaker
```

### When to Use

- Contested architectural or security decisions.
- Triggered when CoT produces conflicting outputs across agents.
- Decisions with significant long-term impact that benefit from adversarial review.

### Trigger Conditions

CoD is invoked when any of the following agents detect conflicting CoT outputs:

| Triggering Agent | Scenario |
|---|---|
| **AGA** | Gate evaluation produces ambiguous pass/fail |
| **STMA** | Threat model yields contradictory risk assessments |
| **REA** | Reliability analysis produces conflicting redundancy recommendations |

### Defaults

| Parameter | Value |
|---|---|
| Min participating agents | 2 |
| Max participating agents | 4 |
| Max debate rounds | 2 |
| Tiebreaker | HAA (Human Approval Authority) |
| No consensus after max rounds | Escalate to HAA |

### Structured Response Format

Each agent in a debate must use this format:

```yaml
debate_response:
  agent: <agent_id>
  round: <round_number>
  position: <summary of position>
  evidence:
    - <supporting fact or data point 1>
    - <supporting fact or data point 2>
  risk_if_rejected: <what happens if this position is not adopted>
  concessions: <points from opposing position the agent accepts>
```

---

## 5. ReAct + CoT (Hybrid)

### Pattern

```
Phase 1 -- ReAct:
  Loop (up to N iterations):
    Thought → Action → Observation
  Collect findings.

Phase 2 -- CoT Synthesis:
  Break findings into reasoning steps.
  Reason through implications.
  Synthesize final conclusion.
  Self-check.
```

### When to Use

- Agent must both gather data from external systems AND reason about complex implications.
- Planning tasks where tool-based verification is required alongside strategic reasoning.
- Metric analysis where raw data must be collected before trend analysis.

### Assigned Agents

| Agent | Typical Hybrid Use |
|---|---|
| **PPMA** (Plan & Project Management Agent) | Gather sprint data via tools, then reason about plan construction and dependencies |
| **QMSA** (Quality Metrics & Scoring Agent) | Collect metrics from Supabase, then reason about quality trends and scoring |

### Defaults

| Parameter | Value |
|---|---|
| ReAct max iterations | 5 |
| CoT passes | 1 synthesis + 1 self-check |
| Escalation trigger | ReAct phase exceeds max iterations without sufficient data |
| Escalation target | HAA |

---

## Loop Depth Defaults

Summary of all reasoning pattern defaults in one table for quick reference.

| Pattern | Max Iterations / Rounds | Candidates | Self-Check | Escalation Trigger | Escalation Target |
|---|---|---|---|---|---|
| **ReAct** | 5 iterations | -- | -- | 3 consecutive failed tool calls | HAA |
| **CoT** | 1 pass | -- | 1 self-check | Self-check contradicts conclusion | CoD |
| **ToT** | -- | 3 | -- | < 2 viable candidates | CoD |
| **CoD** | 2 rounds | -- | -- | No consensus after 2 rounds | HAA |
| **ReAct + CoT** | 5 ReAct + 1 CoT | -- | 1 self-check | ReAct exceeds max without data | HAA |

---

## Pattern Selection Flowchart

```
START
  |
  v
Does the task require tool interaction?
  |
  +-- YES --> Is complex reasoning also needed?
  |             |
  |             +-- YES --> ReAct + CoT (Hybrid)
  |             +-- NO  --> ReAct
  |
  +-- NO  --> Are there multiple valid approaches?
                |
                +-- YES --> Is the decision high-stakes?
                |             |
                |             +-- YES --> Tree-of-Thought
                |             +-- NO  --> Chain-of-Thought
                |
                +-- NO  --> Chain-of-Thought
                              |
                              v
                        Did CoT produce conflicting outputs?
                              |
                              +-- YES --> Chain of Debates
                              +-- NO  --> Done
```

---

## References

- Gulli, A. (2025). *Agentic Design Patterns*. Reasoning patterns (Ch. 3).
- Yao, S. et al. (2023). "ReAct: Synergizing Reasoning and Acting in Language Models."
- Wei, J. et al. (2022). "Chain-of-Thought Prompting Elicits Reasoning in Large Language Models."
- Yao, S. et al. (2023). "Tree of Thoughts: Deliberate Problem Solving with Large Language Models."
- HELIos Escalation Protocols: `HELIos/reference/escalation-protocols.md`
