# Security Categorization Decision Memorandum
## MedCore Electronic Health Records Platform (EHRP) v4.2.1

---

**MEMORANDUM**

**DATE:** January 15, 2026  
**TO:** Authorizing Official — Marcus T. Hargrove, CEO  
**FROM:** Amara Osei, Information System Security Officer (ISSO)  
**THROUGH:** Jonathan E. Steele, Chief Information Security Officer (CISO)  
**SUBJECT:** Formal Security Categorization Decision — MedCore Electronic Health Records Platform (EHRP) v4.2.1  
**CLASSIFICATION:** SENSITIVE — FOR OFFICIAL USE ONLY  

---

## 1. Purpose

This memorandum documents the formal security categorization decision for the MedCore Electronic Health Records Platform (EHRP) version 4.2.1, in accordance with Federal Information Processing Standard (FIPS) Publication 199, *Standards for Security Categorization of Federal Information and Information Systems*, and NIST Special Publication 800-60 Volume I and II, *Guide for Mapping Types of Information and Information Systems to Security Categories*.

The purpose of this categorization is to establish the system's impact level, which drives selection of the appropriate NIST SP 800-53 Rev 5 security control baseline and forms the foundation for the Risk Management Framework (RMF) process for the EHRP system.

---

## 2. System Description

| Attribute | Detail |
|-----------|--------|
| System Name | MedCore Electronic Health Records Platform (EHRP) |
| System Version | v4.2.1 |
| System Owner | Dr. Priya Nambiar, CIO |
| Organization | MedCore Health Systems, Atlanta, Georgia |
| Operating Environment | Hybrid — AWS GovCloud (Primary) + On-Premises (Legacy Components) |
| System Type | Major Application |
| Primary Function | Electronic Health Record management, clinical workflow support, patient data storage and retrieval |
| Primary Data Types | Electronic Protected Health Information (ePHI), Personally Identifiable Information (PII), clinical records, billing and claims data, laboratory results, medical imaging |
| User Population | ~1,847 authorized users (clinicians, administrative staff, IT personnel) |
| Number of Records | Approximately 340,000 patient records |

---

## 3. Information Types and Security Categories

The following information types were identified and analyzed using NIST SP 800-60 Volume II to determine the applicable security impact levels for Confidentiality, Integrity, and Availability:

### 3.1 Electronic Protected Health Information (ePHI) / Patient Clinical Records

**NIST SP 800-60 Reference:** C.3.1.1 — Individual Health Information  
**Rationale:**

- **Confidentiality: HIGH** — Unauthorized disclosure of patient clinical information violates HIPAA Privacy Rule requirements and could cause serious harm to patients, including discrimination in employment or insurance, emotional distress, and reputational damage. Given the sensitivity of mental health, substance abuse, and HIV-related records present in the EHRP system, the potential impact of a confidentiality breach is assessed as HIGH.

- **Integrity: HIGH** — Unauthorized modification or corruption of patient clinical records could result in incorrect diagnoses, medication errors, inappropriate treatments, or patient death. The direct connection between data integrity and patient safety outcomes justifies a HIGH integrity impact level.

- **Availability: HIGH** — The EHRP system is the primary platform for clinical workflow across all MedCore facilities. System unavailability during a clinical emergency could prevent timely access to critical patient data (medication allergies, active diagnoses, treatment histories) and result in patient harm. A HIGH availability impact level is warranted given the 24/7/365 operational requirement and patient safety implications.

**SC: ePHI/Patient Clinical Records = {(C, HIGH), (I, HIGH), (A, HIGH)}**

### 3.2 Billing and Claims Information

**NIST SP 800-60 Reference:** C.2.8.1 — Financial Management  
**Rationale:**

- **Confidentiality: MODERATE** — Billing information includes personally identifiable financial data. While unauthorized disclosure would cause significant harm, the primary patient harm vector is clinical rather than financial.
- **Integrity: HIGH** — Integrity failures in billing data could result in fraudulent claims, regulatory violations (False Claims Act), and patient financial harm.
- **Availability: MODERATE** — Billing operations can tolerate short-term interruptions without direct patient safety impact, though prolonged unavailability would cause significant operational disruption.

**SC: Billing/Claims = {(C, MODERATE), (I, HIGH), (A, MODERATE)}**

### 3.3 Administrative and Operational Data

**NIST SP 800-60 Reference:** C.2.1.1 — General Administrative Information  
**Rationale:**

- **Confidentiality: MODERATE** — Administrative data contains PII (employee records, scheduling) but is less sensitive than clinical ePHI.
- **Integrity: MODERATE** — Errors in administrative data cause operational disruptions but do not directly threaten patient safety.
- **Availability: MODERATE** — Administrative functions can operate in degraded mode for limited periods.

**SC: Administrative Data = {(C, MODERATE), (I, MODERATE), (A, MODERATE)}**

### 3.4 System and Audit Log Data

**NIST SP 800-60 Reference:** C.2.7.1 — Information System Security  
**Rationale:**

- **Confidentiality: MODERATE** — Audit logs may reveal system architecture details useful to adversaries but do not directly contain ePHI.
- **Integrity: HIGH** — Tampering with audit logs would undermine accountability, incident response capability, and regulatory compliance (HIPAA requires audit controls under 45 CFR §164.312(b)).
- **Availability: LOW** — Real-time access to audit logs is not required for clinical operations.

**SC: Audit Log Data = {(C, MODERATE), (I, HIGH), (A, LOW)}**

### 3.5 Medical Imaging Data

**NIST SP 800-60 Reference:** C.3.1.1 — Individual Health Information  
**Rationale:**

- **Confidentiality: HIGH** — Medical imaging constitutes ePHI and carries the same confidentiality protections as clinical records.
- **Integrity: HIGH** — Corruption or unauthorized modification of imaging data could lead to misdiagnosis and patient harm.
- **Availability: HIGH** — Imaging data is critical for emergency and surgical procedures; unavailability could result in direct patient harm.

**SC: Medical Imaging Data = {(C, HIGH), (I, HIGH), (A, HIGH)}**

---

## 4. System-Level Security Categorization

### 4.1 Categorization Determination

Applying the high-water mark principle in accordance with FIPS 199, the system-level security categorization is determined by taking the highest impact level across all information types for each security objective:

| Security Objective | Highest Impact Level Identified | Information Type Driving the Rating |
|--------------------|---------------------------------|--------------------------------------|
| Confidentiality | HIGH | ePHI / Patient Clinical Records; Medical Imaging Data |
| Integrity | HIGH | ePHI / Patient Clinical Records; Medical Imaging Data |
| Availability | HIGH | ePHI / Patient Clinical Records; Medical Imaging Data |

### 4.2 Official System Categorization

**SC: MedCore EHRP = {(Confidentiality, HIGH), (Integrity, HIGH), (Availability, HIGH)}**

**Overall System Impact Level: HIGH**

This HIGH impact level designation means that a loss of confidentiality, integrity, or availability of the MedCore EHRP system could be expected to have a **severe or catastrophic adverse effect** on MedCore Health Systems' operations, assets, or individuals — including potential loss of life, major financial harm, or significant harm to individual patients through compromised clinical care.

---

## 5. Implications of HIGH Categorization

The HIGH system categorization has the following direct implications for the MedCore EHRP RMF process:

**Security Control Baseline:** NIST SP 800-53 Rev 5 HIGH Baseline — 265 security controls across 20 control families apply as the minimum baseline for the EHRP system.

**Assessment Rigor:** All controls in the HIGH baseline must be assessed using the HIGH depth and coverage requirements defined in NIST SP 800-53A Rev 5. This requires comprehensive testing, examination, and interviews — not sampling.

**Authorization Duration:** Per MedCore policy, HIGH systems undergo a formal ATO review no less than every three years, with annual ConMon reporting required throughout the authorization period.

**Personnel Requirements:** HIGH system ISSO must hold or be actively pursuing a recognized security certification (CISSP, CISM, CAP) and must receive additional RMF training commensurate with HIGH system responsibilities.

**Encryption Requirements:** All ePHI at rest and in transit must be encrypted using FIPS 140-2 validated cryptographic modules, consistent with the HIGH confidentiality impact level.

**Incident Response Escalation:** Security incidents involving the EHRP system must be escalated to the CISO within 1 hour and to the AO within 4 hours of confirmed incident declaration, regardless of time of day.

---

## 6. Comparison to Previous Categorization

This is the initial formal categorization of the MedCore EHRP under the NIST RMF process. Prior to this assessment, the system operated under an informal HIPAA-based risk assessment framework. The formal FIPS 199 categorization process identified the following important differences from the prior informal assessment:

- The HIGH availability categorization was not previously formalized; the system was informally treated as moderate priority. The RMF assessment process identified patient safety implications that justify the HIGH availability designation.
- Medical imaging data was not previously explicitly included in the system boundary documentation; this assessment formally incorporates it within the EHRP authorization boundary.
- The HIGH integrity designation formalizes requirements for immutable audit logs and integrity monitoring that were previously implemented on an ad-hoc basis.

---

## 7. Categorization Team

The following individuals participated in the categorization analysis and review:

| Name | Title | Role in Categorization |
|------|-------|------------------------|
| Amara Osei | ISSO | Lead analyst; primary author of FIPS 199 worksheet and this memorandum |
| Jonathan E. Steele | CISO | Technical review and approval |
| Dr. Priya Nambiar | CIO / System Owner | System description validation; concurrence on boundary definition |
| Dr. Rachel Feinberg | Privacy Officer | ePHI impact analysis; HIPAA alignment review |
| Dr. Kevin Marsh | Chief Medical Officer | Clinical impact assessment for Integrity and Availability levels |
| Sarah J. Coleman | IT Risk Manager | Risk alignment review; comparison to enterprise risk register |

---

## 8. Decision

Based on the analysis documented in this memorandum and the accompanying FIPS 199 Worksheet (see step-1-categorize/fips-199-worksheet.md), the information system security categorization for the MedCore Electronic Health Records Platform (EHRP) v4.2.1 is formally established as:

**SC: MedCore EHRP = {(Confidentiality, HIGH), (Integrity, HIGH), (Availability, HIGH)}**
**Overall System Impact Level: HIGH**

This categorization will remain in effect unless a significant change to the system, its information types, or its operating environment warrants a re-categorization review. The ISSO will evaluate the need for re-categorization as part of the annual authorization review and following any significant system change.

---

## 9. Signatures and Concurrences

**Prepared By:**

| Name | Amara Osei |
|------|------------|
| Title | Information System Security Officer (ISSO) |
| Signature | [Signed] |
| Date | January 15, 2026 |

**Reviewed and Concurred:**

| Name | Jonathan E. Steele |
|------|-------------------|
| Title | Chief Information Security Officer (CISO) |
| Signature | [Signed] |
| Date | January 16, 2026 |

| Name | Dr. Priya Nambiar |
|------|------------------|
| Title | Chief Information Officer (CIO) / System Owner |
| Signature | [Signed] |
| Date | January 16, 2026 |

| Name | Dr. Rachel Feinberg |
|------|---------------------|
| Title | Privacy Officer |
| Signature | [Signed] |
| Date | January 17, 2026 |

**Approved By:**

| Name | Marcus T. Hargrove |
|------|--------------------|
| Title | Chief Executive Officer / Authorizing Official |
| Signature | [Signed] |
| Date | January 20, 2026 |

---

## 10. Related Documents

| Document | Location |
|----------|----------|
| FIPS 199 Worksheet | step-1-categorize/fips-199-worksheet.md |
| Risk Management Strategy | step-0-prepare/risk-management-strategy.md |
| Roles and Responsibilities | step-0-prepare/roles-and-responsibilities.md |
| Control Allocation Table | step-2-select/control-allocation-table.md |
| System Security Plan | step-3-implement/system-security-plan.md |

---

*MedCore Health Systems — SENSITIVE / FOR OFFICIAL USE ONLY*  
*Document: Categorization-Decision-Memo-EHRP-v1.0 | January 2026*  
*Retain in accordance with MedCore Records Retention Schedule — Security Documentation (7 years)*
