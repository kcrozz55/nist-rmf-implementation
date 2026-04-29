# Security Control Tailoring Decisions
## MedCore Electronic Health Records Platform (EHRP) v4.2.1
### Step 2: Select Security Controls

---

**Organization:** MedCore Health Systems
**System Name:** MedCore Electronic Health Records Platform (EHRP)
**System Version:** v4.2.1
**Baseline:** NIST SP 800-53 Rev 5 HIGH Impact Baseline (265 controls)
**Document Version:** 1.0
**Classification:** SENSITIVE FOR OFFICIAL USE ONLY
**Prepared By:** Amara Osei, ISSO
**Reviewed By:** Jonathan E. Steele, CISO
**Approved By:** Marcus T. Hargrove, Authorizing Official
**Document Date:** February 1, 2026

---

## 1. Purpose

This document records the formal tailoring decisions made to the NIST SP 800-53 Rev 5 HIGH security control baseline for the MedCore Electronic Health Records Platform (EHRP). Tailoring is the process of modifying the initial baseline through scoping, adding organization-defined parameters, assigning parameter values, supplementing controls, and applying compensating controls to ensure the baseline accurately reflects the operational requirements and risk environment of the EHRP system.

All tailoring decisions documented here have been reviewed by the CISO and approved by the Authorizing Official. Departures from the baseline are fully documented with rationale and compensating or alternative measures that maintain an equivalent or higher security posture.

---

## 2. Baseline Summary

| Attribute | Detail |
|-----------|--------|
| Starting Baseline | NIST SP 800-53 Rev 5 HIGH Impact Baseline |
| Total Baseline Controls | 265 controls across 20 control families |
| Tailoring Actions | 12 scoping decisions, 18 parameter value assignments, 7 control enhancements added, 4 compensating controls applied |
| Final Control Count | 272 controls (after additions, prior to implementation) |
| Organization-Defined Parameters Set | 84 parameter values assigned across the applicable control set |

---

## 3. Scoping Decisions - Controls Not Applicable

The following HIGH baseline controls were determined not applicable to the MedCore EHRP system based on scoping guidance in NIST SP 800-53 Rev 5 and the specific operational characteristics of the EHRP environment:

### 3.1 Physical and Environmental Protection (PE)

| Control | Control Name | Decision | Rationale |
|---------|-------------|----------|-----------|
| PE-20 | Asset Monitoring and Tracking | NOT APPLICABLE | EHRP does not include portable physical devices requiring active RFID or GPS tracking. Physical asset inventory is managed under CM-8. |

### 3.2 Program Management (PM)

| Control | Control Name | Decision | Rationale |
|---------|-------------|----------|-----------|
| PM-14 | Testing, Training, and Monitoring | INHERITED | Fully satisfied by MedCore enterprise Information Security Program. EHRP SSP references the organization-level implementation. |
| PM-17 | Protecting CUI on External Systems | NOT APPLICABLE | EHRP does not process Controlled Unclassified Information (CUI). Patient data is governed under HIPAA, not the CUI framework. |

### 3.3 Supply Chain Risk Management (SR)

| Control | Control Name | Decision | Rationale |
|---------|-------------|----------|-----------|
| SR-6 | Supplier Assessments and Reviews | TAILORED - REDUCED SCOPE | MedCore is not a federal agency and does not operate under DFARS supply chain requirements. Implemented at the enterprise level for critical vendors only. EHRP-specific supply chain risk addressed through SA-9 and SA-12. |

### 3.4 Personally Identifiable Information Processing (PT)

| Control | Control Name | Decision | Rationale |
|---------|-------------|----------|-----------|
| PT-7 | Specific Categories of PII | NOT APPLICABLE - ALTERNATIVE | EHRP handles ePHI governed by HIPAA rather than the Federal Privacy Act. Equivalent protections provided through HIPAA-aligned privacy controls. Cross-reference mapping maintained in privacy documentation. |

---

## 4. Control Enhancements Added (Supplemental Controls)

The following control enhancements were added beyond the HIGH baseline to address specific risks identified in the MedCore EHRP risk assessment and HIPAA Security Rule requirements:

### 4.1 AC-2(13) - Account Management: Disable Accounts for High-Risk Individuals

**Rationale:** Healthcare environments present an elevated risk of insider threat from terminated or suspended clinical staff retaining access to ePHI. This enhancement formalizes near-immediate account disablement (within 1 hour of termination notification) and directly addresses HIPAA 164.308(a)(3)(ii)(C) - Termination Procedures.

**Parameter Value:** Account disablement for high-risk individuals must occur within 1 hour of notification to the IAM Administrator.

### 4.2 AU-3(2) - Centralized Management of Planned Audit Record Content

**Rationale:** Given the HIGH integrity impact level and HIPAA audit control requirements (45 CFR 164.312(b)), centralized management of audit record content ensures consistency across all EHRP components (cloud and on-premises) and prevents component-level tampering with audit configurations.

### 4.3 AU-9(3) - Cryptographic Protection of Audit Information

**Rationale:** To satisfy the HIGH integrity requirement for audit logs, cryptographic protection using HMAC-SHA-256 is applied to all audit records stored in the centralized Splunk SIEM. This prevents undetected modification of log records that could undermine forensic investigations or HIPAA compliance audits.

### 4.4 IA-2(12) - Acceptance of PIV Credentials

**Rationale:** All EHRP administrative and privileged user accounts are required to accept PIV-equivalent credentials (FIDO2/WebAuthn hardware keys). This aligns with NIST SP 800-63B Authenticator Assurance Level 3 (AAL3) requirements for accounts with access to HIGH-impact systems processing ePHI.

### 4.5 SC-8(3) - Cryptographic Protection for Message Externals

**Rationale:** The EHRP system transmits ePHI to external parties (Insurance Payers via EDI/X12, Surescripts via e-Rx). Cryptographic protection of message externals prevents metadata-based patient identification even when message content is encrypted.

### 4.6 SI-4(23) - Host-Based Devices

**Rationale:** CrowdStrike Falcon EDR is deployed on all EHRP hosts (cloud and on-premises). This enhancement formalizes the host-based monitoring requirement and ensures EDR coverage is documented as a formal security control, not merely an operational tool.

### 4.7 CA-7(5) - Automation Support for Continuous Monitoring

**Rationale:** The MedCore EHRP ConMon program leverages AWS Security Hub, GuardDuty, Config, and Qualys for automated continuous monitoring. This enhancement formalizes the automation requirements and aligns the ConMon strategy with documented control implementation.

---

## 5. Organization-Defined Parameter Values

The following parameter values were assigned for controls across the HIGH baseline:

### 5.1 Access Control (AC) Parameters

| Control | Parameter | Assigned Value | Rationale |
|---------|-----------|---------------|-----------|
| AC-2(a) | Account types | Individual user, service, privileged/admin, shared emergency break-glass accounts | Reflects EHRP account types in production |
| AC-2(j) | Account review frequency | Quarterly | Aligns with HIPAA requirements; more frequent than annual baseline |
| AC-7 | Invalid login attempts before lockout | 5 consecutive attempts | Balances security with clinical usability |
| AC-7 | Lock-out period | 30 minutes or unlock by administrator | Clinical environment requires administrator override for patient safety |
| AC-11 | Session lock inactivity period | 10 minutes (standard); 3 minutes (patient area workstations) | Patient area workstations require shorter timeout due to ePHI exposure risk |
| AC-12 | Session termination | 8 hours (standard); 4 hours (privileged sessions) | Balances operational continuity with security |

### 5.2 Audit and Accountability (AU) Parameters

| Control | Parameter | Assigned Value | Rationale |
|---------|-----------|---------------|-----------|
| AU-11 | Audit log retention period | 7 years | Exceeds HIPAA minimum (6 years); aligns with MedCore records retention policy |
| AU-5 | Audit processing failure response | Alert ISSO within 15 minutes; system continues with degraded audit capability up to 4 hours | Prioritizes patient care continuity while ensuring timely security notification |

### 5.3 Configuration Management (CM) Parameters

| Control | Parameter | Assigned Value | Rationale |
|---------|-----------|---------------|-----------|
| CM-2 | Baseline configuration update frequency | Upon any significant change; full annual review | Maintains current baseline while managing change control workload |
| CM-6 | Security configuration settings | CIS Level 2 Benchmarks (servers); DISA STIGs (applicable components); MedCore EHRP Security Baseline v2.1 | Documented in SSP CM-6 section |

### 5.4 Identification and Authentication (IA) Parameters

| Control | Parameter | Assigned Value | Rationale |
|---------|-----------|---------------|-----------|
| IA-5(1) | Password minimum length | 14 characters | Exceeds NIST SP 800-63B minimum |
| IA-5(1) | Password history | Last 24 passwords | Prevents password cycling |
| IA-5(1) | Maximum password age | 365 days (no mandatory rotation with MFA per NIST SP 800-63B) | Aligned with NIST guidance - mandatory rotation without compromise creates weaker passwords |

### 5.5 Incident Response (IR) Parameters

| Control | Parameter | Assigned Value | Rationale |
|---------|-----------|---------------|-----------|
| IR-6 | Internal incident reporting timeframe | ISSO: 1 hour; CISO: 4 hours; AO: 24 hours of confirmed incident | Enables timely HIPAA Breach Notification Rule compliance |
| IR-6 | External reporting to HHS OCR | Within 60 days of discovery of breach affecting 500+ individuals | HIPAA Breach Notification Rule - 45 CFR 164.408 |

---

## 6. Compensating Controls

The following compensating controls were implemented where the standard HIGH baseline control cannot be fully implemented due to technical limitations or operational constraints:

### 6.1 Legacy HL7 Interface Engine - Encryption at Rest (SC-28)

**Limitation:** The on-premises Legacy HL7 Interface Engine does not support native encryption of message queues at rest due to hardware and software version constraints (installed 2011).

**Compensating Controls:**
- HL7 message data purged from queue within 15 minutes of successful transmission (data minimization)
- Server uses full-disk encryption (BitLocker with TPM 2.0)
- Network access restricted to only the Local Gateway via dedicated VLAN
- Physical access restricted to IT Operations staff with badge access logging

**AO Acceptance:** Accepted by Marcus T. Hargrove, January 20, 2026. Scheduled full replacement in FY2027 capital plan.

### 6.2 Lab Equipment - FIPS-Validated Cryptography (SC-13)

**Limitation:** Laboratory analyzers and instrument interfaces use proprietary protocols that do not support FIPS 140-2 validated cryptographic modules.

**Compensating Controls:**
- Lab equipment isolated in a dedicated network VLAN with strict firewall rules
- All data transmitted through Local Gateway, which performs protocol translation and encryption before database insertion
- Lab equipment cannot directly access the internet or any non-lab VLAN
- Annual vendor security assessment required under SA-9

**AO Acceptance:** Accepted by Marcus T. Hargrove, January 20, 2026. Vendor assessments scheduled for Q3 2026.

### 6.3 Billing Analytics Read-Only Accounts - MFA (IA-2(1))

**Limitation:** 14 read-only reporting accounts used by the billing analytics team access EHRP data through a read-only database replica on a platform that does not currently support hardware MFA tokens.

**Compensating Controls:**
- Accounts restricted to a network-isolated read replica (no write access to any EHRP component)
- All read-only account activity monitored via SIEM with anomalous query alerts
- Accounts individually named (no shared accounts) and reviewed monthly
- TOTP-based software MFA (Okta Verify) enforced for all read-only accounts
- Platform upgrade for FIDO2/hardware token support scheduled Q2 2026 (POA-2026-M09)

**AO Acceptance:** Accepted by Marcus T. Hargrove, January 20, 2026. Tracked in POA&M as POA-2026-M09.

### 6.4 Emergency Break-Glass Accounts - Standard Account Management (AC-2)

**Limitation:** Four emergency break-glass accounts for use during Active Directory outages cannot follow standard lifecycle management procedures without creating patient care risk.

**Compensating Controls:**
- Break-glass accounts stored in a physical locked safe accessible only to CISO and designated alternates
- All use triggers an immediate SIEM alert to ISSO and CISO
- Passwords rotated immediately after any use and on a quarterly schedule
- All activity reviewed by CISO within 24 hours of any use
- Break-glass account access logged, audited, and reviewed at quarterly security reviews

**AO Acceptance:** Accepted by Marcus T. Hargrove, January 20, 2026.

---

## 7. Inherited Common Controls

The following HIGH baseline controls are fully inherited from MedCore's enterprise Common Control Program:

| Control Family | Inherited Controls | Common Control Provider |
|----------------|-------------------|------------------------|
| PE - Physical Protection | PE-1 through PE-18 (all physical controls) | MedCore Facilities and Physical Security Team |
| PM - Program Management | PM-1 through PM-10, PM-14 | MedCore Information Security Program Office |
| AT - Awareness and Training | AT-1, AT-2 | MedCore Human Resources / Security Awareness Program |
| SA-22 | Unsupported System Components (enterprise policy) | MedCore IT Asset Management |
| CP-6, CP-7 | Alternate Storage/Processing Site | MedCore Business Continuity Program |

---

## 8. Approval

| Role | Name | Signature | Date |
|------|------|-----------|------|
| ISSO | Amara Osei | [Signed] | February 1, 2026 |
| CISO | Jonathan E. Steele | [Signed] | February 3, 2026 |
| System Owner | Dr. Priya Nambiar | [Signed] | February 3, 2026 |
| Authorizing Official | Marcus T. Hargrove | [Signed] | February 5, 2026 |

---

*MedCore Health Systems - SENSITIVE / FOR OFFICIAL USE ONLY*
*Document: Tailoring-Decisions-EHRP-v1.0 | February 2026*
