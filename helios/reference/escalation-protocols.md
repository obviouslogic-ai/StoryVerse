# Escalation Protocols

## When Agents Stop

Every agent has defined stop conditions. When an agent stops, it must:
1. Document what it was doing
2. Identify why it stopped
3. Specify what information or decision is needed
4. Identify who should resolve the issue

## Escalation Paths

### Level 1: Agent Self-Resolution
- Agent retries with adjusted approach (max 3 iterations in self-review loop)
- If resolved, proceed normally and log the retry
- If not resolved after 3 iterations, escalate to Level 2

### Level 2: Peer Agent Resolution
- Agent consults a higher-authority agent
- Example: CEA encounters architectural ambiguity → escalate to AGA
- Example: ATADA finds compliance gap → escalate to STMA
- Higher agent provides guidance or blocks

### Level 3: Human Approval Authority
- Triggered when: agents disagree, irreversible decisions needed, compliance exceptions requested, scope changes required, policy interpretation ambiguous
- HAA receives: clear description, options, risks, recommendation
- HAA responds: APPROVE / REJECT / REQUEST REVISION

## Escalation Decision Tree

```
Issue detected
    │
    ├─ Is it within agent's authority? → Yes → Resolve
    │
    ├─ Can a higher agent resolve? → Yes → Escalate to that agent
    │
    ├─ Is it a compliance exception? → Yes → Escalate to HAA
    │
    ├─ Is it an irreversible decision? → Yes → Escalate to HAA
    │
    └─ Is it ambiguous? → Yes → STOP and escalate to HAA
```

## Common Escalation Scenarios

| Scenario | Escalation Path |
|----------|----------------|
| Test failure on PR | CEA → ATADA (investigate) → CEA (fix) |
| Architectural violation detected | CEA → AGA (review) → CEA (redesign or AGA approves exception) |
| Security concern in code | CEA → STMA (threat assessment) → CEA (remediate) |
| Compliance policy conflict | Any agent → STMA (analyze) → HAA (decide exception or redesign) |
| Dependency vulnerability found | DSCA → CEA (patch) or AGA (if architectural change needed) |
| Quality grade drops to F | QMSA → PPMA (plan remediation) → CEA (implement) |
| Documentation contradicts code | DMA → CEA/AGA (determine which is correct) → DMA (update docs) |
| Agent disagreement | Both agents → next higher authority → or HAA if equal authority |
| Scope change requested | PPMA → HAA (approve/reject scope change) |
| Production incident | ORFA → STMA (assess) → PPMA (plan fix) → CEA (implement) |

## Escalation Documentation
All escalations must be documented:
- What was the issue
- Who escalated
- Who resolved
- What was decided
- Where is the decision recorded (PR comment, ADR, exception register)
