# Monthly Continuous Monitoring Report — Template
## MedCore Electronic Health Records Platform (EHRP) v4.2.1

---

> **INSTRUCTIONS FOR ISSO:** Complete all [BRACKETED] fields before submission. Remove this instruction block prior to distribution. Submit to CISO by the 15th of each month. CISO forwards to AO by the 20th.

---

**MONTHLY CONMON REPORT**

**Organization:** MedCore Health Systems
**System:** MedCore Electronic Health Records Platform (EHRP) v4.2.1
**Reporting Period:** [MONTH YEAR] (e.g., April 2026)
**Report Number:** ConMon-[YEAR]-[MONTH NUMBER] (e.g., ConMon-2026-04)
**Prepared By:** Amara Osei, ISSO
**Reviewed By:** Jonathan E. Steele, CISO
**Date Submitted to CISO:** [DATE - must be on or before 15th of month]
**Date Forwarded to AO:** [DATE - must be on or before 20th of month]
**ATO Expiration Date:** March 28, 2029
**Classification:** SENSITIVE FOR OFFICIAL USE ONLY

---

## Section 1: Executive Summary

### 1.1 Overall Security Posture — RAG Status

| Domain | Status | Change from Last Month | Notes |
|--------|--------|----------------------|-------|
| Vulnerability Management | [GREEN / AMBER / RED] | [IMPROVED / STABLE / DEGRADED] | [Brief note] |
| Access Control | [GREEN / AMBER / RED] | [IMPROVED / STABLE / DEGRADED] | [Brief note] |
| Incident Response | [GREEN / AMBER / RED] | [IMPROVED / STABLE / DEGRADED] | [Brief note] |
| Configuration Compliance | [GREEN / AMBER / RED] | [IMPROVED / STABLE / DEGRADED] | [Brief note] |
| POA&M Health | [GREEN / AMBER / RED] | [IMPROVED / STABLE / DEGRADED] | [Brief note] |
| **Overall System Posture** | **[GREEN / AMBER / RED]** | **[IMPROVED / STABLE / DEGRADED]** | |

**Overall Posture Narrative:**
[2-3 sentences summarizing the security posture this month. Note any significant events, improvements, or concerns. Example: "The MedCore EHRP maintained an overall GREEN security posture during [month]. Vulnerability management metrics remained within target thresholds, with all HIGH findings remediated within SLA. One new MODERATE finding was identified during monthly scanning and added to the POA&M."]

### 1.2 Key Highlights This Month

- [HIGHLIGHT 1 - e.g., Completed quarterly user access recertification with 0 exceptions identified]
- [HIGHLIGHT 2 - e.g., Successfully patched 3 HIGH-rated vulnerabilities (CVE-XXXX-XXXXX) within 15-day SLA]
- [HIGHLIGHT 3 - e.g., Completed annual incident response tabletop exercise with no major gaps identified]
- [Add or remove bullets as needed]

### 1.3 Key Concerns or Risks This Month

- [CONCERN 1 - e.g., Two MODERATE POA&M items approaching their scheduled completion dates - remediation in progress]
- [CONCERN 2 - if none, state "No significant concerns identified this reporting period"]

---

## Section 2: Vulnerability Management

### 2.1 Scan Coverage

| Scan Type | Assets in Scope | Assets Scanned | Coverage % | Tool Used | Scan Date |
|-----------|----------------|---------------|------------|-----------|-----------|
| Authenticated network scan (cloud) | [#] | [#] | [%] | Qualys | [DATE] |
| Authenticated network scan (on-prem) | [#] | [#] | [%] | Qualys | [DATE] |
| Configuration compliance scan | [#] | [#] | [%] | Tenable.sc | [DATE] |
| AWS Inspector container scan | [#] | [#] | [%] | AWS Inspector | [DATE] |
| Web application scan | [#] | [#] | [%] | [Tool] | [DATE] |

**Coverage Notes:** [Note any assets not scanned and reason - e.g., "Lab equipment not included in network scan per compensating control documentation in SAP."]

### 2.2 Vulnerability Summary

| Severity | New This Month | Previously Known | Total Open | Remediated This Month | Overdue (Past SLA) |
|----------|---------------|-----------------|------------|----------------------|-------------------|
| CRITICAL | [#] | [#] | [#] | [#] | [#] |
| HIGH | [#] | [#] | [#] | [#] | [#] |
| MODERATE | [#] | [#] | [#] | [#] | [#] |
| LOW | [#] | [#] | [#] | [#] | [#] |
| TOTAL | [#] | [#] | [#] | [#] | [#] |

### 2.3 SLA Compliance

| Metric | Target | Actual This Month | Status |
|--------|--------|-------------------|--------|
| Critical vulns patched within 15 days | 100% | [%] | [MET / MISSED] |
| High vulns patched within 30 days | 100% | [%] | [MET / MISSED] |
| Moderate vulns patched within 90 days | 100% | [%] | [MET / MISSED] |
| Assets scanned | 100% | [%] | [MET / MISSED] |

### 2.4 Notable Vulnerabilities This Month

[List any notable CVEs, zero-days, or significant findings discovered. If none, state "No critical or high-risk vulnerabilities requiring executive attention were identified this reporting period."]

| CVE | CVSS Score | Component Affected | Remediation Status | Scheduled Completion |
|-----|-----------|-------------------|-------------------|---------------------|
| [CVE-XXXX-XXXXX] | [Score] | [Component] | [Status] | [Date] |

---

## Section 3: Access Control and Identity Management

### 3.1 Account Management Summary

| Metric | Count | Notes |
|--------|-------|-------|
| Total active user accounts | [#] | Standard users + privileged combined |
| Privileged/admin accounts | [#] | Accounts with elevated permissions |
| Service accounts | [#] | |
| Accounts created this month | [#] | |
| Accounts disabled/removed this month | [#] | |
| Orphaned accounts discovered | [#] | Should be 0; if not, explanation required |
| Orphaned accounts remediated | [#] | |

### 3.2 MFA Compliance

| Account Type | Total Accounts | MFA Enabled | MFA % | Target | Status |
|-------------|---------------|-------------|-------|--------|--------|
| Privileged accounts | [#] | [#] | [%] | 100% | [MET / NOT MET] |
| Standard user accounts | [#] | [#] | [%] | 100% | [MET / NOT MET] |
| Service accounts | [#] | [#] | [%] | 100% | [MET / NOT MET] |

### 3.3 Access Review Activity

[Note any access reviews conducted, recertification campaigns completed, or anomalous access detected this month.]

**Quarterly Recertification:** [COMPLETED / PENDING / NOT DUE THIS MONTH]
**Exceptions Found:** [#] | **Exceptions Remediated:** [#]

---

## Section 4: Incident and Event Summary

### 4.1 Security Events and Incidents

| Metric | Count | Notes |
|--------|-------|-------|
| Total SIEM alerts triggered | [#] | Automated detections |
| Alerts escalated to investigation | [#] | Required manual analyst review |
| Formal security incidents declared | [#] | Per IR plan criteria |
| Incidents resolved this month | [#] | Fully closed |
| Incidents carried over (open) | [#] | Still under investigation |
| Potential ePHI exposure incidents | [#] | Must be 0; if not, immediate escalation required |

### 4.2 Incident Details (if applicable)

[For each formal incident declared this month, provide a brief summary. If no incidents, state "No formal security incidents were declared during this reporting period."]

| Incident ID | Date Declared | Severity | Category | Status | Resolution Summary |
|-------------|--------------|----------|----------|--------|--------------------|
| [INC-YYYY-###] | [DATE] | [P1/P2/P3] | [Category] | [OPEN/CLOSED] | [Brief description] |

### 4.3 Detection Metrics

| Metric | Target | Actual | Status |
|--------|--------|--------|--------|
| Mean Time to Detect (MTTD) | < 4 hours | [HH:MM] | [MET / NOT MET] |
| Mean Time to Respond (MTTR) - P1 | < 24 hours | [HH:MM] | [MET / NOT MET] |
| SIEM false positive rate | < 20% | [%] | [MET / NOT MET] |

---

## Section 5: Configuration and Patch Management

### 5.1 Benchmark Compliance Scores

| Component Group | Benchmark | Last Month Score | This Month Score | Change | Target |
|----------------|-----------|-----------------|-----------------|--------|--------|
| Linux servers (AWS) | CIS Level 2 | [%] | [%] | [+/-]% | ≥ 85% |
| Windows servers (on-prem) | CIS Level 2 | [%] | [%] | [+/-]% | ≥ 85% |
| AWS Config rules compliance | AWS Config | [%] | [%] | [+/-]% | ≥ 95% |
| Database hardening | CIS PostgreSQL | [%] | [%] | [+/-]% | ≥ 85% |

### 5.2 Patch Status Summary

| Patch Category | Patches Released | Patches Applied | % Applied | Deferred (with justification) |
|----------------|-----------------|-----------------|-----------|-------------------------------|
| OS - Critical/High | [#] | [#] | [%] | [#] |
| OS - Moderate | [#] | [#] | [%] | [#] |
| Application patches | [#] | [#] | [%] | [#] |
| Third-party components | [#] | [#] | [%] | [#] |

### 5.3 Change Management Activity

[Summarize significant system changes implemented this month. Include security impact assessment reference number for each change.]

| Change ID | Change Description | Implementation Date | Security Impact | SIA Reference |
|-----------|-------------------|--------------------|-----------------|----|
| [CHG-YYYY-###] | [Description] | [DATE] | [LOW/MOD/HIGH] | [SIA-###] |

---

## Section 6: POA&M Status

### 6.1 POA&M Summary

| Category | Count |
|----------|-------|
| Total open POA&M items | [#] |
| HIGH risk findings open | [#] |
| MODERATE risk findings open | [#] |
| LOW risk findings open | [#] |
| Items with milestones met this month | [#] |
| Items closed this month | [#] |
| New items added this month | [#] |
| Items overdue (past scheduled completion) | [#] - **Should be 0** |

### 6.2 HIGH Risk POA&M Items Status

[Required: Provide status for ALL open HIGH risk items]

| POA&M ID | Finding Summary | Original Completion | Current Status | % Complete | Revised Completion (if delayed) |
|----------|----------------|---------------------|---------------|------------|--------------------------------|
| [POA-ID] | [Summary] | [DATE] | [Status] | [%] | [DATE if changed] |

### 6.3 POA&M Health Assessment

**Overall POA&M Status:** [GREEN / AMBER / RED]

[2-3 sentences describing POA&M health. Example: "All HIGH risk POA&M items remain on track for their scheduled completion dates. Two MODERATE items are approaching their 90-day SLA and are actively being remediated. No items are currently overdue."]

---

## Section 7: Training and Awareness

### 7.1 Security Awareness Training Completion

| Training Category | Total Required | Completed | Completion % | Target | Status |
|------------------|---------------|-----------|-------------|--------|--------|
| Annual security awareness (all users) | [#] | [#] | [%] | 100% | [MET / NOT MET] |
| HIPAA privacy and security training | [#] | [#] | [%] | 100% | [MET / NOT MET] |
| Phishing simulation completion | [#] | [#] | [%] | 90% | [MET / NOT MET] |
| Role-based training (privileged users) | [#] | [#] | [%] | 100% | [MET / NOT MET] |

---

## Section 8: Upcoming Activities

### 8.1 Next Month Planned Activities

| Activity | Planned Date | Responsible Party |
|----------|-------------|-------------------|
| [Activity - e.g., Quarterly access recertification] | [DATE] | [Name/Team] |
| [Activity - e.g., AWS Config rule review] | [DATE] | [Name/Team] |
| [Activity - e.g., Monthly vulnerability scan] | [DATE] | [Name/Team] |
| [Activity - e.g., POA&M milestone due] | [DATE] | [Name/Team] |

### 8.2 Upcoming Major Milestones

| Milestone | Target Date | Status |
|-----------|------------|--------|
| [Milestone - e.g., Quarterly ConMon briefing to AO] | [DATE] | [ON TRACK / AT RISK] |
| [Milestone - e.g., Annual security controls assessment] | [DATE] | [ON TRACK / AT RISK] |
| [Milestone - e.g., ATO annual review] | [DATE] | [ON TRACK / AT RISK] |

---

## Section 9: Risk Summary

### 9.1 New Risks Identified This Month

[Document any new risks identified this month that are not already captured in a POA&M item. If none, state "No new risks requiring AO attention were identified this reporting period."]

| Risk ID | Risk Description | Likelihood | Impact | Risk Rating | Proposed Response |
|---------|-----------------|------------|--------|-------------|-------------------|
| [RISK-YYYY-###] | [Description] | [H/M/L] | [H/M/L] | [H/M/L] | [Mitigate / Accept / Transfer / Avoid] |

### 9.2 Risks Closed This Month

[Document any risks that have been fully mitigated and closed.]

| Risk / POA&M ID | Description | Closure Date | Evidence of Remediation |
|-----------------|-------------|-------------|------------------------|
| [ID] | [Description] | [DATE] | [Evidence reference] |

### 9.3 Overall Risk Posture Change

**Risk Posture vs. Last Month:** [IMPROVED / STABLE / DEGRADED]

[1-2 sentences summarizing the change in risk posture this month and key drivers.]

---

## Section 10: ISSO Attestation

I attest that the information contained in this report is accurate to the best of my knowledge and that the MedCore Electronic Health Records Platform (EHRP) continues to operate within the terms and conditions of the Authorization to Operate issued on March 28, 2026.

| Field | Detail |
|-------|--------|
| ISSO Name | Amara Osei |
| Signature | [Signed] |
| Date | [DATE OF SUBMISSION] |

**CISO Review:**

| Field | Detail |
|-------|--------|
| CISO Name | Jonathan E. Steele |
| Signature | [Signed] |
| Date | [DATE OF CISO REVIEW] |

---

*MedCore Health Systems - SENSITIVE / FOR OFFICIAL USE ONLY*
*Template: Monthly-ConMon-Report-EHRP | Version 1.0 | Effective April 2026*
*This template is updated annually in February. Current version approved by CISO February 28, 2026.*
