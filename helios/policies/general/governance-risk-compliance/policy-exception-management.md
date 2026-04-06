# Policy Exception Management

## Purpose
Define how SSC records, reviews, approves, and tracks exceptions to information technology and information security policies, standards, and practices. A control deficiency in one area can jeopardize other processes or resources through erroneous data, compromised privacy, or creation of intrusion conduits.

## Scope
All published SSC IT and information security policies, standards, and practices. Applies to all SSC users including employees, contractors, technical support staff, and managers responsible for implementing security controls.

## Compliance Status
SSC is not currently certified under SOC 2 or HIPAA. This policy defines readiness controls.

## Policy
- Require documented approval for all policy exceptions with defined expiration dates.
- Assess risks and compensating controls for each exception.
- Track exception status and remediation activities.
- An exception may be granted in the following situations:
  - **Temporary exception**: immediate compliance would disrupt critical operations.
  - **Equivalent solution**: another acceptable solution with equivalent protection is available.
  - **Superior solution**: a demonstrably superior solution is available.
  - **Legacy system**: a system is being retired and compliance is not possible (risk must be managed with compensating controls).
  - **Long-term exception**: compliance would adversely impact SSC business operations.
  - **Cost-based exception**: the cost to comply offsets the risk of non-compliance (i.e., cost to comply exceeds the reduced risk from compliance).
- Final approval authority rests with the CTO or VP of IT.

## Standards and Procedures
- Submit exception requests through the IT ticketing system for review by the Security Lead.
- Exception evaluation must include:
  - The specific policy or standard for which the exception is requested.
  - The specific device, application, or service affected.
  - Data classification category of the associated asset.
  - The type of data affected (directly or indirectly).
  - The nature of the non-compliance (specific deviation from policy).
  - Business justification and alternatives considered.
  - Assessment of potential risk posed by non-compliance.
  - Plan for managing or mitigating those risks (compensating controls).
  - Anticipated duration of non-compliance.
- Maintain an exception register with owners, compensating controls, and expiry dates.
- Review all active exceptions at least quarterly.
- Require remediation plans for all time-bound exceptions.
- Revoke exceptions in the event of a security incident or control failure.

## Roles and Responsibilities
- CTO / VP of IT: reviews and provides final approval or denial of exception requests.
- Security Lead: maintains exception register, conducts risk assessments, manages the exception process, and recommends changes.
- Executive Sponsor: approves high-risk exceptions.
- Control Owners: implement compensating controls and execute remediation plans.
- All Personnel: submit exception requests when compliance cannot be achieved.

## Review and Exceptions
- Review the exception management process annually or upon significant policy changes.
- Determine if blanket exceptions are appropriate and communicate to the organization.

## References
- `../index.md`
- `../development-change/change-management.md`
- `../governance-risk-compliance/risk-management.md`
- `../governance-risk-compliance/information-security.md`

## Compliance Mapping
- CAIQ CCC: CCC-08.2
- CAIQ GRC: GRC-04.1
- NIST SP 800-53: CA-7, PL-6
