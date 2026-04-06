# Secure SDLC Policy

## Purpose
Define secure development practices across planning, design, implementation, testing, and deployment.

## Scope
All software developed and maintained for SSC, including the SSC Cloud product.

## Policy
- Embed security and privacy requirements in the SDLC.
- Use code review, automated testing, and secure build pipelines.
- Require remediation of security defects based on severity.
- Maintain secure coding standards aligned with OWASP Top 10 and SANS Top 25.
- Maintain dependency controls and monitor third-party library vulnerabilities.
- Define testing criteria to accept new systems, upgrades, and new versions while ensuring application security and compliance adherence.
- Require web application security assessments for new and major releases based on risk classification.

## Standards and Procedures
- Document security requirements for new features.
- Perform peer code reviews for all changes; require review by leads from different teams for production changes.
- Run automated tests and security checks in CI/CD.
- Track and remediate security vulnerabilities.
- Define acceptance criteria for new releases including security, compliance, and business delivery goals.
- Conduct web application security assessments at Full (manual + automated OWASP), Expedited (automated OWASP Top 10 scan), or Targeted (remediation verification) levels based on release risk.
- Maintain separate environments and databases for development, testing, staging, and production.
- Prohibit use of production data in non-production environments.

## Roles and Responsibilities
- Engineering: implements secure coding practices.
- Security Lead: defines security requirements and reviews exceptions.
- Product Owners: ensure security requirements are in scope.

## Review and Exceptions
- Review annually or upon major process changes.
- Exceptions require documented approval and compensating controls.

## References
- `../index.md`
- `../security-operations/vulnerability-management.md`
- `../development-change/change-management.md`
- `../appendices/system-evidence.md`

## Compliance Mapping
- SOC 2 TSC: CC5, CC8
- HIPAA Security Rule: 164.308(a)(1), 164.308(a)(8)
