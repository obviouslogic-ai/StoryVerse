# Policy Document Changelog

---

## Phase 5 — STA Section CSA Supply Chain Interpretation (February 10, 2026)

**Purpose:** Align STA (Supply Chain) answers with the Cloud Security Alliance (CSA) CAIQ interpretation of "supply chain" as the third-party ecosystem (cloud providers, vendors, subprocessors, dependencies) and third-party risk management (TPRM), not physical logistics.

**Rationale:** CSA assesses whether the organization identifies and inventories third parties, performs security due diligence, assesses vendor risk, contractually requires security controls, and monitors vendor posture. SSC's vendor and subprocessor management policy supports these controls.

### Questionnaire CSV Changes (SSC_Security_Questionnaire_Answered.csv)
- **STA reclassified from NA to Yes (14 questions):** STA-01.1, 01.2, 02.1, 02.2, 03.1, 05.1, 06.1, 07.1, 08.1, 10.1, 12.1, 13.1, 14.1, 15.1, 16.1. Minimal descriptions added per plan.
- **Unchanged:** STA-04.1 (NA — customer SSRM guidance not in scope), STA-09.1, 09.2 (NA — no formal BOM/SBOM process), STA-11.1 (already Yes).

### Policy Document Changes
- **vendor-subprocessor-management.md:** Updated with CSA supply chain definition (third-party ecosystem); policy bullets for supply chain inventory, risk-based assessments, SSRM documentation and annual review, and provider compliance requirements; standards for SSRM review/validation and control ownership delineation; Security Lead role extended to SSRM responsibilities; CAIQ STA compliance mapping restored (STA-01 through STA-08, STA-10 through STA-16).

---

## Phase 4 — Full Questionnaire Critical Review (February 10, 2026)

**Purpose:** Apply consistent, minimal-information reasoning across every section of the CAIQ questionnaire. Reclassify answers where the section topic does not apply to SSC's SaaS business model. Strip all verbose, redundant, or volunteered descriptions from Column D. Align the vendor-subprocessor-management policy with the updated STA posture.

### Questionnaire CSV Changes (SSC_Security_Questionnaire_Answered.csv)

#### STA: Supply Chain (15 Yes → NA)
- **Rationale:** SSC is a SaaS company with no supply chain to manage. Supply chain risk management, SSRM, and supply chain compliance/assessment questions are not applicable.
- STA-01.1, 01.2, 02.1, 02.2, 03.1, 05.1, 06.1, 07.1, 08.1, 10.1, 12.1, 13.1, 14.1, 15.1, 16.1: Changed from Yes to NA.
- STA-04.1, 09.1, 09.2: Already NA; descriptions blanked.
- STA-11.1: Kept as Yes (customer service agreements, not supply chain).

#### DCS: Data Center Security (21 description cleanups)
- DCS-01.1: Trimmed to brief one-liner ("Cloud-hosted SaaS with no owned data centers.").
- DCS-01.2, 02.1–02.3, 03.1–03.3, 05.1–05.2, 08.1–18.1: Already NA; descriptions blanked (first NA in section establishes the reason).

#### I&S: Infrastructure (1 reclassification + 4 description trims)
- I&S-04.1: Changed from Yes to NA. We use fully managed cloud services and do not manage host/guest OS, hypervisors, or infrastructure control planes.
- I&S-01.1, 03.1, 05.1, 06.1: Descriptions trimmed to remove internal technical specifics.

#### GRC: Governance (1 reclassification)
- GRC-08.1: Changed from Yes to NA. SSC does not participate in cloud-related special interest groups. The original SiteMetric spreadsheet also had this as "Not Applicable."

#### CEK: Encryption (2 cleanups)
- CEK-08.1: Kept as No; description blanked (the No is the answer).
- CEK-15.1: Already NA; description blanked.

#### BCR: Business Continuity (2 description cleanups + 2 trims)
- BCR-10.2: Trimmed to "No owned data centers."
- BCR-11.1: Already NA; description blanked.
- BCR-08.1, 08.2: Descriptions trimmed to remove extra detail.

#### LOG: Logging (1 description blank + 1 trim)
- LOG-13.1: Already NA; description blanked.
- LOG-08.1: Trimmed to remove implementation specifics.

#### DSP: Data Security & Privacy (7 description trims)
- DSP-02.1, 07.1, 08.1, 08.2, 10.1, 16.1, 17.1: Descriptions trimmed to remove internal technical specifics and extra sentences.

#### CCC: Change Control (2 description trims)
- CCC-07.1, 09.1: Descriptions trimmed to remove tool-specific language and extra detail.

#### IAM: Identity & Access (3 description trims)
- IAM-10.1, 13.1, 13.2: Descriptions trimmed to remove implementation specifics.

### Policy Document Changes

#### vendor-subprocessor-management.md (REWRITTEN)
- Removed all supply chain terminology ("supply chain," "SSRM," "shared security responsibility model").
- Removed supply chain-specific procedures: SSRM documentation, supply chain provider compliance requirements, supply chain agreements review, supply chain risk assessments, supply chain conformance assessments.
- Removed Compliance Lead role (supply chain conformance assessment role).
- Removed CAIQ STA mapping (no longer applicable).
- Retained core vendor/subprocessor management: due diligence, written agreements, subprocessor tracking, risk review, security reviews, offboarding procedures, annual agreement review.

### Guiding Principles Applied
1. If a section topic does not apply, answers are NA — same logic as "no supply chain to manage."
2. First NA in a logical group states the brief reason; all subsequent NAs are blank.
3. No descriptions with the answer is No — the No speaks for itself.
4. Never volunteer weaknesses or mention what is partial/in progress.
5. No internal technical details (library names, config variables, architecture specifics).
6. Column D is optional — only include when it adds genuine value.

---

## Phase 3 — Legacy Policy Rewrite (February 10, 2026)

**Purpose:** Rewrite all content from the legacy SSC IT Governance Guide and IT Policy Guide (SharePoint) into the new standardized markdown policy format, ensuring a single unified policy set that covers both CAIQ/cloud requirements and established IT governance content.

**Source Documents Rewritten:**
- SSC - IT Governance Guide.docx → distributed across applicable policy files
- SSC - IT Policy Guide.docx → distributed across applicable policy files

### New Policy Files Created

#### configuration-management.md (NEW)
**Source:** IT Policy Guide — Configuration Management Policy
- Baseline configuration and system hardening policy with standards for physical, logical, and cloud assets.
- Default password change requirements.
- Prohibition on hardcoded passwords.
- Least privilege, RBAC for cloud services, MFA for admin/super-admin/root.
- IP allowlisting for production administrative access.
- AES-256 at rest, TLS 1.2 in transit encryption standards.
- Cloud storage security (no public S3 with PII, IAM roles over ACLs).
- Cross-region replication for geographic redundancy.
- WAF deployment with IP reputation and known-bad-input rule sets.
- Endpoint configuration via MDM (USB restrictions, Admin group controls).
- Configuration change monitoring via automated notifications.
- NIST SP 800-53 CM family compliance mapping.

#### ai-usage.md (NEW)
**Source:** IT Policy Guide — Artificial Intelligence Usage Policy
- Prohibition on entering PII into any AI tool.
- Prohibition on entering business-sensitive data (sales, marketing, code, finances, contracts) into external AI tools.
- Requirement for Security Lead approval of AI tools.
- AI responses not to be used as reliable sources for legal/medical/adjudication decisions.
- AI-generated code subject to same SDLC review as human code.
- Awareness that external AI services copy, store, and use submitted data.
- Approved AI tools list maintenance.

### Existing Policies Substantially Rewritten

#### asset-management-acceptable-use.md (REWRITTEN)
**Source:** IT Policy Guide — Acceptable Use Policy, Blogging/Social Media, System/Network Activities
- Expanded from 37 lines to comprehensive policy covering:
  - Asset management with lifecycle tracking.
  - General acceptable use standards (10-minute screensaver lock, audit rights).
  - Prohibited activities: illegal activity, IP violations, unauthorized access, malware introduction, password sharing, security breaches, port scanning, network sniffing.
  - Email/communication rules: no spam, no harassment, no forged headers.
  - Social media/blogging policy: disclaimers required, no confidential info, no reputational harm.
  - Enforcement provisions.

#### workplace-security.md (REWRITTEN)
**Source:** IT Governance Guide — Physical Security; IT Policy Guide — Physical Security Policy, Clean Desk Policy
- Expanded from 34 lines to comprehensive policy covering:
  - Physical security perimeters and access controls.
  - 24-hour video surveillance, badge access, physical locks, visitor sign-in.
  - Office security (SSC offices do not house cloud infrastructure).
  - Visitor escort and monitoring requirements.
  - Complete Clean Desk policy (locked storage, screen lock, shutdown at EOD, secure document disposal, whiteboard erasure, printer clearing).
  - Environmental protections (fire, flood, earthquake, explosion, utilities).
  - NIST SP 800-53 PE family and HIPAA Physical Safeguards mapping.

#### data-retention-disposal.md (REWRITTEN)
**Source:** IT Policy Guide — Data Retention Policy, Data Destruction and Sanitization Policy
- Expanded from 37 lines to comprehensive policy covering:
  - Retention aligned with business, legal, and regulatory needs.
  - NIST SP 800-88 media sanitization requirements.
  - Physical print media disposal: cross-cut shredding, locked disposal bins, incineration.
  - Electronic media disposal: overwriting, degaussing, physical destruction.
  - IT processing requirement for all equipment disposal.
  - Destruction logging and evidence retention.
  - Legal hold provisions.

#### access-control-iam.md (REWRITTEN)
**Source:** IT Governance Guide — Access Control; IT Policy Guide — User Account Management Policy
- Expanded from 39 lines to comprehensive policy covering:
  - RBAC and least privilege with unique user identities.
  - Shared administrative account prohibition for production.
  - Access review cadence: annual for regular, quarterly for privileged.
  - Provisioning via ticketing system with approval workflows.
  - Deprovisioning on termination (disable immediately, remove per timeline).
  - Service accounts in approved credential manager.
  - Root access restricted to IT; business users cannot promote to admin roles.
  - Audit provisions for access reviews.
  - NIST SP 800-53 AC family compliance mapping.

#### endpoint-management.md (REWRITTEN)
**Source:** IT Policy Guide — Mobile Device Acceptable Use Policy, Software Installation Policy, MDM sections
- Expanded from 49 lines to comprehensive policy covering:
  - Endpoint security baselines (encryption, anti-malware, firewall, auto-lock).
  - MDM enrollment required for all corporate-connected devices (including personal).
  - MDM capabilities: location tracking, remote lock, remote wipe.
  - Mobile device security: strong password (not PIN), encrypted storage, no jailbreaking.
  - No credential saving on mobile devices.
  - Software installation controls: manager approval, IT installation, approved software list.
  - Network access via VPN with SSL.
  - Lost/stolen device reporting and response.
  - BYOD requirements.
  - NIST SP 800-53 AC-19, MP-7, SC-7 compliance mapping.

#### backup-recovery.md (REWRITTEN)
**Source:** IT Governance Guide — Disaster Recovery; IT Policy Guide — Backup Policy
- Expanded from 37 lines to comprehensive policy covering:
  - Full weekly + daily incremental backup schedule.
  - Retention aligned with regulatory requirements.
  - Cloud-managed backup verification.
  - Geographic separation for disaster recovery.
  - RTO/RPO alignment with BCDR policy.
  - Change Management for backup configuration changes.
  - NIST SP 800-53 CP-9, CP-10 compliance mapping.

#### malware-protection.md (REWRITTEN)
**Source:** IT Policy Guide — Application Requirements (Malware Protection section)
- Expanded from 40 lines to comprehensive policy covering:
  - Real-time scanning and hourly definition updates.
  - Centralized cloud-based administration console.
  - Protection modules: anti-malware, advanced threat control, firewall, content control, device control.
  - Device scan scope: local drives, CD/DVD, USB.
  - Automated email notifications on detection.
  - Non-corporate device anti-malware requirements.
  - NIST SP 800-53 SI-3 compliance mapping.

#### policy-exception-management.md (REWRITTEN)
**Source:** IT Governance Guide — Information Security Exception Request Process
- Expanded from 37 lines to comprehensive policy covering:
  - Six defined exception situations: temporary, equivalent solution, superior solution, legacy system, long-term, cost-based.
  - Detailed evaluation criteria: specific policy, affected asset, data classification, data types, nature of non-compliance, alternatives, risk assessment, compensating controls, duration.
  - CTO/VP of IT final approval authority.
  - Ticketing system submission process.
  - Quarterly exception review.
  - Revocation on incident or control failure.

#### privacy-hipaa.md (REWRITTEN)
**Source:** IT Policy Guide — Data Protection Policy, Data Privacy Policy
- Expanded from 37 lines to comprehensive policy covering:
  - Explicit prohibition on selling, renting, or sharing customer data.
  - Processing only for intended purpose.
  - User access, correction, amendment, and deletion rights.
  - Physical, logical, and process safeguards.
  - PII encrypted at rest and in transit.
  - Immediate reporting of suspected data exposure.
  - Privacy impact assessments for new systems.
  - NIST SP 800-53 privacy control family mapping.

#### business-continuity-disaster-recovery.md (REWRITTEN)
**Source:** IT Governance Guide — Disaster Recovery & Business Continuity; IT Policy Guide — related sections
- Expanded from 37 lines to comprehensive policy covering:
  - BCDR plan documentation requirements.
  - RTO/RPO definitions for critical services.
  - Stakeholder notification 2 weeks before planned testing.
  - 99.99% availability objective.
  - Scheduled maintenance windows.
  - Cloud provider coordination.
  - NIST SP 800-53 CP family compliance mapping.

#### governance-program.md (REWRITTEN)
**Source:** IT Governance Guide — Information Security Program, Security Controls, Risk Management
- Expanded from 37 lines to comprehensive policy covering:
  - NIST SP 800-53 foundational framework with ITIL policy prescriptions.
  - CIA triad principles.
  - Layered security program (training, policies, procedures, standards, frameworks, guidelines).
  - Security benchmarking and measurement.
  - Security Committee with defined roles.
  - Monthly security audits, quarterly training, manual code review, pen testing.
  - Compliance readiness against SOC 2, HIPAA, NIST SP 800-53.
  - NIST SP 800-53 PM family compliance mapping.

#### workforce-security-awareness.md (REWRITTEN)
**Source:** IT Governance Guide — Personnel Security, Security Awareness Training; IT Policy Guide — Work from Home Policy
- Expanded from 41 lines to comprehensive policy covering:
  - Background check scope: criminal, employment verification, education verification, OFAC.
  - Insurance requirements for employees.
  - Training cadence: onboarding + annual all-staff + quarterly IT/engineering.
  - Training content specifics.
  - Complete remote work policy: workspace requirements, Wi-Fi speed minimums, VPN for PII, equipment responsibilities, property return on termination.
  - NIST SP 800-53 AT and PS family compliance mapping.

#### logging-monitoring.md (UPDATED)
- Added 180-day minimum log retention requirement (from IT Governance Guide).
- Added periodic log verification requirement for forensic investigation readiness.
- Added industry-standard log management tool requirement.

### index.md (REORGANIZED)
- Reorganized Policy Catalog from flat list to categorized sections:
  - Governance, Risk, and Compliance
  - Access Control and Identity
  - Data Protection and Privacy
  - Security Operations
  - Infrastructure and Configuration
  - Development and Change
  - Business Continuity
  - Endpoint and Asset Management
  - Workforce and Training
  - Third Party and Contracts
- Added new policies (configuration-management.md, ai-usage.md) to catalog.
- Updated SOC 2 TSC mapping with new policy references.
- Updated HIPAA mapping with new policy references.
- Added comprehensive NIST SP 800-53 control family mapping section.

---

## Phase 2 — Legacy Policy Alignment (February 10, 2026)

**Purpose:** Align new CAIQ-based policies with existing SSC IT Governance Guide and IT Policy Guide from the Technology SharePoint to ensure no governance-level contradictions exist and to incorporate established framework references, standards, and procedures into the cloud-product-oriented policy set.

**Source Documents Reviewed:**
- SSC - IT Governance Guide.docx (Policy Documentation folder)
- SSC - IT Policy Guide.docx (Policy Documentation folder)
- 2024-11-13 SSC Customer Portal Website Terms of Use.DOCX
- Azure Migration Plan 2025.docx
- SOP_HyperV_Failback_ASR.docx

### 11. information-security.md

**Changes (Legacy Alignment):**
- Added NIST SP 800-53 as the foundational security framework reference (existing governance doc claims NIST SP 800-53 compliance)
- Added ITIL-based process governance reference for service management, incident management, and change management
- Added monthly security control reviews for core infrastructure and applications (aligns with existing monthly security audit practice)
- Added compliance readiness against SOC 2, HIPAA, and NIST SP 800-53 frameworks
- Added NIST SP 800-53 control family references to Compliance Mapping

### 12. encryption-key-management.md

**Changes (Legacy Alignment):**
- Added FIPS 140-2 cryptographic module requirement (existing Encryption Key Management Policy references FIPS 140-2)
- Added AES-256 minimum for data at rest (matches existing standard of AES-256 bit encryption)
- Added TLS 1.2 minimum for data in transit (matches existing HTTPS/TLS 1.2 standard)
- Added FIPS 140-2 validation to Standards and Procedures

### 13. authentication-credentials.md

**Changes (Legacy Alignment):**
- Added minimum 12-character password requirement (matches existing Password Construction Guidelines)
- Added password complexity requirements: uppercase, lowercase, digits, special characters (matches existing guidelines)
- Added NIST SP 800-63B reference: no arbitrary periodic rotation, force change on compromise evidence (matches existing Password Protection Policy)
- Added unique password per work-related account requirement (matches existing guidelines)
- Added approved credential management tool requirement (matches existing LastPass policy)
- Added no plaintext password transmission requirement (matches existing application development standards)
- Added immediate account disable/delete on transfer/termination (matches existing User Account Management Policy)
- Added shared administrative account prohibition for production data (matches existing governance standards)
- Added access control review cadence: annually for regular, quarterly for privileged (matches existing governance standards)
- Added NIST SP 800-63B to Compliance Mapping

### 14. vulnerability-management.md

**Changes (Legacy Alignment):**
- Added 90-day remediation timeline for critical/high severity vulnerabilities (matches existing Patch Management Policy)
- Added expedited process for imminent threats (matches existing governance language)
- Added OWASP Top 10 and SANS Top 25 references for application vulnerability prevention (matches existing Web Application Security Policy)
- Added OWASP Risk Rating Methodology for severity levels (matches existing risk classification approach)
- Added periodic static and dynamic application security assessments (matches existing code review and assessment requirements)
- Added non-production testing requirement before applying patches to production (matches existing patch management standards)

### 15. breach-notification.md

**Changes (Legacy Alignment):**
- Added 48-hour notification to regulators (matches existing Data Breach Notification Policy)
- Added 1-hour internal escalation for critical incidents (matches existing incident notification timeline)
- Added 24-hour written report requirement (matches existing reporting timeline)
- Added forensic investigation requirement with qualified investigators (matches existing forensic investigation procedures)
- Added communication plan for internal employees, public, and affected parties (matches existing Data Breach Notification Policy)
- Added final breach report requirements: extent, data compromised, evidence/logs, corrective actions, security impact (matches existing procedures)
- Added executive approval requirement for external communications (matches existing governance standards)

### 16. secure-sdlc.md

**Changes (Legacy Alignment):**
- Added OWASP Top 10 and SANS Top 25 reference for secure coding standards (matches existing Web Application Security Policy)
- Added web application security assessment requirement for new/major releases (matches existing assessment policy)
- Added three assessment levels: Full (manual + automated OWASP), Expedited (automated OWASP Top 10), Targeted (remediation verification) — matches existing Web Application Security Policy
- Added peer code review by leads from different teams for production changes (matches existing code review process)
- Added separate environments requirement for dev, testing, staging, production (matches existing SDLC process)
- Added prohibition of production data in non-production environments (matches existing application requirements)

### 17. incident-response.md

**Changes (Legacy Alignment):**
- Added 4-phase IRP structure: Preparation, Detection/Analysis, Containment/Eradication/Recovery, Post-Incident Activity (matches existing Incident Response Plan structure)
- Added severity scoring methodology based on: affected scope, escalation probability, commonality, damage potential, business impact (matches existing severity scoring system)
- Added 1-hour critical incident escalation timeline (matches existing notification requirements)
- Added 24-hour written report requirement for critical incidents (matches existing RCA timeline)
- Added After Action Report (AAR) requirement for significant incidents (matches existing post-incident process)
- Added 24x7x365 coverage for critical incidents (matches existing monitoring standards)
- Added CTO engagement requirement for critical incidents (matches existing escalation procedures)
- Added incident report content requirements: description, downtime, SLA impact, history, resolution, root cause, prevention plan (matches existing RCA template)

### 18. change-management.md

**Changes (Legacy Alignment):**
- Added Standard Change definition: pre-authorized repeatable change with documented procedure and predictable outcomes (matches existing Change Management Policy)
- Added Normal Change definition: follows full change management process with risk assessment and approval (matches existing policy)
- Added Emergency Change definition: urgent change requiring immediate implementation, still requires CTO/delegate authorization (matches existing policy)
- Added requirement for documented implementation and backout/rollback steps specific enough for any qualified engineer (matches existing Jira ticket requirements)
- Added non-production testing requirement before production deployment (matches existing change management standards)
- Added change management system logging requirement (matches existing PCM board process)

### 19. data-classification-handling.md

**Changes (Legacy Alignment):**
- Documented 4-tier model as evolution of existing 3-tier model (Public/Internal/Confidential) with addition of Regulated tier for regulatory compliance
- Added PII must be treated as Confidential or Regulated (matches existing Data Classification Policy)
- Added prohibition on unsecured channel transfers for Confidential/Regulated data (matches existing handling requirements)
- Added AES-256 and TLS 1.2 encryption specifics for Confidential/Regulated data (matches existing encryption standards)
- Added mobile device/media encryption requirement for Confidential/Regulated data (matches existing classification policy)
- Added Internal as default classification when none assigned (matches existing policy)
- Added NIST SP 800-88 reference for data disposal/sanitization (matches existing Data Destruction and Sanitization Policy)

### 20. workforce-security-awareness.md

**Changes (Legacy Alignment):**
- Added background check scope: criminal record, employment verification, education verification (matches existing Personnel Security standards)
- Updated training cadence: annual refreshers for all staff plus quarterly security sessions for IT/engineering teams (reconciles existing quarterly security training practice with annual minimum baseline)
- Added remote work security specifics: encrypted Wi-Fi, VPN for PII access, physical workspace security (matches existing Work from Home Policy)

### Legacy Alignment Notes

**No contradictions found** between existing IT Governance Guide / IT Policy Guide and the new CAIQ-aligned policies. All changes in this phase are additive enhancements that bring governance-level specificity from the legacy documents into the new cloud-product-oriented policy set.

**Technology-specific differences (intentional and acceptable):**
- Legacy docs reference on-premises infrastructure (Hyper-V, physical DCs, Addigy MDM, local AD). New policies reference AWS cloud infrastructure. These are different technology stacks for different products.
- Legacy docs reference background screening application. New policies reference SSC Cloud product.
- Legacy docs reference Salesforce, Jira, CircleCI, GitHub Advanced Security. New policies reference cloud-native tooling.
- AWS regions: Legacy governance doc references us-east-1 and us-west-2 for the background screening application. Cloud product infrastructure may use different regions.

**Governance-level alignment (confirmed consistent):**
- NIST SP 800-53 as foundational framework
- FIPS 140-2 for cryptographic standards
- OWASP/SANS for application security
- NIST SP 800-63B for password/authentication standards
- NIST SP 800-88 for media sanitization
- 4-phase incident response structure
- Standard/Normal/Emergency change types
- Data classification tiers (3→4, additive)
- Vendor security review process and requirements
- Clean desk, physical security, and remote work requirements
- Annual penetration testing by independent third parties
- Background check requirements and personnel security standards

---

## Phase 1 — CAIQ Questionnaire Alignment (February 10, 2026)

**Purpose:** Align all policy documents with CAIQ v4.1.0 Security Questionnaire responses to ensure every claim in the questionnaire is supported by documented policy language.

---

## 1. vulnerability-management.md

**Changes:**
- Added monthly minimum detection cadence (supports TVM-03.1)
- Added risk-based prioritization using industry-recognized framework (supports TVM-09.1)
- Added requirement to identify and track third-party and open-source library vulnerabilities (supports TVM-06.1)
- Added requirement to update detection tools, threat signatures, and compromise indicators weekly (supports TVM-05.1)
- Added penetration testing by independent third parties requirement (supports TVM-07.1)
- Added scheduled and emergency response to vulnerability identification (supports TVM-08.1)
- Added vulnerability metrics establishment and monitoring at defined intervals (supports TVM-12.1)
- Added tracking and reporting to stakeholders requirement (supports TVM-11.1)
- Added reference to threat-analysis.md
- Updated CAIQ compliance mapping to include TVM-01 through TVM-12

---

## 2. logging-monitoring.md

**Changes:**
- Added log protection language to include modification and deletion (supports LOG-10.1)
- Added requirement to report monitoring system anomalies and failures (supports LOG-14.1)
- Added requirement to immediately notify accountable parties about anomalies (supports LOG-14.2)
- Added monitoring and reporting on cryptographic operations and encryption activities (supports LOG-11.1)
- Added key lifecycle event logging requirement (supports LOG-12.1)
- Added anomaly response procedures to Standards section (supports LOG-05.2)
- Added anomaly and failure reporting procedures to Standards section (supports LOG-14.1)
- Added encryption and key management events to logging scope (supports LOG-11.1, LOG-12.1)
- Added audit log access restriction to Standards section (supports LOG-04.1)
- Added reference to encryption-key-management.md
- Updated CAIQ compliance mapping to include LOG-01 through LOG-14

---

## 3. key-lifecycle-custody.md

**Changes:**
- Updated Purpose to include change review, risk management
- Added requirement to review and approve crypto technology changes through change management (supports CEK-05.1)
- Added downstream impact analysis for proposed crypto changes including residual risk, cost, and benefits (supports CEK-06.1)
- Added crypto risk program including risk assessment, treatment, context, monitoring, and feedback (supports CEK-07.1)
- Added operational continuity risk assessment versus key material control risk (supports CEK-20.1)
- Added corresponding Standards and Procedures entries for each new policy item
- Added references to change-management.md and risk-management.md

---

## 4. incident-response.md

**Changes:**
- Added requirement to maintain incident records in a secure repository (supports SEF-09.1)
- Added incident response plan testing at planned intervals (supports SEF-04.1)
- Added information security incident metrics establishment and monitoring (supports SEF-05.1)
- Added triage procedures for security-related events (supports SEF-06.1)
- Added regular review of incident records for patterns, root causes, and systemic vulnerabilities (supports SEF-09.2)
- Added corresponding Standards and Procedures entries for testing, metrics, records, and corrective measures
- Added reference to law-enforcement-requests.md
- Updated CAIQ compliance mapping to include SEF-01 through SEF-10

---

## 5. vendor-subprocessor-management.md

**Changes (Phase 1):**
- Updated Purpose to include shared security responsibilities
- Added shared security responsibility model (SSRM) and supply chain language (supports STA-02.1, STA-03.1, STA-05.1, STA-06.1, STA-12.1 through STA-16.1)
- Added Compliance Lead role for internal conformance assessments
- Added reference to customer-contract-change-controls.md
- Updated CAIQ compliance mapping to include STA-01 through STA-16

**Note:** Phase 4 subsequently removed all supply chain and SSRM language. STA questions reclassified as NA. See Phase 4 changelog above.

---

## 6. customer-contract-change-controls.md

**Changes:**
- Updated Purpose to include service agreements
- Added data access upon contract termination provisions including data format, storage duration, scope, and deletion policy (supports IPY-04.1)
- Added service agreement provisions covering: scope and location of services, information security requirements, change management, logging and monitoring, incident management, right to audit, service termination, interoperability, data privacy, and operational resilience (supports STA-11.1)
- Added Standards entries for data portability and service agreement completeness review
- Added Legal/Compliance responsibility for service agreement provisions
- Added reference to interoperability-portability.md
- Updated CAIQ compliance mapping to include STA-11.1

---

## 7. encryption-key-management.md

**Changes:**
- Added key transition monitoring, review, and approval procedures (supports CEK-16.1)
- Added key deactivation procedures at time of expiration (supports CEK-17.1)
- Updated CAIQ compliance mapping to include CEK-01 through CEK-21

---

## 8. audit-assurance.md

**Changes:**
- Added requirement to regularly review and report remediation status of audit findings to relevant stakeholders (supports A&A-06.2)
- Updated CAIQ compliance mapping to include A&A-02 and A&A-04

---

## 9. threat-analysis.md

**Changes:**
- Added risk-based method for threat prioritization and mitigation using industry-recognized framework (supports TVM-10.1)
- Updated CAIQ compliance mapping to include TVM-10.1

---

## 10. secure-sdlc.md

**Changes:**
- Added testing criteria requirement to accept new systems, upgrades, and new versions while ensuring security and compliance (supports AIS-05.1)
- Added acceptance criteria definition for new releases in Standards section (supports AIS-05.1)

---

## Policies Reviewed With No Changes Required

The following policies were reviewed and confirmed to already support all claims made in the CAIQ questionnaire responses:

- access-control-iam.md
- api-security-review.md
- asset-management-acceptable-use.md
- authentication-credentials.md
- backup-recovery.md
- breach-notification.md
- business-continuity-disaster-recovery.md
- change-management.md
- compliance-requirements-register.md
- compliance-verification.md
- data-classification-handling.md
- data-flow-documentation.md
- data-ownership-stewardship.md
- data-retention-disposal.md
- endpoint-management.md
- environment-risk-classification.md
- governance-program.md
- hipaa-security-rule-safeguards.md
- independent-audit-plan.md
- information-security.md
- interoperability-portability.md
- law-enforcement-requests.md
- log-sanitization.md
- malware-protection.md
- network-configuration-review.md
- non-production-data-handling.md
- policy-exception-management.md
- privacy-hipaa.md
- privacy-impact-assessment.md
- privileged-access-governance.md
- risk-management.md
- stakeholder-engagement.md
- time-synchronization.md
- workforce-security-awareness.md
- workplace-security.md
