# Configuration Management Policy

## Purpose
Define standards for establishing, maintaining, and monitoring secure configuration baselines across physical, logical, and application assets to minimize security risk from misconfiguration.

## Scope
All assets under SSC management including cloud infrastructure, application services, endpoints, network devices, and software configurations supporting the SSC Cloud product and corporate IT.

## Compliance Status
SSC is not currently certified under SOC 2 or HIPAA. This policy defines SSC's target controls and is maintained as part of our compliance readiness program.

## Policy
- Establish and maintain secure configuration baselines for all production and non-production assets.
- Change all vendor-supplied default passwords before deployment.
- Prohibit hardcoded passwords within scripts or applications.
- Keep systems and libraries patched and up-to-date with critical security patches per the Vulnerability Management Policy.
- Apply least privilege access for all applications and services.
- Use role-based access controls (RBAC) for all cloud services; assign users to roles, not directly to resources.
- Require MFA for all administrative, super-admin, and root accounts accessing production environments (service accounts used for non-interactive authentication are exempt).
- Use IP allowlisting to control administrative access to production applications where applicable.
- Manage all configuration changes to production environments through the Change Management process.
- Encrypt all data at rest using AES-256 minimum and all data in transit using TLS 1.2 minimum.
- Ensure cloud storage (e.g., S3 buckets) is not publicly accessible unless explicitly designed for public content; public storage must not contain PII.
- Use IAM roles (not ACLs) to manage access to cloud storage resources.
- Implement cross-region replication for critical components to provide geographic redundancy.

## Standards and Procedures
- Maintain documented configuration baselines for each asset class (endpoints, servers, cloud services, applications).
- Deploy a Web Application Firewall (WAF) for production web applications with rules including IP reputation lists and known-bad-input rule sets.
- Enforce endpoint configurations through the approved MDM solution including USB device restrictions, default group membership controls, and Admin group restrictions.
- End users must not be added to the Admin group on endpoints without ticket submission and IT management approval.
- Monitor configuration changes via automated notifications to designated channels.
- Log all configuration changes through application logging and cloud provider audit trails.
- Review configuration baselines monthly at security team meetings and update compensating controls as needed.
- Validate cloud resource configurations against documented baselines at least quarterly.

## Roles and Responsibilities
- Security Lead: defines configuration baselines and reviews compliance.
- Engineering/DevOps: implements and maintains configurations in alignment with baselines.
- IT Operations: manages endpoint configuration through MDM and monitors for drift.
- All Personnel: report suspected configuration anomalies.

## Review and Exceptions
- Review annually or upon significant infrastructure or application changes.
- Exceptions require documented approval through the Policy Exception Management process with compensating controls.

## References
- `../index.md`
- `../governance-risk-compliance/information-security.md`
- `../development-change/change-management.md`
- `../security-operations/vulnerability-management.md`
- `../infrastructure-configuration/encryption-key-management.md`
- `../endpoint-asset-management/endpoint-management.md`

## Compliance Mapping
- NIST SP 800-53: CM-1 through CM-11
- SOC 2 TSC: CC5, CC6, CC8
- HIPAA Security Rule: 164.312(a)(1), 164.312(e)(1)
