# Step 0 — Prepare: Risk Management Strategy
## MedCore Health Systems | NIST SP 800-37 Rev 2

**Document Type:** Organizational Risk Management Strategy | **Version:** 1.0 | **Date:** April 2026

---

## Purpose

This document establishes MedCore Health Systems' organizational risk management strategy as required by NIST SP 800-37 Rev 2, Step 0. The risk management strategy provides the foundation for all risk-related decisions across the organization, including those made during the RMF lifecycle for individual information systems.

---

## Organizational Risk Tolerance

MedCore Health Systems operates as a regional healthcare provider processing Protected Health Information (PHI) for approximately 280,000 patients. Given the sensitivity of clinical data, the criticality of system availability to patient care, and the regulatory obligations under HIPAA, PCI-DSS, and state privacy laws, MedCore's organizational risk tolerance is defined as **Low**.

| Risk Category | Tolerance Level | Rationale |
|--------------|----------------|----------|
| Patient Data Confidentiality (PHI/PII) | Very Low | HIPAA penalties, patient harm, and reputational damage |
| Clinical System Availability | Very Low | System downtime directly impacts patient care and safety |
| Data Integrity (Clinical Records) | Very Low | Corrupted records could cause adverse patient outcomes |
| Financial Data (Payment Card) | Low | PCI-DSS obligations and financial liability |
| Regulatory Compliance | Very Low | HIPAA, PCI-DSS, GDPR, CCPA penalties |
| Reputational Risk | Low | Patient trust is fundamental to the healthcare mission |

---

## Risk Management Approach

MedCore Health Systems uses the NIST Risk Management Framework (SP 800-37 Rev 2) as its primary approach for managing security and privacy risk across all information systems. This framework is supplemented by:

- **NIST SP 800-30 Rev 1** — Risk assessment methodology for identifying and evaluating threats, vulnerabilities, and likelihood of adverse events
- **NIST SP 800-39** — Organization-wide risk management (Tier 1, Tier 2, Tier 3 integration)
- **NIST SP 800-53 Rev 5** — Security and privacy controls catalog
- **HIPAA Security Rule** — Administrative, physical, and technical safeguard requirements
- **ISO/IEC 27001:2005** — ISMS framework (reference alignment)

---

## Three-Tier Risk Management Model

### Tier 1 — Organization Level
The MedCore Board of Directors and executive leadership establish organizational risk tolerance and allocate resources for cybersecurity programs. The CISO reports risk posture quarterly to the Board.

### Tier 2 — Mission/Business Process Level
The CISO and CIO assess risk at the mission level — evaluating how security risks impact clinical operations, revenue cycle, and regulatory compliance. The Risk Management Committee (RMC) meets monthly.

### Tier 3 — Information System Level
The ISSO conducts system-level risk assessments for each information system using the NIST RMF. System-level risks are escalated to Tier 2 when they exceed the acceptable risk threshold.

---

## Risk Assessment Frequency

| Assessment Type | Frequency | Responsible Party |
|----------------|-----------|------------------|
| System-level risk assessment (NIST SP 800-30) | Annual | ISSO + SCA |
| Vulnerability scanning (authenticated) | Weekly | ISSO / Tenable Nessus |
| Penetration testing | Annual | Third-party assessor |
| Security control assessment | Annual | Independent SCA (CyberProof Solutions) |
| Privacy impact assessment (PIA) | When system changes occur | Privacy Officer |
| Business impact analysis (BIA) | Biennial | ISSO + Business Continuity team |

---

## Risk Response Options

MedCore Health Systems recognizes four risk response options per NIST SP 800-39:

| Response | Definition | When Used |
|---------|-----------|----------|
| **Accept** | Acknowledge the risk and take no additional action | Low-impact findings within tolerance |
| **Avoid** | Eliminate the risk by removing the activity | When risk exceeds tolerance and avoidance is feasible |
| **Mitigate** | Reduce likelihood or impact through controls | Primary response for most identified risks |
| **Transfer** | Share or shift risk to another party (insurance, vendor SLA) | For residual risk that cannot be fully mitigated |

**Default Response:** For HIGH-impact systems like the MedCore EHRP, the default risk response is **Mitigate**. Risk acceptance is only permitted by the Authorizing Official after documented review.

---

## Risk Prioritization Framework

Risk prioritization uses a standard 5x5 likelihood-impact matrix:

| Impact / Likelihood | Very Low | Low | Moderate | High | Very High |
|--------------------|---------|-----|---------|------|----------|
| **Critical** | Moderate | High | High | Critical | Critical |
| **High** | Low | Moderate | High | High | Critical |
| **Moderate** | Low | Low | Moderate | High | High |
| **Low** | Very Low | Low | Low | Moderate | Moderate |
| **Very Low** | Very Low | Very Low | Low | Low | Moderate |

**Risk Ratings:**
- **Critical:** Immediate remediation required — escalate to AO within 24 hours
- **High:** Remediation required within 30 days — POA&M required
- **Moderate:** Remediation required within 90 days — POA&M required
- **Low:** Remediation within 180 days — monitor and document
- **Very Low / Informational:** Accept or schedule for next review cycle

---

## Residual Risk Acceptance

After security controls are implemented, residual risk may remain. Residual risk acceptance is governed by the following:

1. The ISSO documents all residual risks in the POA&M with planned remediation
2. The System Owner reviews and endorses residual risks before submission to the AO
3. The AO formally accepts residual risk as part of the ATO decision
4. Residual risks rated **Critical** or **High** require the AO's explicit written acceptance
5. Any new High or Critical residual risk discovered post-authorization must be reported to the AO within 72 hours

---

## Continuous Risk Monitoring

MedCore Health Systems maintains a continuous risk monitoring program per NIST SP 800-137:

- **Daily:** Automated SIEM (Splunk) alerts for anomalous activity
- **Weekly:** Vulnerability scan results review by ISSO
- **Monthly:** POA&M status update and ConMon report to AODR
- **Quarterly:** Risk posture briefing to CISO and executive leadership
- **Annually:** Full security control assessment and risk assessment update

---

*Document Owner: CISO — Jonathan E. Steele | Approved By: AO — Marcus T. Hargrove | Next Review: April 2027*
*MedCore Health Systems is fictional. Created for cybersecurity portfolio demonstration purposes only.*
