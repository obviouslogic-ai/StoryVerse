# Encryption and Key Management Policy

## Purpose
Define standards for cryptography, encryption, and key lifecycle management.

## Scope
All systems and data requiring encryption, including secrets, tokens, and backups.

## Policy
- Encrypt Confidential and Regulated data at rest and in transit.
- Use approved cryptographic algorithms and libraries adhering to FIPS 140-2 requirements.
- Require AES-256 minimum encryption for data at rest.
- Require TLS 1.2 minimum encryption for data in transit.
- Manage keys securely with defined rotation and revocation processes.
- Separate keys by purpose and restrict access to key material.

## Standards and Procedures
- Define key generation, storage, rotation, and destruction procedures.
- Enforce key rotation cadence based on risk and regulatory needs.
- Require authenticated encryption where feasible.
- Maintain key inventory and access logs.
- Monitor, review, and approve key transitions (e.g., activation, suspension, deactivation).
- Define key deactivation procedures at the time of expiration.
- Validate cryptographic modules against FIPS 140-2 standards.

## Roles and Responsibilities
- Security Lead: defines crypto standards and rotation cadence.
- Engineering: implements encryption and key handling.
- Operations: secures secrets management and access controls.

## Review and Exceptions
- Review annually or upon cryptography changes.
- Exceptions require documented approval and compensating controls.

## References
- `../index.md`
- `../access-control/authentication-credentials.md`
- `../appendices/system-evidence.md`

## Compliance Mapping
- SOC 2 TSC: CC6, Confidentiality
- HIPAA Security Rule: 164.312(a)(2)(iv), 164.312(e)(2)(ii)
- CAIQ CEK: CEK-01 through CEK-21
