# Phase 3: Feature Development (Ongoing)

## Goal

Build features using the standard development loop. This is the steady-state operating phase.

## Duration

Ongoing (6–8 weeks for MVP)

## Active Agents

**ALL agents are active during Phase 3.** This is the full pipeline.

| Agent | Primary Responsibility |
|-------|----------------------|
| Project Manager (PPMA) | Spec → Task conversion, execution plans |
| Coding Execution Agent (CEA) | Implementation |
| Architecture Guardian (AGA) | Structural review |
| Test Architect (ATADA) | Test strategy and coverage |
| Security Agent (STMA) | Auth/data review |
| Quality Metrics Agent (QMSA) | Quality tracking |
| Release Readiness Agent (RRA) | Merge verdicts |
| Document Manager (DMA) | Doc currency |
| Observability Agent (ORFA) | Production monitoring |
| Human Approval Authority (HAA) | Escalation decisions |

## The Development Loop

See `lifecycle/development-loop.md` for the detailed cycle:

```
Specify → Task → Execute → Gate → Merge → Validate
```

## Feature Development Process

1. **Spec**: Product Manager creates spec in Notion/docs, PM Agent creates execution plan
2. **Branch**: Create branch from main: `[linear-id]-short-description`
3. **Build**: CEA implements in Cursor (interactive) or Codex (batch)
4. **Test**: Write tests alongside code, run locally before PR
5. **PR**: Open PR with Linear issue link, compliance rule references
6. **Review**: CI + Compliance Gate + Reliability Gate + Codex review + agent gates
7. **Merge**: RRA issues GO, merge to main, auto-deploy
8. **Close**: Linear issue → Done, Notion changelog updated

## Quality Cadence

| Cadence | Activity | Owner |
|---------|----------|-------|
| Per feature | Review QUALITY_SCORE.md, update domain grades | QMSA |
| Weekly | Doc gardening (DMA via Codex), review tech debt | DMA, ARA |
| Per sprint | Review velocity, agent effectiveness | PPMA |

## Compliance During Feature Dev

1. **Before coding**: CEA reads applicable manifests for scoped domains
2. **During PR**: PR descriptions reference rule IDs for compliance-relevant changes
3. **At gate**: Compliance gate runs on every PR
4. **Before merge**: RRA verifies compliance before issuing GO

## Reliability During Feature Dev

1. **Before coding**: CEA maps side effects to idempotency keys and retry classes
2. **During implementation**: persisted attempt record precedes irreversible external calls
3. **At gate**: Reliability gate validates retry policy and dedupe/reconciliation evidence
4. **Before merge**: RRA verifies SLO-impact assessment and rollback path

## Batch Execution via Codex

For well-defined tasks with clear acceptance criteria:
1. PPMA writes execution plan with CODEX HANDOFF section
2. Task submitted to Codex with plan, context files, and constraints
3. Codex executes, opens PR
4. Standard gate process applies (no shortcuts for batch work)

## Phase 3 Checklist (Per Feature)

- [ ] Product spec written and approved
- [ ] Execution plan created with compliance section
- [ ] Linear issue created with acceptance criteria
- [ ] Code implemented by CEA
- [ ] Tests written and passing
- [ ] Compliance manifests consulted (if scoped domain)
- [ ] Reliability standards applied for side-effecting flows
- [ ] CI pipeline passes
- [ ] Documentation updated
- [ ] PR reviewed and merged
- [ ] Deployed and validated

## Cross-References

- Development loop: `lifecycle/development-loop.md`
- Quality management: `lifecycle/phase-4-quality-entropy.md`
- Release process: `lifecycle/phase-5-testing-iteration.md`
- Execution plan template: `templates/exec-plan.md`
