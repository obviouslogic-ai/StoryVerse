# Compliance Control Mapping Framework

> Defines how HELIos pipeline activities map to external compliance framework controls. Establishes the control library structure, evidence mapping model, evidence bundle specifications, and gate enforcement linkages. HELIos produces compliance-ready evidence — it does not determine compliance truth (the external compliance platform is the system of record for compliance determinations).

---

## Purpose

Regulated environments require demonstrable evidence that engineering processes satisfy specific control requirements. Rather than treating compliance as a separate overlay, HELIos embeds evidence production into its existing SOP execution and gate enforcement. This framework defines:

1. **What controls** HELIos maps to (control library structure)
2. **How evidence maps** to those controls (control-to-evidence model)
3. **What constitutes** a compliant evidence bundle (bundle specification)
4. **How gates enforce** evidence completeness (gate enforcement linkage)

---

## Scope

### Compliance Frameworks Covered

| Framework | Governing Body | Relevance |
|-----------|---------------|-----------|
| **SOC 2 Type II** | AICPA | Trust Services Criteria — Security, Availability, Processing Integrity, Confidentiality, Privacy |
| **HIPAA Security Rule** | HHS/OCR | Administrative, Physical, and Technical safeguards for PHI-adjacent data handling |
| **NIST Cybersecurity Framework (CSF) 2.0** | NIST | Govern, Identify, Protect, Detect, Respond, Recover functions |
| **CSA CCM / CAIQ** | Cloud Security Alliance | Cloud Controls Matrix and Consensus Assessment Initiative Questionnaire for cloud service assurance |

### Boundary Rule

HELIos produces compliance-ready evidence. HELIos does NOT:
- Make compliance determinations (that is the external compliance platform's system-of-record responsibility)
- Certify compliance status (that requires external auditors)
- Replace GRC tooling (HELIos feeds into GRC processes, not replaces them)

---

## 1. Control Library Structure

### Control Definition Model

Each control in the library is defined with the following attributes:

| Attribute | Description |
|-----------|-------------|
| `control_id` | Unique identifier (format: `{framework}-{category}-{sequence}`, e.g., `SOC2-CC6-001`) |
| `framework` | Source compliance framework |
| `category` | Framework-specific category (e.g., SOC 2 Trust Services Category, NIST CSF Function) |
| `control_title` | Human-readable control name |
| `control_description` | Full text of the control requirement |
| `helios_applicability` | Whether and how HELIos can produce evidence for this control |
| `evidence_type` | What kind of evidence satisfies the control (artifact, log, attestation, configuration) |
| `responsible_agents` | Which HELIos agents contribute evidence for this control |
| `gate_enforcement` | Which lifecycle gates check for this control's evidence |

### SOC 2 Trust Services Criteria — HELIos Mappings

| TSC Category | Control Area | HELIos Evidence Source |
|-------------|-------------|----------------------|
| CC1 — Control Environment | Governance and oversight | Constitution, governance framework, HAA authority records |
| CC2 — Communication | Information and communication | Agent communication protocol, escalation records, intelligence briefs |
| CC3 — Risk Assessment | Risk identification and analysis | STMA threat models, ORFA incident analysis, RRA risk assessments |
| CC5 — Control Activities | Control implementation | SOP execution logs, gate enforcement records, PGA audit trails |
| CC6 — Logical Access | Access controls | Supabase RLS policies, PDA access control matrices, STMA security configurations |
| CC7 — System Operations | Change management, incident response | CEA PR records, ATADA CI/CD logs, ORFA incident workflows, RRA release records |
| CC8 — Change Management | Change authorization and testing | Gate transition records, ATADA test results, ARA compliance evidence packages |
| CC9 — Risk Mitigation | Vendor and third-party risk | DSCA dependency reviews, DSCA SBOM attestations, PIA platform assessments |

### HIPAA Security Rule — HELIos Mappings

| Safeguard | Requirement | HELIos Evidence Source |
|-----------|-------------|----------------------|
| Administrative — Risk Analysis | Identify PHI risks | PDA data classification, STMA threat models |
| Administrative — Information Access Management | Authorize access to PHI | PDA access control matrices, Supabase RLS policies |
| Administrative — Security Awareness | Workforce training evidence | SOP execution records (agents are "trained" by SOPs) |
| Technical — Access Control | Unique user/agent identification | Agent registry, authentication records |
| Technical — Audit Controls | Activity logging | SOP execution logs, agent communication logs, ORFA monitoring |
| Technical — Integrity | Data integrity verification | DSCA provenance attestations, ATADA artifact integrity checks |
| Technical — Transmission Security | Encrypted data in transit | Agent communication protocol data classification enforcement |

### NIST CSF 2.0 — HELIos Mappings

| Function | Category | HELIos Evidence Source |
|----------|----------|----------------------|
| Govern (GV) | Organizational context, risk management strategy | Charter, governance framework, KPI framework |
| Identify (ID) | Asset management, risk assessment | Agent registry, integration matrix, PIA platform assessments |
| Protect (PR) | Access control, data security, platform security | PDA policies, STMA configurations, DSCA supply chain controls |
| Detect (DE) | Continuous monitoring, anomaly detection | ORFA observability, SOA SLO monitoring, PIA health checks |
| Respond (RS) | Incident management, analysis, mitigation | ORFA incident workflows, escalation protocols |
| Recover (RC) | Recovery planning, improvements | RRA rollback plans, retrospective records |

---

## 2. Control-to-Evidence Mapping Model

### Mapping Structure

Each control maps to one or more evidence requirements:

```
Control → Required SOP Steps → Required Artifacts → Gate Enforcement Points
```

| Mapping Level | Description |
|--------------|-------------|
| **Control → SOP Steps** | Which specific SOP steps produce evidence for this control |
| **SOP Steps → Artifacts** | What artifacts (logs, reports, attestations) each step produces |
| **Artifacts → Gates** | Which lifecycle gates require these artifacts for transition approval |

### Example Mapping Chain

**Control:** SOC2-CC7-003 — "Changes to infrastructure and software are authorized, designed, developed, configured, documented, tested, approved, and implemented."

| Required SOP Step | Artifact Produced | Gate Enforcement |
|-------------------|-------------------|------------------|
| REA-001: Requirement normalization | Requirement object with trace ID | Gate 0→1 (requirement must exist) |
| CEA-004: Implementation proof bundle | PR with requirement trace, test evidence | Gate 3→4 (merge requires proof bundle) |
| ATADA-001: CI validation | CI pass certificate | Gate 3→4 (merge requires CI pass) |
| ARA-004: Compliance evidence packaging | Evidence bundle with control mapping | Gate 4→5 (release requires evidence package) |
| RRA-004: Change enablement gate | Authorization record, rollback plan | Gate 5 (release requires change authorization) |

---

## 3. Evidence Bundle Specification

An evidence bundle is a structured collection of artifacts that demonstrates compliance with one or more controls.

### Bundle Structure

| Component | Description | Required |
|-----------|-------------|----------|
| `bundle_id` | Unique identifier for the bundle | Yes |
| `correlation_id` | Links to the workflow that produced the evidence | Yes |
| `framework` | Which compliance framework this bundle addresses | Yes |
| `controls_addressed` | List of control_ids satisfied by this bundle | Yes |
| `artifacts` | List of evidence artifacts with references | Yes |
| `completeness_status` | Whether all required artifacts are present | Yes |
| `produced_by` | Agent(s) that assembled the bundle | Yes |
| `validated_by` | Agent that validated bundle completeness (ARA or PGA) | Yes |
| `timestamp` | When the bundle was assembled | Yes |
| `retention_class` | How long the bundle must be retained | Yes |

### Artifact Reference Format

Each artifact in a bundle must include:

| Field | Description |
|-------|-------------|
| `artifact_id` | Unique identifier |
| `artifact_type` | Category: `log`, `report`, `attestation`, `configuration`, `screenshot`, `certificate` |
| `source_agent` | Agent that produced the artifact |
| `source_sop` | SOP step that produced the artifact |
| `immutable_reference` | Hash or immutable URL for the artifact (artifacts cannot be modified after bundle assembly) |
| `data_classification` | Sensitivity level per Agent Communication Protocol |

### Retention Requirements

| Framework | Minimum Retention |
|-----------|-------------------|
| SOC 2 | 12 months (audit period) |
| HIPAA | 6 years |
| NIST CSF | Per organizational policy (recommended: 3 years) |
| CSA CAIQ | Per SLA with customer (recommended: 3 years) |

---

## 4. Gate Enforcement Linkage

Lifecycle gates reference control mappings so that transitions require evidence objects — not subjective confirmation.

### Gate-to-Control Mapping

| Gate Transition | Controls Enforced | Evidence Required |
|----------------|-------------------|-------------------|
| Phase 0 → Phase 1 | CC1 (governance), GV.RM (risk strategy) | Project setup checklist, requirement register initialized |
| Phase 1 → Phase 2 | CC7, PR.DS (data security) | Requirements with acceptance criteria, security requirements |
| Phase 2 → Phase 3 | CC8 (change management) | Architecture decision records, threat model |
| Phase 3 → Phase 4 | CC5 (control activities), CC7, CC8 | Implementation proof bundle (CEA-004), CI certificate (ATADA) |
| Phase 4 → Phase 5 | CC7, CC8, CC9 (risk mitigation) | Test results, dependency review, SLO readiness certificate |
| Phase 5 → Phase 6 | All applicable controls | Complete evidence bundle (ARA-004), release authorization (RRA-004) |

### Enforcement Mechanism

1. Gate checks query the evidence store for required artifacts
2. Each required artifact is validated for presence and integrity (immutable reference check)
3. Missing artifacts block the gate transition
4. The blocking is logged with the specific missing control evidence
5. PGA audits gate enforcement records for compliance

---

## 5. Agent Responsibility Matrix for Evidence Production

| Agent | Evidence Role | Frameworks Served |
|-------|-------------|-------------------|
| **ARA** | Evidence bundle assembly and completeness validation | All |
| **PGA** | Evidence audit and gate enforcement verification | All |
| **PDA** | Data classification evidence, access control documentation | HIPAA, SOC 2 (CC6) |
| **STMA** | Security configuration evidence, threat model documentation | SOC 2 (CC6, CC7), NIST (PR), HIPAA (Technical) |
| **DSCA** | Supply chain evidence, SBOM attestations, provenance | SOC 2 (CC9), NIST (ID.SC) |
| **ATADA** | CI/CD evidence, test results, DORA metrics | SOC 2 (CC7, CC8), NIST (PR.DS) |
| **CEA** | Implementation evidence, PR records, proof bundles | SOC 2 (CC7, CC8) |
| **REA** | Requirement traceability evidence, change control records | SOC 2 (CC7, CC8) |
| **SOA** | SLO compliance evidence, availability records | SOC 2 (A1), NIST (DE) |
| **ORFA** | Incident response evidence, monitoring records | SOC 2 (CC7), NIST (DE, RS) |
| **RRA** | Release authorization evidence, rollback plans | SOC 2 (CC7, CC8), NIST (RC) |

---

## Related Documents

- Agent Communication Protocol: `agent-communication-protocol.md`
- SOP Execution Data Model: `sop-execution-data-model.md`
- Governance Framework: `../governance/helios-governance-framework-v1.md`
- Escalation Protocols: `escalation-protocols.md`
- KPI Framework: `../governance/kpi-framework.md`
