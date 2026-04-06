# HELIos Canonical Lexicon

> **Authoritative Term Dictionary** — Version 1.0
> All documents must conform to these definitions.
> Approved by: Daniel DeZago, HAA, ObviousLogic.ai
> Date: 2026-03-25

---

## Introduction

**Purpose:** This lexicon eliminates ambiguity across all HELIos documentation by defining every significant term with exactly one meaning. When a term appears in any HELIos document — agent definition, SOP, policy, template, or configuration — it must carry the meaning defined here.

**Scope:** Every term used across agents, SOPs, policies, reference materials, governance, lifecycle, setup, and template documents.

**Enforcement:** All new and revised documents must use terms exactly as defined in this lexicon. PGA (Process Governance Analyst) validates terminology compliance during SOP review.

**Update Process:** Changes to this lexicon require HAA (Daniel DeZago) approval. Submit a PR modifying the lexicon file with a rationale for each change.

---

## Glossary

Terms listed alphabetically. Each entry provides the canonical form, definition, category, common confusions, and correct usage.

### A

**ABE (AI Bug Evaluation Agent)**
- **Definition:** Tier 3 agent that evaluates, classifies, and optionally auto-fixes bugs using a 3-tier autonomy model (A/B/C).
- **Category:** Agent
- **Do NOT confuse with:** Do NOT use 'AI Build Engine' or 'Automated Bug Eliminator'.
- **Example:** ABE classified the null pointer exception as Tier B, requiring human approval before fix execution.

**acceptance criteria**
- **Definition:** Testable conditions that define when a feature or specification is complete. Must be verifiable and unambiguous.
- **Category:** Process
- **Do NOT confuse with:** Do NOT confuse with 'success criteria' (plan-level completion conditions).
- **Example:** All acceptance criteria from the product spec are met before the PR is opened.

**ADR (Architecture Decision Record)**
- **Definition:** Formal document capturing a significant architectural decision, managed by AGA. Stored at `docs/architecture/decisions/`.
- **Category:** Architecture
- **Do NOT confuse with:** Do NOT confuse with 'design doc' (broader design proposals in `docs/design-docs/`).
- **Example:** ADR-017 was accepted, mandating RLS for all tables with user data.

**AGA (Architecture Guardian Agent)**
- **Definition:** Tier 1 agent that reviews architectural compliance, manages ADRs, and detects architectural drift.
- **Category:** Agent
- **Do NOT confuse with:** Do NOT use 'Automated Gate Agent' or 'Architecture Sentinel'.
- **Example:** AGA blocked the PR because it violated the established data layer boundary.

**agent**
- **Definition:** An AI system with a defined role, authority, and set of responsibilities in the HELIos pipeline. One of the 20 named agents arranged in authority tiers 0-3 plus Support.
- **Category:** Architecture
- **Do NOT confuse with:** Do NOT confuse with 'threat actor agent' (human insider) or 'platform agent' (Cursor/Codex execution tool).
- **Example:** The agent escalated the unresolved conflict to HAA for human decision.

**AGENTS.md**
- **Definition:** Repository root file that serves as the primary instruction source for Codex. Contains the agent roster, governance rules, and self-review checklist.
- **Category:** Infrastructure
- **Do NOT confuse with:** Do NOT confuse with agent definition files in `agents/` directory.
- **Example:** CEA reads AGENTS.md before every Codex-mode execution.

**artifact**
- **Definition:** A produced output of a process step. Always qualify: 'build artifact' (compiled output), 'compliance artifact' (audit evidence), 'evidence artifact' (proof bundle or evidence bundle), 'deployment artifact' (release package).
- **Category:** Process
- **Do NOT confuse with:** Never use unqualified 'artifact'. The most common ambiguity is between build artifacts and compliance artifacts.
- **Example:** ARA packaged the compliance artifact for the SOC 2 CC6 audit.

**audit**
- **Definition:** A formal examination of a system or process. Always qualify: 'compliance audit' (framework-level examination), 'security audit' (STMA threat review), 'code audit' (manual code review), 'audit trail' (chronological event log in `helios_audit_trail`).
- **Category:** Process
- **Do NOT confuse with:** Never use unqualified 'audit'. 'Audit trail' is the most common usage and refers specifically to the `helios_audit_trail` database table.
- **Example:** The compliance audit covered SOC 2 CC6 and CC7 controls.

**ARA (Autonomous Refactor Agent)**
- **Definition:** Tier 3 agent that identifies, proposes, and executes code refactors with safety proofs. Authorized to open PRs.
- **Category:** Agent
- **Do NOT confuse with:** Do NOT use 'Audit & Review' (diagram error).
- **Example:** ARA proposed a refactor to reduce cyclomatic complexity in the auth module.

**ATADA (Autonomous Test Architect & Deployment Agent)**
- **Definition:** Tier 1 agent that architects test strategies, configures CI pipelines, generates compliance test suites, and emits DORA metrics.
- **Category:** Agent
- **Do NOT confuse with:** Do NOT use 'Automated Testing Agent' or 'Automated Test Adequacy & Design Agent'.
- **Example:** ATADA generated compliance tests from the latest enforcement manifests.

**authority tier**
- **Definition:** The hierarchical level of an agent in the HELIos governance system. Tier 0 (HAA/human), Tier 1 (core authority), Tier 2 (signal/quality enforcement), Tier 3 (planning/execution), Support.
- **Category:** Architecture
- **Do NOT confuse with:** Do NOT confuse with 'autonomy tier' (ABE A/B/C), 'subscription tier' (Free/Pro), or 'architecture layer'.
- **Example:** Tier 2 agents cannot override Tier 1 decisions.

**autonomy control level**
- **Definition:** UIBGA-specific mode (0=LOCKED, 1=CONSTRAINED, 2=GUIDED, 3=OPEN) governing how strictly UI governance rules are applied.
- **Category:** Process
- **Do NOT confuse with:** Do NOT confuse with 'authority tier' or 'autonomy tier'.
- **Example:** The autonomy control level is LOCKED by default; product owner authorization is required to change it.

**autonomy tier**
- **Definition:** ABE-specific classification (A/B/C) determining how much autonomy ABE has over a bug fix. A=full autonomy, B=human approval required, C=analysis only.
- **Category:** Process
- **Do NOT confuse with:** Do NOT confuse with 'authority tier' (agent hierarchy 0-3).
- **Example:** Critical-severity bugs are always assigned autonomy tier C.

### B

**BLOCK (verdict)**
- **Definition:** The hardest release readiness verdict. Deployment is prohibited. Only HAA can override. One of three RRA verdicts: GO / HOLD / BLOCK.
- **Category:** Process
- **Do NOT confuse with:** Do NOT confuse with 'block merge' (PR action) or 'Blocked' (dependency state in exec plans).
- **Example:** RRA issued a BLOCK verdict because the compliance signal was missing.

**block merge**
- **Definition:** Action taken by an agent (AGA, STMA, DSCA) to prevent a PR from being merged. Applied via GitHub labels and review status.
- **Category:** Process
- **Do NOT confuse with:** Do NOT confuse with 'BLOCK' (RRA release verdict).
- **Example:** AGA applied block merge with the architecture-violation label.

**brand voice**
- **Definition:** Standard for how user-facing text should sound: calm, confident, clear, direct, respectful, action-oriented. Enforced by UIBGA.
- **Category:** Process
- **Example:** UIBGA flagged the error message for violating brand voice guidelines.

**burn rate**
- **Definition:** Rate of error budget consumption relative to expected pace. Levels: Normal (1x), Warning (2x), Critical (5x), Emergency (10x+).
- **Category:** Data
- **Do NOT confuse with:** Do NOT confuse with velocity or throughput.
- **Example:** The burn rate hit 5x, triggering a critical error budget alert.

### C

**CAIQ v4.1.0**
- **Definition:** Cloud Security Alliance Consensus Assessments Initiative Questionnaire, version 4.1.0. One of four compliance frameworks.
- **Category:** Compliance
- **Do NOT confuse with:** Always include version (v4.1.0) in formal references.
- **Example:** Policy alignment verified against CAIQ v4.1.0 security questionnaire responses.

**CEA (Coding Execution Agent)**
- **Definition:** Tier 3 agent that receives execution plans from PPMA and implements code changes. Operates in Cursor-Mode (interactive) or Codex-Mode (async/batch).
- **Category:** Agent
- **Do NOT confuse with:** Do NOT use 'Code Execution Agent'.
- **Example:** CEA received the execution plan and began implementation in Codex-Mode.

**CI/CD pipeline**
- **Definition:** The GitHub Actions automated workflow that runs lint, types, tests, build, and structural checks on every PR.
- **Category:** Infrastructure
- **Do NOT confuse with:** Do NOT confuse with 'HELIos pipeline' (the overall governance system).
- **Example:** The CI/CD pipeline blocked the merge due to a failing type check.

**Codex**
- **Definition:** OpenAI's async code generation and review platform. Used as CEA's batch execution environment. Accessed at chatgpt.com/codex.
- **Category:** Infrastructure
- **Do NOT confuse with:** Do NOT confuse with 'CODEX HANDOFF' (execution plan section).
- **Example:** CEA read AGENTS.md before executing the plan in Codex.

**CODEX HANDOFF**
- **Definition:** Mandatory section in execution plans produced by PPMA. Contains execution mode, instruction strictness, stop conditions, and other directives for CEA.
- **Category:** Process
- **Do NOT confuse with:** Do NOT confuse with the Codex platform itself.
- **Example:** The execution plan included a CODEX HANDOFF block with all required fields.

**compliance domain**
- **Definition:** A category within a compliance framework (e.g., SOC 2 CC6 = Logical Access, CC7 = System Operations).
- **Category:** Compliance
- **Do NOT confuse with:** Do NOT confuse with 'scoped domain' (code areas requiring manifest checks) or 'application domain' (code directories).
- **Example:** The change affects compliance domain CC6 (Logical Access Controls).

**Cortex**
- **Definition:** The predecessor system to HELIos. Referenced historically. All new work uses HELIos terminology and governance structures.
- **Category:** Architecture
- **Do NOT confuse with:** Do NOT confuse with HELIos (the current system). Cortex is deprecated.
- **Example:** The Cortex agent definitions were migrated into the HELIos agent registry.

**compliance exception**
- **Definition:** A formal deviation from an active enforcement manifest, requiring HAA approval, documented in the exception register at `/docs/compliance/exception-register.md`.
- **Category:** Compliance
- **Do NOT confuse with:** Do NOT confuse with a runtime error or software exception.
- **Example:** HAA approved a 90-day compliance exception for the pilot deployment.

**correlation ID**
- **Definition:** UUID linking all messages in a single workflow instance. Propagated across agent-to-agent communications via the Agent Communication Protocol.
- **Category:** Infrastructure
- **Do NOT confuse with:** Do NOT confuse with 'requirement trace ID' (REQ-xxx format).
- **Example:** All messages in this workflow share correlation ID c4f2e9a1-...

**CycloneDX**
- **Definition:** An open standard SBOM format for software supply chain transparency. One of two SBOM formats supported by DSCA (the other being SPDX).
- **Category:** Compliance
- **Do NOT confuse with:** Do NOT confuse with SPDX (an alternative SBOM format). Both are valid for DSCA output.
- **Example:** DSCA generated the SBOM in CycloneDX format for the Phase 4→5 gate.

**critical path**
- **Definition:** One of 6 designated system paths that must have full observability compliance: Authentication, Authorization, Payments, Data Mutation, External Integrations, Admin Actions.
- **Category:** Architecture
- **Do NOT confuse with:** Do NOT confuse with project management 'critical path'.
- **Example:** ORFA audited the Authentication critical path and found missing trace propagation.

**Cursor**
- **Definition:** Cursor IDE — the interactive development platform for agent-assisted coding. CEA operates in Cursor-Mode for interactive tasks.
- **Category:** Infrastructure
- **Example:** New feature implementation was assigned to Cursor-Mode for interactive feedback.

### D

**data classification**
- **Definition:** Four-level sensitivity taxonomy: PUBLIC, INTERNAL, CONFIDENTIAL, RESTRICTED. Managed by PDA. Determines encryption, access, retention, and handling requirements.
- **Category:** Data
- **Do NOT confuse with:** Do NOT confuse with asset classification (content-type taxonomy).
- **Example:** Customer PII is classified as CONFIDENTIAL under the data classification scheme.

**Dependabot**
- **Definition:** GitHub's automated dependency update tool. Configured by DSCA via `dependabot.yml`. Creates PRs labeled with 'dependabot' and 'needs-dsca-review'.
- **Category:** Infrastructure
- **Example:** Dependabot opened a PR to update lodash to 4.17.21.

**deployment environment**
- **Definition:** One of three runtime stages: Development, Preview (Staging), Production. Distinct from environment variables.
- **Category:** Infrastructure
- **Do NOT confuse with:** Do NOT confuse with 'environment variable' (config values) or 'runtime environment' (execution context).
- **Example:** The change was tested in the Preview deployment environment before promotion to Production.

**design doc**
- **Definition:** A structured proposal document for design decisions. Broader than an ADR. Stored at `docs/design-docs/`. Uses the `design-doc.template.md` format.
- **Category:** Process
- **Do NOT confuse with:** Do NOT confuse with 'ADR' (formal architecture decisions managed by AGA).
- **Example:** The design doc was reviewed and approved before implementation began.

**development loop**
- **Definition:** The 6-step cycle that runs continuously during Phases 2-5: Specify → Task → Execute → Gate → Merge → Validate.
- **Category:** Lifecycle
- **Do NOT confuse with:** Do NOT confuse with 'lifecycle phases' (0-6).
- **Example:** The development loop iterates until all acceptance criteria are met.

**DMA (Document Manager Agent)**
- **Definition:** Support-tier agent that manages documentation quality, freshness, and consistency across the repository.
- **Category:** Agent
- **Do NOT confuse with:** Do NOT use 'Documentation Management Agent'.
- **Example:** DMA flagged 3 stale documents during the weekly doc gardening cycle.

**doc gardening**
- **Definition:** Weekly entropy management activity where DMA reviews, updates, and verifies documentation accuracy. Executed as a Codex recurring task.
- **Category:** Process
- **Example:** The doc gardening cycle found 5 outdated API references.

**DORA metrics**
- **Definition:** Four DevOps Research and Assessment delivery performance metrics: Deployment Frequency, Lead Time for Changes, Change Failure Rate, and Time to Restore Service (MTTR).
- **Category:** Data
- **Example:** ATADA-005 emits DORA metrics after each deployment.

**drift**
- **Definition:** Divergence of actual state from intended state. Qualified by type: architectural drift (AGA), inventory drift (DSCA), documentation drift (DMA).
- **Category:** Architecture
- **Do NOT confuse with:** Always qualify with type.
- **Example:** AGA detected architectural drift in the payment module's service layer boundaries.

**DSCA (Dependency & Supply Chain Agent)**
- **Definition:** Tier 1 agent that reviews dependency changes, maintains the dependency inventory, responds to security advisories, and manages SBOM/provenance attestation.
- **Category:** Agent
- **Example:** DSCA blocked the dependency update due to a known CVE.

**DXA (Developer Experience Agent)**
- **Definition:** Tier 2 agent that detects developer friction, optimizes CI, and validates onboarding experience.
- **Category:** Agent
- **Example:** DXA reported S2-severity friction in the CI pipeline (8-minute build times).

### E

**edge function**
- **Definition:** A Supabase Edge Function — serverless Deno-based function deployed on Supabase infrastructure. Always use 'Supabase Edge Function' or 'Edge Function' (capitalized). Located at `supabase/functions/`.
- **Category:** Infrastructure
- **Do NOT confuse with:** Do NOT confuse with Vercel Edge Functions (different runtime) or generic 'serverless function'. HELIos uses Supabase Edge Functions exclusively.
- **Example:** The `create-violation` Edge Function accepts violation data from CI and inserts into the database.

**enforcement manifest**
- **Definition:** A YAML file extracting machine-parsable rules from markdown compliance policies. Located at `policies/enforcement/manifests/`. Agents must consult applicable manifests before acting on scoped domains.
- **Category:** Compliance
- **Do NOT confuse with:** Do NOT use 'compliance manifest' or 'policy manifest' as synonyms. The canonical term is 'enforcement manifest'.
- **Example:** CEA read the data-handling-enforcement.yml manifest before modifying the user profile service.

**entropy**
- **Definition:** System-level quality decay — the tendency for agent output and documentation to drift from standards over time. Managed via weekly doc gardening, tech debt tracking, and dependency scanning.
- **Category:** Process
- **Example:** Entropy management runs prevented documentation staleness across the repository.

**environment variable**
- **Definition:** A configuration value stored outside the application code (in Vercel, GitHub Secrets, or .env files). Distinct from deployment environment.
- **Category:** Infrastructure
- **Do NOT confuse with:** Do NOT confuse with 'deployment environment' (dev/staging/prod).
- **Example:** Set the SUPABASE_URL environment variable in Vercel for all deployment environments.

**error budget**
- **Definition:** The allowed failure margin for a service, calculated as 1 - SLO Target. Four policy states: Normal (>50% remaining), Caution (20-50%), Critical (0-20%), Exhausted (0%).
- **Category:** Data
- **Do NOT confuse with:** Do NOT confuse with 'burn rate' (consumption rate).
- **Example:** The error budget for API availability dropped to Caution (35% remaining).

**evidence bundle**
- **Definition:** Compliance evidence collection organized by framework, assembled by ARA for audit purposes. Distinct from 'proof bundle' (CEA per-PR evidence).
- **Category:** Compliance
- **Do NOT confuse with:** Do NOT confuse with 'proof bundle' (per-PR implementation receipt) or 'gate evidence' (phase transition attestation).
- **Example:** ARA packaged the evidence bundle for the SOC 2 CC6 audit.

**Executive Sponsor**
- **Definition:** The CTO for ObviousLogic.ai projects. Use 'Executive Sponsor (CTO)' in policy documents. Equivalent to HAA in the agent layer.
- **Category:** Role
- **Do NOT confuse with:** Do NOT use 'Executive Sponsor' and 'CTO' as separate roles.
- **Example:** Executive Sponsor (CTO) approved the governance framework and risk appetite.

**execution plan**
- **Definition:** PPMA's primary deliverable: a structured, deterministic, Codex-executable plan stored at `docs/exec-plans/active/`. Contains OBJECTIVE, SUCCESS CRITERIA, SCOPE, DEPENDENCIES, and CODEX HANDOFF sections.
- **Category:** Process
- **Example:** PPMA generated the execution plan for the user profile feature.

### F

**friction**
- **Definition:** Any impediment to developer/agent productivity, measured by DXA across five domains. Severity: S1 (Critical) through S4 (Low), mapped to the standard 4-tier scale.
- **Category:** Process
- **Example:** DXA detected S3-severity friction in the onboarding documentation.

### G

**gate**
- **Definition:** A validation checkpoint where work must pass before proceeding. Always qualify: 'CI gate' (pipeline check), 'phase gate' (lifecycle transition), 'release gate' (RRA evaluation), 'quality gate' (generic automated check).
- **Category:** Process
- **Do NOT confuse with:** Always qualify with type. Never use unqualified 'gate'.
- **Example:** The phase gate from Phase 3→4 requires all security tests to pass.

**GO (verdict)**
- **Definition:** Positive release readiness verdict. All input signals present and satisfactory. Deployment may proceed.
- **Category:** Process
- **Do NOT confuse with:** Do NOT confuse with informal usage of 'go' (proceed).
- **Example:** RRA issued a GO verdict — all 8 input signals were satisfactory.

**golden signals**
- **Definition:** The four observability signals per Google SRE principles: Latency, Traffic, Errors, Saturation. Governance owned by SOA.
- **Category:** Data
- **Do NOT confuse with:** ORFA monitors the same signals but calls the Traffic signal 'Throughput'.
- **Example:** SOA validated golden signal instrumentation for the payment service.

### H

**HAA (Human Approval Authority)**
- **Definition:** Tier 0 — the human override authority for the HELIos pipeline. Daniel DeZago, CTO, ObviousLogic.ai. Final arbiter for all escalations, compliance exceptions, and BLOCK overrides.
- **Category:** Agent
- **Do NOT confuse with:** Do NOT use 'Human Approval Agent'. In policy documents, equivalent to 'Executive Sponsor (CTO)'.
- **Example:** HAA approved the compliance exception for the pilot deployment.

**HELIos**
- **Definition:** The portable, drop-in operating system for agent-first software development. The overarching governance/agent/compliance/lifecycle system. Folder name in repository: `helios/`.
- **Category:** Architecture
- **Do NOT confuse with:** Do NOT confuse with the CI/CD pipeline (a component of HELIos). Capitalization: use 'HELIos' in documentation.
- **Example:** HELIos provisions the governance, agents, configurations, and compliance infrastructure.

**HELIos pipeline**
- **Definition:** The entire HELIos system operating as a development pipeline. Encompasses all agents, SOPs, policies, and lifecycle phases.
- **Category:** Architecture
- **Do NOT confuse with:** Do NOT confuse with 'CI/CD pipeline' (GitHub Actions workflows only).
- **Example:** The HELIos pipeline ensures every project benefits from standardized governance.

**HIPAA Security Rule**
- **Definition:** Health Insurance Portability and Accountability Act Security Rule (45 CFR 164.302-164.318). Governs PHI safeguards. Abbreviated as HIPAA in framework references.
- **Category:** Compliance
- **Do NOT confuse with:** The full HIPAA includes Privacy Rule and Breach Notification Rule — specify which rule when citing specific requirements.
- **Example:** PDA enforces HIPAA Security Rule technical safeguards for all PHI-adjacent data.

**HOLD (verdict)**
- **Definition:** Middle release readiness verdict. Issues identified but believed to be resolvable within a reasonable timeframe. Release is paused, not permanently blocked.
- **Category:** Process
- **Do NOT confuse with:** Do NOT confuse with 'BLOCK' (permanent until HAA override).
- **Example:** RRA issued a HOLD — the dependency audit signal was missing but expected within 4 hours.

### I

**idempotency key**
- **Definition:** A deterministic identifier used to prevent duplicate processing. Used at three levels: message envelope, workflow automation, and deployment session.
- **Category:** Infrastructure
- **Example:** The idempotency key prevented the deployment step from executing twice.

**infrastructure**
- **Definition:** The underlying systems that support application execution: databases (Supabase), hosting (Vercel), CI/CD (GitHub Actions), MCP servers. Distinct from 'platform' (the SaaS tools themselves).
- **Category:** Architecture
- **Do NOT confuse with:** Do NOT confuse with 'platform' (external SaaS tool) or 'resource' (a component within infrastructure).
- **Example:** The infrastructure layer consists of Supabase (database), Vercel (hosting), and GitHub Actions (CI/CD).

**instance**
- **Definition:** A running copy of a system component. Always qualify: 'Supabase instance' (database project), 'agent instance' (a running agent execution), 'PIA instance' (one PIA per monitored platform).
- **Category:** Infrastructure
- **Do NOT confuse with:** Never use unqualified 'instance'. Do NOT confuse with 'resource' (a managed object within an instance).
- **Example:** Each monitored platform has its own PIA instance (PIA-GH, PIA-LI, etc.).

### L

**lifecycle phase**
- **Definition:** One of 7 numbered phases of the HELIos development lifecycle: Phase 0 (Setup), Phase 1 (Knowledge Base), Phase 2 (Scaffold & CI), Phase 3 (Feature Development), Phase 4 (Quality & Entropy), Phase 5 (Testing & Iteration), Phase 6 (Retrospective).
- **Category:** Lifecycle
- **Do NOT confuse with:** Do NOT confuse with WHATS_NEXT roadmap stages (1-10) or SOP template implementation phases.
- **Example:** The project is currently in Phase 3 (Feature Development).

**Linear**
- **Definition:** The issue tracking and project management platform used for sprint management, bug tracking, and work coordination.
- **Category:** Infrastructure
- **Do NOT confuse with:** Linear uses 'Cycles' for time-boxed iterations — HELIos calls these 'sprints'.
- **Example:** PPMA created 3 Linear issues for the execution plan tasks.

### M

**MCP (Model Context Protocol)**
- **Definition:** Protocol providing AI agents with real-time access to databases, repos, and issue trackers via MCP servers. Each platform has its own MCP server.
- **Category:** Infrastructure
- **Example:** CEA used the GitHub MCP to read the repository structure.

**migration**
- **Definition:** A controlled change to a system's structure or data. Always qualify: 'schema migration' (Supabase database DDL change, stored at `supabase/migrations/`), 'data migration' (moving data between systems), 'platform migration' (changing from one SaaS tool to another).
- **Category:** Infrastructure
- **Do NOT confuse with:** Never use unqualified 'migration'. The most common usage in HELIos is 'schema migration' (Supabase).
- **Example:** The schema migration added RLS policies to all user-facing tables.

**MTTR (Mean Time to Restore)**
- **Definition:** Average time from incident detection to service restoration. One of four DORA metrics. Expanded as 'Time to Restore Service'.
- **Category:** Data
- **Do NOT confuse with:** Some contexts expand MTTR as 'Mean Time to Repair' or 'Mean Time to Recovery' — HELIos uses 'Restore'.
- **Example:** MTTR for the API gateway incident was 45 minutes.

### N

**NIST SP 800-53**
- **Definition:** National Institute of Standards and Technology Special Publication 800-53 — security and privacy controls catalog. One of four compliance frameworks. Always include 'SP' prefix.
- **Category:** Compliance
- **Do NOT confuse with:** Do NOT confuse with NIST CSF (Cybersecurity Framework) — a different NIST publication.
- **Example:** The access control policy maps to NIST SP 800-53 AC-2 and AC-6.

### O

**ORFA (Observability & Runtime Feedback Agent)**
- **Definition:** Tier 2 agent that ensures runtime observability compliance, manages critical path audits, configures runtime signals, and coordinates incident response.
- **Category:** Agent
- **Do NOT confuse with:** Do NOT use 'Observability & Reliability Feedback Agent' or 'Ops & Reliability'.
- **Example:** ORFA issued a BLOCK signal because the payments critical path lacked trace propagation.

**OSCAL (Open Security Controls Assessment Language)**
- **Definition:** A machine-readable format for security control documentation, assessment plans, and assessment results. Used for automated compliance documentation.
- **Category:** Compliance
- **Example:** Compliance artifacts are structured in OSCAL format for automated audit processing.

### P

**PDA (Privacy & Data Protection Agent)**
- **Definition:** Tier 2 agent that enforces data classification, manages privacy impact assessments, and ensures HIPAA/SOC 2 data handling compliance.
- **Category:** Agent
- **Do NOT confuse with:** Do NOT use 'Performance & Data Agent'.
- **Example:** PDA classified the customer health records as RESTRICTED.

**PGA (Process Governance Analyst)**
- **Definition:** Tier 2 agent that reviews SOP currency, validates cross-reference integrity, assesses platform change impacts, and onboards new platforms.
- **Category:** Agent
- **Do NOT confuse with:** Do NOT use 'Policy Governance Agent'.
- **Example:** PGA identified 3 broken cross-references during the monthly SOP review.

**phase gate**
- **Definition:** A governance checkpoint at lifecycle phase transitions (e.g., Phase 3→4, Phase 4→5). Requires evidence bundle and passing compliance checks.
- **Category:** Lifecycle
- **Do NOT confuse with:** Do NOT confuse with 'CI gate' (pipeline check on every PR).
- **Example:** The Phase 4→5 gate requires a complete SBOM and passing security attestation.

**PHI (Protected Health Information)**
- **Definition:** Health information subject to HIPAA safeguards. Higher sensitivity than PII. Includes data that could indirectly identify individuals ('PHI-adjacent').
- **Category:** Data
- **Do NOT confuse with:** PHI is a subset of sensitive data, not a synonym for PII.
- **Example:** PHI-adjacent data elements must be tagged as CONFIDENTIAL at minimum.

**PIA (Platform Intelligence Agent)**
- **Definition:** Tier 2 agent that monitors external platform changes, generates Platform Intelligence Briefs, and manages platform-specific knowledge. One PIA instance per monitored platform.
- **Category:** Agent
- **Example:** PIA-GH detected a breaking change in the GitHub Actions runner version.

**PII (Personally Identifiable Information)**
- **Definition:** Data that can identify an individual. Must be classified as CONFIDENTIAL or RESTRICTED. Must never appear in log messages.
- **Category:** Data
- **Do NOT confuse with:** Do NOT confuse with PHI (health information — higher sensitivity).
- **Example:** PII fields must be encrypted at rest and redacted from all log output.

**pipeline**
- **Definition:** Always qualify: 'HELIos pipeline' (the overall system), 'CI/CD pipeline' (GitHub Actions), or 'Notion changelog pipeline'. Never use unqualified 'pipeline'.
- **Category:** Architecture
- **Do NOT confuse with:** The most common ambiguity in the corpus. Always qualify.
- **Example:** The CI/CD pipeline runs lint, types, tests, build on every PR.

**platform**
- **Definition:** An external SaaS tool in the HELIos technology stack: GitHub, Linear, Notion, Lovable, Vercel, Supabase, Cursor, Codex, Figma.
- **Category:** Infrastructure
- **Do NOT confuse with:** Do NOT use 'platform' to mean HELIos itself.
- **Example:** PIA monitors 10 platforms for breaking changes.

**plan**
- **Definition:** A structured document guiding future actions. Always qualify: 'execution plan' (PPMA's primary deliverable for CEA), 'remediation plan' (steps to fix a violation or gap), 'rollback plan' (steps to revert a failed deployment), 'test plan' (ATADA's test strategy). The canonical unqualified 'plan' in HELIos context means 'execution plan'.
- **Category:** Process
- **Do NOT confuse with:** Do NOT confuse 'execution plan' (machine-executable PPMA artifact) with 'remediation plan' (human-readable fix steps).
- **Example:** PPMA generated the execution plan and handed it off to CEA via SOP-PPMA-003.

**production environment**
- **Definition:** The live deployment environment serving end users. One of three deployment environments: Development, Preview (Staging), Production. All changes to the production environment must go through the change management process.
- **Category:** Infrastructure
- **Do NOT confuse with:** Do NOT use 'production' to mean the production deployment environment AND the act of producing output. In deployment contexts, always means the live environment.
- **Example:** All configuration changes to the production environment require documented approval.

**provisioning**
- **Definition:** The process of creating accounts, assigning roles, and granting access to systems and data. Requires documented approval via ticketing system. Privileged accounts require manager or supervisor approval.
- **Category:** Process
- **Do NOT confuse with:** Do NOT confuse with 'deprovisioning' (revoking access). Together they form the account lifecycle.
- **Example:** Provisioning of the new developer account was completed within the 24-hour SLA.

**PPMA (Premiere Project Manager Agent)**
- **Definition:** Tier 3 agent that generates execution plans, manages sprints, sequences tasks, and produces CODEX HANDOFF blocks for CEA.
- **Category:** Agent
- **Do NOT confuse with:** Do NOT abbreviate to 'Project Manager Agent' (drops 'Premiere').
- **Example:** PPMA generated a 3-phase execution plan for the dashboard feature.

**proof bundle**
- **Definition:** Four-part evidence package required for every PR before merge, assembled by CEA: requirement trace, implementation summary, test results, governance compliance.
- **Category:** Process
- **Do NOT confuse with:** Do NOT confuse with 'evidence bundle' (ARA compliance audit artifact).
- **Example:** CEA attached the proof bundle to the PR before requesting review.

### Q

**QMSA (Quality Metrics & SLO Agent)**
- **Definition:** Tier 2 agent that defines quality standards, manages SLO definitions (quality dimension), enforces quality model gates, and tracks error budget burn rates.
- **Category:** Agent
- **Do NOT confuse with:** SLO quality metrics are QMSA's domain. Runtime SLO enforcement is SOA's domain.
- **Example:** QMSA flagged the reliability SLO as approaching the Caution threshold.

### R

**RBAC (Role-Based Access Control)**
- **Definition:** Access control model where permissions are assigned to roles, and users are assigned to roles — not directly to resources. Required for all cloud services in HELIos policy.
- **Category:** Infrastructure
- **Do NOT confuse with:** Do NOT confuse with ACL (which assigns permissions directly to identities). RBAC is the mandatory model; ACLs are deprecated.
- **Example:** All Supabase access is governed by RBAC — users are assigned to roles, not directly to tables.

**REA (Requirements Engineering Agent)**
- **Definition:** Tier 2 agent that normalizes requirements, assigns requirement trace IDs (REQ-xxx format), and manages the traceability matrix.
- **Category:** Agent
- **Do NOT confuse with:** Do NOT use 'Reliability Engineering Agent' (reasoning guide error).
- **Example:** REA assigned trace ID REQ-CRX-0042 to the new user authentication requirement.

**resource**
- **Definition:** A broad term for anything consumed, allocated, or managed within a platform or infrastructure layer. Always qualify: 'cloud resource' (Supabase/Vercel/GitHub provisioned items), 'compute resource' (CPU/memory), 'IAM resource' (identity/role/policy), 'API resource' (REST endpoint or entity), 'access resource' (permission target — database, storage bucket, API key). When unqualified in policy documents, typically means cloud resource.
- **Category:** Infrastructure
- **Do NOT confuse with:** Do NOT confuse with 'asset' (tracked organizational items with unique IDs and owners), 'component' (application building blocks), 'platform' (the SaaS tool itself), or 'instance' (a running copy).
- **Example:** Use IAM roles to manage access to cloud storage resources.

**remediation**
- **Definition:** The process of addressing and resolving a security finding, vulnerability, policy violation, or audit gap. Includes root cause analysis, fix implementation, and verification. Distinct from 'compensating control' (temporary alternative) and 'exception' (formal waiver).
- **Category:** Process
- **Do NOT confuse with:** Do NOT confuse with 'patch' (a specific code change) or 'compensating control' (an alternative measure, not a fix).
- **Example:** The vulnerability remediation was completed within the 72-hour SLA for High severity findings.

**release candidate**
- **Definition:** The assembled artifact evaluated by RRA before production deployment. Includes all code changes, documentation updates, and compliance evidence.
- **Category:** Process
- **Example:** RRA began evaluation of the release candidate after all 8 input signals were collected.

**request trace ID**
- **Definition:** A UUID identifying a request across services in distributed tracing. Used by ORFA. Field name: `trace_id`.
- **Category:** Infrastructure
- **Do NOT confuse with:** Do NOT confuse with 'requirement trace ID' (REQ-xxx format used by REA).
- **Example:** The request trace ID propagated across all microservice hops.

**requirement trace ID**
- **Definition:** Unique identifier for requirements in format REQ-{project_code}-{sequence}. Assigned by REA. Stored in the requirement register.
- **Category:** Process
- **Do NOT confuse with:** Do NOT confuse with 'request trace ID' (UUID for distributed tracing).
- **Example:** REQ-CRX-0042 traces from the product spec through implementation to test coverage.

**review**
- **Definition:** A formal evaluation of an artifact against criteria. Always qualify: 'code review' (PR-level review by agents or humans), 'architecture review' (AGA structural evaluation per SOP-AGA-002), 'security review' (STMA PR review per SOP-STMA-003), 'SOP review' (PGA process audit), 'release review' (RRA evaluation).
- **Category:** Process
- **Do NOT confuse with:** Never use unqualified 'review'. Each review type has a different owning agent and SOP.
- **Example:** AGA completed the architecture review and issued an Approved verdict.

**RLS (Row-Level Security)**
- **Definition:** Supabase database-level access control mechanism. Constitutional requirement: must be enabled on ALL tables with user data.
- **Category:** Infrastructure
- **Example:** RLS policies enforce per-user data isolation in the profiles table.

**RRA (Release Readiness Agent)**
- **Definition:** Tier 1 agent that evaluates release candidates against 8 input signals and issues GO/HOLD/BLOCK verdicts.
- **Category:** Agent
- **Example:** RRA collected all 8 input signals and issued a GO verdict.

### S

**secret**
- **Definition:** A sensitive credential stored outside application code. Always qualify: 'environment secret' (GitHub Actions secret or Vercel env var), 'API key' (platform-specific auth token), 'database credential' (Supabase connection string), 'signing key' (cryptographic key for JWT or SBOM attestation).
- **Category:** Infrastructure
- **Do NOT confuse with:** Do NOT confuse with 'token' (runtime auth mechanism) or 'environment variable' (may or may not contain secrets).
- **Example:** API keys are stored as environment secrets in GitHub Actions and Vercel.

**safety proof**
- **Definition:** Four mandatory verification checks before any refactor by ARA: Test Coverage Verification, Behavioral Equivalence Check, Architectural Rule Compliance, Security Assumption Preservation.
- **Category:** Process
- **Example:** ARA's safety proof passed all four checks for the service layer refactor.

**SBOM (Software Bill of Materials)**
- **Definition:** Supply chain manifest listing all build dependencies. Generated by DSCA in SPDX or CycloneDX format.
- **Category:** Compliance
- **Example:** DSCA generated the SBOM in CycloneDX format for the Phase 4→5 gate.

**scoped domain**
- **Definition:** A code area where enforcement manifests must be consulted before making changes: authentication, authorization, data handling, encryption, logging, PHI/PII, key management.
- **Category:** Compliance
- **Do NOT confuse with:** Do NOT confuse with 'compliance domain' (framework categories) or 'application domain' (code directories).
- **Example:** The change touches the encryption scoped domain — read the encryption enforcement manifest first.

**server**
- **Definition:** A computing system that provides services to other systems or users. Always qualify when context is ambiguous: 'MCP server' (Model Context Protocol integration — e.g., GitHub MCP, Linear MCP), 'database server' (Supabase PostgreSQL instance), 'edge server' (Vercel edge runtime), 'application server' (backend compute). In configuration management policies, refers to any compute asset requiring a configuration baseline. In HELIos's cloud-native context, does NOT typically mean a physical rack-mounted machine.
- **Category:** Infrastructure
- **Do NOT confuse with:** Do NOT confuse with 'platform' (the SaaS product that hosts servers), 'service' (an application-level abstraction), or 'instance' (a running copy). The most common usage in SOPs is 'MCP server'; the most common in policies is 'compute asset'.
- **Example:** CEA used the GitHub MCP server to read the repository structure.

**Security Lead**
- **Definition:** The person responsible for the security program: maintains the security program, oversees access governance, maintains the approved AI tools list.
- **Category:** Role
- **Do NOT confuse with:** Do NOT confuse with STMA (the agent).
- **Example:** Security Lead approved the quarterly access review results.

**self-review loop**
- **Definition:** Pre-PR process where an agent reviews its own output against AGENTS.md: review changes, run lints/tests, verify no compliance violations, iterate until clean.
- **Category:** Process
- **Example:** CEA ran the self-review loop 3 times before convergence.

**service**
- **Definition:** An application-level abstraction that provides specific functionality. Always qualify when context is ambiguous: 'cloud service' (a SaaS/PaaS offering like Supabase Auth), 'application service' (a backend module or function), 'edge service' (Supabase Edge Function or Vercel serverless function).
- **Category:** Architecture
- **Do NOT confuse with:** Do NOT confuse with 'server' (the compute system hosting a service), 'platform' (the SaaS product), or 'component' (a UI building block).
- **Example:** The authentication service handles all user login and session management.

**service account**
- **Definition:** A non-interactive system identity used for automated processes, CI/CD pipelines, and service-to-service communication. Exempt from MFA requirements. Credentials must be stored in the approved credential management tool, never shared with humans.
- **Category:** Infrastructure
- **Do NOT confuse with:** Do NOT confuse with 'user account' (an interactive human identity) or 'shared account' (prohibited for production access).
- **Example:** The CI pipeline uses a service account with scoped permissions to deploy to Vercel.
- **Definition:** Pre-PR process where an agent reviews its own output against AGENTS.md: review changes, run lints/tests, verify no compliance violations, iterate until clean.
- **Category:** Process
- **Example:** CEA ran the self-review loop 3 times before convergence.

**severity**
- **Definition:** Four-level classification for issues: Critical (blocks deployment), High (blocks merge), Medium (requires review), Low (warning only). All agents must use this scale.
- **Category:** Process
- **Do NOT confuse with:** DXA uses S1/S2/S3/S4 internally — map S1=Critical, S2=High, S3=Medium, S4=Low in all cross-agent communications.
- **Example:** The vulnerability was classified as High severity with a 48-hour remediation SLA.

**signal**
- **Definition:** A data point consumed by an agent to make a decision. Always qualify: 'observability signal' (ORFA runtime metrics — golden signals), 'release signal' (one of RRA's 8 input signals), 'quality signal' (QMSA metric), 'compliance signal' (enforcement manifest check result). Tier 2 agents are "Signal and Quality Enforcement" agents — they produce signals consumed by Tier 1.
- **Category:** Process
- **Do NOT confuse with:** Do NOT confuse with 'alert' (a triggered notification) or 'flag' (a non-blocking warning).
- **Example:** RRA requires 8 input signals before issuing a release verdict.

**SLA (Service Level Agreement)**
- **Definition:** A contractual commitment to a customer defining service availability, performance, and support response times. Distinct from SLO (an internal reliability target).
- **Category:** Data
- **Do NOT confuse with:** Do NOT confuse with SLO (internal target, not contractual). SLOs should be stricter than SLAs to provide a buffer.
- **Example:** The SLA guarantees 99.5% uptime; the internal SLO targets 99.9%.

**SLO (Service Level Objective)**
- **Definition:** A target reliability level for a measurable SLI (Service Level Indicator), with an associated error budget and measurement window.
- **Category:** Data
- **Do NOT confuse with:** Do NOT confuse with SLA (contractual obligation to a customer).
- **Example:** The API availability SLO is 99.9% measured over a 30-day rolling window.

**SOA (SLO & Observability Agent)**
- **Definition:** Support-tier agent that manages runtime SLOs, golden signal governance, error budget enforcement, and SLO readiness certification.
- **Category:** Agent
- **Do NOT confuse with:** Runtime SLO enforcement is SOA's domain. Quality SLO metrics are QMSA's domain.
- **Example:** SOA triggered a deployment freeze recommendation because the error budget was exhausted.

**SOC 2 Type II**
- **Definition:** System and Organization Controls 2 Type II audit framework. Trust Services Criteria CC1-CC9 plus Confidentiality, Privacy, Availability.
- **Category:** Compliance
- **Do NOT confuse with:** Always write 'SOC 2' (with space) in prose. Use 'SOC2' (no space) only in framework reference IDs.
- **Example:** SOC 2 CC6 controls are enforced via RLS and the access control enforcement manifest.

**SOP (Standard Operating Procedure)**
- **Definition:** A formal process document governing agent behavior. Managed by PGA. Follows the standard 10-section format.
- **Category:** Process
- **Example:** SOP-AGA-001 defines the ADR creation and management process.

**sprint**
- **Definition:** A time-boxed development iteration (1-2 weeks). Managed in Linear. Linear's native term is 'Cycle' — HELIos uses 'sprint'.
- **Category:** Process
- **Do NOT confuse with:** Do NOT use 'cycle' or 'iteration' as synonyms in HELIos documentation.
- **Example:** PPMA planned 12 story points for the current sprint.

**SSC**
- **Definition:** SSC is ObviousLogic.ai — the internal/legal entity name used throughout policy documents. SSC and ObviousLogic.ai refer to the same organization. Use 'SSC' in policy and compliance documents; use 'ObviousLogic.ai' in product-facing and external contexts.
- **Category:** Organization
- **Do NOT confuse with:** SSC and ObviousLogic.ai are the same entity. Do NOT treat them as separate organizations.
- **Example:** All SSC employees must complete security awareness training annually.

**SPDX (Software Package Data Exchange)**
- **Definition:** An open standard format for communicating software bill of materials (SBOM) information. One of two SBOM formats supported by DSCA (the other being CycloneDX).
- **Category:** Compliance
- **Do NOT confuse with:** Do NOT confuse with CycloneDX (an alternative SBOM format). Both are valid for DSCA output.
- **Example:** DSCA generated the SBOM in SPDX format for the external audit.

**STMA (Security & Threat Modeling Agent)**
- **Definition:** Tier 1 agent that maintains the threat model, generates abuse cases, performs security PR reviews, and conducts agentic LLM security assessments.
- **Category:** Agent
- **Do NOT confuse with:** Do NOT use 'Security Compliance' (phantom name).
- **Example:** STMA applied the security-violation label after finding an unmitigated injection risk.

**STRIDE**
- **Definition:** Threat classification model: Spoofing, Tampering, Repudiation, Information Disclosure, Denial of Service, Elevation of Privilege. Used by STMA for threat model analysis.
- **Category:** Compliance
- **Example:** STMA classified the injection risk under the Tampering category of the STRIDE model.

**SLSA (Supply-chain Levels for Software Artifacts)**
- **Definition:** A security framework for ensuring the integrity of software artifacts throughout the supply chain. Provides graduated levels of assurance.
- **Category:** Compliance
- **Example:** The build pipeline meets SLSA Level 2 requirements for provenance attestation.

**stop condition**
- **Definition:** A situation where an agent must halt and escalate. Each agent defines its own stop conditions. CEA stops immediately on any test failure.
- **Category:** Process
- **Do NOT confuse with:** Do NOT confuse with STOP verdict or BLOCK verdict.
- **Example:** CEA hit a stop condition when the build failed on the third iteration.

**system**
- **Definition:** A broad term for any combination of hardware, software, and data that provides a capability. Always qualify when precision is needed: 'production system' (live deployed application), 'SSC system' (any system under organizational management), 'HELIos system' (the governance framework). When used in policy documents without qualification, typically means any SSC-managed IT system.
- **Category:** Infrastructure
- **Do NOT confuse with:** Do NOT use 'system' when you mean a specific server, service, or platform. Qualify whenever the specific meaning matters.
- **Example:** All SSC systems must enforce role-based access control.

**System Owner**
- **Definition:** The designated person accountable for a specific system's access roles, approval requirements, and security posture. Responsible for defining who can access the system and under what conditions.
- **Category:** Role
- **Do NOT confuse with:** Do NOT confuse with 'Data Steward' (responsible for data, not the system) or 'Manager' (responsible for people, not systems).
- **Example:** The System Owner for the customer portal approved the new access role definition.

### T

**table**
- **Definition:** A structured data store. Always qualify: 'database table' (Supabase PostgreSQL table — e.g., `helios_agents`), 'decision table' (structured rule lookup, often in markdown), 'lookup table' (reference data for UI display).
- **Category:** Infrastructure
- **Do NOT confuse with:** When unqualified in HELIos context, 'table' means a Supabase database table. For markdown tables in documentation, use 'reference table' or 'decision table'.
- **Example:** The `helios_agents` database table stores all 20 agent definitions with RLS enabled.

**tier**
- **Definition:** Always qualify: 'authority tier' (agent hierarchy), 'autonomy tier' (ABE A/B/C), 'subscription tier' (platform plan), 'environment tier' (deployment classification). Never use unqualified.
- **Category:** Architecture
- **Do NOT confuse with:** Most overloaded term in the corpus.
- **Example:** Authority tier 1 agents have override power over tier 2 and tier 3 agents.

**TLS (Transport Layer Security)**
- **Definition:** Cryptographic protocol for securing data in transit. HELIos requires TLS 1.2 minimum for all data in transit.
- **Category:** Infrastructure
- **Example:** All API communications use TLS 1.2 or higher.

**token**
- **Definition:** A credential used for runtime authentication or authorization. Always qualify: 'auth token' (Supabase JWT session token), 'API token' (platform Personal Access Token — e.g., GitHub PAT, Linear API key), 'CSRF token' (cross-site request forgery protection). Stored as secrets, not in code.
- **Category:** Infrastructure
- **Do NOT confuse with:** Do NOT confuse with 'secret' (the storage mechanism) or 'API key' (a type of token). 'Token' refers to the credential itself; 'secret' refers to how it is stored.
- **Example:** The GitHub API token is stored as a GitHub Actions secret and used by the CI/CD pipeline.

### U

**UIBGA (UX/Brand Governor Agent)**
- **Definition:** Support-tier agent that enforces UX behavior, UI structure, brand voice, naming conventions, and visual consistency.
- **Category:** Agent
- **Example:** UIBGA blocked the UI proposal due to a fundamental naming violation.

### V

**validate**
- **Definition:** To confirm that inputs or data meet defined correctness criteria. Use for input checking and data quality.
- **Category:** Process
- **Do NOT confuse with:** Do NOT confuse with 'verify' (compliance checks) or 'enforce' (blocking actions).
- **Example:** CEA validates all inputs against the execution plan checklist.

**verdict**
- **Definition:** A formal decision issued by RRA after release readiness evaluation: GO (deploy), HOLD (pause), BLOCK (prohibit). Only HAA can override BLOCK.
- **Category:** Process
- **Do NOT confuse with:** Do NOT use for informal decisions.
- **Example:** The verdict was GO — all signals passed.

**verify**
- **Definition:** To confirm that an artifact or process complies with a governance rule or standard. Use for compliance and governance checks.
- **Category:** Process
- **Do NOT confuse with:** Do NOT confuse with 'validate' (input correctness) or 'enforce' (blocking actions).
- **Example:** AGA verified the change is consistent with ADR-017.

**VPN (Virtual Private Network)**
- **Definition:** An encrypted network tunnel required for remote access to SSC data and systems. MFA is required in conjunction with VPN access.
- **Category:** Infrastructure
- **Example:** Remote access to the production database requires both VPN and MFA.

### W

**WAF (Web Application Firewall)**
- **Definition:** A security appliance or service that filters and monitors HTTP traffic to web applications. Required for all production web applications. Must include IP reputation lists and known-bad-input rule sets.
- **Category:** Infrastructure
- **Example:** The WAF blocked a SQL injection attempt targeting the login endpoint.

**webhook**
- **Definition:** An HTTP callback triggered by a platform event. Used for: GitHub webhook (PR events → CI triggers), Linear webhook (issue state changes → Notion sync), Supabase webhook (database changes → Edge Function triggers).
- **Category:** Infrastructure
- **Do NOT confuse with:** Do NOT confuse with 'MCP server' (bidirectional tool integration) or 'API endpoint' (request-response pattern). Webhooks are event-driven push notifications.
- **Example:** The GitHub webhook triggers the compliance-gate workflow on every PR event.

**wave**
- **Definition:** A commit grouping in the HELIos deployment sequence: Wave 1 (Reliability Core), Wave 2 (Resilience & Operations), Wave 3 (Governance/Automation/Observability), Wave 4 (Pilot & Hardening).
- **Category:** Lifecycle
- **Do NOT confuse with:** Do NOT confuse with lifecycle phases (0-6) or roadmap stages.
- **Example:** Wave 2 commits cover resilience patterns and operational playbooks.

**WCAG (Web Content Accessibility Guidelines)**
- **Definition:** W3C standard for web accessibility. Used by UIBGA to enforce accessibility requirements in UI governance reviews.
- **Category:** Compliance
- **Example:** UIBGA flagged the modal component for failing WCAG 2.1 AA contrast requirements.

---

## Synonym Resolution Table

Map every deprecated variant to its canonical replacement. All documents must use the canonical term.

| Deprecated Term | Canonical Term | Notes |
|---|---|---|
| Architecture Sentinel | Architecture Guardian Agent (AGA) | Phantom name — does not exist |
| Technical Authority | HAA or AGA (context-dependent) | Phantom name — clarify per context |
| Security Compliance | STMA (Security & Threat Modeling Agent) | Phantom name in ARA interaction table |
| CI/Quality Gate | ATADA + QMSA | Phantom entity conflating two agents |
| CORE | HAA or AGA | Phantom name in DXA SOPs — resolve to correct agent |
| SAGE | AGA (Architecture Guardian Agent) | Phantom name in DXA SOPs |
| AI Build Engine (ABE) | AI Bug Evaluation Agent (ABE) | Incorrect name in SDLC role map |
| Automated Bug Eliminator (ABE) | AI Bug Evaluation Agent (ABE) | Incorrect name in memory-architecture.md |
| Reliability Engineering Agent (REA) | Requirements Engineering Agent (REA) | Incorrect name in reasoning-model-guide.md |
| Automated Gate Agent (AGA) | Architecture Guardian Agent (AGA) | Incorrect name in reasoning-model-guide.md |
| Performance & Data Agent (PDA) | Privacy & Data Protection Agent (PDA) | Incorrect name in reasoning-model-guide.md |
| Human Approval Agent (HAA) | Human Approval Authority (HAA) | Incorrect name in reasoning-model-guide.md |
| Code Execution Agent (CEA) | Coding Execution Agent (CEA) | Minor variant — standardize |
| Documentation Management Agent (DMA) | Document Manager Agent (DMA) | Minor variant — standardize |
| Policy Governance Agent (PGA) | Process Governance Analyst (PGA) | Name conflict in compliance docs |
| compliance manifest | enforcement manifest | Use canonical term |
| policy manifest | enforcement manifest | Use canonical term |
| halt (as agent stop) | stop (stop condition) | Use 'stop condition' for agent halt triggers |
| cycle (time-boxed iteration) | sprint | HELIos uses 'sprint', not Linear's 'cycle' |
| iteration | sprint | Standardize on 'sprint' |
| SOC2 (no space) | SOC 2 (with space) | Use 'SOC 2' in prose; 'SOC2' only in framework reference IDs |
| NIST 800-53 (without SP) | NIST SP 800-53 | Always include 'SP' prefix |
| Helios (lowercase h) | HELIos | Use branded capitalization |
| Project Manager Agent (PPMA) | Premiere Project Manager Agent (PPMA) | Include 'Premiere' in full name |
| Test Architect (ATADA) | Autonomous Test Architect & Deployment Agent (ATADA) | Use full name or abbreviation |
| Platform Intelligence Analyst (PIA) | Platform Intelligence Agent (PIA) | Incorrect name in governance framework |
| IT/Operations | IT Operations | Standardize — no slash |
| production environment (unqualified) | Production deployment environment | Use 'deployment environment' terminology |
| non-production environment | Development or Preview deployment environment | Specify which deployment environment |
| test environment | Development deployment environment or Preview deployment environment | Use specific deployment environment name |
| dev environment | Development deployment environment | Use canonical deployment environment name |

---

## Compliance Framework Reference

| Framework | Abbreviation | Version | Scope |
|---|---|---|---|
| SOC 2 Type II | SOC2 | Trust Services Criteria CC1-CC9 | Security, availability, processing integrity, confidentiality, privacy |
| HIPAA Security Rule | HIPAA | 45 CFR 164.302-164.318 | Protected Health Information safeguards (admin, physical, technical) |
| NIST SP 800-53 | NIST | Rev. 5 (current) | Security and privacy controls catalog |
| CAIQ v4.1.0 | CAIQ | v4.1.0 | Cloud Security Alliance security questionnaire |

---

## Agent Quick Reference

Complete roster of all 20 HELIos agents.

| # | Full Name | Abbr | Tier | Can Block? | Primary Domain |
|---|---|---|---|---|---|
| 1 | Human Approval Authority | HAA | 0 | Yes (final) | Human governance override |
| 2 | Release Readiness Agent | RRA | 1 | Yes | Release verdicts (GO/HOLD/BLOCK) |
| 3 | Architecture Guardian Agent | AGA | 1 | Yes | Architecture, ADR management |
| 4 | Security & Threat Modeling Agent | STMA | 1 | Yes | Threat models, security PR review |
| 5 | Autonomous Test Architect & Deployment Agent | ATADA | 1 | Yes | Test strategy, CI pipeline, DORA |
| 6 | Dependency & Supply Chain Agent | DSCA | 1 | Yes | Dependencies, SBOM, advisories |
| 7 | Quality Metrics & SLO Agent | QMSA | 2 | Yes | Quality metrics, SLO definitions |
| 8 | Observability & Runtime Feedback Agent | ORFA | 2 | Yes | Runtime observability, incidents |
| 9 | Developer Experience Agent | DXA | 2 | Yes (limited) | Developer friction, CI optimization |
| 10 | Process Governance Analyst | PGA | 2 | No | SOP review, cross-reference integrity |
| 11 | Platform Intelligence Agent | PIA | 2 | No | Platform change monitoring |
| 12 | Requirements Engineering Agent | REA | 2 | Yes | Requirements, traceability |
| 13 | Privacy & Data Protection Agent | PDA | 2 | Yes | Data classification, HIPAA/privacy |
| 14 | Premiere Project Manager Agent | PPMA | 3 | No | Execution plans, sprint management |
| 15 | Coding Execution Agent | CEA | 3 | No | Code implementation, self-review |
| 16 | Autonomous Refactor Agent | ARA | 3 | No | Refactoring, safety proofs, evidence |
| 17 | AI Bug Evaluation Agent | ABE | 3 | No | Bug triage, auto-fix (Tier A/B/C) |
| 18 | Document Manager Agent | DMA | Support | Yes (docs) | Documentation quality, freshness |
| 19 | UX/Brand Governor Agent | UIBGA | Support | Yes (UI) | UI governance, brand voice |
| 20 | SLO & Observability Agent | SOA | Support | No | SLO enforcement, golden signals |
