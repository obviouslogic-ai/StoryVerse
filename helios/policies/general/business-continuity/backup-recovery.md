# Backup and Recovery Policy

## Purpose
Ensure data and system recovery capabilities meet business, regulatory, and continuity requirements by defining backup standards, schedules, retention, and restoration procedures.

## Scope
All production data stores, configuration repositories, critical services, and business applications supporting SSC and the SSC Cloud product.

## Compliance Status
SSC is not currently certified under SOC 2 or HIPAA. This policy defines SSC's target controls and is maintained as part of our compliance readiness program.

## Policy
- Perform regular backups of critical data and configurations for all services used to deliver the SSC Cloud product and business operations.
- For each service delivering a backup, a backup, snapshot, or other form of replication must be in place to provide for recovery from an incident.
- Protect backups with encryption and access controls.
- Test restoration procedures on a defined cadence.
- Document backup retention, storage locations, and recovery procedures.
- Ensure backup strategies support the Recovery Time Objectives (RTO) and Recovery Point Objectives (RPO) defined in the Business Continuity and Disaster Recovery Policy.

## Standards and Procedures
- Define backup frequency and retention per service:
  - **Full backups**: at least weekly for critical systems.
  - **Incremental backups**: daily for systems with frequent changes.
  - **Retention**: daily, weekly, monthly, and annual backups with retention period aligned to business and regulatory requirements.
- Monitor backup success and alert on failures; investigate and remediate failed backups promptly.
- Perform periodic restore tests and document results to validate recovery capability.
- Maintain recovery runbooks aligned with BCDR objectives.
- Use automated backup solutions provided by cloud infrastructure (e.g., managed database backups, storage replication) with verified configuration.
- Store backups in geographically separate locations where feasible for disaster recovery purposes.
- All backup schedules and configurations are managed through the Change Management process.

## Roles and Responsibilities
- Operations/Engineering: owns backup execution, monitoring, configuration, and restore testing.
- Security Lead: verifies backup protection controls (encryption, access) and reviews compliance.
- Executive Sponsor: approves RTO/RPO targets and resource commitments.

## Enforcement
- Failure to maintain backup procedures may result in escalation to executive management.

## Review and Exceptions
- Review annually or upon system changes.
- Exceptions require documented approval and compensating controls.

## References
- `../index.md`
- `../business-continuity/business-continuity-disaster-recovery.md`
- `../data-protection/data-retention-disposal.md`
- `../development-change/change-management.md`

## Compliance Mapping
- SOC 2 TSC: CC9, A1
- HIPAA Security Rule: 164.308(a)(7)(ii)(A), 164.308(a)(7)(ii)(B)
- NIST SP 800-53: CP-9, CP-10
