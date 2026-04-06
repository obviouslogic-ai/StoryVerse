# Vendor and Subprocessor Management Policy

## Purpose
Manage risks from third-party vendors and subprocessors that support SSC's operations and product delivery. For cloud and CSA CAIQ purposes, this policy covers **supply chain risk management** in the sense of the full ecosystem of third parties, dependencies, and upstream/downstream relationships that could impact the security, integrity, availability, or confidentiality of the service.

## Scope
All third-party services, cloud providers, and subprocessors used by SSC, including those supporting the SSC Cloud product.

**Supply chain (CSA definition):** All external entities, technologies, and dependencies that contribute to the delivery, operation, or support of the Cloud service and whose failure or compromise could materially impact security, availability, integrity, or compliance. This includes (by way of example) cloud infrastructure providers, hosting and CDN providers, identity providers, SaaS integrations, key software dependencies, CI/CD tooling, and contractors or vendors with system access.

## Policy
- Perform due diligence before onboarding vendors and other supply chain relationships.
- Maintain an inventory of supply chain relationships (third parties, subprocessors, and key dependencies).
- Maintain written agreements addressing security, privacy, and compliance obligations.
- Require all supply chain service providers to comply with information security, confidentiality, access control, privacy, audit, personnel policy, and service level requirements and standards.
- Perform risk-based security assessments and periodic risk reviews of supply chain relationships.
- Document and apply shared security responsibility with the infrastructure provider and with customers; review and validate this documentation at least annually.
- Review supply chain (vendor and subprocessor) agreements and providers' IT governance posture at least annually or upon significant changes.
- Track subprocessors and communicate changes to stakeholders where required.

## Standards and Procedures
- Conduct security reviews of prospective vendors and document outcomes.
- Require contractual commitments for data protection and breach notification.
- Maintain a subprocessor and vendor inventory and defined review cadence.
- Establish offboarding procedures to remove access and data upon vendor termination.
- Review vendor agreements and compliance posture at least annually.
- Review and validate shared security responsibility (SSRM) documentation at least annually.
- Implement, operate, and assess the portions of the SSRM for which the organization is responsible.
- Delineate and document control ownership (organization vs. infrastructure provider vs. customer) per the shared responsibility model.

## Roles and Responsibilities
- Procurement/Legal: manages contracts and compliance clauses.
- Security Lead: reviews vendor security posture and SSRM responsibilities.
- System Owners: maintain vendor and supply chain inventories and usage.

## Review and Exceptions
- Review annually or upon major vendor or supply chain changes.
- Exceptions require documented risk acceptance.

## References
- `../index.md`
- `../governance-risk-compliance/risk-management.md`
- `../data-protection/privacy-hipaa.md`
- `../third-party-contracts/customer-contract-change-controls.md`

## Compliance Mapping
- SOC 2 TSC: CC9
- HIPAA Security Rule: 164.308(b)
- CAIQ STA: STA-01 through STA-08, STA-10 through STA-16 (STA-04.1 and STA-09.1/09.2 may be NA where customer SSRM guidance or formal BOM process is not in scope).
