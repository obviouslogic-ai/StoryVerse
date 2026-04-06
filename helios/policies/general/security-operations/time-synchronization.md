# Time Synchronization Policy

## Purpose
Define SSC requirements for maintaining reliable and consistent time sources across all systems.

## Scope
All SSC Cloud application servers, infrastructure, and supporting services.

## Compliance Status
SSC is not currently certified under SOC 2 or HIPAA. This policy defines readiness controls.

## Policy
- Use a reliable, authoritative time source (e.g., NTP) across all systems.
- Synchronize all system clocks to a common reference.
- Monitor for time drift and alert on deviations.
- Document time synchronization configuration.

## Standards and Procedures
- Configure NTP or equivalent on all servers and services.
- Define acceptable time drift thresholds.
- Log and investigate synchronization failures.
- Review time synchronization settings at least annually.

## Roles and Responsibilities
- Operations: configures and monitors time synchronization.
- Security Lead: reviews synchronization requirements for logging integrity.

## Review and Exceptions
- Review annually or upon significant changes.
- Exceptions require documented approval.

## References
- `../index.md`
- `../security-operations/logging-monitoring.md`

## Compliance Mapping
- CAIQ LOG: LOG-05.2, LOG-06.1
