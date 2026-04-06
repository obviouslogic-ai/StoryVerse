# Policies Index (SOC 2 + HIPAA + NIST SP 800-53)

## Purpose
This index maps organizational policies to SOC 2 Trust Services Criteria (TSC), HIPAA, and NIST SP 800-53 requirements, and serves as the single source of truth for compliance documentation coverage.

## Scope
All SSC systems, environments, and personnel supporting the SSC Cloud product and related services.

## Compliance Status
SSC is not currently certified under SOC 2 or HIPAA. This policy set defines SSC's target controls and is maintained as part of our compliance readiness program.

## Policy Catalog

### Governance, Risk, and Compliance (`governance-risk-compliance/`)
- `governance-risk-compliance/governance-program.md`
- `governance-risk-compliance/information-security.md`
- `governance-risk-compliance/risk-management.md`
- `governance-risk-compliance/compliance-requirements-register.md`
- `governance-risk-compliance/compliance-verification.md`
- `governance-risk-compliance/audit-assurance.md`
- `governance-risk-compliance/independent-audit-plan.md`
- `governance-risk-compliance/policy-exception-management.md`
- `governance-risk-compliance/stakeholder-engagement.md`

### Access Control and Identity (`access-control/`)
- `access-control/access-control-iam.md`
- `access-control/authentication-credentials.md`
- `access-control/privileged-access-governance.md`

### Data Protection and Privacy (`data-protection/`)
- `data-protection/data-classification-handling.md`
- `data-protection/data-flow-documentation.md`
- `data-protection/data-ownership-stewardship.md`
- `data-protection/data-retention-disposal.md`
- `data-protection/privacy-hipaa.md`
- `data-protection/privacy-impact-assessment.md`
- `data-protection/hipaa-security-rule-safeguards.md`
- `data-protection/non-production-data-handling.md`
- `data-protection/law-enforcement-requests.md`

### Security Operations (`security-operations/`)
- `security-operations/logging-monitoring.md`
- `security-operations/log-sanitization.md`
- `security-operations/time-synchronization.md`
- `security-operations/incident-response.md`
- `security-operations/breach-notification.md`
- `security-operations/vulnerability-management.md`
- `security-operations/malware-protection.md`
- `security-operations/threat-analysis.md`

### Infrastructure and Configuration (`infrastructure-configuration/`)
- `infrastructure-configuration/configuration-management.md`
- `infrastructure-configuration/network-configuration-review.md`
- `infrastructure-configuration/environment-risk-classification.md`
- `infrastructure-configuration/encryption-key-management.md`
- `infrastructure-configuration/key-lifecycle-custody.md`

### Development and Change (`development-change/`)
- `development-change/secure-sdlc.md`
- `development-change/change-management.md`
- `development-change/api-security-review.md`

### Business Continuity (`business-continuity/`)
- `business-continuity/business-continuity-disaster-recovery.md`
- `business-continuity/backup-recovery.md`

### Endpoint and Asset Management (`endpoint-asset-management/`)
- `endpoint-asset-management/asset-management-acceptable-use.md`
- `endpoint-asset-management/endpoint-management.md`
- `endpoint-asset-management/workplace-security.md`

### Workforce and Training (`workforce-training/`)
- `workforce-training/workforce-security-awareness.md`
- `workforce-training/ai-usage.md`

### Third Party and Contracts (`third-party-contracts/`)
- `third-party-contracts/vendor-subprocessor-management.md`
- `third-party-contracts/customer-contract-change-controls.md`
- `third-party-contracts/interoperability-portability.md`

## SOC 2 TSC Mapping (High Level)
- CC1, CC2 (Control Environment, Communication): `governance-risk-compliance/information-security.md`, `governance-risk-compliance/governance-program.md`, `workforce-training/workforce-security-awareness.md`
- CC3, CC4 (Risk Assessment, Monitoring): `governance-risk-compliance/risk-management.md`, `security-operations/logging-monitoring.md`
- CC5 (Control Activities): `access-control/access-control-iam.md`, `development-change/change-management.md`, `development-change/secure-sdlc.md`, `infrastructure-configuration/configuration-management.md`
- CC6 (Logical and Physical Access): `access-control/access-control-iam.md`, `access-control/authentication-credentials.md`, `endpoint-asset-management/asset-management-acceptable-use.md`, `endpoint-asset-management/workplace-security.md`, `endpoint-asset-management/endpoint-management.md`
- CC7 (System Operations): `security-operations/logging-monitoring.md`, `security-operations/incident-response.md`, `security-operations/vulnerability-management.md`, `security-operations/malware-protection.md`
- CC8 (Change Management): `development-change/change-management.md`, `development-change/secure-sdlc.md`
- CC9 (Risk Mitigation): `business-continuity/business-continuity-disaster-recovery.md`, `business-continuity/backup-recovery.md`, `third-party-contracts/vendor-subprocessor-management.md`
- Confidentiality: `infrastructure-configuration/encryption-key-management.md`, `data-protection/data-classification-handling.md`, `workforce-training/ai-usage.md`
- Privacy: `data-protection/privacy-hipaa.md`, `data-protection/data-retention-disposal.md`, `security-operations/breach-notification.md`
- Governance & Audit: `governance-risk-compliance/audit-assurance.md`, `governance-risk-compliance/independent-audit-plan.md`, `governance-risk-compliance/compliance-verification.md`, `governance-risk-compliance/governance-program.md`
- Endpoint Security (CAIQ UEM): `endpoint-asset-management/endpoint-management.md`
- Threat & Vulnerability (CAIQ TVM): `security-operations/malware-protection.md`, `security-operations/threat-analysis.md`, `security-operations/vulnerability-management.md`
- Logging & Monitoring (CAIQ LOG): `security-operations/log-sanitization.md`, `security-operations/time-synchronization.md`, `security-operations/logging-monitoring.md`

## HIPAA Mapping (High Level)
- HIPAA Privacy Rule: `data-protection/privacy-hipaa.md`, `data-protection/data-retention-disposal.md`, `security-operations/breach-notification.md`
- HIPAA Security Rule Administrative Safeguards: `governance-risk-compliance/information-security.md`, `governance-risk-compliance/risk-management.md`, `workforce-training/workforce-security-awareness.md`, `security-operations/incident-response.md`, `third-party-contracts/vendor-subprocessor-management.md`, `infrastructure-configuration/configuration-management.md`
- HIPAA Security Rule Physical Safeguards: `endpoint-asset-management/asset-management-acceptable-use.md`, `business-continuity/business-continuity-disaster-recovery.md`, `endpoint-asset-management/workplace-security.md`, `endpoint-asset-management/endpoint-management.md`
- HIPAA Security Rule Technical Safeguards: `access-control/access-control-iam.md`, `access-control/authentication-credentials.md`, `security-operations/logging-monitoring.md`, `infrastructure-configuration/encryption-key-management.md`
- HIPAA Program Support: `data-protection/privacy-impact-assessment.md`, `data-protection/law-enforcement-requests.md`, `governance-risk-compliance/policy-exception-management.md`

## NIST SP 800-53 Mapping (High Level)
- AC (Access Control): `access-control/access-control-iam.md`, `access-control/authentication-credentials.md`, `access-control/privileged-access-governance.md`
- AT (Awareness and Training): `workforce-training/workforce-security-awareness.md`
- AU (Audit and Accountability): `security-operations/logging-monitoring.md`, `governance-risk-compliance/audit-assurance.md`
- CA (Assessment, Authorization, and Monitoring): `governance-risk-compliance/compliance-verification.md`, `governance-risk-compliance/risk-management.md`
- CM (Configuration Management): `infrastructure-configuration/configuration-management.md`, `development-change/change-management.md`
- CP (Contingency Planning): `business-continuity/business-continuity-disaster-recovery.md`, `business-continuity/backup-recovery.md`
- IA (Identification and Authentication): `access-control/authentication-credentials.md`, `access-control/access-control-iam.md`
- IR (Incident Response): `security-operations/incident-response.md`, `security-operations/breach-notification.md`
- MP (Media Protection): `data-protection/data-retention-disposal.md`, `endpoint-asset-management/endpoint-management.md`
- PE (Physical and Environmental): `endpoint-asset-management/workplace-security.md`
- PL (Planning): `governance-risk-compliance/governance-program.md`, `governance-risk-compliance/information-security.md`
- PS (Personnel Security): `workforce-training/workforce-security-awareness.md`
- RA (Risk Assessment): `governance-risk-compliance/risk-management.md`, `security-operations/threat-analysis.md`
- SA (System and Services Acquisition): `third-party-contracts/vendor-subprocessor-management.md`, `development-change/secure-sdlc.md`
- SC (System and Communications Protection): `infrastructure-configuration/encryption-key-management.md`, `infrastructure-configuration/network-configuration-review.md`
- SI (System and Information Integrity): `security-operations/vulnerability-management.md`, `security-operations/malware-protection.md`

## Appendices
- `appendices/system-evidence.md` (system-specific control evidence references)
- `appendices/document-library.md` (policy and artifact library map)

## References
- `CAIQ_architecture_overview.md` (project-specific; add during setup if required)
- `CAIQ_completed.csv` (project-specific; add during setup if required)
