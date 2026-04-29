# Security Assessment Plan
## MedCore Electronic Health Records Platform (EHRP) v4.2.1
### Step 4: Assess Security Controls

---

**Organization:** MedCore Health Systems
**System Name:** MedCore Electronic Health Records Platform (EHRP)
**System Version:** v4.2.1
**Baseline:** NIST SP 800-53 Rev 5 HIGH Impact Baseline
**Document Version:** 1.0
**Classification:** SENSITIVE FOR OFFICIAL USE ONLY
**Prepared By:** Amara Osei, ISSO
**Reviewed By:** Jonathan E. Steele, CISO
**Approved By:** Marcus T. Hargrove, Authorizing Official
**SAP Issue Date:** February 10, 2026
**Planned Assessment Period:** February 17, 2026 - March 10, 2026

---

## 1. Purpose and Scope

### 1.1 Purpose

This Security Assessment Plan (SAP) describes the approach, methodology, scope, schedule, and responsibilities for conducting the initial security control assessment of the MedCore Electronic Health Records Platform (EHRP) v4.2.1 in support of the Authorization to Operate (ATO) process. The assessment is conducted in accordance with NIST Special Publication 800-53A Rev 5, *Assessing Security and Privacy Controls in Information Systems and Organizations*.

The primary objectives of this assessment are to:
- Determine whether the security controls defined in the MedCore EHRP System Security Plan (SSP) have been correctly implemented
- Assess whether the controls are operating as intended and producing the desired outcomes
- Identify control weaknesses, deficiencies, or gaps that require remediation
- Provide the Authorizing Official with the evidence and findings necessary to make an informed authorization decision
- Produce a Security Assessment Report (SAR) documenting all findings, evidence, and recommendations

### 1.2 Assessment Scope

The security assessment covers all 272 security controls (265 HIGH baseline controls plus 7 added enhancements) documented in the MedCore EHRP SSP. The assessment encompasses all components within the EHRP authorization boundary as defined in the SSP, including:

**Cloud Infrastructure (AWS GovCloud):**
- API Gateway (OIDC/Auth)
- Core Application Services (Patient Management, Clinical Records, Scheduling, Billing and Claims)
- Data Layer (Clinical Database/PostgreSQL, Medical Imaging/S3, Session Cache/Redis)
- Message Broker (Kafka/RabbitMQ)
- Security Services (AWS CloudTrail, CloudWatch, Security Hub, GuardDuty, Config, Macie, KMS)

**On-Premises Components:**
- Legacy HL7 Interface Engine (IBM MQ Series)
- Local Gateway
- Lab Equipment Integration Points

**Supporting Systems and Interconnections:**
- External Health Information Exchange (HIE) connection
- Insurance Payer EDI/X12 connections
- Surescripts e-Rx connection
- Identity Provider (OAuth2/OIDC)

### 1.3 Out of Scope

The following items are explicitly out of scope for this assessment:
- Common controls inherited from the MedCore enterprise Common Control Program (assessed separately)
- Physical security controls (PE family) - assessed under MedCore Facilities Security program
- Third-party service provider internal controls (covered under SA-9 review, not full control assessment)
- Patient-facing mobile application (subject to separate application security assessment)

---

## 2. Assessment Team

### 2.1 Lead Assessor

**Name:** Dr. Sandra Kowalski, CISSP, CISA, CAP
**Organization:** Meridian Security Advisors, LLC (Third-Party Independent Assessor)
**Role:** Lead Security Control Assessor; overall responsible for assessment execution, team supervision, and SAR production
**Independence:** Dr. Kowalski and Meridian Security Advisors have no prior contractual or employment relationship with MedCore Health Systems. All assessment personnel have executed non-disclosure agreements and conflict of interest disclosures.

### 2.2 Assessment Team Members

| Name | Organization | Specialty | Primary Assessment Areas |
|------|-------------|-----------|--------------------------|
| Marcus Webb, OSCP | Meridian Security Advisors | Penetration Testing | CA-8, RA-5, SI-3, SI-4 |
| Jennifer Cho, CISA | Meridian Security Advisors | GRC / Documentation Review | CA-2, CA-5, PL-2, PM controls |
| David Okafor, AWS Security Specialty | Meridian Security Advisors | Cloud Security | All AWS GovCloud controls |
| Priscilla Nguyen, CISSP | Meridian Security Advisors | IAM / Cryptography | AC, IA, SC families |
| Robert Tanner, CHFI | Meridian Security Advisors | Forensics / Audit | AU family, incident response |

### 2.3 MedCore Support Personnel

| Name | Title | Role During Assessment |
|------|-------|----------------------|
| Amara Osei | ISSO | Primary MedCore point of contact; evidence coordinator; artifact provider |
| Jonathan E. Steele | CISO | Technical review of assessment scope; escalation point for access issues |
| Dr. Priya Nambiar | CIO / System Owner | Approver for assessment activities requiring production system access |
| System Administration Team | IT Operations | Technical support for assessment testing; evidence pull requests |
| Network Engineering Team | IT Operations | Network topology documentation; firewall rule exports |

---

## 3. Assessment Methodology

### 3.1 Assessment Methods

The assessment uses the three assessment methods defined in NIST SP 800-53A Rev 5:

**Examine:** Review of documentation, specifications, mechanisms, and activities to understand, clarify, or obtain evidence. Applies to SSPs, policies, procedures, configurations, logs, reports, and prior assessment artifacts.

**Interview:** Discussions with organizational personnel to facilitate understanding of control implementations, clarify documentation, or gather supplemental evidence. Interviews are conducted with system owners, administrators, the ISSO, privacy officer, and end users as appropriate.

**Test:** Exercise of assessment objects under specified conditions to compare actual behavior with expected/required behavior. Includes configuration testing, functional testing, penetration testing, and vulnerability scanning.

### 3.2 Depth and Coverage

Per NIST SP 800-53A Rev 5, the HIGH impact level requires the most rigorous assessment depth and coverage:

**Depth:** Comprehensive — The assessor must understand the mechanisms, implementations, and operational effectiveness of each control fully. Sampling is minimized; key controls must be assessed end-to-end.

**Coverage:** Comprehensive — All implemented instances of each control must be assessed, not just representative samples. For controls that span multiple system components (e.g., AU-2 across all logging sources), all components must be verified.

### 3.3 Rules of Engagement

The following rules govern the assessment activities, particularly penetration testing and active scanning:

1. All active testing must be coordinated with Amara Osei (ISSO) at least 48 hours in advance
2. Production environment testing is permitted only during the approved testing window (Sundays 2:00 AM - 6:00 AM EST) unless a separate test environment is used
3. Penetration testing must not include actual exploitation of production systems without explicit written approval from Dr. Priya Nambiar (System Owner) and Marcus T. Hargrove (AO)
4. All testing activity must be logged by the assessment team with timestamps, tools used, and target IP ranges
5. Denial of service testing against production systems is prohibited
6. Any discovery of a critical, actively exploitable vulnerability must be reported to the ISSO within 1 hour of discovery
7. Assessment team members must not retain copies of ePHI encountered during the assessment beyond what is necessary for evidence documentation
8. All assessment artifacts containing system-specific details are classified as SENSITIVE and must be protected accordingly

---

## 4. Assessment Schedule

### 4.1 Pre-Assessment Activities (February 10 - February 16, 2026)

| Activity | Responsible | Completion Date |
|----------|-------------|-----------------|
| SAP review and approval by System Owner and AO | Dr. Priya Nambiar, M. Hargrove | February 12, 2026 |
| Evidence request package distributed to ISSO | Lead Assessor | February 10, 2026 |
| System Security Plan provided to assessment team | Amara Osei, ISSO | February 13, 2026 |
| Prior assessment artifacts and POA&M provided | Amara Osei, ISSO | February 13, 2026 |
| Assessment team NDAs and COIs executed | All assessors | February 10, 2026 |
| Test environment access credentials provisioned | System Admin Team | February 16, 2026 |
| Assessment kick-off meeting | All parties | February 17, 2026 |

### 4.2 Assessment Execution (February 17 - March 6, 2026)

| Week | Focus Areas | Assessment Methods |
|------|-------------|-------------------|
| Week 1 (Feb 17-21) | AC, AT, AU, CA control families; Documentation review and kickoff interviews | Examine, Interview |
| Week 2 (Feb 24-28) | CM, CP, IA, IR, MA control families; Configuration testing; System admin interviews | Examine, Interview, Test |
| Week 3 (Mar 2-6) | PE (inherited review), PL, PM, RA, SA control families; Vulnerability scanning; Penetration test preparation | Examine, Test |
| Week 4 (Mar 2-6 overlap) | SC, SI, SR control families; Penetration testing (Sunday Mar 1, 2:00-6:00 AM); Cloud security testing | Examine, Test |

### 4.3 Post-Assessment Activities (March 7 - March 21, 2026)

| Activity | Responsible | Completion Date |
|----------|-------------|-----------------|
| Assessment team internal debrief and finding consolidation | Assessment team | March 7-9, 2026 |
| Preliminary findings briefing to ISSO and CISO | Lead Assessor | March 10, 2026 |
| MedCore factual accuracy review of draft SAR | Amara Osei, ISSO | March 11-14, 2026 |
| Final SAR delivered to ISSO | Lead Assessor | March 17, 2026 |
| ISSO prepares Authorization Package for AO | Amara Osei, ISSO | March 18-21, 2026 |
| Authorization Package submitted to AO | ISSO | March 21, 2026 |

---

## 5. Evidence Requirements

### 5.1 Documentation Evidence Requested

The following documentation artifacts were requested from MedCore Health Systems prior to assessment commencement:

| Document | Requested From | Status |
|----------|---------------|--------|
| System Security Plan (SSP) v1.0 | ISSO | Provided February 13, 2026 |
| FIPS 199 Worksheet and Categorization Memo | ISSO | Provided February 13, 2026 |
| Control Allocation Table and Tailoring Decisions | ISSO | Provided February 13, 2026 |
| Network topology diagrams (current) | Network Engineering | Provided February 14, 2026 |
| System architecture diagrams | CIO Office | Provided February 13, 2026 |
| Authorization boundary documentation | ISSO | Provided February 13, 2026 |
| Incident response plan and procedures | ISSO | Provided February 14, 2026 |
| Business continuity / disaster recovery plan | IT Operations | Provided February 15, 2026 |
| Vulnerability scan reports (last 90 days) | Security Operations | Provided February 14, 2026 |
| User access list (privileged and standard accounts) | IAM Administrator | Provided February 15, 2026 |
| Patch management records (last 90 days) | Systems Administrator | Provided February 15, 2026 |
| Security awareness training completion records | Human Resources | Provided February 15, 2026 |
| Privacy impact assessment | Privacy Officer | Provided February 15, 2026 |
| Third-party service provider agreements (ISAs, MOUs) | Procurement / Legal | Provided February 16, 2026 |
| POA&M (if existing items) | ISSO | Not applicable - initial assessment |
| Change management logs (last 12 months) | IT Operations | Provided February 15, 2026 |
| AWS Config compliance reports | Cloud Security Engineer | Provided February 14, 2026 |
| Firewall rule sets | Network Engineering | Provided February 14, 2026 |

### 5.2 Technical Access Required

| Access Type | Purpose | Approved By |
|------------|---------|------------|
| Read-only AWS GovCloud console access | Review CloudTrail, Config, Security Hub, GuardDuty findings | Dr. Priya Nambiar, February 16, 2026 |
| Splunk SIEM read-only access | Review audit log configurations and sample records | Dr. Priya Nambiar, February 16, 2026 |
| Network scan authorization (test environment) | Authenticated vulnerability scanning | Dr. Priya Nambiar, February 16, 2026 |
| Tenable.sc and Qualys report access | Review vulnerability scan results | Amara Osei, February 16, 2026 |
| Active Directory read-only access | Review account configurations, group policies | System Admin Team, February 16, 2026 |

---

## 6. Reporting

### 6.1 Preliminary Findings Briefing

A preliminary findings briefing will be conducted with the ISSO and CISO on March 10, 2026 to present initial findings, provide MedCore an opportunity to clarify any potential misunderstandings, and begin planning remediation priorities. The preliminary briefing is not the final finding set.

### 6.2 Draft SAR Review

MedCore will have a 3-business-day factual accuracy review period (March 11-14, 2026) to review the draft SAR for factual inaccuracies, organizational name errors, and description errors. MedCore may not dispute findings based on subjective disagreement; only factual corrections are accepted. If MedCore disagrees with an assessor finding, a written rebuttal may be appended to the SAR.

### 6.3 Final SAR Delivery

The final SAR will be delivered by March 17, 2026 and will include:
- Executive summary with overall risk posture assessment
- Complete findings table with risk ratings (HIGH, MODERATE, LOW, INFORMATIONAL)
- Detailed findings for all HIGH and MODERATE risk items
- Evidence references for all findings
- Recommended remediation actions for each finding
- Strengths identified during the assessment
- Retest recommendations

### 6.4 Finding Risk Ratings

Findings will be rated using the following criteria aligned with NIST SP 800-30 Rev 1:

| Rating | Likelihood x Impact Criteria | Remediation Expectation |
|--------|------------------------------|------------------------|
| HIGH | High likelihood of exploitation; severe adverse impact on C, I, or A | Required prior to ATO or immediate POA&M item with 30-day SLA |
| MODERATE | Moderate likelihood or moderate impact | POA&M item with 90-day SLA |
| LOW | Low likelihood or low impact | POA&M item with 180-day SLA |
| INFORMATIONAL | Observation; no direct risk; best practice recommendation | Tracked at MedCore discretion |

---

## 7. Approvals

| Role | Name | Signature | Date |
|------|------|-----------|------|
| ISSO | Amara Osei | [Signed] | February 10, 2026 |
| CISO | Jonathan E. Steele | [Signed] | February 11, 2026 |
| System Owner | Dr. Priya Nambiar | [Signed] | February 12, 2026 |
| Authorizing Official | Marcus T. Hargrove | [Signed] | February 12, 2026 |
| Lead Assessor | Dr. Sandra Kowalski | [Signed] | February 10, 2026 |

---

## 8. Related Documents

| Document | Location |
|----------|----------|
| System Security Plan (SSP) | step-3-implement/system-security-plan.md |
| Security Assessment Report (SAR) | step-4-assess/security-assessment-report.md |
| FIPS 199 Worksheet | step-1-categorize/fips-199-worksheet.md |
| Control Allocation Table | step-2-select/control-allocation-table.md |
| Tailoring Decisions | step-2-select/tailoring-decisions.md |
| ATO Memorandum | step-5-authorize/authorization-to-operate-memo.md |

---

*MedCore Health Systems - SENSITIVE / FOR OFFICIAL USE ONLY*
*Document: SAP-EHRP-v1.0 | February 2026*
