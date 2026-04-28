# Step 1 — Categorize: FIPS 199 Security Categorization Worksheet
## MedCore Electronic Health Records Platform (EHRP)

**Standard:** Federal Information Processing Standards Publication 199 (FIPS 199)
**Supporting Guidance:** NIST SP 800-60 Vol I & II, NIST SP 800-37 Rev 2
**System:** MedCore EHRP | MedCore Health Systems (Fictional)
**Document Version:** 1.0 | **Date:** April 2026
**Prepared By:** ISSO — Amara Osei | **Reviewed By:** System Owner — Jonathan E. Steele

---

## FIPS 199 Overview

FIPS 199 (Standards for Security Categorization of Federal Information and Information Systems) requires the categorization of information and information systems based on the potential impact to organizational operations, organizational assets, or individuals should there be a breach of security. The three security objectives are:

- **Confidentiality** — Preserving authorized restrictions on information access and disclosure
- **Integrity** — Guarding against improper modification or destruction of information
- **Availability** — Ensuring timely and reliable access to and use of information

Impact levels are: **LOW**, **MODERATE**, or **HIGH**

---

## System Information

| Field | Value |
|-------|-------|
| System Name | MedCore Electronic Health Records Platform (EHRP) |
| System Abbreviation | EHRP |
| System Owner | Jonathan E. Steele, CISO |
| ISSO | Amara Osei, Director of Cybersecurity and Compliance |
| System Type | Major Application |
| Operating Status | Operational |
| Authorization Boundary | Defined in medcore-health-systems repository |

---

## Information Types Processed

The MedCore EHRP processes the following information types (per NIST SP 800-60):

| # | Information Type | SP 800-60 Identifier | Description |
|---|-----------------|---------------------|-------------|
| 1 | Health Care Delivery Services | C.3.1.1 | Patient clinical records, diagnoses, treatment plans |
| 2 | Patient Identity Information | C.3.1.2 | PHI including name, DOB, SSN, address, MRN |
| 3 | Health Care Payment | C.3.1.3 | Insurance claims, billing, payment card data |
| 4 | Health Care Research | C.3.1.4 | De-identified clinical research data |
| 5 | System Administration | D.17.1 | IT administrative configurations and logs |
| 6 | Audit and Accountability Information | D.17.2 | System audit logs and access records |
| 7 | Financial Management | D.4.1 | Accounts payable, receivable, financial reporting |

---

## Security Impact Analysis by Information Type

### 1. Health Care Delivery Services (C.3.1.1)

| Objective | Impact Level | Justification |
|-----------|-------------|---------------|
| Confidentiality | HIGH | Unauthorized disclosure of clinical records causes significant patient harm, violates HIPAA, and results in regulatory penalties up to $1.9M per violation category |
| Integrity | HIGH | Unauthorized modification of clinical records (diagnoses, medications, lab results) could directly endanger patient safety and result in patient harm or death |
| Availability | HIGH | Unavailability of the EHRP disrupts clinical operations across 3 hospital campuses and 12 outpatient clinics, directly impacting patient care delivery |

**Information Type Categorization: SC Health Care Delivery = {(C, HIGH), (I, HIGH), (A, HIGH)}**

---

### 2. Patient Identity Information — PHI/PII (C.3.1.2)

| Objective | Impact Level | Justification |
|-----------|-------------|---------------|
| Confidentiality | HIGH | PHI/PII disclosure violates HIPAA Privacy Rule and causes significant harm to individuals (identity theft, discrimination, financial harm). HIPAA penalties can reach $1.9M per violation category per year |
| Integrity | HIGH | Inaccurate patient identity data (incorrect name, DOB, allergies) could result in wrong-patient medical errors with life-threatening consequences |
| Availability | MODERATE | While important, patient identity data can be reconstructed from paper records in a temporary outage without immediate patient safety risk |

**Information Type Categorization: SC Patient Identity = {(C, HIGH), (I, HIGH), (A, MODERATE)}**

---

### 3. Health Care Payment (C.3.1.3)

| Objective | Impact Level | Justification |
|-----------|-------------|---------------|
| Confidentiality | HIGH | Payment card and insurance data is subject to PCI-DSS. Breach could expose thousands of patient payment records, resulting in significant financial penalties and reputational damage |
| Integrity | MODERATE | Payment data manipulation could result in billing fraud or incorrect charges, but recovery procedures exist |
| Availability | MODERATE | Temporary payment system unavailability is operationally disruptive but does not endanger patient safety |

**Information Type Categorization: SC Health Care Payment = {(C, HIGH), (I, MODERATE), (A, MODERATE)}**

---

### 4. System Administration (D.17.1)

| Objective | Impact Level | Justification |
|-----------|-------------|---------------|
| Confidentiality | MODERATE | Disclosure of system configuration details could provide attackers with information to exploit vulnerabilities |
| Integrity | HIGH | Unauthorized modification of system configurations could compromise all security controls and enable unauthorized access to PHI |
| Availability | MODERATE | Temporary loss of administrative access is disruptive but can be restored from backup configurations |

**Information Type Categorization: SC System Administration = {(C, MODERATE), (I, HIGH), (A, MODERATE)}**

---

### 5. Audit and Accountability Information (D.17.2)

| Objective | Impact Level | Justification |
|-----------|-------------|---------------|
| Confidentiality | MODERATE | Audit logs contain security-sensitive information about system activities that should not be publicly disclosed |
| Integrity | HIGH | Tampered audit logs destroy the evidentiary chain needed for incident response, forensic investigation, and regulatory compliance |
| Availability | MODERATE | Temporary loss of audit logging is a compliance gap but does not immediately endanger operations |

**Information Type Categorization: SC Audit Info = {(C, MODERATE), (I, HIGH), (A, MODERATE)}**

---

## System-Level Security Categorization

Per FIPS 199, the system-level security categorization is determined by taking the **high water mark** (maximum) across all information types for each security objective.

| Security Objective | Information Type with Highest Impact | System Impact Level |
|-------------------|-------------------------------------|--------------------|
| **Confidentiality** | Health Care Delivery, PHI/PII, Payment | **HIGH** |
| **Integrity** | Health Care Delivery, PHI/PII, System Admin | **HIGH** |
| **Availability** | Health Care Delivery | **HIGH** |

---

## Final System Categorization

> **SC MedCore EHRP = {(Confidentiality, HIGH), (Integrity, HIGH), (Availability, HIGH)}**
>
> **Overall System Security Categorization: HIGH**

---

## Rationale for HIGH Categorization

The MedCore EHRP receives a HIGH overall categorization based on the following:

1. **Patient Safety Impact:** Compromise of the integrity of clinical records (diagnoses, medication orders, lab results) could directly endanger patient health and safety — a clearly HIGH-impact scenario per FIPS 199
2. **Regulatory Obligations:** HIPAA Security Rule, PCI-DSS, and applicable state law impose substantial penalties for unauthorized disclosure of PHI/PII. The potential harm to affected individuals is significant and widespread
3. **Mission Criticality:** The EHRP is the primary clinical system supporting 3 hospital campuses and 12 outpatient clinics. Extended unavailability would disrupt patient care delivery across the organization
4. **Volume of Sensitive Data:** Approximately 280,000 patient records containing PHI, PII, and financial data are processed by this system

---

## Impact on Control Baseline Selection

A HIGH overall categorization requires use of the **NIST SP 800-53 Rev 5 High baseline** as the minimum set of security controls. The control selection rationale and tailoring decisions are documented in:

- [Step 2 — Control Baseline Selection](../step-2-select/baseline-selection-rationale.md)
- [Step 2 — Tailoring Decisions](../step-2-select/tailoring-decisions.md)

---

## Categorization Approval

| Role | Name | Signature | Date |
|------|------|-----------|------|
| Prepared By (ISSO) | Amara Osei | [Signed] | April 1, 2026 |
| Reviewed By (System Owner) | Jonathan E. Steele | [Signed] | April 3, 2026 |
| Approved By (AO) | Marcus T. Hargrove | [Signed] | April 5, 2026 |

---

*MedCore Health Systems is fictional. Created for cybersecurity portfolio demonstration purposes only.*
