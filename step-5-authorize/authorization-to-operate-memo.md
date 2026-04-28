# Step 5 — Authorize: Authorization to Operate (ATO) Memorandum
## MedCore Electronic Health Records Platform (EHRP)

---

**MEMORANDUM**

**TO:** Jonathan E. Steele, CISO (System Owner)
**FROM:** Marcus T. Hargrove, CEO (Authorizing Official)
**CC:** Dr. Priya Nambiar, CIO (AODR); Amara Osei, ISSO; Dr. Rachel Feinberg, Privacy Officer
**DATE:** April 15, 2026
**SUBJECT:** Authorization to Operate — MedCore Electronic Health Records Platform (EHRP) v4.2.1
**REFERENCE:** NIST SP 800-37 Rev 2, Step 5 — Authorization Decision

---

## Authorization Decision

Pursuant to my authority as the Authorizing Official (AO) for MedCore Health Systems, and in accordance with the NIST Risk Management Framework (NIST SP 800-37 Rev 2), I hereby issue this **Authorization to Operate (ATO)** for the MedCore Electronic Health Records Platform (EHRP).

**System Name:** MedCore Electronic Health Records Platform (EHRP)
**System Version:** 4.2.1
**Authorization Type:** Full Authorization to Operate (ATO)
**Authorization Effective Date:** April 15, 2026
**Authorization Expiration Date:** April 14, 2029 (3-year authorization term)
**Security Categorization:** HIGH (Confidentiality, Integrity, Availability)
**Control Baseline:** NIST SP 800-53 Rev 5 — HIGH Baseline (265 controls)

---

## Authorization Package Reviewed

I have reviewed the following documents comprising the authorization package for the MedCore EHRP:

| Document | Version | Date | Status |
|---------|---------|------|--------|
| System Security Plan (SSP) | 1.2 | April 10, 2026 | Accepted |
| Security Assessment Report (SAR) | 1.0 | April 5, 2026 | Reviewed |
| Plan of Action & Milestones (POA&M) | 1.0 | April 12, 2026 | Accepted |
| FIPS 199 Security Categorization | 1.0 | April 5, 2026 | Accepted |
| Privacy Impact Assessment (PIA) | 2.1 | March 30, 2026 | Accepted |
| Rules of Behavior (RoB) | 3.0 | January 15, 2026 | Current |
| Contingency Plan (ISCP) | 2.3 | February 28, 2026 | Current |

---

## Risk Determination

Based on my review of the authorization package, including the Security Assessment Report prepared by CyberProof Solutions (independent SCA), I have determined that the residual risk to organizational operations, organizational assets, and individuals from operating the MedCore EHRP is **ACCEPTABLE**, subject to the conditions specified in this authorization.

**Assessment Summary:**
- Controls Satisfied: 238 of 265 (89.8%)
- HIGH Findings: 4 (all with POA&M entries and committed remediation)
- MODERATE Findings: 11 (all with POA&M entries)
- LOW / Informational Findings: 12 (tracked in POA&M)

**Risk Acceptance Rationale:**
The EHRP implements strong controls in the areas of cryptographic protection (AES-256, TLS 1.3), multi-factor authentication (Azure AD MFA for all users), access management (RBAC, least privilege), and security monitoring (Splunk SIEM, CrowdStrike EDR). The 4 HIGH findings, while significant, have committed remediation timelines of 30 days or less. I accept the residual risk of operating the system during the remediation period, contingent on the conditions below.

---

## Conditions of Authorization

This ATO is issued with the following mandatory conditions. Failure to meet these conditions may result in suspension or revocation of this authorization:

**Condition 1 — HIGH Finding Remediation (Mandatory, 30 Days)**
All 4 HIGH findings identified in SAR-2026 must be fully remediated or have documented accepted risk with my explicit written approval by May 15, 2026. The ISSO will provide written confirmation of remediation to the AODR.

**Condition 2 — POA&M Maintenance (Ongoing)**
The ISSO will maintain the POA&M with current status of all open findings and provide monthly updates to the AODR. Findings past their scheduled completion date require escalation to the System Owner within 5 business days.

**Condition 3 — Continuous Monitoring (Ongoing)**
The ISSO will conduct continuous monitoring activities per the EHRP Continuous Monitoring Strategy and provide monthly ConMon reports to the AODR. Any Critical or HIGH risk finding discovered post-authorization must be reported to me within 72 hours.

**Condition 4 — Significant Change Notification (Ongoing)**
Any significant change to the EHRP (major software upgrade, architecture change, new system interconnection, new data type processed) must be reported to the ISSO for security impact analysis. Changes determined to be significant may require re-authorization.

**Condition 5 — Annual Review (Ongoing)**
The ISSO will conduct an annual review of the SSP, POA&M, and risk posture. An annual security control assessment will be conducted by an independent assessor. Results will be presented to the AODR and me within 60 days of assessment completion.

---

## Scope of Authorization

This ATO authorizes operation of the MedCore EHRP within the authorization boundary documented in the SSP and system description, specifically:

**Authorized Components:**
- EHRP Application Servers (AWS GovCloud us-gov-east-1)
- Amazon RDS PostgreSQL (PHI database)
- AWS S3 (EHRP data storage and audit logs)
- AWS KMS and Secrets Manager
- AWS WAF and Load Balancer
- Splunk SIEM (EHRP log processing)
- Active Directory / Azure AD (EHRP authentication)
- CrowdStrike Falcon (EHRP endpoint protection)
- Palo Alto Firewalls (EHRP network boundary)
- Cisco AnyConnect VPN (EHRP remote access)

**This authorization does NOT cover:**
- Surescripts e-Prescribing platform (requires separate authorization)
- State HIE connection (governed by Georgia DHR authorization)
- Physical data center infrastructure (covered by facilities security authorization)

---

## Revocation Conditions

This ATO may be suspended or revoked immediately if:
1. A HIGH or CRITICAL security incident occurs affecting PHI confidentiality, integrity, or availability
2. A HIPAA breach requiring HHS notification is confirmed
3. HIGH findings are not remediated by May 15, 2026
4. A significant unauthorized change is discovered
5. The system's operating environment changes materially from what is described in the SSP

---

## Authorization Signatures

**Authorizing Official:**

Name: Marcus T. Hargrove
Title: Chief Executive Officer, MedCore Health Systems
Date: April 15, 2026
Signature: [Digitally Signed — DocuSign ID: MC-ATO-2026-001]

---

**AODR Acknowledgment:**

Name: Dr. Priya Nambiar
Title: Chief Information Officer, MedCore Health Systems
Date: April 15, 2026
Signature: [Digitally Signed — DocuSign ID: MC-ATO-2026-002]

---

**System Owner Receipt:**

Name: Jonathan E. Steele
Title: CISO, MedCore Health Systems
Date: April 15, 2026
Signature: [Digitally Signed — DocuSign ID: MC-ATO-2026-003]

---

**ISSO Receipt:**

Name: Amara Osei
Title: Director of Cybersecurity and Compliance, MedCore Health Systems
Date: April 15, 2026
Signature: [Digitally Signed — DocuSign ID: MC-ATO-2026-004]

---

*This Authorization to Operate is issued for the MedCore EHRP as described in the authorization package dated April 2026. This document is SENSITIVE and should be distributed only to authorized personnel with a need to know.*

*MedCore Health Systems is fictional. Created for cybersecurity portfolio demonstration purposes only.*
