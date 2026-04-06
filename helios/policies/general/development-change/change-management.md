# Change Management Policy

## Purpose
Control changes to systems and configurations to reduce risk and maintain service stability.

## Scope
All code, infrastructure, configurations, and third-party integrations supporting SSC and the SSC Cloud product.

## Policy
- Require documented change requests with risk assessment.
- Enforce peer review and testing for production changes.
- Maintain rollback procedures for critical changes.
- Track change approvals and deployment records.

## Standards and Procedures
- Define change categories:
  - **Standard Change**: A repeatable change pre-authorized by the Change Authority through a documented procedure with predictable outcomes and controlled risk.
  - **Normal Change**: A change that follows the full change management process with risk assessment, peer review, testing, and approval. Priority determined by authorized personnel.
  - **Emergency Change**: A change required immediately due to potential negative service impact. Must still be authorized by the CTO or delegate and documented after-the-fact.
- Require all changes to include documented implementation steps and backout/rollback procedures specific enough for any qualified engineer to execute.
- Require pre-deployment testing and validation in non-production environments.
- Log all production deployments and configuration changes in the change management system.
- Perform post-change verification and monitoring.

## Roles and Responsibilities
- Change Owner: prepares and documents change.
- Approver: validates risk and approves change.
- Engineering/Operations: executes and monitors change.

## Review and Exceptions
- Review annually or upon major process changes.
- Emergency changes must be documented after-the-fact within defined timelines.

## References
- `../index.md`
- `../development-change/secure-sdlc.md`
- `../appendices/system-evidence.md`

## Compliance Mapping
- SOC 2 TSC: CC8
- HIPAA Security Rule: 164.308(a)(8)
