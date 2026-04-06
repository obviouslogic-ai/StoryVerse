
# HELIos Diagram Index

> Master catalog of all visual diagrams, flowcharts, directory trees, and architecture illustrations in the HELIos corpus. Organized by diagram technology (Mermaid, ASCII, directory tree) and cross-referenced by file path, diagram type, and content description. Use this index to locate existing diagrams before creating new ones.

---

## 1. Mermaid Diagrams

Mermaid diagrams render in GitHub, Notion, and most Markdown viewers that support fenced code blocks.

| # | File | Diagram Type | Description | Lines |
|---|------|-------------|-------------|-------|
| 1 | `reference/sop-execution-data-model.md` | `erDiagram` | Phase 1 baseline — 9-entity SOP execution data model (definitions, versions, steps, runs, step_runs, artifacts, observability, controls, mappings) | 49–163 |
| 2 | `reference/diagrams/erd-enhanced-data-model.md` | `erDiagram` | Phase 2+ target — 23-entity enhanced data model (adds organizations, projects, environments, integrations, agent config, permissions, IO schemas, policies, hashes, ACLs, retention, evidence bundles, control catalogs, incidents, actions, postmortems) | 25–290 |
| 3 | `reference/diagrams/agent-sdlc-role-map.md` | `graph LR` | Agent-to-SDLC function role map — 23 agents organized by tier mapped to 15 SDLC functions with primary/support edges | 23–100 |
| 4 | `reference/diagrams/sop-template-structure.md` | `graph TD` | Gap analysis — current 10-section SOP pattern mapped to proposed 14-field autonomous SOP template (gaps marked with ⭐) | 65–104 |
| 5 | `reference/diagrams/sdlc-roadmap-and-milestones.md` | `gantt` | Implementation milestone Gantt — 6 milestones across Foundation, Compliance, Supply Chain, Operations, and Hardening sections (sequencing only, no effort estimates) | 52–73 |
| 6 | `reference/diagrams/sdlc-roadmap-and-milestones.md` | `graph TD` | Milestone dependency graph — directed acyclic graph showing M1→M6 dependencies | 90–105 |
| 7 | `reference/diagrams/sdlc-roadmap-and-milestones.md` | `stateDiagram-v2` | 3-stage agent autonomy rollout — Observe-Only → Limited Writes → Full Writes with nested states and rollback transitions | 113–138 |
| 8 | `reference/diagrams/sop-workflow-examples.md` | `sequenceDiagram` | Supply chain attestation gate — DSCA → ATADA → RRA with SBOM generation, provenance attestation, and BLOCK/HOLD/GO paths | 29–75 |
| 9 | `reference/diagrams/sop-workflow-examples.md` | `sequenceDiagram` | Requirement change control — REA → PPMA → CEA with security/privacy domain routing, trace link enforcement, and scope gating | 101–150 |
| 10 | `reference/diagrams/sop-workflow-examples.md` | `sequenceDiagram` | Incident-driven rollback — ORFA → RRA → SOA with SLO burn-rate evaluation, rollback/compensating action paths, and postmortem generation | 176–223 |

---

## 2. ASCII Flowcharts & Decision Trees

ASCII diagrams using box-drawing characters (│ ├ └ ─) for decision trees, escalation flows, and process flowcharts.

| # | File | Diagram Type | Description | Lines |
|---|------|-------------|-------------|-------|
| 1 | `reference/escalation-protocols.md` | Decision tree | Escalation routing flowchart — 5-question decision tree (authority? → higher agent? → compliance exception? → irreversible? → ambiguous?) | ~46–57 |
| 2 | `lifecycle/development-loop.md` | Flow diagram | Development loop cycle — SPECIFY → TASK → EXECUTE → GATE (fail/pass loop) → MERGE → VALIDATE | ~86–89 |
| 3 | `governance/strategy-alignment.md` | Decision tree | 7-question strategy alignment gate — sequential filter from "increases manual effort?" through "fits platform pattern?" with REJECT/HOLD/RETURN/APPROVED outcomes | ~158–200 |
| 4 | `sops/cea/sop-cea-003-error-handling-escalation.md` | Escalation tree | CEA error routing — PPMA as first responder, with secondary routing to AGA, STMA, DSCA, DXA, or relevant Tier 1/2 agent | ~212–222 |
| 5 | `sops/cea/sop-cea-002-self-review-loop.md` | Flowchart | 6-step self-review loop — lint → test → compliance → success criteria → iteration check, with restart-on-failure and escalation at >3 iterations | ~248–264 |
| 6 | `sops/ara/sop-ara-002-refactor-execution-verification.md` | Decision tree | 5-check refactor verification gate — tests pass? → no new warnings? → performance OK? → readability improved? → docs updated? → proceed to PR | ~167–191 |
| 7 | `policies/README.md` | Architecture diagram | 2-layer policy architecture — Layer 1 (policy markdown) extracts into Layer 2 (enforcement YAML manifests) | ~22–36 |
| 8 | `policies/README.md` | Pipeline diagram | Agent pipeline consumption — manifests consumed by Security, Architecture Guardian, Test Architect, Coding Execution, Cursor rule, CI, and Release Readiness | ~147–157 |

---

## 3. ASCII Architecture Diagrams

Larger box-drawing diagrams illustrating multi-layer system architecture and data flow.

| # | File | Diagram Type | Description | Lines |
|---|------|-------------|-------------|-------|
| 1 | `automation/health/status-signals.md` | 4-layer architecture | Health status signal pipeline — Source Platforms → Collection Layer (webhooks, polls, reads) → Aggregation Layer (normalization, thresholds, GREEN/YELLOW/RED) → Output (HEALTH.md) → Visibility Layer (repo, Linear, Asana, Notion, CI, alerts) | ~203–266 |

---

## 4. Directory Tree Diagrams

Structural representations of file and folder layouts using tree characters (├── └── │).

| # | File | Description | Lines |
|---|------|-------------|-------|
| 1 | `templates/repo-scaffold.md` | Project root structure (AGENTS.md, ARCHITECTURE.md, README.md, package.json, etc.) | ~25–32 |
| 2 | `templates/repo-scaffold.md` | Source directories (src/, tests/, scripts/, docs/, helios/, .cursor/, .github/) | ~40–47 |
| 3 | `templates/repo-scaffold.md` | Documentation structure (design-docs/, product-specs/, exec-plans/, references/, architecture/) | ~55–74 |
| 4 | `templates/repo-scaffold.md` | Source code structure (app/, components/, services/, hooks/, providers/, lib/, types/, config/) | ~82–110 |
| 5 | `templates/repo-scaffold.md` | Test structure (unit/, integration/, e2e/, compliance/, fixtures/) | ~120–132 |
| 6 | `templates/repo-scaffold.md` | Cursor rules directory (.cursor/rules/) | ~144–147 |
| 7 | `templates/repo-scaffold.md` | GitHub workflows directory (.github/workflows/) | ~158–163 |
| 8 | `QUICK-START.md` | Full project directory tree (comprehensive overview) | ~125–152 |
| 9 | `sops/atada/sop-atada-002-compliance-test-suite-generation.md` | Compliance test directory structure (/tests/compliance/) | ~72–92 |
| 10 | `policies/client/CLIENT-ONBOARDING.template.md` | Client policy directory template | ~67–74 |
| 11 | `policies/README.md` | Full policies directory structure (general/, client/, enforcement/) | ~108–141 |

---

## 5. Summary Statistics

| Category | Count | Files |
|----------|:-----:|:-----:|
| Mermaid diagrams | 10 | 6 |
| ASCII flowcharts & decision trees | 8 | 6 |
| ASCII architecture diagrams | 1 | 1 |
| Directory tree diagrams | 11 | 5 |
| **Total visual elements** | **30** | **15** |

### Mermaid Diagram Types

| Type | Count | Use Case |
|------|:-----:|----------|
| `erDiagram` | 2 | Data model entity relationships |
| `sequenceDiagram` | 3 | Multi-agent SOP workflow coordination |
| `graph` (LR/TD) | 3 | Role mappings, gap analysis, dependency graphs |
| `gantt` | 1 | Implementation milestone sequencing |
| `stateDiagram-v2` | 1 | Agent autonomy rollout stages |

---

## 6. Conventions

### When to Use Each Diagram Type

| Need | Recommended Type | Example |
|------|-----------------|---------|
| Entity relationships and data models | Mermaid `erDiagram` | SOP execution data model |
| Multi-agent coordination flows | Mermaid `sequenceDiagram` | Supply chain attestation gate |
| Role mappings and dependency graphs | Mermaid `graph` | Agent-to-SDLC function mapping |
| Timeline sequencing (no effort estimates) | Mermaid `gantt` | Implementation milestones |
| State transitions with conditions | Mermaid `stateDiagram-v2` | Agent autonomy rollout |
| Quick decision trees in SOPs | ASCII box-drawing | Escalation routing |
| File/folder structure documentation | ASCII directory tree | Repository scaffold |
| Multi-layer system architecture | ASCII box-drawing (large) | Health status signal pipeline |

### Diagram Governance Rules

1. **Mermaid preferred** for any diagram that will be rendered in GitHub, Notion, or documentation sites
2. **ASCII preferred** for quick inline decision trees within SOPs where rendering is not guaranteed
3. **No effort estimates** in any Gantt chart or timeline diagram per standing governance rules
4. **All Mermaid blocks** must be fenced with ` ```mermaid ` and ` ``` ` markers
5. **All ASCII diagrams** must be fenced in code blocks (` ``` `) to preserve formatting
6. **Update this index** when adding new visual diagrams to the corpus

---

## Related Documents

- Enhanced Data Model ERD: [`helios/reference/diagrams/erd-enhanced-data-model.md`](erd-enhanced-data-model.md)
- Agent-SDLC Role Map: [`helios/reference/diagrams/agent-sdlc-role-map.md`](agent-sdlc-role-map.md)
- SOP Template Structure: [`helios/reference/diagrams/sop-template-structure.md`](sop-template-structure.md)
- SOP Workflow Examples: [`helios/reference/diagrams/sop-workflow-examples.md`](sop-workflow-examples.md)
- SDLC Roadmap & Milestones: [`helios/reference/diagrams/sdlc-roadmap-and-milestones.md`](sdlc-roadmap-and-milestones.md)
- Baseline Data Model: [`helios/reference/sop-execution-data-model.md`](../sop-execution-data-model.md)
