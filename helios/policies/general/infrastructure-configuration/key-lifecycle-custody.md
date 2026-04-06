# Key Lifecycle and Custody Policy

## Purpose
Define SSC requirements for key custody, archival, compromise handling, change review, risk management, and crypto-related audits.

## Scope
All cryptographic keys, secrets, and certificates used by SSC systems and the SSC Cloud product.

## Compliance Status
SSC is not currently certified under SOC 2 or HIPAA. This policy defines readiness controls.

## Policy
- Maintain custody procedures for keys and secrets throughout their lifecycle.
- Define archival and destruction requirements for keys.
- Establish procedures for compromised or suspected-compromised keys.
- Audit key management processes on a defined cadence.
- Review and approve cryptography, encryption, and key management technology changes through standard change management procedures.
- Account for downstream effects of proposed crypto changes, including residual risk, cost, and benefits analysis.
- Maintain a crypto risk program including risk assessment, risk treatment, risk context, monitoring, and feedback.
- Assess operational continuity risks versus the risk of losing control of keying material.

## Standards and Procedures
- Maintain a key inventory with owners and purpose.
- Define key archival storage requirements and access controls.
- Require key compromise response procedures and documentation.
- Conduct annual reviews of key management processes.
- Require change review for all cryptography and key management changes, incorporating internal and external sources.
- Document downstream impact analysis for proposed encryption or key management changes.
- Perform periodic crypto risk assessments and maintain risk treatment records.
- Evaluate operational continuity risks related to key material control and data exposure.

## Roles and Responsibilities
- Security Lead: owns key lifecycle policies, risk assessments, and reviews.
- Engineering: implements key custody, archival practices, and change execution.
- Operations: manages secrets storage, access controls, and continuity planning.

## Review and Exceptions
- Review annually or upon significant changes.
- Exceptions require documented approval.

## References
- `../index.md`
- `../infrastructure-configuration/encryption-key-management.md`
- `../development-change/change-management.md`
- `../governance-risk-compliance/risk-management.md`
- `../governance-risk-compliance/policy-exception-management.md`

## Compliance Mapping
- CAIQ CEK: CEK-05.1, CEK-06.1, CEK-07.1, CEK-09.1, CEK-09.2, CEK-18.1, CEK-19.1, CEK-20.1
