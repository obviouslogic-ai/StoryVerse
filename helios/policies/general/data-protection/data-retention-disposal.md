# Data Retention and Disposal Policy

## Purpose
Define retention periods and secure disposal procedures for data across its lifecycle, ensuring proper sanitization of all media to protect confidential information and PII from unauthorized disclosure.

## Scope
All data stored or processed by SSC, including backups, logs, physical media, electronic media, and all surplus hardware and storage for the SSC Cloud product and corporate IT.

## Compliance Status
SSC is not currently certified under SOC 2 or HIPAA. This policy defines SSC's target controls and is maintained as part of our compliance readiness program.

## Policy
- Retain data only as long as required for business, legal, and regulatory needs.
- Apply secure disposal methods for data at end of life in accordance with NIST SP 800-88 guidelines.
- Document retention schedules and disposal approvals.
- Ensure retention for regulated data (PHI, PII) aligns with applicable regulations.
- IT hardware, documentation, and storage used to process, store, or transmit Confidential Information or PII must not be released for surplus or disposal until properly sanitized.
- All computer desktops, laptops, hard drives, and portable media must be processed through the IT department for proper disposal.
- Authorize personnel to dispose of sensitive information or equipment only through approved methods.

## Standards and Procedures — Retention
- Maintain a retention schedule for each data class aligned with the Data Classification Policy.
- Automate deletions where feasible and log all disposal actions.
- Verify deletion across storage systems and backups.
- Hold data under legal hold when required; legal holds override standard retention schedules.
- Conduct data purging on a regular cadence using the Change Management process.

## Standards and Procedures — Disposal
- **Physical Print Media** shall be disposed of by one or a combination of:
  - Cross-cut shredding using SSC-issued shredders.
  - Locked disposal bins serviced by licensed and bonded information disposal contractors.
  - Incineration by licensed and bonded information disposal contractors.
- **Electronic Media** (disks, tape cartridges, CDs, printer ribbons, flash drives, printer/copier hard drives) shall be disposed of by:
  - Overwriting: using a program to write binary data sector by sector onto the media requiring sanitization.
  - Degaussing: using strong magnets or electric degaussing equipment to magnetically scramble data into an unrecoverable state.
  - Physical Destruction: complete destruction by crushing or disassembling the asset to ensure no data can be extracted or recreated.
- Maintain data destruction and surplus disposal logs of all equipment identified for disposal.
- Retain physical evidence of sanitized assets and data destruction/cleansing actions.
- Follow NIST SP 800-88 guidelines for all media sanitization; simple deletion and formatting are not sufficient.

## Roles and Responsibilities
- Data Owners: define retention periods for their data classes.
- Security Lead: verifies secure disposal processes and maintains disposal audit records.
- IT/Engineering: implements retention controls, executes sanitization, and processes surplus equipment.
- All Personnel: follow disposal procedures for sensitive hard copy documents and report disposal needs.

## Enforcement
- Staff members found in policy violation may be subject to disciplinary action, up to and including termination.

## Review and Exceptions
- Review annually or upon regulatory changes.
- Exceptions require documented approval through the Policy Exception Management process.

## References
- `../index.md`
- `../data-protection/data-classification-handling.md`
- `../appendices/system-evidence.md`
- `../endpoint-asset-management/asset-management-acceptable-use.md`

## Compliance Mapping
- NIST SP 800-88: Media Sanitization
- SOC 2 TSC: Confidentiality, Privacy
- HIPAA Privacy Rule: 164.530(j)
- HIPAA Security Rule: 164.310(d)(2)
