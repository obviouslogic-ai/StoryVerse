# Integration Pattern: Orchestrator (Parse-Route-Delegate-Report)

## Purpose

This document defines the orchestrator pattern used for multi-agent coordination in the HELIos pipeline. The orchestrator agent parses requests, routes to specialist agents, delegates with clear instructions, and reports outcomes.

**Primary Agent:** Premiere Project Manager Agent (PPMA)

**Origin:** Genericized from the Cortex Nexus orchestrator model.

---

## 1. Pattern Overview

The orchestrator pattern separates **coordination** from **execution**. The orchestrating agent never performs specialist work -- it identifies the correct agent, provides clear instructions, and tracks completion.

```
Request
   |
   v
[PARSE] -- Analyze the request type, domain, and requirements
   |
   v
[ROUTE] -- Identify the correct specialist agent(s)
   |
   v
[DELEGATE] -- Provide precise, self-contained instructions
   |
   v
[REPORT] -- Track completion and report outcomes
```

---

## 2. The Four Steps

### Step 1: Parse

The orchestrator analyzes incoming requests to determine:

| Question | Why It Matters |
|----------|---------------|
| What type of task is this? | Determines which agent handles it |
| Which domain does it belong to? | Maps to agent authority and compliance scope |
| Is this a one-time or recurring need? | Affects planning and automation decisions |
| Does an existing agent handle this? | Routes to specialist or flags a capability gap |
| What autonomy level applies? | Determines approval requirements |
| What is the business value? | Included in execution plan |

### Step 2: Route

Based on the parse, the orchestrator identifies the correct agent or agents:

**Single-agent routing:** The request maps to one specialist. The orchestrator delegates directly.

**Multi-agent routing:** The request requires coordination across agents. The orchestrator:
1. Identifies all required agents
2. Determines execution order (sequential or parallel)
3. Identifies dependencies between agent outputs
4. Creates a coordination plan

**Capability gap:** No existing agent handles the request. The orchestrator:
1. Identifies the gap
2. Determines if the need is recurring (worth building a new capability) or one-time
3. Recommends whether to extend an existing agent or define a new one
4. Escalates the gap to human governance for decision

### Step 3: Delegate

Delegation must be **precise and self-contained.** The specialist agent should be able to execute without asking clarifying questions.

A delegation instruction includes:

| Element | Description |
|---------|-------------|
| **Task** | Clear statement of what to do |
| **Context** | Relevant background the specialist needs |
| **Scope** | Boundaries -- what is in scope and out of scope |
| **Inputs** | What the specialist receives (files, data, references) |
| **Expected Output** | What the specialist should produce |
| **Acceptance Criteria** | How to verify the output is correct |
| **Autonomy Level** | What approval is needed |
| **Deadline** | When the output is needed (if applicable) |

### Step 4: Report

After delegation, the orchestrator:

1. Tracks whether the specialist has completed the work
2. Verifies the output meets acceptance criteria
3. Reports completion status to the requestor
4. Logs the action and its business value
5. Triggers downstream steps if this is part of a multi-agent workflow

---

## 3. Orchestrator Discipline

### What the Orchestrator Does

- Parses requests and identifies the right specialist
- Provides clear, actionable delegation instructions
- Coordinates multi-agent workflows
- Tracks completion and reports status
- Identifies capability gaps
- Manages execution plan sequencing and gating

### What the Orchestrator Does NOT Do

- Execute specialist work (code writing, bug fixing, testing, documentation)
- Make architectural decisions (that's AGA)
- Make security decisions (that's STMA)
- Override another agent's gate (Constitution Section 7, Rule 6)
- Resolve conflicts by compromise (Constitution Section 8)

### The Orchestrator's Default Response

When the orchestrator cannot route a request:

```
STOP. Flag the request as unrouteable.
Do not attempt to handle it as a generalist.
Escalate to human governance for routing decision.
```

This follows the Constitutional default: **uncertainty = STOP, not inference.**

---

## 4. Multi-Agent Coordination

When a task requires multiple agents, the orchestrator creates a coordination plan:

### Sequential Workflow

```
PPMA (plan)
   → AGA (validate architecture)
   → CEA (implement)
   → ATADA (test)
   → DMA (document)
   → RRA (release gate)
```

Each step waits for the previous step to complete and pass before proceeding.

### Parallel Workflow

```
PPMA (plan)
   → AGA (validate architecture)     ─┐
   → STMA (security review)           ├─ All must pass
   → DSCA (dependency check)          ├─ before proceeding
   → QMSA (quality gate check)       ─┘
   → CEA (implement)
```

Parallel steps execute independently. All must pass before the next sequential step begins.

### Gated Workflow

The Canonical Execution Lifecycle (Constitution Section 6) defines the mandatory gate sequence. The orchestrator enforces this sequence -- shortcuts are prohibited.

---

## 5. Mapping to HELIos Agents

| Orchestrator Role | HELIos Agent | Notes |
|-------------------|-------------|-------|
| Primary orchestrator | PPMA | Produces plans, coordinates sequencing, manages delegation |
| Architecture gate | AGA | Validates before execution |
| Security gate | STMA | Parallel validation |
| Test gate | ATADA | Post-implementation verification |
| Quality gate | QMSA | Parallel validation |
| Release gate | RRA | Final GO/HOLD/BLOCK |
| Execution | CEA | Implements approved plans |
| Documentation | DMA | Post-implementation sync |

---

## 6. Delegation Templates

### Single-Agent Delegation

```markdown
## DELEGATION: [Agent Name]

**Task:** [Clear description of what to do]
**Context:** [Relevant background]
**Scope:** [In scope / out of scope]
**Inputs:** [Files, references, data]
**Expected Output:** [What the agent should produce]
**Acceptance Criteria:** [How to verify correctness]
**Autonomy Level:** [low/medium/high/critical]
```

### Multi-Agent Coordination Plan

```markdown
## COORDINATION PLAN

**Objective:** [What the combined workflow achieves]
**Agents Required:** [List of agents in execution order]
**Dependencies:** [Which steps depend on which]
**Timeline:** [Expected duration]
**Autonomy Level:** [Overall plan autonomy]

### Step 1: [Agent Name]
- Task: [description]
- Output: [what feeds into next step]
- Gate: [pass/fail criteria]

### Step 2: [Agent Name]
- Depends on: Step 1
- Task: [description]
- Output: [what feeds into next step]
- Gate: [pass/fail criteria]

[...]
```

---

## 7. Anti-Patterns

1. **Orchestrator-as-executor.** The orchestrator writes code, fixes bugs, or performs specialist work instead of delegating. This violates separation of concerns.
2. **Vague delegation.** Instructions like "fix the problem" without context, scope, or acceptance criteria. The specialist should not need to ask clarifying questions.
3. **Skipping gates.** The orchestrator routes directly from planning to implementation without validation. The Canonical Execution Lifecycle exists to prevent this.
4. **Implicit routing.** The orchestrator assumes which agent handles a request without checking. When uncertain, STOP and flag.
5. **Coordination overhead.** Creating a multi-agent workflow for a task that requires only one agent. Keep coordination proportional to complexity.
6. **Silent failures.** Not reporting when a delegated task fails or is blocked. The orchestrator must track and surface all outcomes.
