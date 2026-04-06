# HELIos Compliance Policy Framework

## Two-Layer Architecture

HELIos uses a **two-layer** compliance system to separate human-auditable policy from machine-executable enforcement:

```
LAYER 1: Policy Documents (Markdown)              LAYER 2: Enforcement Manifests (YAML)
─────────────────────────────────────            ─────────────────────────────────────
policies/general/                                  policies/enforcement/manifests/
  access-control/                                    access-control.manifest.yml
    authentication-credentials.md  ──extracts──►       AUTH-001: min 12-char passwords
    access-control-iam.md          ──extracts──►       AC-001: RBAC enforcement
  data-protection/                                   data-protection.manifest.yml
    data-classification-handling.md──extracts──►       DC-001: AES-256 at rest
  security-operations/                               security-operations.manifest.yml
    logging-monitoring.md          ──extracts──►       LOG-001: 180-day retention
  ...                                                ...

policies/client/ (optional)                          client-overrides.manifest.yml
  [client-specific policies]  ──extracts──►           [client rules]
```

- **Layer 1 (Markdown):** Authoritative, audit-ready, human-readable. Used for audits, training, and policy review.
- **Layer 2 (YAML):** Machine-parsable, agent-executable. Used by agents, CI, and release gates.

Policies stay as markdown. Manifests are **extracted** from policies during Phase 1 setup.

---

## Onboarding Guide

### For a New Project (No Client Overrides)

**Step 1: Copy baseline policies**

Baseline policies are in `general/` (SSC policy set). If starting fresh:

```bash
# Baseline is already in helios/policies/general/
# Verify structure:
ls general/index.md general/access-control general/data-protection general/security-operations
```

**Step 2: Generate enforcement manifests**

Manifests in `enforcement/manifests/` are pre-populated from the baseline. Validate against schema:

```bash
# Each manifest must conform to manifest-schema.yml
# Rule IDs must be unique across all manifests
# source_policies paths must match actual files in general/
```

**Step 3: Validate cross-references**

- Every `source_policies.path` in each manifest must point to an existing file in `general/`
- Run doc gardening to ensure no broken links

**Step 4: Verify CI integration**

- Copy `configs/github/workflows/compliance-gate.yml` to `.github/workflows/`
- Open a test PR that violates a rule (e.g., add `console.log` in `src/`)
- Confirm compliance-gate blocks or flags the PR

**Step 5: Copy Cursor rule**

- Copy `configs/cursor/rules/compliance-enforcement.mdc` to `.cursor/rules/`
- Agents will read manifests before writing code in scoped domains

---

### For a Client Project (Client-Specific Policies)

Use `client/CLIENT-ONBOARDING.template.md` for the full process. Summary:

**Step 1:** Complete Steps 1–5 above (baseline)

**Step 2:** Gather client requirements (policies, regulations, contracts)

**Step 3:** Author client policy documents in `client/` using the same domain structure

**Step 4:** Generate `client-overrides.manifest.yml` from client policies

**Step 5:** Merge rules: baseline + client overrides = complete enforcement. Client can ADD rules or INCREASE severity; cannot weaken baseline.

**Step 6:** Add CI checks for any client rules that need automation

---

## Directory Structure

```
policies/
├── README.md                          # This file — onboarding guide
├── manifest-schema.yml                # Schema for all manifests
├── general/                           # Baseline policies (SSC set)
│   ├── index.md
│   ├── BASELINE-README.md
│   ├── access-control/
│   ├── data-protection/
│   ├── development-change/
│   ├── security-operations/
│   ├── infrastructure-configuration/
│   ├── business-continuity/
│   ├── governance-risk-compliance/
│   ├── endpoint-asset-management/
│   ├── workforce-training/
│   ├── third-party-contracts/
│   ├── appendices/
│   └── second-tier-artifacts/
├── client/                            # Client-specific policies
│   ├── CLIENT-ONBOARDING.template.md
│   └── [domain folders as needed]
└── enforcement/
    ├── manifests/                     # YAML enforcement manifests
    │   ├── access-control.manifest.yml
    │   ├── data-protection.manifest.yml
    │   ├── development-change.manifest.yml
    │   ├── security-operations.manifest.yml
    │   ├── infrastructure-config.manifest.yml
    │   ├── business-continuity.manifest.yml
    │   └── client-overrides.manifest.yml
    ├── policy-gate-checklist.md       # Pre-release verification
    ├── compliance-test-vectors.md     # Test implementation template
    └── violation-classifications.md   # Severity and actions
```

---

## How Manifests Flow Through the Pipeline

```
enforcement/manifests/*.manifest.yml
         │
         ├──► Security Agent: models abuse cases against manifest rules
         ├──► Architecture Guardian: validates architecture supports requirements
         ├──► Test Architect: generates compliance tests from check_description
         ├──► Coding Execution: reads manifests as constraints during implementation
         ├──► Cursor rule (compliance-enforcement.mdc): surfaces violations inline
         ├──► CI (compliance-gate.yml): runs ci_checkable rules
         └──► Release Readiness: all manifest rules verified before GO
```

---

## Manifest Schema (Summary)

Every manifest must have:

- `domain`: string (e.g., `access-control`)
- `source_policies`: array of `{path, title}` pointing to markdown policies
- `framework_refs`: array of framework IDs (SOC2, HIPAA, NIST)
- `rules`: array of rule objects, each with:
  - `id`, `rule`, `technical_req`, `scope`, `severity`, `enforced_by`
  - `ci_checkable`, `check_description`, `violation_action`

Full schema: `manifest-schema.yml`

---

## Key Documents

| Document | Purpose |
|----------|---------|
| `manifest-schema.yml` | Structure that all manifests must follow |
| `enforcement/violation-classifications.md` | Severity levels and violation actions |
| `enforcement/compliance-test-vectors.md` | Template for turning rules into tests |
| `enforcement/policy-gate-checklist.md` | Pre-release verification checklist |
| `client/CLIENT-ONBOARDING.template.md` | Client policy onboarding steps |

---

## Resilience Controls (Required for Outage-Sensitive Systems)

In addition to baseline compliance controls, systems with external dependency risk must include:

- documented degrade-mode behavior (read-only, queue-only, or fail-closed)
- regional health checks for critical dependencies
- failover and rollback runbook
- replay and reconciliation evidence after failover drills
- release-delta evaluation process for model/provider/platform updates

Recommended references:

- `reference/operations/supabase-failover-playbook.md`
- `reference/operations/release-delta-eval-gate.md`

Evidence should be attached to release readiness artifacts for auditability.

---

## Key Principle

**Compliance is a system property, not a phase.** Every line of code passes through compliance enforcement. No exceptions without Human Approval Authority sign-off and documentation in the exception register.
