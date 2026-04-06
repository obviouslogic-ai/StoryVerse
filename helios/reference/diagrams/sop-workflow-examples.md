
# Multi-Agent SOP Workflow Examples

> Three reference workflow diagrams illustrating how multiple HELIos agents coordinate through SOP execution chains. Each example shows the trigger, participating agents, decision points, evidence artifacts produced, and escalation paths. These are representative patterns — actual execution depends on platform implementation.

---

## 1. Supply Chain Attestation Gate

**Agents:** DSCA (Dependency & Supply Chain) → ATADA (Automated Testing & Deployment) → RRA (Release Readiness)

**Purpose:** Prevent promotion of build artifacts to release unless the artifact has (a) SBOM in an accepted format and (b) provenance attestation aligned to a chosen SLSA target level.

**Triggers:** Build completion event from CI, dependency update merged, or release readiness evaluation.

```mermaid
sequenceDiagram
    participant CI as CI Pipeline
    participant DSCA as DSCA<br/>(Supply Chain)
    participant ATADA as ATADA<br/>(Testing & Deploy)
    participant RRA as RRA<br/>(Release Readiness)
    participant Store as Artifact Store
    participant HAA as HAA<br/>(Human Authority)

    CI->>DSCA: Build completion event<br/>(artifact digest, commit SHA, build ID)
    activate DSCA

    DSCA->>DSCA: Verify artifact digest matches registry
    DSCA->>Store: Generate SBOM (SPDX/CycloneDX)
    Store-->>DSCA: SBOM stored with artifact reference

    DSCA->>DSCA: Schema-validate SBOM format
    alt SBOM invalid or missing
        DSCA->>RRA: BLOCK — SBOM generation failed
        RRA->>RRA: Gate state = BLOCKED
    end

    DSCA->>ATADA: Request provenance attestation
    deactivate DSCA
    activate ATADA

    ATADA->>ATADA: Generate provenance attestation<br/>(in-toto SLSA predicate)
    ATADA->>ATADA: Sign attestation, verify integrity
    ATADA->>Store: Store provenance + signature

    alt Provenance absent or digest mismatch
        ATADA->>RRA: BLOCK — Provenance verification failed
        RRA->>RRA: Gate state = BLOCKED
    else Low-risk exception exists
        ATADA->>RRA: HOLD — Exception requires approval
        RRA->>HAA: Request human approval
        HAA-->>RRA: Approved / Rejected
    else Policy satisfied
        ATADA->>RRA: GO — All attestations valid
    end
    deactivate ATADA

    activate RRA
    RRA->>Store: Emit evidence bundle<br/>(SBOM + provenance + gate decision)
    RRA->>RRA: Update release gate state
    deactivate RRA
```

### Evidence Artifacts Produced
| Artifact | Type | Producing Agent | Classification |
|----------|------|-----------------|----------------|
| SBOM (SPDX or CycloneDX) | Attestation | DSCA | INTERNAL |
| Provenance attestation (SLSA predicate) | Attestation | ATADA | INTERNAL |
| Signature record | Certificate | ATADA | CONFIDENTIAL |
| Gate decision record | Report | RRA | INTERNAL |
| Evidence bundle | Bundle | RRA | INTERNAL |

### KPIs
- Coverage: % of release artifacts with SBOM + provenance
- Mean time to resolve supply chain violations (by severity)
- Pipeline failure rate attributable to supply chain gates

---

## 2. Requirement Change Control & Traceability

**Agents:** REA (Requirements Engineering) → PPMA (Project Management) → CEA (Code Engineering)

**Purpose:** Maintain requirement integrity and traceability so every production change is linked to normalized requirements and acceptance criteria, preserving lifecycle traceability per ISO 29148.

**Triggers:** New requirement submitted, existing requirement modified, or PR opened without linked requirement.

```mermaid
sequenceDiagram
    participant Source as Stakeholder /<br/>Cloud Ticket
    participant REA as REA<br/>(Requirements)
    participant PPMA as PPMA<br/>(Project Mgmt)
    participant CEA as CEA<br/>(Code Engineering)
    participant ATADA as ATADA<br/>(Testing)
    participant STMA as STMA<br/>(Security)
    participant PDA as PDA<br/>(Privacy)

    Source->>REA: Requirement draft + stakeholder metadata
    activate REA

    REA->>REA: Normalize into structured format<br/>(singular, testable, unambiguous, bounded)
    REA->>REA: Generate unique requirement ID
    REA->>REA: Attach acceptance criteria

    REA->>REA: Risk domain check
    alt Touches security domain
        REA->>STMA: Request security review
        STMA-->>REA: Security assessment
    end
    alt Touches privacy/data domain
        REA->>PDA: Request privacy review
        PDA-->>REA: Privacy assessment
    end

    REA->>PPMA: Normalized requirement object<br/>(ID, priority, acceptance criteria,<br/>risk tags, trace links)
    deactivate REA
    activate PPMA

    PPMA->>PPMA: Scope assessment<br/>(fits current project boundaries?)
    alt Out of scope
        PPMA->>Source: Deferred / rejected<br/>with rationale
    else In scope
        PPMA->>CEA: Implementation spec<br/>with requirement trace ID
    end
    deactivate PPMA

    activate CEA
    CEA->>CEA: Implement with trace links<br/>(PR references requirement ID)
    CEA->>ATADA: Acceptance criteria for test generation
    ATADA-->>CEA: Test results linked to requirement

    alt PR missing trace links
        CEA->>CEA: BLOCK merge readiness
        CEA->>REA: Request trace link completion
    end
    deactivate CEA
```

### Evidence Artifacts Produced
| Artifact | Type | Producing Agent | Classification |
|----------|------|-----------------|----------------|
| Normalized requirement object | Report | REA | INTERNAL |
| Traceability matrix update | Report | REA | INTERNAL |
| Change control record | Report | REA | INTERNAL |
| Scope assessment | Report | PPMA | INTERNAL |
| Implementation spec with trace IDs | Report | CEA | INTERNAL |
| Acceptance test results | Attestation | ATADA | INTERNAL |

### KPIs
- Trace completeness: % of PRs with requirement IDs and acceptance criteria coverage
- Requirement churn rate post-design freeze

---

## 3. Incident-Driven Rollback & Postmortem

**Agents:** ORFA (Ops & Reliability) → RRA (Release Readiness) → SOA (SLO & Observability)

**Purpose:** Restore normal operation quickly and consistently, and generate post-incident learning artifacts. Aligns incident handling with ITIL incident management and SRE error-budget practices.

**Triggers:** SLO burn rate breach, deployment-related error spike, or customer-impact incident declared.

```mermaid
sequenceDiagram
    participant Alert as Monitoring /<br/>SLO Alert
    participant SOA as SOA<br/>(SLO & Observability)
    participant ORFA as ORFA<br/>(Ops & Reliability)
    participant RRA as RRA<br/>(Release Readiness)
    participant HAA as HAA<br/>(Human Authority)
    participant Store as Incident Store

    Alert->>SOA: SLO burn rate breach detected
    activate SOA
    SOA->>SOA: Evaluate error budget remaining
    SOA->>ORFA: Incident trigger<br/>(correlation IDs, SLO data,<br/>budget remaining)
    deactivate SOA

    activate ORFA
    ORFA->>ORFA: Classify severity<br/>(deterministic rules, not judgment)

    alt Severity = Critical
        ORFA->>HAA: Page human on-call
        HAA-->>ORFA: Acknowledged
    end

    ORFA->>ORFA: Assess recent deployments<br/>and feature flag state

    alt Budget rapidly burning + deployment suspected
        ORFA->>RRA: Recommend rollback
        activate RRA
        RRA->>RRA: Verify rollback plan artifact exists
        alt Rollback plan available
            RRA->>RRA: Execute rollback<br/>(idempotent deployment operation)
        else No rollback plan
            RRA->>RRA: Execute compensating action<br/>(feature flag disable)
        end
        RRA->>Store: Record rollback action + evidence
        deactivate RRA
    else Budget stable or non-deployment cause
        ORFA->>ORFA: Apply mitigation playbook
    end

    ORFA->>Store: Create incident record<br/>(timeline, actions, evidence)
    ORFA->>ORFA: Create postmortem draft
    ORFA->>ORFA: File corrective action items<br/>(at least 1 required)
    deactivate ORFA

    SOA->>SOA: Update error budget tracking
    SOA->>RRA: SLO status update<br/>(affects future release gates)
```

### Evidence Artifacts Produced
| Artifact | Type | Producing Agent | Classification |
|----------|------|-----------------|----------------|
| Incident record with timeline | Report | ORFA | INTERNAL |
| Rollback execution record | Log | RRA | INTERNAL |
| Rollback evidence | Attestation | RRA | INTERNAL |
| Postmortem draft | Report | ORFA | INTERNAL |
| Corrective action items | Report | ORFA | INTERNAL |
| Error budget update | Report | SOA | INTERNAL |

### KPIs
- Failed deployment recovery time (DORA dimension)
- Time to restore service
- % incidents with completed postmortems and closed corrective actions

---

## Interaction Pattern Summary

| Pattern | Flow | Coordination Mechanism |
|---------|------|----------------------|
| Supply Chain → Release | DSCA → ATADA → RRA | Evidence chain: SBOM + provenance required for gate GO |
| Requirements → Implementation → Testing | REA → PPMA → CEA → ATADA | Trace IDs: every PR must reference a requirement |
| Incident → Rollback → Learning | ORFA → RRA → SOA | SLO signals drive rollback decisions; postmortems produce backlog items |

---

## Related Documents

- Agent Communication Protocol: [`helios/reference/agent-communication-protocol.md`](../agent-communication-protocol.md)
- Enhanced Data Model: [`helios/reference/diagrams/erd-enhanced-data-model.md`](erd-enhanced-data-model.md)
- Escalation Protocols: [`helios/reference/escalation-protocols.md`](../escalation-protocols.md)
