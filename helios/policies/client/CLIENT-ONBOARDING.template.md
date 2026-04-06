# Client Policy Onboarding Template

Use this template when onboarding a new client's compliance requirements into the HELIos pipeline. Complete each section before generating enforcement manifests.

---

## Client Information

| Field | Value |
|-------|-------|
| **Client Name** | [Client name] |
| **Project** | [Project name] |
| **Onboarding Date** | [YYYY-MM-DD] |
| **Compliance Contact** | [Name / email] |

---

## Step 1: Gather Client Requirements

Collect from the client:

- [ ] Written policies (PDF, Word, or markdown)
- [ ] Industry regulations (e.g., HIPAA, PCI-DSS, FedRAMP)
- [ ] Internal security standards
- [ ] Contractual obligations (SLAs, data handling)
- [ ] Audit findings or previous compliance reports (if applicable)

**Notes:**

```
[Record key requirements, deadlines, and constraints here]
```

---

## Step 2: Map to Policy Domains

Map each client requirement to the existing HELIos policy structure. Client requirements can ADD rules or INCREASE severity. They CANNOT weaken baseline protections.

| Client Requirement | HELIos Domain | Action (add / strengthen) | Notes |
|-------------------|---------------|---------------------------|-------|
| [e.g., PCI-DSS encryption] | infrastructure-config | add | AES-256 for cardholder data |
| [e.g., 24-month log retention] | security-operations | strengthen | Baseline is 180 days; client requires 730 |
| [e.g., SSO-only for admin] | access-control | add | MFA + SSO for privileged accounts |

---

## Step 3: Author Client Policy Documents

Create markdown policy files under `policies/client/` using the same structure as `general/`:

```
policies/client/
├── index.md                    # Overview of client-specific policies
├── access-control/             # If client has access requirements
├── data-protection/            # If client has data handling requirements
├── security-operations/        # If client has logging/monitoring requirements
├── infrastructure-configuration/
└── [other domains as needed]
```

**Template for each client policy file:**

```markdown
# [Policy Title]

**Source:** [Client name / regulation]  
**Effective:** [Date]  
**Framework mappings:** SOC2-CC[X], HIPAA-XXX, NIST-XXX, etc.

## Purpose
[One paragraph describing the policy and why it exists.]

## Technical Requirements
1. [Requirement 1 - specific, testable]
2. [Requirement 2]
3. [Requirement 3]

## Enforcement
- **Severity:** critical | high | medium | low
- **CI checkable:** yes | no
- **Check description:** [How to verify compliance]
- **Violation action:** block-merge | require-review | warn | log
```

---

## Step 4: Generate client-overrides.manifest.yml

Extract enforceable rules from client policies into `enforcement/manifests/client-overrides.manifest.yml`.

**Manifest structure (follow manifest-schema.yml):**

```yaml
manifest:
  domain: "client-overrides"
  source_policies:
    - path: "client/[domain]/[policy-file].md"
      title: "[Policy Title]"
  framework_refs:
    - "[Client]-[Requirement]"
    - "SOC2-CC6"  # if maps to baseline

  rules:
    - id: "CLIENT-001"
      rule: "[Plain-language enforceable statement]"
      technical_req: "[Specific technical requirement]"
      scope: ["auth", "databases", "api", "storage", "logging"]
      severity: critical | high | medium | low
      enforced_by: ["security-agent", "architecture-guardian", "test-architect"]
      ci_checkable: true | false
      check_description: "[How to verify]"
      violation_action: block-merge | require-review | warn | log
```

**Merge rules:**
- General manifests + client-overrides = complete enforcement
- Client rules ADD to baseline; they never remove or weaken baseline rules
- If client rule conflicts with baseline, the STRICTER rule prevails

---

## Step 5: Validate Manifests

- [ ] Run manifest against `manifest-schema.yml`
- [ ] Every rule has unique ID (CLIENT-XXX format)
- [ ] Every rule has severity and violation_action
- [ ] ci_checkable rules have check_description
- [ ] No rule weakens a baseline rule

---

## Step 6: Update CI (if needed)

If client rules require additional CI checks not covered by `compliance-gate.yml`:

1. Add a new job in `compliance-gate.yml` or create a client-specific workflow
2. Reference rule IDs in check output
3. Ensure failures block merge for critical/high severity

---

## Step 7: Document Exceptions

If any baseline rule has a client-approved exception:

| Rule ID | Exception | Approved By | Document Location |
|---------|-----------|-------------|-------------------|
| [e.g., LOG-001] | 90-day retention approved for pilot | [HAA / client] | [Link to exception register] |

---

## Verification Checklist

- [ ] Client policy documents authored in `policies/client/`
- [ ] `client-overrides.manifest.yml` generated and validated
- [ ] CI updated if client requires extra checks
- [ ] Exceptions documented (if any)
- [ ] Compliance contact informed of active policy set
- [ ] Policy gate checklist updated for release

---

## Related Documents

| Document | Purpose |
|----------|---------|
| `policies/README.md` | Policy framework overview |
| `policies/manifest-schema.yml` | Manifest structure |
| `configs/cursor/rules/compliance-enforcement.mdc` | Agent enforcement rules |
| `configs/github/workflows/compliance-gate.yml` | CI compliance checks |
| `policies/enforcement/policy-gate-checklist.md` | Pre-release verification |
