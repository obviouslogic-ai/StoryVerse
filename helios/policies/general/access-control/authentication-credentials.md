# Authentication and Credential Management Policy

## Purpose
Define standards for authentication strength, credential storage, rotation, and recovery.

## Scope
All SSC system users, service accounts, API clients, and administrators supporting the SSC Cloud product and corporate IT.

## Compliance Status
SSC is not currently certified under SOC 2 or HIPAA. This policy defines SSC's target controls and is maintained as part of our compliance readiness program.

## Policy
- Require strong authentication mechanisms for all access.
- Protect credentials using approved cryptographic methods.
- Enforce credential lifecycle management (creation, rotation, revocation).
- Secure password reset and account recovery processes.
- Require minimum 12-character passwords with complexity requirements (uppercase, lowercase, digits, special characters).
- Require unique passwords for each work-related account.
- Do not require arbitrary periodic password rotation per NIST SP 800-63B; force change only upon evidence of compromise.
- Require use of an approved credential management tool for storing passwords.

## Standards and Procedures
- Passwords must be hashed using strong algorithms; plaintext storage is prohibited.
- Passwords must not be transmitted in plaintext over any network.
- Token secrets and encryption keys must be stored securely and rotated on schedule.
- Implement MFA for privileged and administrative access; encourage MFA for all access.
- Log authentication events and monitor for anomalies.
- Disable or delete accounts immediately following employment transfers, terminations, or account inactivity.
- Shared administrative accounts must not be used to access production data; service accounts must use the approved credential manager.
- Review access controls at least annually for regular access and quarterly for privileged access.

## Roles and Responsibilities
- Security Lead: defines credential standards and rotation cadence.
- Engineering: implements and maintains authentication controls.
- Users: safeguard credentials and report compromise promptly.

## Review and Exceptions
- Review annually or upon material changes.
- Exceptions require documented risk assessment and approval.

## References
- `../index.md`
- `../infrastructure-configuration/encryption-key-management.md`
- `../security-operations/logging-monitoring.md`
- `../appendices/system-evidence.md`

## Compliance Mapping
- NIST SP 800-63B: Digital Identity Guidelines
- SOC 2 TSC: CC6, CC7
- HIPAA Security Rule: 164.308(a)(5), 164.312(d)
