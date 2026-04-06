# Endpoint and Mobile Device Management Policy

## Purpose
Define SSC requirements for securing, managing, and monitoring all endpoints and mobile devices that access SSC systems or data, including software installation controls and mobile device acceptable use.

## Scope
All SSC-managed and third-party endpoints (laptops, desktops, smartphones, tablets, e-readers, portable computing devices, wearable devices) used by SSC personnel or contractors to access the SSC Cloud product or corporate IT. This applies to both company-owned and personal devices used to access corporate resources.

## Compliance Status
SSC is not currently certified under SOC 2 or HIPAA. This policy defines SSC's target controls and is maintained as part of our compliance readiness program.

## Policy — Endpoint Security
- Maintain an inventory of all endpoints used to access SSC systems or data.
- Require automatic screen lock on all interactive endpoints after a defined period of inactivity.
- Require storage encryption on all managed endpoints.
- Require anti-malware detection and prevention on all managed endpoints.
- Require software firewall configuration on all managed endpoints.
- Configure data loss prevention (DLP) controls on managed endpoints per risk assessment.
- Enable remote geo-location capabilities on managed mobile endpoints where legally permitted.
- Enable remote wipe capabilities on managed endpoints containing SSC data.
- Validate endpoint compatibility with operating systems and applications before deployment.
- Manage endpoint OS patches, updates, and application changes through the Change Management process.
- Enforce endpoint security controls for all endpoints permitted to access, store, transmit, or process SSC data.

## Policy — Mobile Device Management (MDM)
- All endpoints connecting to corporate resources must be enrolled in the approved MDM solution for consistent inventory, monitoring, patch management, and configuration management.
- Personal devices owned by employees must have the MDM client application installed before connecting to corporate resources.
- Devices not enrolled in MDM or not in compliance with security policies will be denied network access.
- MDM enables IT to take actions on mobile devices including location tracking and remote lock.
- Any attempt to contravene or bypass the MDM implementation will result in immediate disconnection from corporate resources and additional consequences per this policy.
- IT reserves the right to refuse the ability to connect devices to corporate infrastructure if such equipment poses risk.

## Policy — Mobile Device Security
- All mobile devices must be protected by a strong password (not just a PIN).
- All data stored on mobile devices must be encrypted using strong encryption.
- Employees must employ reasonable physical security measures to secure devices against loss or theft.
- Passwords and confidential data must not be stored unencrypted on mobile devices.
- Employees must not save user credentials or sessions when accessing company resources from smartphones or tablets.
- Users must make no modifications that change the nature of the device (jailbreaking, rooting, replacing OS) without express IT approval.
- Report lost or stolen devices to IT immediately; the device will be remotely locked or wiped.
- Follow enterprise-sanctioned data removal procedures when company data is no longer required on a device.

## Policy — Software Installation
- Employees may not install software on SSC computing devices without authorization.
- All software requests require manager approval and must be submitted to IT via the ticketing system.
- Software must be selected from the approved software list maintained by IT, unless no suitable option exists; exceptions require CTO or VP of IT approval.
- IT obtains and tracks software licenses, tests for conflicts and compatibility, and performs installation.
- Software deployments to endpoints are managed through the approved MDM solution.

## Policy — Network Access
- Smart mobile devices access the corporate network using mobile VPN software installed by IT.
- Non-corporate computers used to synchronize or backup data on mobile devices must have current anti-virus and anti-malware software.
- Enterprise data must not be accessed on any hardware that fails to meet SSC's IT security standards.

## Standards and Procedures
- Define minimum endpoint security baselines (encryption, anti-malware, firewall, auto-lock, MDM enrollment).
- Maintain endpoint configuration standards and approved application lists.
- Conduct periodic endpoint compliance checks.
- Maintain an approved list of mobile devices and related software; devices not on the list require IT review.
- Establish audit trails to track endpoint attachment to the corporate network.
- Review and update endpoint policies at least annually or upon significant changes.

## Roles and Responsibilities
- IT/Operations: maintains endpoint/mobile device inventory, MDM administration, configuration, and compliance monitoring.
- Security Lead: defines endpoint security baselines, reviews exceptions, and audits compliance.
- Managers: ensure team compliance with endpoint and mobile device requirements.
- All Personnel: comply with endpoint security requirements, report lost/stolen devices, and refrain from unauthorized software installation.

## Enforcement
- Employees found in violation may be subject to disciplinary action, up to and including termination. Non-compliant devices will be immediately disconnected from corporate resources.

## Review and Exceptions
- Review annually or upon significant changes to device landscape or security posture.
- Exceptions require documented approval by the Security Lead or CTO and compensating controls.

## References
- `../index.md`
- `../endpoint-asset-management/asset-management-acceptable-use.md`
- `../workforce-training/workforce-security-awareness.md`
- `../development-change/change-management.md`
- `../infrastructure-configuration/configuration-management.md`
- `../security-operations/malware-protection.md`

## Compliance Mapping
- CAIQ UEM: UEM-01 through UEM-14
- NIST SP 800-53: AC-19, MP-7, SC-7
- SOC 2 TSC: CC6
- HIPAA Security Rule: 164.310(d), 164.312(a)(1)
