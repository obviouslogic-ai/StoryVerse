# Autonomy Classification Guide

## Purpose

This document defines the four autonomy levels that govern every agent action in the HELIos pipeline. Autonomy classification determines whether an action may proceed without human involvement, require notification, need pre-approval, or demand formal sign-off.

**Constitutional Authority:** Constitution Section 13 (Autonomy Classification)

---

## 1. Autonomy Levels

| Level | Name | Description | Approval Required |
|-------|------|-------------|-------------------|
| `low` | Fully Autonomous | Agent executes and logs. No human involvement needed. | None |
| `medium` | Autonomous with Notification | Agent executes and notifies relevant stakeholders after completion. | None (notification only) |
| `high` | Pre-Approval Required | Agent proposes the action and waits for approval before executing. | PPMA or designated reviewer |
| `critical` | Human Authority Required | Requires Human Approval Authority (HAA) sign-off with documented justification. | HAA |

### Key Rule

**The default autonomy level for any unclassified action is `high`.**

This means: if the plan does not specify the autonomy level, the action requires pre-approval. This prevents unintended autonomous execution.

---

## 2. Default Agent Assignments

Each agent has a default autonomy level. Specific actions may override the default (see Section 3).

### Tier 0 -- Human Governance

| Agent | Default Autonomy | Rationale |
|-------|-----------------|-----------|
| Human Approval Authority (HAA) | `critical` | HAA is the ultimate arbiter; its decisions are by definition critical-level |

### Tier 1 -- Core Authority Agents

| Agent | Default Autonomy | Rationale |
|-------|-----------------|-----------|
| Release Readiness Agent (RRA) | `high` | GO/HOLD/BLOCK decisions affect shipping |
| Architecture Guardian Agent (AGA) | `high` | Architectural decisions have long-term impact |
| Security & Threat Modeling Agent (STMA) | `high` | Security decisions affect system safety |
| Autonomous Test Architect (ATADA) | `high` | Test enforcement gates affect code flow |
| Dependency & Supply Chain Agent (DSCA) | `high` | Dependency decisions affect supply chain security |

### Tier 2 -- Signal and Quality Enforcement

| Agent | Default Autonomy | Rationale |
|-------|-----------------|-----------|
| Quality Metrics & SLO Agent (QMSA) | `medium` | Measurement and reporting are non-destructive |
| Observability & Runtime Feedback Agent (ORFA) | `medium` | Monitoring and signal generation are read-only |
| Developer Experience Agent (DXA) | `medium` | DX improvements are advisory |

### Tier 3 -- Planning and Execution

| Agent | Default Autonomy | Rationale |
|-------|-----------------|-----------|
| Premiere Project Manager Agent (PPMA) | `high` | Plans drive all downstream execution |
| Coding Execution Agent (CEA) | `high` | Code changes are write operations |
| Autonomous Refactor Agent (ARA) | `high` | Refactoring modifies existing code |

### Support Agents

| Agent | Default Autonomy | Rationale |
|-------|-----------------|-----------|
| Document Manager Agent (DMA) | `medium` | Documentation updates are non-destructive and reversible |
| UX/UI/Brand Governor Agent (UIBGA) | `medium` | Design governance is advisory |

---

## 3. Action-Specific Overrides

An agent's default autonomy level applies to most of its actions, but specific actions may require a different level. Overrides are defined in each agent's definition file under `## Autonomy Level`.

### Common Override Patterns

#### Read-Only Operations: `low`

Any agent performing read-only operations (code analysis, metric collection, signal generation, documentation review) operates at `low` autonomy regardless of its default level.

Examples:
- AGA analyzing code structure (low) vs. AGA blocking a PR (high)
- STMA scanning for vulnerabilities (low) vs. STMA requiring a security review (high)
- QMSA collecting metrics (low) vs. QMSA failing a quality gate (high)

#### Write Operations: Agent default or higher

Any write operation operates at the agent's default autonomy level or higher. Write operations include:
- Code modification
- File creation or deletion
- Database mutations
- Deployment triggers
- Configuration changes
- External API calls that modify state

#### Irreversible Operations: `critical`

Any irreversible action requires `critical` autonomy regardless of the agent performing it:
- Production deployments
- Data deletion
- Security policy changes
- Compliance exception requests
- Architecture changes that cannot be rolled back

---

## 4. Autonomy in Execution Plans

Every execution plan produced by PPMA must declare its autonomy level in both the Business Value section and the Codex Handoff block.

### Plan Format

```markdown
## AUTONOMY CLASSIFICATION

- **Plan Autonomy Level:** [low/medium/high/critical]
- **Write Operations:** [list of authorized writes with scope]
- **Escalation Required:** [yes/no -- if yes, who approves]
```

### Codex Handoff Block

```markdown
## CODEX HANDOFF

| Field | Value |
|-------|-------|
| Task Title | [description] |
| Branch Name | [branch] |
| Autonomy Level | [low/medium/high/critical] |
| Files to Modify | [list] |
| Acceptance Criteria | [criteria] |
| Time Estimate | [estimate] |
```

---

## 5. Escalation Rules

### Upward Escalation

An agent may request escalation to a higher autonomy level when:

1. The action's impact is greater than initially assessed
2. The action affects a compliance-scoped domain
3. The action conflicts with another agent's gate
4. Uncertainty exists about the correct course of action

Escalation path:
```
low → medium → high → critical → HAA
```

### Escalation Triggers (Automatic)

The following conditions automatically escalate autonomy:

| Condition | Escalates To |
|-----------|-------------|
| Action affects compliance-scoped domain | `high` minimum |
| Action modifies production environment | `critical` |
| Action conflicts with another agent's output | `high` minimum |
| Action scope exceeds plan authorization | `critical` |
| Agent detects ambiguity in requirements | STOP (not escalation) |

### Who May Not Escalate

**No agent may escalate its own autonomy level.** Autonomy levels are assigned by:
- This constitution (default assignments)
- The agent registry (agent-specific defaults)
- Individual agent definition files (action-specific overrides)
- The execution plan (plan-level classification)

Self-escalation is a compliance violation.

---

## 6. Autonomy and the Read-Only Default

Constitution Section 14 (Safety Invariants) establishes that all agent operations are **read-only by default**. Autonomy classification layers on top of this:

| Operation Type | Read-Only Default | Autonomy Applies? |
|----------------|-------------------|-------------------|
| Read-only (analysis, metrics, review) | Permitted by default | Yes -- but typically `low` |
| Write (code change, file creation) | Requires plan authorization | Yes -- at agent's default or higher |
| Irreversible (deploy, delete, security change) | Requires plan + explicit authorization | Yes -- always `critical` |

A write operation must satisfy **both** requirements:
1. Explicitly authorized in the execution plan (with target, scope, rollback, autonomy level)
2. Autonomy level approval obtained (if `high` or `critical`)

---

## 7. Mapping from Cortex Autonomy Model

For projects migrating from Cortex, the following mapping applies:

### Cortex Terminator Model

| Cortex Category | HELIos Autonomy Level |
|----------------|----------------------|
| Fix immediately without asking (syntax, imports, linting, style, type hints) | `low` (read) or `medium` (write with notification) |
| Require approval (DB schema, breaking API, high/critical security, >10 files, deploy config, auth logic) | `high` or `critical` |

### Cortex YAML Agent Autonomy

| Cortex YAML Value | HELIos Autonomy Level |
|-------------------|----------------------|
| `autonomy: "high"` (Cortex meaning: agent has high independence) | `high` (HELIos meaning: requires pre-approval) -- **Note: inverted semantics** |
| `autonomy: "medium"` (Cortex meaning: moderate independence) | `medium` (HELIos meaning: autonomous with notification) |
| Schema changes `required: true` | `critical` |

**Important:** Cortex uses "high autonomy" to mean "the agent can do a lot independently." HELIos uses "high autonomy level" to mean "this action requires pre-approval." The semantics are inverted. When migrating, map Cortex `autonomy: "high"` to HELIos `high` (the action is consequential and needs approval).

---

## 8. Compliance Interaction

Autonomy classification interacts with compliance enforcement as follows:

1. Any action in a compliance-scoped domain (authentication, authorization, data handling, encryption, logging, PHI/PII, key management) has a **floor** of `high` autonomy
2. Compliance manifests may specify required autonomy levels for specific operations
3. A compliance exception requires `critical` autonomy + HAA sign-off + documentation in the exception register
4. Autonomy escalation in a compliance context is itself a security-relevant event (logged by STMA)

---

## 9. Anti-Patterns

1. **Autonomy shopping.** Reframing an action to fit a lower autonomy level. If the action modifies production code, it's `high` regardless of how it's described.
2. **Blanket approvals.** "Approve all future actions" is not a valid approval. Each execution plan declares its own autonomy level.
3. **Silent upgrades.** Adding scope to an approved plan without re-evaluating autonomy. If scope changes, autonomy must be re-assessed.
4. **Notification-as-approval.** `medium` (notification) is not `high` (approval). An agent at `medium` does not wait for a response -- it notifies and proceeds.
5. **Default avoidance.** Not declaring autonomy level in a plan to avoid the default `high`. The default exists precisely for this case -- undeclared = `high`.
