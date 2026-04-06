# Data Classification and Handling Policy

## Purpose
Classify data by sensitivity and define handling requirements across the lifecycle.

## Scope
All data processed, stored, or transmitted by SSC, including the SSC Cloud product.

## Policy
- Define data classes (Public, Internal, Confidential, Regulated) extending the established three-tier classification model (Public, Internal, Confidential) with a fourth Regulated tier for data subject to specific regulatory requirements (e.g., PHI, PII under HIPAA).
- Apply protection controls based on classification.
- Limit access to confidential and regulated data to authorized roles on a need-to-know basis.
- Use approved storage, transfer, and disposal methods.
- Treat all PII as Confidential or Regulated data.
- Prohibit transfer of Confidential or Regulated data via unsecured channels (unencrypted email, text messaging, instant messaging, unencrypted FTP).

## Standards and Procedures
- Maintain a data inventory and classification assignments.
- Require AES-256 minimum encryption for Confidential and Regulated data at rest and TLS 1.2 minimum for data in transit.
- Require encryption for Confidential and Regulated data stored on mobile devices and media.
- Prohibit sharing of regulated data outside approved channels.
- Internal data is the default classification when no explicit classification has been assigned.
- Review classifications annually or upon changes to data processing.
- Dispose of data in accordance with NIST SP 800-88 guidelines for media sanitization.

## Roles and Responsibilities
- Data Owners: classify data and approve access.
- Security Lead: defines handling standards and audits compliance.
- Engineering: implements technical protections.

## Review and Exceptions
- Review annually or upon major data changes.
- Exceptions require documented approval and risk assessment.

## References
- `../index.md`
- `../infrastructure-configuration/encryption-key-management.md`
- `../data-protection/data-retention-disposal.md`

## Compliance Mapping
- SOC 2 TSC: CC6, Confidentiality
- HIPAA Security Rule: 164.308(a)(4), 164.312(a)(1)
