# Integration Pattern: Read-Only Default

## Purpose

This document defines the read-only-by-default safety pattern for the HELIos pipeline. All agent operations are read-only unless the execution plan explicitly authorizes write operations. This pattern prevents unintended state changes and ensures every write is deliberate, scoped, and reversible.

**Constitutional Authority:** Constitution Section 14 (Safety Invariants)

**Origin:** Genericized from the Cortex autonomy authority model (Terminator agent's autonomous-vs-approval classification).

---

## 1. Core Principle

**All agent operations are read-only by default.**

An agent does not have permission to modify anything unless the active execution plan explicitly lists and authorizes the write operation.

This is not a recommendation. It is a safety invariant enforced by the constitution.

---

## 2. Operation Classification

### Read-Only Operations (Permitted by Default)

These operations do not modify state and may proceed without explicit write authorization:

| Operation | Examples |
|-----------|---------|
| Code analysis | Static analysis, linting (report-only), complexity measurement |
| Metric collection | Coverage reports, performance benchmarks, quality scores |
| Documentation review | Checking for drift, completeness audit, cross-reference validation |
| Signal generation | Producing warnings, recommendations, or gate results |
| Plan creation | Drafting execution plans for review |
| Test execution (isolated) | Running tests in CI that do not modify the codebase |
| Dependency scanning | Checking for vulnerabilities without modifying lockfiles |
| Search and retrieval | Finding files, reading configurations, querying data |

### Write Operations (Require Explicit Authorization)

These operations modify state and must be listed in the active execution plan:

| Operation | Examples |
|-----------|---------|
| Code modification | Adding, changing, or deleting source code |
| File creation/deletion | Creating new files, removing existing files |
| Database mutations | Schema changes, data modifications, migration execution |
| Deployment triggers | Initiating builds, deployments, or releases |
| Configuration changes | Modifying environment variables, platform settings, CI configs |
| External API calls (state-modifying) | Creating issues, posting comments, sending notifications |
| Package modifications | Updating dependencies, modifying lockfiles |
| Branch operations | Creating branches, merging, rebasing |

---

## 3. Write Authorization Requirements

Every authorized write operation in an execution plan must specify four elements:

### Target

**What** is being modified.

```
Target: src/lib/auth/session.ts
```

Be specific. "Source code" is not a valid target. The file path, database table, or service endpoint must be named.

### Scope

**What changes** are permitted.

```
Scope: Add session expiry validation to the validateSession() function.
       No changes to the session creation flow.
```

Scope defines the boundary of the write. The agent may not exceed this scope even if related changes seem beneficial.

### Rollback Procedure

**How to revert** if the write causes problems.

```
Rollback: Revert commit [hash] or restore from branch main.
          No database migration involved -- pure code change.
```

Every write must be reversible. If a write cannot be rolled back (e.g., data deletion), it requires `critical` autonomy.

### Autonomy Level

**What approval** is required for this specific write.

```
Autonomy Level: high (requires PPMA approval before execution)
```

The autonomy level for a write operation is always equal to or higher than the executing agent's default autonomy level.

---

## 4. Write Authorization in Plans

### Execution Plan Format

```markdown
## AUTONOMY CLASSIFICATION

- **Plan Autonomy Level:** high
- **Write Operations:**
  1. **Target:** src/lib/auth/session.ts
     **Scope:** Add session expiry check to validateSession()
     **Rollback:** Git revert
     **Autonomy:** high
  2. **Target:** src/lib/auth/__tests__/session.test.ts
     **Scope:** Add test cases for session expiry
     **Rollback:** Git revert
     **Autonomy:** high
- **Escalation Required:** No
```

### Rules

1. **No unlisted writes.** An agent may not perform a write operation not listed in the active execution plan.
2. **No scope expansion.** An agent may not expand the scope of an authorized write beyond what is specified.
3. **No self-authorization.** An agent may not authorize its own write operations. Write authorization comes from the plan, which is produced by PPMA and validated by higher-tier agents.
4. **Compliance check first.** Write operations in compliance-scoped domains require enforcement manifest verification before execution.
5. **Emergency exception.** Emergency write operations for incident remediation may proceed with retroactive documentation within 24 hours. This exception requires post-incident review.

---

## 5. The Authorization Flow

```
PPMA creates execution plan
   |
   v
Plan lists all write operations (target, scope, rollback, autonomy)
   |
   v
AGA validates architectural impact of writes
   |
   v
STMA reviews security implications (if applicable)
   |
   v
Plan is approved at the declared autonomy level
   |
   v
CEA/ARA executes ONLY the authorized writes
   |
   v
ATADA verifies writes did not break tests
   |
   v
DMA updates documentation if write changes behavior
   |
   v
RRA includes write summary in release readiness assessment
```

---

## 6. Mapping from Cortex Authority Model

The Cortex Terminator agent defines two categories that map directly to this pattern:

### Autonomous Authority (Fix Immediately)

| Cortex Category | HELIos Mapping |
|-----------------|---------------|
| Syntax errors | Read-only analysis (detection) + `low` autonomy write (auto-fix in CI) |
| Import errors | Read-only analysis + `low` autonomy write |
| Linter warnings (PEP8, formatting) | Read-only analysis + `low` autonomy write |
| Unused imports | Read-only analysis + `low` autonomy write |
| Code style issues | Read-only analysis + `low` autonomy write |
| Type hint errors | Read-only analysis + `low` autonomy write |

These are mechanical fixes with zero behavioral impact. They can be authorized as `low` autonomy writes in the plan or handled by CI auto-fix pipelines.

### Require Approval

| Cortex Category | HELIos Mapping |
|-----------------|---------------|
| Database schema changes | `critical` autonomy write (irreversible) |
| Breaking API changes | `high` autonomy write (broad impact) |
| Security vulnerabilities (high/critical) | `critical` autonomy write (security scope) |
| Changes affecting >10 files | `high` autonomy write (broad scope) |
| Deployment configuration | `high` autonomy write (infrastructure) |
| External API integrations | `high` autonomy write (external dependency) |
| Authentication/authorization logic | `critical` autonomy write (compliance scope) |

These require explicit plan authorization with full target/scope/rollback/autonomy specification.

---

## 7. Interaction with Other Patterns

### Orchestrator Pattern

The orchestrator (PPMA) creates plans that define writes. The orchestrator itself never performs writes -- it delegates to execution agents (CEA, ARA) who operate within the plan's write authorizations.

### Autonomy Classification

Read-only default and autonomy classification are complementary:
- Read-only default controls **what can be modified** (nothing, unless authorized)
- Autonomy classification controls **who must approve** the modification

A write must satisfy both: it must be listed in the plan (read-only default) AND approved at the correct autonomy level.

### Compliance Enforcement

Writes in compliance-scoped domains have additional requirements:
- The relevant enforcement manifest must be consulted before the write is planned
- The write must satisfy all applicable compliance constraints
- The compliance verification must be recorded in the execution log

---

## 8. Anti-Patterns

1. **Implicit writes.** An agent makes a "small fix" not listed in the plan because it seems harmless. All writes must be authorized, regardless of size.
2. **Blanket authorization.** A plan authorizes "any necessary changes to the auth module." This is not a valid scope -- specific files and modifications must be named.
3. **Read-as-write.** An agent performs a write operation and categorizes it as "reading and updating." If the state changed, it was a write.
4. **Rollback theater.** Listing "git revert" as the rollback for a database migration that dropped a column. The rollback must actually work.
5. **Emergency abuse.** Using the emergency exception for non-emergency writes to avoid the authorization flow. Emergency writes require retroactive review.
6. **Scope creep.** An agent discovers an additional change needed during execution and makes it without updating the plan. The correct action is to STOP, flag the scope change, and request plan amendment.
