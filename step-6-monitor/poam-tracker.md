# Step 6 — Monitor: Plan of Action and Milestones (POA&M)
## MedCore Electronic Health Records Platform (EHRP)

**Document Type:** Plan of Action and Milestones (POA&M)
**System:** MedCore EHRP | MedCore Health Systems (Fictional)
**Current Version:** 1.1 | **Date:** April 15, 2026
**POA&M Owner:** ISSO — Amara Osei
**Update Frequency:** Monthly (due 15th of each month)
**Submitted To:** AODR — Dr. Priya Nambiar

---

## POA&M Summary Dashboard

| Risk Level | Open | In Progress | Completed | Overdue |
|-----------|:----:|:-----------:|:---------:|:-------:|
| HIGH | 4 | 0 | 0 | 0 |
| MODERATE | 11 | 0 | 0 | 0 |
| LOW | 8 | 0 | 0 | 0 |
| INFORMATIONAL | 4 | 0 | 0 | 0 |
| **TOTAL** | **27** | **0** | **0** | **0** |

**Overall POA&M Health:** At Risk — 4 HIGH findings require immediate attention
**Last Updated:** April 15, 2026 | **Next Review:** May 15, 2026

---

## HIGH Risk Findings

---

**POA&M Item ID:** POA-2026-H01
**Finding Reference:** SAR-2026-H01
**Control:** IA-5(1) — Authenticator Management (Password-Based)
**Weakness:** Password policy for standard users does not meet NIST SP 800-63B requirements. Minimum length is 10 characters (SSP requires 14). Common and dictionary passwords are not blocked.
**Risk Level:** HIGH
**Likelihood:** Moderate | **Impact:** HIGH
**Resources Required:** Azure AD P2 license (already owned); 4 hours ISSO time for policy update and testing
**Scheduled Completion:** May 15, 2026
**Responsible Party:** ISSO — Amara Osei
**Milestone 1:** Update Azure AD Password Protection policy to block common passwords — April 20, 2026
**Milestone 2:** Enforce 14-character minimum via Conditional Access — April 25, 2026
**Milestone 3:** Force password reset for all accounts not meeting new requirements — May 10, 2026
**Milestone 4:** Verify compliance via Azure AD audit log review — May 15, 2026
**Status:** OPEN — Not yet started
**AO Risk Acceptance:** Not applicable — remediation in progress

---

**POA&M Item ID:** POA-2026-H02
**Finding Reference:** SAR-2026-H02
**Control:** SI-2 — Flaw Remediation
**Weakness:** 3 critical and 7 high vulnerabilities on EHRP application servers exceed required patch remediation timeframes. Oldest critical vulnerability is 47 days old (15-day SLA).
**Risk Level:** HIGH
**Likelihood:** High | **Impact:** HIGH
**Resources Required:** 16 hours IT Infrastructure team time; 2-hour maintenance window per server (3 servers)
**Scheduled Completion:** April 25, 2026
**Responsible Party:** Director of IT Infrastructure — Luis Castillo
**Milestone 1:** Apply critical patches to all 3 affected servers — April 20, 2026
**Milestone 2:** Apply high patches to all affected servers — April 23, 2026
**Milestone 3:** Verify patch compliance via Tenable Nessus rescan — April 25, 2026
**Milestone 4:** Review patch management process; update SLA monitoring procedures — April 30, 2026
**Status:** OPEN — Patches scheduled for maintenance window April 19-20, 2026
**AO Risk Acceptance:** Not applicable — remediation in progress

---

**POA&M Item ID:** POA-2026-H03
**Finding Reference:** SAR-2026-H03
**Control:** AU-9 — Protection of Audit Information
**Weakness:** 3 EHRP application servers not forwarding audit logs to Splunk SIEM for approximately 22 days. Security events on affected servers have not been centrally logged.
**Risk Level:** HIGH
**Likelihood:** High | **Impact:** HIGH
**Resources Required:** 8 hours ISSO/IT Infrastructure time; Splunk Forwarder configuration
**Scheduled Completion:** April 18, 2026
**Responsible Party:** ISSO — Amara Osei (primary); IT Infrastructure (support)
**Milestone 1:** Identify root cause of Splunk Forwarder failure — April 16, 2026
**Milestone 2:** Remediate Splunk Universal Forwarder on 3 affected servers — April 17, 2026
**Milestone 3:** Verify log forwarding is active and events appearing in Splunk — April 17, 2026
**Milestone 4:** Conduct manual review of local logs for 22-day gap period; document review results — April 18, 2026
**Milestone 5:** Implement automated monitoring alert for log pipeline health — April 25, 2026
**Status:** OPEN — Targeted for completion April 18, 2026 (IMMEDIATE)
**AO Risk Acceptance:** Not applicable — remediation in progress

---

**POA&M Item ID:** POA-2026-H04
**Finding Reference:** SAR-2026-H04
**Control:** AC-17 — Remote Access
**Weakness:** 3 contractor VPN accounts remain active 14-67 days after contract expiration.
**Risk Level:** HIGH
**Likelihood:** High | **Impact:** HIGH
**Resources Required:** 1 hour ISSO time; immediate account disablement
**Scheduled Completion:** April 10, 2026 (IMMEDIATE)
**Responsible Party:** ISSO — Amara Osei; HR — Catherine Park
**Milestone 1:** Immediately disable all 3 contractor VPN accounts — April 10, 2026
**Milestone 2:** Review access logs for all 3 accounts during unauthorized period — April 12, 2026
**Milestone 3:** Implement automated HR-IT integration for contractor account deprovisioning — May 1, 2026
**Milestone 4:** Update contractor offboarding procedure; train HR staff — May 10, 2026
**Status:** OPEN — IMMEDIATE action required. Accounts to be disabled upon ATO issuance today.
**AO Risk Acceptance:** AO accepts risk for period prior to remediation; no evidence of unauthorized activity

---

## MODERATE Risk Findings

| POA&M ID | Finding ID | Control | Weakness Summary | Scheduled Completion | Responsible Party | Status |
|---------|-----------|---------|-----------------|---------------------|------------------|--------|
| POA-2026-M01 | SAR-2026-M01 | CM-6 | 12 servers deviate from CIS L2 baseline — SNMP v1, FTP binaries present | June 15, 2026 | IT Infrastructure | OPEN |
| POA-2026-M02 | SAR-2026-M02 | CA-7 | ConMon plan lacks documented frequency for 6 AWS Config rules | May 30, 2026 | ISSO | OPEN |
| POA-2026-M03 | SAR-2026-M03 | SC-28(1) | 2 S3 buckets using SSE-S3 instead of CMK-based encryption | May 15, 2026 | IT Infrastructure | OPEN |
| POA-2026-M04 | SAR-2026-M04 | CP-9 | Database backup restoration not tested in 12 months | May 31, 2026 | IT Infrastructure | OPEN |
| POA-2026-M05 | SAR-2026-M05 | IA-8 | Non-organizational user authentication not using approved external IdP | June 30, 2026 | ISSO | OPEN |
| POA-2026-M06 | SAR-2026-M06 | SC-7(5) | Default deny firewall rule not consistently applied to all EHRP network segments | June 15, 2026 | IT Infrastructure | OPEN |
| POA-2026-M07 | SAR-2026-M07 | SA-11 | No formal SAST/DAST integration in EHRP CI/CD pipeline | July 31, 2026 | System Owner | OPEN |
| POA-2026-M08 | SAR-2026-M08 | AC-6(1) | Some privileged functions accessible to non-privileged accounts in EHRP admin module | May 30, 2026 | ISSO | OPEN |
| POA-2026-M09 | SAR-2026-M09 | CM-11 | User-installed software policy not technically enforced on all EHRP workstations | June 30, 2026 | IT Infrastructure | OPEN |
| POA-2026-M10 | SAR-2026-M10 | SI-12(3) | De-identification procedures for research data exports not formally documented | June 15, 2026 | Privacy Officer | OPEN |
| POA-2026-M11 | SAR-2026-M11 | PT-3 | Privacy notice to patients not updated to reflect current EHRP data processing | May 31, 2026 | Privacy Officer | OPEN |

---

## LOW Risk Findings

| POA&M ID | Finding ID | Control | Weakness Summary | Scheduled Completion | Status |
|---------|-----------|---------|-----------------|---------------------|--------|
| POA-2026-L01 | SAR-2026-L01 | AT-2 | 23 users overdue on annual security awareness training (94% completion) | May 1, 2026 | OPEN |
| POA-2026-L02 | SAR-2026-L02 | PL-2 | SSP annual review signature 14 days overdue | April 20, 2026 | OPEN |
| POA-2026-L03 | SAR-2026-L03 | RA-5 | Vulnerability scan report not distributed within 48-hour SLA | May 1, 2026 | OPEN |
| POA-2026-L04 | SAR-2026-L04 | MA-4 | Remote maintenance session logs not reviewed on monthly schedule | May 15, 2026 | OPEN |
| POA-2026-L05 | SAR-2026-L05 | IR-3 | Tabletop incident response exercise documentation incomplete | May 31, 2026 | OPEN |
| POA-2026-L06 | SAR-2026-L06 | CM-3 | 4 minor change requests approved without security impact analysis | May 1, 2026 | OPEN |
| POA-2026-L07 | SAR-2026-L07 | SA-9 | Surescripts third-party security assessment overdue by 30 days | May 31, 2026 | OPEN |
| POA-2026-L08 | SAR-2026-L08 | SC-20 | DNSSEC not enabled on external EHRP domain | June 30, 2026 | OPEN |

---

## POA&M Management Procedures

### Monthly Update Process
1. ISSO reviews all open POA&M items by the 10th of each month
2. Responsible parties provide status updates to ISSO by the 12th
3. ISSO prepares updated POA&M and monthly ConMon report by the 15th
4. ISSO submits POA&M and ConMon report to AODR by the 15th
5. AODR reviews and escalates any overdue HIGH findings to System Owner within 2 business days

### Escalation Procedures
- Items approaching scheduled completion without progress: Escalate to System Owner 14 days prior
- Items past scheduled completion: Escalate to AODR immediately; notify AO if HIGH severity
- New HIGH or CRITICAL findings discovered post-authorization: Notify AO within 72 hours

### Closure Requirements
Findings may only be marked **CLOSED** when:
1. Remediation is fully implemented (not just planned)
2. ISSO has verified remediation through inspection, testing, or review
3. Documentary evidence of remediation is attached to the POA&M entry
4. For HIGH findings: System Owner provides written sign-off on closure

---

*Document Owner: ISSO — Amara Osei | Update Cycle: Monthly | Classification: Sensitive*
*MedCore Health Systems is fictional. Created for cybersecurity portfolio demonstration purposes only.*
