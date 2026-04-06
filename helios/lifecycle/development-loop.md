# The HELIos Development Loop

The standard cycle for every feature, bug fix, or improvement.

## The Loop

```
1. SPECIFY → 2. TASK → 3. EXECUTE → 4. GATE → 5. MERGE → 6. VALIDATE
```

### 1. Specify

- Product spec written in Notion and/or `docs/product-specs/`
- Acceptance criteria defined (testable, measurable)
- Architecture implications assessed by Architecture Guardian
- Compliance implications assessed (which policy domains affected)
- **Agent**: Project Manager (PPMA)

### 2. Task

- Linear issue created with acceptance criteria, spec link, compliance considerations
- Execution plan written (exec-plan template) with CODEX HANDOFF
- Dependencies identified
- **Agent**: Project Manager (PPMA)

### 3. Execute

- Code written by Coding Execution Agent (Cursor interactive or Codex batch)
- Compliance manifests consulted for scoped domains
- Self-review loop: review own changes → run lints/tests → iterate → open PR
- **Agent**: Coding Execution Agent (CEA)

### 4. Gate

- CI pipeline runs: lint, types, tests, build, structural checks
- Compliance gate runs: secret scan, encryption check, logging check
- Reliability gate runs: idempotency, retry-policy, and reconciliation checks for scoped domains
- Codex review triggered
- Architecture Guardian reviews structural changes
- Security Agent reviews auth/data changes
- **Agent**: ATADA, AGA, STMA, QMSA, RRA

### 5. Merge

- Release Readiness Agent issues GO / HOLD / BLOCK
- Human Approval Authority reviews if required (irreversible changes, policy exceptions)
- Merge to main triggers auto-deploy to Vercel
- **Agent**: RRA, HAA (if needed)

### 6. Validate

- Notion changelog updated (automated)
- Linear issue marked Done
- Observability Agent monitors production impact
- Document Manager ensures docs are current
- **Agent**: DMA, ORFA

---

## Loop Duration

| Scope | Duration |
|-------|----------|
| Simple bug fix | Hours |
| Standard feature | 1–3 days |
| Complex feature | 1–2 weeks (multiple loop iterations) |

## When the Loop Breaks

If any gate fails, the loop returns to **Step 3 (Execute)** with specific remediation requirements. The loop does not advance until all gates pass.

```
SPECIFY → TASK → EXECUTE → GATE (fail) → EXECUTE → GATE (pass) → MERGE → VALIDATE
                    ↑          ↓
                    └──────────┘
```

## Cross-References

- Phase 3 steady-state operations: `lifecycle/phase-3-feature-dev.md`
- Gate details and CI pipeline: `lifecycle/phase-2-scaffold-ci.md`
- Quality cadence: `lifecycle/phase-4-quality-entropy.md`
- Release process: `lifecycle/phase-5-testing-iteration.md`
- Reliability invariants: `reference/reliability/cross-wave-invariants-slos.md`
