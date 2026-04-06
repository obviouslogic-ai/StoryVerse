# Log Sanitization Policy

## Purpose
Define SSC requirements for scrubbing, tokenizing, or masking sensitive data in logs to prevent unauthorized exposure.

## Scope
All SSC Cloud application and infrastructure logs.

## Compliance Status
SSC is not currently certified under SOC 2 or HIPAA. This policy defines readiness controls.

## Policy
- Prevent sensitive or regulated data from appearing in logs.
- Scrub, tokenize, or mask PII, PHI, and credentials before log storage.
- Provide mechanisms for service customers to detect sensitive data in logs where applicable.
- Review log sanitization controls at least annually.

## Standards and Procedures
- Define sensitive data categories that must not appear in logs.
- Implement automated scrubbing or redaction in logging pipelines.
- Test log sanitization controls periodically.
- Document log sanitization rules and exceptions.

## Roles and Responsibilities
- Engineering: implements and maintains log sanitization controls.
- Security Lead: defines sensitive data categories and reviews compliance.

## Review and Exceptions
- Review annually or upon significant changes.
- Exceptions require documented approval.

## References
- `../index.md`
- `../security-operations/logging-monitoring.md`
- `../data-protection/data-classification-handling.md`

## Compliance Mapping
- CAIQ LOG: LOG-07.2, LOG-08.1
