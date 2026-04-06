# Access Control and IAM Policy

## Purpose
Ensure only authorized identities can access systems and data, access is limited to least privilege, and the full account lifecycle is governed from provisioning through deprovisioning.

## Scope
All SSC users, services, and system accounts that access SSC systems or data, including the SSC Cloud product and corporate IT systems.

## Compliance Status
SSC is not currently certified under SOC 2 or HIPAA. This policy defines SSC's target controls and is maintained as part of our compliance readiness program.

## Policy
- Enforce role-based access control (RBAC) and least privilege for all systems and applications.
- Require unique user identities; each person must have a unique individual account that authenticates their access.
- Prohibit shared administrative accounts for accessing production data or systems.
- Segregate privileged roles and require documented approval for elevation.
- Require access reviews at defined intervals: annually for regular access, quarterly for privileged access.
- Employ access control mechanisms capable of detecting, logging, and reporting attempts to breach security.
- Ensure all technology systems can distinguish access privileges and enforce authorization.
- Limit systems access to personnel needed to perform specific responsibilities in support of their role.

## Standards and Procedures
- Provisioning requires documented approval (via ticketing system) and role assignment; privileged accounts require manager or supervisor approval.
- Deprovision access upon termination or role change without delay:
  - Disable accounts on the date of termination for critical applications.
  - Remove inactive accounts per defined timelines.
- When shared accounts are required (service accounts), credentials must be stored in the approved credential management tool.
- No business teams shall be granted root-level access to production infrastructure.
- Super-admin and domain-admin role assignment is restricted to IT management; business users must not promote accounts to administrative roles.
- Enforce account lockout and session controls.
- Maintain access reviews at least annually for regular access and quarterly for privileged access; document and remediate findings.
- SSC or its auditors may audit access reviews upon request with reasonable notice.
- Establish procedures for remote access to SSC data and systems including VPN and MFA requirements.

## Roles and Responsibilities
- System Owners: define access roles and approval requirements.
- Security Lead: oversees access governance, reviews, and audit compliance.
- Managers: approve access for direct reports and ensure timely deprovisioning.
- IT/Operations: executes provisioning, deprovisioning, and maintains access infrastructure.
- All Personnel: safeguard credentials and report unauthorized access.

## Enforcement
- Employees found in violation of this policy may be subject to disciplinary action, up to and including termination of employment.

## Review and Exceptions
- Review annually or upon material changes to roles or systems.
- Exceptions require documented approval and compensating controls through the Policy Exception Management process.

## References
- `../index.md`
- `../access-control/authentication-credentials.md`
- `../access-control/privileged-access-governance.md`
- `../appendices/system-evidence.md`

## Compliance Mapping
- SOC 2 TSC: CC6
- HIPAA Security Rule: 164.308(a)(4), 164.312(a)(1)
- NIST SP 800-53: AC-1 through AC-25
