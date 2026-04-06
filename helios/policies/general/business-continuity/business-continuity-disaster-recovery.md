# Business Continuity and Disaster Recovery Policy

## Purpose
Ensure continuity of critical services and timely recovery from disruptive events by maintaining comprehensive disaster recovery and business continuity plans that describe the actions and resources required for continuous operation and recovery.

## Scope
All business processes, systems, third-party dependencies, and personnel supporting SSC and the SSC Cloud product.

## Compliance Status
SSC is not currently certified under SOC 2 or HIPAA. This policy defines SSC's target controls and is maintained as part of our compliance readiness program.

## Policy
- Maintain documented business continuity and disaster recovery (BCDR) plans.
- Define Recovery Time Objectives (RTO) and Recovery Point Objectives (RPO) for all critical services.
- The BCDR plan must describe the actions and resources required to provide continuous operation and, in the event of interruption, recovery of functions and data within an RTO sufficient to sustain contracted service levels.
- Test BCDR plans at least annually.
- Notify stakeholders at least two weeks prior to planned BCDR testing that may impact the environment or service delivery.
- Maintain communication procedures for internal and external stakeholders during disruptive events.
- Application infrastructure resides in cloud regions providing inherent redundancy and geographic distribution.

## Standards and Procedures
- Identify critical services, dependencies, and single points of failure.
- Document backup, failover, and restoration procedures for each critical service.
- Conduct tabletop exercises or live recovery exercises and record results.
- Review and update plans after significant changes to infrastructure, applications, or third-party dependencies.
- If issues or concerns are raised regarding the BCDR plan, address them in good faith in a timely manner.
- Maintain an application availability objective of 99.99% outside of scheduled maintenance windows.
- Define scheduled maintenance windows and communicate them to affected parties.
- Coordinate with cloud infrastructure providers on their continuity and redundancy capabilities.

## Roles and Responsibilities
- CTO: owns the BCDR plan, approves resource commitments, and authorizes testing.
- Operations/Engineering: maintains BCDR plans, executes exercises, and ensures technical recovery procedures are current.
- Executive Sponsor: approves RTO/RPO targets and business impact assessments.
- All Teams: participate in BCDR exercises and understand their roles during disruptive events.

## Enforcement
- Failure to maintain or test BCDR plans may result in escalation to executive management.

## Review and Exceptions
- Review annually or after major changes or disruptive events.
- Exceptions require documented approval and compensating controls.

## References
- `../index.md`
- `../business-continuity/backup-recovery.md`
- `../security-operations/incident-response.md`
- `CAIQ_architecture_overview.md`

## Compliance Mapping
- SOC 2 TSC: CC9, A1
- HIPAA Security Rule: 164.308(a)(7)
- NIST SP 800-53: CP-1 through CP-13
