# Non-Production Data Handling Policy

## Purpose
Define SSC requirements for using production or sensitive data in non-production environments.

## Scope
All SSC non-production environments, testing, staging, and development systems.

## Compliance Status
SSC is not currently certified under SOC 2 or HIPAA. This policy defines readiness controls.

## Policy
- Prohibit use of regulated or sensitive production data in non-production unless approved.
- Require data masking, anonymization, or synthetic data where feasible.
- Maintain approvals and tracking for exceptions.

## Standards and Procedures
- Define approval criteria for any production data use in non-production.
- Maintain a register of approved datasets and purposes.
- Ensure non-production access controls are enforced.

## Roles and Responsibilities
- Security Lead: approves exceptions for data use.
- Engineering: implements masking and access controls.
- Data Owners: approve data usage and purpose.

## Review and Exceptions
- Review annually or upon significant changes.
- Exceptions require documented approval.

## References
- `../index.md`
- `../data-protection/data-classification-handling.md`
- `../governance-risk-compliance/policy-exception-management.md`

## Compliance Mapping
- CAIQ DSP: DSP-15.1
- CAIQ I&S: I&S-05.2
