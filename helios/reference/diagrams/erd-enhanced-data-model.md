
# Enhanced SOP Execution Data Model — Target State ERD

> Phase 2+ target-state entity-relationship model for the HELIos SOP execution engine. Extends the Phase 1 baseline model (9 entities) to a comprehensive 23-entity schema covering multi-tenancy, agent configuration, supply chain integrity, incident management, and machine-readable compliance controls.
>
> **Relationship to baseline model:** The Phase 1 baseline ERD is documented in [`helios/reference/sop-execution-data-model.md`](../sop-execution-data-model.md). That model covers the core SOP lifecycle (definitions → versions → steps → runs → step_runs → artifacts → observability → controls). This enhanced model adds organizational context, agent runtime configuration, artifact integrity/access/retention, incident management, and OSCAL-aligned control catalogs. Both models coexist — the baseline is implementable now; this model is the migration target.

---

## 1. Entity Relationship Diagram

```mermaid
erDiagram
  organizations ||--o{ projects : owns
  organizations ||--o{ agent_configurations : configures
  organizations ||--o{ integrations : connects
  organizations ||--o{ control_catalogs : governs

  projects ||--o{ work_items : tracks
  projects ||--o{ environments : uses
  projects ||--o{ sop_runs : executes
  projects ||--o{ artifacts : produces
  projects ||--o{ incidents : experiences

  agent_configurations ||--o{ agent_permissions : grants
  agent_configurations ||--o{ sop_definitions : owns

  sop_definitions ||--o{ sop_versions : versions
  sop_versions ||--o{ sop_steps : contains
  sop_versions ||--o{ sop_io_schemas : specifies
  sop_versions ||--o{ sop_policies : constrains

  sop_runs ||--o{ sop_step_runs : traces
  sop_runs ||--o{ observability_events : emits
  sop_runs ||--o{ evidence_bundles : compiles

  artifacts ||--o{ artifact_hashes : verifies
  artifacts ||--o{ artifact_acls : protects
  artifacts ||--o{ artifact_retention : retains

  control_catalogs ||--o{ control_definitions : contains
  control_definitions ||--o{ control_mappings : maps
  control_mappings }o--|| sop_steps : "step_evidence"
  control_mappings }o--|| artifacts : "artifact_evidence"
  control_mappings }o--|| evidence_bundles : "bundle_evidence"

  incidents ||--o{ incident_actions : mitigates
  incidents ||--o{ postmortems : documents
  evidence_bundles }o--|| incidents : "supports"

  organizations {
    uuid id PK
    text name
    jsonb settings
  }

  integrations {
    uuid id PK
    uuid org_id FK
    text provider
    jsonb connection_metadata
    text status
  }

  agent_configurations {
    uuid id PK
    uuid org_id FK
    text agent_abbr
    text tier
    int authority_rank
    bool can_block
    bool active
    jsonb runtime_limits
  }

  agent_permissions {
    uuid id PK
    uuid agent_configuration_id FK
    text permission_scope
    text target_resource
    text access_level
  }

  sop_definitions {
    uuid id PK
    uuid org_id FK
    text sop_key
    text owner_agent_abbr
    text title
  }

  sop_versions {
    uuid id PK
    uuid sop_definition_id FK
    int version
    text status
    jsonb metadata
    timestamptz published_at
  }

  sop_steps {
    uuid id PK
    uuid sop_version_id FK
    int step_index
    text step_kind
    jsonb action_spec
    jsonb decision_spec
  }

  sop_io_schemas {
    uuid id PK
    uuid sop_version_id FK
    text direction
    jsonb schema_definition
  }

  sop_policies {
    uuid id PK
    uuid sop_version_id FK
    text policy_type
    jsonb policy_definition
  }

  sop_runs {
    uuid id PK
    uuid project_id FK
    uuid sop_version_id FK
    text trigger_type
    text correlation_id
    text idempotency_group
    text status
    timestamptz started_at
    timestamptz ended_at
  }

  sop_step_runs {
    uuid id PK
    uuid sop_run_id FK
    uuid sop_step_id FK
    text status
    text agent_executing
    timestamptz started_at
    timestamptz completed_at
    int duration_ms
    text error_message
    text output_summary
  }

  artifacts {
    uuid id PK
    uuid project_id FK
    uuid sop_run_id FK
    text artifact_type
    text storage_ref
    text classification
    bool immutable
    timestamptz created_at
  }

  artifact_hashes {
    uuid id PK
    uuid artifact_id FK
    text algorithm
    text hash_value
    timestamptz computed_at
  }

  artifact_acls {
    uuid id PK
    uuid artifact_id FK
    text principal
    text access_level
    timestamptz granted_at
  }

  artifact_retention {
    uuid id PK
    uuid artifact_id FK
    text retention_class
    timestamptz expires_at
    text disposition_action
  }

  evidence_bundles {
    uuid id PK
    uuid sop_run_id FK
    text bundle_type
    text integrity_hash
    text classification
    timestamptz created_at
  }

  control_catalogs {
    uuid id PK
    uuid org_id FK
    text catalog_name
    text source_format
    jsonb oscal_payload
  }

  control_definitions {
    uuid id PK
    uuid control_catalog_id FK
    text control_key
    text framework
    text family
    text description
  }

  control_mappings {
    uuid id PK
    uuid control_definition_id FK
    uuid sop_step_id FK
    uuid artifact_id FK
    uuid evidence_bundle_id FK
    text expectation
  }

  observability_events {
    uuid id PK
    uuid sop_run_id FK
    text level
    text event_type
    jsonb payload
    timestamptz ts
  }

  projects {
    uuid id PK
    uuid org_id FK
    text name
    jsonb settings
  }

  work_items {
    uuid id PK
    uuid project_id FK
    text external_id
    text source_system
    text status
  }

  environments {
    uuid id PK
    uuid project_id FK
    text name
    text tier
    jsonb configuration
  }

  incidents {
    uuid id PK
    uuid project_id FK
    text severity
    text status
    timestamptz started_at
    timestamptz resolved_at
  }

  incident_actions {
    uuid id PK
    uuid incident_id FK
    text action_type
    text description
    text agent_executing
    timestamptz executed_at
  }

  postmortems {
    uuid id PK
    uuid incident_id FK
    text summary
    text root_cause
    text corrective_actions
    timestamptz created_at
  }
```

---

## 2. Entity Purpose Table

### Organizational Context (New in Enhanced Model)

| Entity | Purpose | Baseline Model? |
|--------|---------|:---------------:|
| `organizations` | Multi-tenant root. All data scoped to an organization for RLS enforcement. | No |
| `projects` | Organizational unit for work items, SOP runs, artifacts, and incidents. | No |
| `environments` | Deployment targets (staging, production, etc.) per project. | No |
| `work_items` | External work item references (Linear issues, GitHub PRs) linked to project context. | No |
| `integrations` | Connection metadata for external platforms (GitHub, Linear, Supabase, Vercel, Notion). | No |

### Agent Runtime Configuration (New in Enhanced Model)

| Entity | Purpose | Baseline Model? |
|--------|---------|:---------------:|
| `agent_configurations` | Runtime parameters per agent: tier, authority rank, blocking capability, active status, resource limits. | No |
| `agent_permissions` | Granular permission grants per agent: scoped to specific resources and access levels (least privilege enforcement). | No |

### SOP Lifecycle (Extended from Baseline)

| Entity | Purpose | Baseline Model? |
|--------|---------|:---------------:|
| `sop_definitions` | Canonical SOP registry. Enhanced: adds `org_id` and `sop_key` for multi-tenant scoping. | Yes (extended) |
| `sop_versions` | Immutable version records. Enhanced: adds `metadata` JSONB and `published_at`. | Yes (extended) |
| `sop_steps` | Step definitions within a version. Enhanced: adds `step_kind`, `action_spec`, `decision_spec` for executable steps. | Yes (extended) |
| `sop_io_schemas` | Typed input/output contracts per SOP version. Enables schema validation before execution. | No |
| `sop_policies` | Constraints and rules per SOP version (retry policies, timeout limits, classification rules). | No |

### Execution Tracing (Same Core, Extended)

| Entity | Purpose | Baseline Model? |
|--------|---------|:---------------:|
| `sop_runs` | Execution instances. Enhanced: adds `project_id`, `idempotency_group` for replay safety. | Yes (extended) |
| `sop_step_runs` | Step-level execution records. Same structure as baseline. | Yes |
| `observability_events` | Runtime events. Enhanced: `sop_run_id` replaces `sop_step_run_id` for broader scope. | Yes (extended) |

### Artifact Management (Significantly Extended)

| Entity | Purpose | Baseline Model? |
|--------|---------|:---------------:|
| `artifacts` | Evidence and output artifacts. Enhanced: `project_id` and `sop_run_id` for project-level scoping. | Yes (extended) |
| `artifact_hashes` | Hash-based integrity verification per artifact (supports multiple algorithms). | No |
| `artifact_acls` | Access control lists per artifact (who can read, principal-based). | No |
| `artifact_retention` | Retention policies per artifact (class, expiry, disposition action). | No |
| `evidence_bundles` | Aggregated evidence packages compiled from SOP runs for compliance gates. | No |

### Compliance & Controls (Significantly Extended)

| Entity | Purpose | Baseline Model? |
|--------|---------|:---------------:|
| `control_catalogs` | OSCAL-aligned control catalog containers (SOC 2, HIPAA, NIST CSF, CSA CAIQ). | No |
| `control_definitions` | Individual controls within catalogs. Enhanced: adds `control_catalog_id` and `family`. | Yes (extended) |
| `control_mappings` | Control-to-evidence linkage. Enhanced: adds `artifact_id` and `evidence_bundle_id` for three-way mapping. | Yes (extended) |

### Incident Management (New in Enhanced Model)

| Entity | Purpose | Baseline Model? |
|--------|---------|:---------------:|
| `incidents` | Incident records scoped to projects. Tracks severity, status, and resolution timeline. | No |
| `incident_actions` | Actions taken during incident response (rollbacks, mitigations, escalations). | No |
| `postmortems` | Post-incident learning artifacts: root cause, corrective actions, and summary. | No |

---

## 3. Migration Path: Baseline → Enhanced

The enhanced model is designed as an additive migration from the Phase 1 baseline:

1. **Add organizational context tables** — `organizations`, `projects`, `environments`, `work_items`, `integrations`
2. **Add agent runtime tables** — `agent_configurations`, `agent_permissions`
3. **Extend SOP tables** — Add columns to `sop_definitions`, `sop_versions`, `sop_steps`; create `sop_io_schemas`, `sop_policies`
4. **Extend artifact tables** — Add columns to `artifacts`; create `artifact_hashes`, `artifact_acls`, `artifact_retention`, `evidence_bundles`
5. **Extend control tables** — Create `control_catalogs`; add columns to `control_definitions`, `control_mappings`
6. **Add incident management** — `incidents`, `incident_actions`, `postmortems`
7. **Apply RLS policies** — Scope all queries to `org_id` at minimum; agent-level scoping via `agent_configurations`

No baseline entities are removed. All baseline foreign key relationships are preserved.

---

## 4. Schema Optimization Notes

| Concern | Recommendation |
|---------|----------------|
| **Indexes** | `correlation_id` (sop_runs), `(project_id, started_at)` (sop_runs, artifacts, incidents), `(sop_version_id, status)` (sop_runs), `hash_value` (artifact_hashes, unique), `control_key` (control_definitions), `started_at` (incidents) |
| **Partitioning** | `observability_events` and `sop_step_runs` — high volume, partition by time for retention management |
| **RLS strategy** | Tenant isolation at `organizations`/`projects` level. No bypass keys outside controlled service contexts |
| **Immutability** | `artifacts` and `evidence_bundles` — no UPDATE/DELETE policies. Write-once semantics enforced at RLS layer |
| **OSCAL payloads** | `control_catalogs.oscal_payload` stored as JSONB for queryability. Supports XML/JSON/YAML import via Edge Functions |

---

## Related Documents

- Phase 1 Baseline ERD: [`helios/reference/sop-execution-data-model.md`](../sop-execution-data-model.md)
- Agent Communication Protocol: [`helios/reference/agent-communication-protocol.md`](../agent-communication-protocol.md)
- Compliance Control Mapping: [`helios/reference/compliance-control-mapping.md`](../compliance-control-mapping.md)
- Platform Readiness Assessment: [`helios/governance/platform-readiness-assessment.md`](../../governance/platform-readiness-assessment.md)
