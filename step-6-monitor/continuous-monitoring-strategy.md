# Continuous Monitoring Strategy
## MedCore Electronic Health Records Platform (EHRP) v4.2.1
### Step 6: Monitor Security Controls

---

**Organization:** MedCore Health Systems  
**System Name:** MedCore Electronic Health Records Platform (EHRP)  
**System Version:** v4.2.1  
**Document Version:** 1.0  
**Classification:** SENSITIVE — FOR OFFICIAL USE ONLY  
**Prepared By:** Amara Osei, ISSO  
**Reviewed By:** Jonathan E. Steele, CISO  
**Approved By:** Marcus T. Hargrove, Authorizing Official  
**Document Date:** April 1, 2026  
**Review Cycle:** Annual or upon significant change  
**ATO Expiration:** March 28, 2029  

---

## 1. Purpose and Scope

### 1.1 Purpose

This Continuous Monitoring (ConMon) Strategy establishes the framework, processes, and procedures for maintaining ongoing awareness of the security posture of the MedCore Electronic Health Records Platform (EHRP) following the issuance of an Authorization to Operate (ATO). This strategy ensures that the security controls implemented to protect electronic Protected Health Information (ePHI) and other sensitive data remain effective, properly implemented, and aligned with the evolving threat landscape.

Continuous monitoring enables MedCore Health Systems to make risk-based decisions in near real-time, sustain the authorization over time, and proactively identify and remediate security weaknesses before they can be exploited. This document is developed in accordance with NIST Special Publication 800-137, *Information Security Continuous Monitoring (ISCM) for Federal Information Systems and Organizations*, and supports the requirements of NIST SP 800-37 Rev 2, Step 6.

### 1.2 Scope

This strategy applies to all components, assets, personnel, and processes within the MedCore EHRP authorization boundary, including:

- AWS GovCloud infrastructure (VPC, EC2 instances, RDS, S3, KMS, CloudTrail, CloudWatch)
- On-premises components (Legacy HL7 Interface Engine, Local Gateway, Lab Equipment)
- All software components of the MedCore EHRP application stack
- Third-party service providers and interconnected systems operating under MedCore agreements
- All personnel with access to or responsibility for the EHRP system

### 1.3 Regulatory and Policy Alignment

| Reference | Description |
|-----------|-------------|
| NIST SP 800-137 | Information Security Continuous Monitoring |
| NIST SP 800-37 Rev 2 | RMF for Information Systems (Step 6) |
| NIST SP 800-53 Rev 5 | Security and Privacy Controls (CA-7) |
| NIST SP 800-53A Rev 5 | Assessing Security and Privacy Controls |
| HIPAA Security Rule | 45 CFR §164.308–312 |
| MedCore Information Security Policy v3.1 | Organizational security requirements |
| MedCore Risk Management Policy v2.4 | Risk tolerance and response procedures |

---

## 2. Continuous Monitoring Program Structure

### 2.1 Program Objectives

The MedCore EHRP Continuous Monitoring Program is designed to achieve the following objectives:

1. **Maintain Situational Awareness** — Continuously track the security state of all system components in real or near-real time to detect changes, anomalies, and potential threats.

2. **Sustain Authorization** — Provide the Authorizing Official with timely, accurate security status information to support ongoing authorization decisions throughout the three-year ATO period.

3. **Manage Ongoing Risk** — Identify new risks introduced by changes to the system, environment, or threat landscape and ensure they are assessed and remediated in accordance with MedCore's risk tolerance.

4. **Drive Remediation** — Ensure all identified vulnerabilities and control deficiencies are tracked in the POA&M and remediated within established timeframes.

5. **Support Compliance** — Maintain compliance with HIPAA Security Rule requirements, NIST SP 800-53 Rev 5 HIGH baseline controls, and applicable MedCore policies.

6. **Enable Timely Reporting** — Provide consistent, accurate security status reporting to leadership, the CISO, and the Authorizing Official on a defined schedule.

### 2.2 Program Governance

**Authorizing Official (AO):** Marcus T. Hargrove, CEO  
The AO is responsible for accepting the residual risk associated with operating the EHRP system and making ongoing authorization decisions based on ConMon reports.

**Chief Information Security Officer (CISO):** Jonathan E. Steele  
The CISO oversees the overall ConMon program, reviews monthly status reports, and escalates significant security events to the AO.

**Information System Security Officer (ISSO):** Amara Osei  
The ISSO is the primary owner and operator of the ConMon program. The ISSO coordinates all monitoring activities, manages the POA&M, prepares monthly reports, and serves as the primary liaison between technical teams and leadership.

**Chief Information Officer (CIO):** Dr. Priya Nambiar  
The CIO coordinates IT change management activities that may affect the EHRP system's security posture and ensures ConMon requirements are integrated into operational procedures.

**System Owner:** Dr. Priya Nambiar  
The System Owner approves significant changes to the system and ensures adequate resources are available to support ConMon activities.

**Privacy Officer:** Dr. Rachel Feinberg  
The Privacy Officer monitors privacy-related controls and coordinates on incidents or findings that involve ePHI or patient data exposure.

---

## 3. Monitoring Frequencies and Activities

### 3.1 Monitoring Frequency Table

The following table defines the monitoring activities, associated controls, frequency, responsible party, and reporting destination for the MedCore EHRP ConMon program:

| Activity | Associated Controls | Frequency | Responsible Party | Report To |
|----------|--------------------|-----------|--------------------|-----------|
| Automated vulnerability scanning (authenticated) | RA-5, SI-2 | Weekly | Security Operations | ISSO |
| Privileged account review (active accounts, permissions) | AC-2, AC-6 | Monthly | IAM Administrator | ISSO |
| User access recertification | AC-2, IA-4 | Quarterly | System Owner / ISSO | CISO |
| Security log review and anomaly analysis | AU-2, AU-6, SI-4 | Daily (automated) + Weekly (manual) | SOC Analyst | ISSO |
| SIEM alert triage and incident correlation | IR-4, SI-4 | Continuous (automated) | SOC Analyst | ISSO |
| Patch management status review | SI-2, CM-6 | Monthly | Systems Administrator | ISSO |
| Configuration compliance scan (SCAP/CIS benchmarks) | CM-6, CM-7 | Monthly | Systems Administrator | ISSO |
| Penetration testing / adversarial assessment | CA-8, RA-5 | Annual | Third-Party Assessor | CISO / AO |
| Security controls spot-check assessment | CA-7, CA-2 | Quarterly (rotating subset) | ISSO | CISO |
| POA&M status update and review | CA-5 | Monthly | ISSO | CISO / AO |
| Third-party / interconnection security review | SA-9, CA-3 | Annual | ISSO + Privacy Officer | CISO |
| Business continuity and disaster recovery test | CP-4 | Annual | IT Operations | CIO / CISO |
| Incident response tabletop exercise | IR-3 | Annual | ISSO + IR Team | CISO |
| Privacy impact assessment review | AR-2, IP-1 | Annual or upon significant change | Privacy Officer | CISO |
| ConMon monthly report submission | CA-7 | Monthly (by 15th) | ISSO | CISO / AO |
| Annual security authorization review | CA-6 | Annual | ISSO + CISO | AO |
| Hardware / software inventory update | CM-8 | Monthly | Systems Administrator | ISSO |
| Media protection and encryption validation | MP-5, SC-28 | Quarterly | Systems Administrator | ISSO |
| Audit log integrity verification | AU-9, AU-10 | Monthly | SOC Analyst | ISSO |
| Network traffic analysis (baseline deviation) | SC-5, SC-7 | Weekly | Network Engineer | ISSO |
| AWS Security Hub / GuardDuty findings review | SI-4, RA-5 | Weekly | Cloud Security Engineer | ISSO |
| Backup and recovery verification | CP-9, CP-10 | Monthly | IT Operations | ISSO |

### 3.2 Automated Monitoring Capabilities

MedCore leverages the following automated tools and services as part of the ConMon program:

**Cloud-Native (AWS GovCloud):**
- **AWS CloudTrail** — Logs all API activity across the EHRP environment; alerts on unauthorized API calls and privilege escalation attempts
- **AWS CloudWatch** — Monitors system performance metrics, resource utilization, and custom security metrics; triggers alarms on defined thresholds
- **AWS Security Hub** — Aggregates findings from GuardDuty, Inspector, Config, and Macie into a unified security posture dashboard
- **Amazon GuardDuty** — Provides continuous threat detection using ML-based analysis of CloudTrail, VPC Flow Logs, and DNS logs
- **AWS Config** — Tracks configuration changes to AWS resources and evaluates compliance against defined rules (CIS AWS Foundations Benchmark)
- **Amazon Macie** — Continuously scans S3 buckets for ePHI and sensitive data exposure
- **AWS Inspector** — Performs automated vulnerability assessments on EC2 instances and container images

**On-Premises and Application Layer:**
- **SIEM Platform (Splunk Enterprise)** — Aggregates and correlates logs from all system components; configured with use cases for HIPAA security event detection
- **Qualys Vulnerability Management** — Performs authenticated network scans on a weekly schedule; integrates with POA&M for vulnerability tracking
- **CrowdStrike Falcon** — Endpoint Detection and Response (EDR) providing continuous host-based monitoring across all EHRP servers
- **Tenable.sc** — Configuration compliance scanning against DISA STIG and CIS benchmarks for on-premises components

---

## 4. Security Metrics and Key Performance Indicators

### 4.1 Core Security Metrics

The following metrics are tracked, measured, and reported as part of the monthly ConMon report submitted to the CISO and AO:

**Vulnerability Management Metrics:**

| Metric | Target | Measurement Method |
|--------|--------|-------------------|
| Mean Time to Patch — Critical vulnerabilities | ≤ 15 days from discovery | Qualys / Splunk dashboard |
| Mean Time to Patch — High vulnerabilities | ≤ 30 days from discovery | Qualys / Splunk dashboard |
| Mean Time to Patch — Moderate vulnerabilities | ≤ 90 days from discovery | Qualys / Splunk dashboard |
| Percentage of assets scanned monthly | 100% | Qualys scan coverage report |
| Open critical/high vulnerabilities (unpatched > SLA) | 0 overdue | POA&M tracker |
| Vulnerability reopen rate (regression) | < 5% | Qualys trend analysis |

**Access Control and Identity Metrics:**

| Metric | Target | Measurement Method |
|--------|--------|-------------------|
| Privileged accounts with MFA enabled | 100% | IAM report |
| Orphaned accounts (departed users active > 24 hrs) | 0 | Monthly access review |
| Users with excessive permissions (beyond least privilege) | < 2% | Quarterly access recertification |
| Failed login attempts exceeding threshold (per user/day) | < 0.1% of user base | SIEM alert dashboard |
| Service accounts with rotating credentials | 100% | Secrets Manager audit |

**Incident and Detection Metrics:**

| Metric | Target | Measurement Method |
|--------|--------|-------------------|
| Mean Time to Detect (MTTD) — Security incidents | < 4 hours | SIEM incident log |
| Mean Time to Respond (MTTR) — Security incidents | < 24 hours (Severity 1) | Incident tracking system |
| SIEM alert false positive rate | < 20% | SOC analyst review |
| Security events escalated to formal incidents | Tracked monthly | Incident register |

**Compliance and Configuration Metrics:**

| Metric | Target | Measurement Method |
|--------|--------|-------------------|
| SCAP/CIS benchmark compliance score (servers) | ≥ 85% | Tenable.sc |
| AWS Config rule compliance rate | ≥ 95% | AWS Config dashboard |
| POA&M items overdue beyond scheduled completion | 0 | POA&M tracker |
| Control assessment coverage (quarterly spot-check) | 25% of controls per quarter | ISSO assessment log |

### 4.2 ConMon Health Scorecard

The ISSO prepares a monthly health scorecard using a Red / Amber / Green (RAG) status system:

| Domain | Green | Amber | Red |
|--------|-------|-------|-----|
| Vulnerability Management | All SLAs met, 0 overdue items | 1–2 items approaching deadline | Any overdue HIGH/CRITICAL items |
| Access Control | 100% MFA, 0 orphans | 1–2 access anomalies under review | Active orphaned privileged accounts |
| Incident Response | MTTD < 4 hrs, 0 unresolved P1 | 1–2 alerts in investigation | Active P1 incident or MTTD > 8 hrs |
| Configuration Compliance | ≥ 95% benchmark compliance | 85–94% compliance | < 85% compliance |
| POA&M Health | 0 overdue items, on-track milestones | 1–2 milestones at risk | Any HIGH finding overdue |

---

## 5. Reporting Structure

### 5.1 Monthly ConMon Report

**Due Date:** 15th of each month (submitted to CISO; forwarded to AO by 20th)  
**Prepared By:** ISSO (Amara Osei)  
**Reviewed By:** CISO (Jonathan E. Steele)  
**Submitted To:** AO (Marcus T. Hargrove)

**Monthly Report Contents:**
1. Executive Summary — Overall security posture (RAG status), significant changes, key findings
2. Vulnerability Management Status — Scan results summary, SLA compliance, new vulnerabilities identified
3. Access Management Status — Account review summary, MFA compliance, access anomalies
4. Incident and Event Summary — Security events, incidents opened/closed, MTTD/MTTR statistics
5. Configuration and Patch Status — Benchmark compliance scores, patching status by priority
6. POA&M Status — Summary table of all open items, milestones met/missed, new items added
7. Change Management Activity — System changes implemented during the reporting period and security impact
8. Upcoming Activities — Scheduled assessments, patching windows, training due dates
9. Risk Summary — Changes to overall risk posture, new risks identified, risks closed

### 5.2 Quarterly Security Status Briefing

**Frequency:** Quarterly (January, April, July, October)  
**Audience:** AO, CISO, CIO, Privacy Officer  
**Format:** Presentation with supporting data package  
**Content:** Trend analysis across three months, control assessment results (rotating subset), third-party assessment updates, risk register review, major milestones achieved

### 5.3 Annual Authorization Package Review

**Frequency:** Annual (aligned with ATO anniversary — March 28)  
**Purpose:** Comprehensive review to determine if the ATO remains valid or if re-authorization is required  
**Deliverables:**
- Updated System Security Plan (SSP)
- Updated Security Assessment Report (SAR)
- Updated POA&M
- Annual ConMon summary and trend analysis
- AO decision memorandum (continued ATO, ATO with conditions, or re-authorization required)

---

## 6. Change Management and Impact Analysis

### 6.1 Security Impact Analysis (SIA) Requirement

All proposed changes to the MedCore EHRP system must undergo a Security Impact Analysis before implementation. Changes that may affect the system's security posture include:

- Hardware additions, removals, or replacements within the authorization boundary
- Software installations, upgrades, or configuration changes
- Network topology modifications, firewall rule changes, or new interconnections
- Changes to authentication mechanisms, encryption standards, or key management
- New third-party service provider engagements or data sharing agreements
- Changes to organizational roles or personnel with elevated system privileges

### 6.2 Change Categories and Security Review Process

| Change Category | Security Review Required | AO Notification | ConMon Update |
|-----------------|--------------------------|-----------------|---------------|
| Significant Change (major architecture, new interconnection) | Full SIA + ISSO + CISO review | Required before implementation | Updated SSP + re-categorization review |
| Moderate Change (software upgrade, new role, subnet change) | ISSO SIA review | Notification within 5 business days | POA&M update if new risks identified |
| Minor Change (patches, minor config, documentation) | Standard change review | Monthly report notification | Logged in change register |
| Emergency Change (active incident response) | Post-implementation SIA within 72 hours | Immediate notification | Incident report + follow-up POA&M item |

### 6.3 Triggers for Re-Authorization

The following conditions require the ISSO to notify the CISO and AO immediately and may trigger a formal re-authorization or interim ATO suspension:

1. A security incident resulting in confirmed or suspected ePHI breach
2. Discovery of an Advanced Persistent Threat (APT) or nation-state activity targeting EHRP
3. A critical vulnerability with no available patch that directly exposes the EHRP to exploitation
4. A significant architectural change that substantially alters the system's risk profile
5. Failure to remediate HIGH findings within the authorized timeframe without an approved exception
6. External audit findings (OCR, OIG, external assessor) that identify material control failures
7. A change in the system's operating environment that invalidates the original categorization
8. Loss or extended unavailability of key security controls (e.g., SIEM outage > 72 hours, MFA system failure)

---

## 7. POA&M Integration

### 7.1 POA&M and ConMon Relationship

The Plan of Action and Milestones (POA&M) is the primary tracking vehicle for all identified security deficiencies. The ConMon program feeds directly into the POA&M through:

- Weekly vulnerability scans identifying new findings added to the POA&M
- Quarterly control spot-checks that may identify implementation gaps
- Automated monitoring alerts that escalate to formal POA&M items when unresolved within 72 hours
- Third-party assessment findings incorporated within 5 business days of report receipt

### 7.2 POA&M Status Categories

| Status | Definition | Action Required |
|--------|------------|-----------------|
| OPEN | Finding identified, remediation in progress | Track milestones; escalate if approaching deadline |
| IN REMEDIATION | Active remediation work underway, evidence being collected | ISSO to verify progress on 10th of each month |
| DELAYED — APPROVED | Milestone extension approved by CISO with documented justification | Monitor per revised schedule; no additional escalation needed |
| DELAYED — ESCALATED | Milestone missed without approved extension | CISO notifies AO; escalation plan required within 5 business days |
| CLOSED — REMEDIATED | Remediation complete, verified by ISSO and independent review | Evidence package archived; SAR updated at next annual review |
| CLOSED — ACCEPTED RISK | Risk formally accepted by AO due to mission impact of remediation | AO risk acceptance memorandum required; re-assessed annually |
| CLOSED — FALSE POSITIVE | Finding determined to be a false positive after investigation | Documentation retained; scanner exclusion rule updated if appropriate |

---

## 8. Training and Awareness

### 8.1 ConMon Team Competency Requirements

All personnel with a defined role in the ConMon program must maintain the following minimum competencies:

| Role | Required Training / Certification | Recurrence |
|------|-----------------------------------|------------|
| ISSO | NIST RMF training (800-37/800-53/800-137), HIPAA Security Rule training | Annual |
| SOC Analyst | SIEM platform training, incident response procedures, log analysis | Annual |
| Systems Administrator | OS/platform hardening, SCAP/STIGs, patch management procedures | Annual |
| Cloud Security Engineer | AWS Security Specialty, AWS Config/GuardDuty operations | Annual |
| IAM Administrator | Access review procedures, least-privilege principles, MFA administration | Annual |

### 8.2 Annual Security Awareness Training

All EHRP system users are required to complete annual security awareness training that covers:
- HIPAA Security Rule requirements and ePHI handling procedures
- Phishing and social engineering recognition
- Incident reporting procedures
- Acceptable use policy acknowledgment
- Password and multi-factor authentication requirements

Completion tracking is managed by the ISSO and reported in the monthly ConMon report. Current completion rate target: 100% prior to each ATO anniversary.

---

## 9. Document Control and Maintenance

### 9.1 Review and Update Schedule

This Continuous Monitoring Strategy shall be reviewed and updated:

- **Annually** — No later than 30 days before the ATO anniversary date (February 28 each year)
- **Upon significant change** — Within 30 days of any significant system or organizational change
- **Upon major finding** — Within 15 business days of a Severity 1 incident or critical audit finding
- **Upon AO direction** — At any time upon request from the Authorizing Official

### 9.2 Document Version History

| Version | Date | Author | Description of Changes |
|---------|------|--------|------------------------|
| 1.0 | April 1, 2026 | Amara Osei, ISSO | Initial release — established at ATO issuance |

### 9.3 Approvals

| Role | Name | Signature | Date |
|------|------|-----------|------|
| ISSO | Amara Osei | [Signed] | April 1, 2026 |
| CISO | Jonathan E. Steele | [Signed] | April 1, 2026 |
| Authorizing Official | Marcus T. Hargrove | [Signed] | April 1, 2026 |

---

## 10. References

| Document | Description |
|----------|-------------|
| NIST SP 800-137 | Information Security Continuous Monitoring (ISCM) |
| NIST SP 800-37 Rev 2 | Risk Management Framework — Step 6 |
| NIST SP 800-53 Rev 5 | Security and Privacy Controls — CA-7 |
| NIST SP 800-53A Rev 5 | Assessing Security and Privacy Controls |
| NIST SP 800-128 | Guide for Security-Focused Configuration Management |
| FIPS 199 | Standards for Security Categorization |
| HIPAA Security Rule | 45 CFR §164.308–312 |
| MedCore EHRP SSP v1.0 | System Security Plan (see step-3-implement/) |
| MedCore EHRP SAR v1.0 | Security Assessment Report (see step-4-assess/) |
| MedCore EHRP ATO Memo | Authorization to Operate Memorandum (see step-5-authorize/) |
| MedCore EHRP POA&M | Plan of Action and Milestones (see step-6-monitor/) |

---

*MedCore Health Systems — SENSITIVE / FOR OFFICIAL USE ONLY*  
*Document: ConMon-Strategy-EHRP-v1.0 | Classification: INTERNAL USE ONLY*  
*This document contains security-sensitive operational information and is intended for authorized MedCore personnel only.*
