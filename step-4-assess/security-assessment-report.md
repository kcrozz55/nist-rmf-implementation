# Step 4 — Assess: Security Assessment Report (SAR)
## MedCore Electronic Health Records Platform (EHRP)

**Document Type:** Security Assessment Report (SAR) | **Version:** 1.0
**Prepared Per:** NIST SP 800-53A Rev 5 | NIST SP 800-37 Rev 2
**Assessor:** CyberProof Solutions (Independent Third-Party SCA)
**Assessment Period:** March 3 — March 28, 2026
**Report Date:** April 5, 2026
**Report Classification:** Sensitive — For Authorized Recipients Only

---

## Executive Summary

CyberProof Solutions conducted an independent security control assessment of the MedCore Electronic Health Records Platform (EHRP) between March 3 and March 28, 2026. The assessment evaluated all 265 security controls selected for the EHRP against the HIGH baseline of NIST SP 800-53 Rev 5, using assessment procedures defined in NIST SP 800-53A Rev 5.

**Assessment Result:** 4 High findings, 11 Moderate findings, 8 Low findings, and 4 Informational findings were identified. The remaining 238 controls were assessed as **Satisfied** with no findings.

Despite the open findings, CyberProof Solutions recommends that the Authorizing Official consider issuing an Authorization to Operate (ATO) contingent on: (1) the 4 High findings being addressed within 30 days, and (2) all Moderate findings being tracked in the POA&M with committed remediation timelines.

---

## Assessment Scope

**In-Scope Systems and Components:**
- EHRP Application Servers (AWS EC2)
- Amazon RDS (PostgreSQL) — PHI database
- AWS S3 buckets (EHRP data and audit logs)
- AWS KMS and Secrets Manager
- Splunk SIEM (log ingestion from EHRP components)
- Active Directory / Azure AD (EHRP authentication)
- CrowdStrike Falcon (endpoint protection on EHRP servers)
- Palo Alto Firewalls (EHRP network boundary)
- Cisco AnyConnect VPN (remote access)
- Tenable Nessus (vulnerability scanning)

**Out of Scope:**
- Surescripts e-Prescribing platform (covered by separate assessment)
- State HIE connection (covered by Georgia DHR assessment)
- Physical data center (covered by facilities security assessment)

---

## Assessment Methodology

The assessment used three assessment methods per NIST SP 800-53A Rev 5:

| Method | Description | Controls Assessed |
|--------|-------------|------------------|
| **Examine** | Review of documentation, policy, configuration files, logs | 265 controls |
| **Interview** | Discussion with ISSO, System Owner, System Administrators, end users | 180 controls |
| **Test** | Technical testing including scanning, configuration inspection, penetration testing | 142 controls |

**Penetration Testing:** A focused penetration test was conducted March 10-14, 2026, targeting the EHRP web application, API Gateway, and external attack surface. No critical vulnerabilities were exploited during the test.

---

## Assessment Findings

### HIGH Findings (4)

---

**Finding ID:** SAR-2026-H01
**Control:** IA-5(1) — Authenticator Management (Password-Based)
**Finding:** Password complexity requirements for standard user accounts do not meet NIST SP 800-63B requirements. Current policy allows dictionary words and common passwords. The password minimum length for standard users is 10 characters, below the SSP-documented 14-character minimum.
**Risk:** Weak passwords increase the likelihood of credential compromise through brute-force or credential stuffing attacks, potentially enabling unauthorized access to PHI.
**Risk Rating:** HIGH
**Recommendation:** Implement NIST SP 800-63B compliant password policy immediately. Deploy Azure AD Password Protection to block common and compromised passwords. Enforce 14-character minimum across all account types.
**Responsible Party:** ISSO
**Required Completion:** May 15, 2026

---

**Finding ID:** SAR-2026-H02
**Control:** SI-2 — Flaw Remediation
**Finding:** Vulnerability scan results identified 3 critical and 7 high vulnerabilities on EHRP application servers that have exceeded the required patch remediation timeframes. The oldest unpatched critical vulnerability is 47 days old (threshold: 15 days).
**Risk:** Unpatched vulnerabilities represent exploitable attack surface that could be leveraged to gain unauthorized access to EHRP systems and PHI.
**Risk Rating:** HIGH
**Recommendation:** Apply all critical patches within 5 business days of this report. Implement automated patch deployment for OS-level patches. Review and remediate patch management process gaps.
**Responsible Party:** Director of IT Infrastructure
**Required Completion:** April 25, 2026

---

**Finding ID:** SAR-2026-H03
**Control:** AU-9 — Protection of Audit Information
**Finding:** Three EHRP application servers are not forwarding audit logs to the Splunk SIEM. The log gap has existed for approximately 22 days. During this period, user access and activity on these servers has not been logged centrally.
**Risk:** Absence of centralized audit logging creates a blind spot for the security monitoring program and may indicate unauthorized activity has gone undetected.
**Risk Rating:** HIGH
**Recommendation:** Immediately remediate the Splunk Universal Forwarder configuration on affected servers. Conduct a manual audit of local logs on affected servers for the 22-day gap period. Implement automated monitoring of log pipeline health.
**Responsible Party:** ISSO
**Required Completion:** April 18, 2026

---

**Finding ID:** SAR-2026-H04
**Control:** AC-17 — Remote Access
**Finding:** Three contractor accounts were found with active VPN access after their contracts expired. These accounts have been active for 14 to 67 days beyond contract end dates.
**Risk:** Unauthorized access by former contractors could allow them to access EHRP systems and PHI without a legitimate business need.
**Risk Rating:** HIGH
**Recommendation:** Immediately disable the three identified contractor accounts. Implement an automated integration between the contractor management system and Active Directory to trigger account deprovisioning on contract expiration.
**Responsible Party:** ISSO + Human Resources
**Required Completion:** April 10, 2026 (Immediate)

---

### MODERATE Findings (Selected — 4 of 11 shown)

**Finding ID:** SAR-2026-M01 | **Control:** CM-6 — Configuration Settings
**Finding:** 12 EHRP application servers have configurations that deviate from the CIS Benchmark Level 2 baseline. Deviations include enabled services not required for EHRP operation (SNMP v1, FTP service binaries present).
**Risk Rating:** MODERATE | **Completion:** June 15, 2026

**Finding ID:** SAR-2026-M02 | **Control:** CA-7 — Continuous Monitoring
**Finding:** The EHRP ConMon plan lacks documented frequency for reviewing specific AWS Config rules. Six Config rules have not been reviewed in 6+ months.
**Risk Rating:** MODERATE | **Completion:** May 30, 2026

**Finding ID:** SAR-2026-M03 | **Control:** SC-28(1) — Cryptographic Protection of Data at Rest
**Finding:** Two S3 buckets used for EHRP operational data are configured with AWS-managed keys (SSE-S3) rather than customer-managed KMS keys as required by SSP Section SC-28.
**Risk Rating:** MODERATE | **Completion:** May 15, 2026

**Finding ID:** SAR-2026-M04 | **Control:** CP-9 — System Backup
**Finding:** EHRP database backup restoration has not been tested within the past 12 months. The SSP requires annual backup restoration testing to validate recovery procedures.
**Risk Rating:** MODERATE | **Completion:** May 31, 2026

---

### LOW and Informational Findings (Summary)

| Finding ID | Control | Finding Summary | Risk Rating |
|-----------|---------|----------------|-------------|
| SAR-2026-L01 | AT-2 | Security awareness training completion rate is 94% (below 100% target) — 23 users overdue | LOW |
| SAR-2026-L02 | PL-2 | SSP review date is 14 days overdue for annual review signature | LOW |
| SAR-2026-L03 | RA-5 | Vulnerability scan report from February was not distributed to System Owner within 48-hour SLA | LOW |
| SAR-2026-L04 | MA-4 | Remote maintenance session logs not reviewed within required monthly timeframe | LOW |
| SAR-2026-L05 | IR-3 | Tabletop incident response exercise documentation is incomplete | LOW |
| SAR-2026-L06 | CM-3 | 4 minor change requests were approved without documented security impact analysis | LOW |
| SAR-2026-L07 | SA-9 | Third-party vendor security assessment for Surescripts is overdue by 30 days | LOW |
| SAR-2026-L08 | SC-20 | DNS DNSSEC is not enabled on the EHRP external domain | LOW |
| SAR-2026-INFO-01 | AC-2 | Account provisioning process takes an average of 4.2 days — below the 2-day target | INFORMATIONAL |
| SAR-2026-INFO-02 | AU-11 | Audit log retention on one legacy server is 180 days, below the 7-year PHI retention requirement | INFORMATIONAL |
| SAR-2026-INFO-03 | SI-3 | CrowdStrike Falcon agent on 2 servers is running a version 2 releases behind current | INFORMATIONAL |
| SAR-2026-INFO-04 | PM-6 | Risk register has not been reviewed and updated in 4 months | INFORMATIONAL |

---

## Assessment Summary Statistics

| Rating | Count | Percentage of Total Controls |
|--------|:-----:|:----------------------------:|
| Satisfied (No Finding) | 238 | 89.8% |
| HIGH | 4 | 1.5% |
| MODERATE | 11 | 4.2% |
| LOW | 8 | 3.0% |
| INFORMATIONAL | 4 | 1.5% |
| **TOTAL** | **265** | **100%** |

---

## Assessor Recommendation

CyberProof Solutions recommends that the Authorizing Official issue an **Authorization to Operate (ATO)** for the MedCore EHRP under the following conditions:

1. The 4 HIGH findings are remediated or have documented accepted risk with executive approval prior to ATO issuance
2. All 11 MODERATE findings are entered into the POA&M with committed remediation timelines and assigned responsible parties
3. LOW and Informational findings are included in the POA&M and tracked to closure
4. The ISSO provides monthly POA&M updates to the AODR

The overall security posture of the MedCore EHRP is adequate for an operational system handling PHI, provided the identified HIGH findings are addressed promptly. The system demonstrates strong controls in the areas of cryptographic protection, multi-factor authentication, and security monitoring.

---

## SAR Approval

| Role | Name | Organization | Date |
|------|------|-------------|------|
| Lead Assessor | Sarah Chen, CISSP | CyberProof Solutions | April 5, 2026 |
| ISSO (Reviewed) | Amara Osei | MedCore Health Systems | April 7, 2026 |
| System Owner (Reviewed) | Jonathan E. Steele | MedCore Health Systems | April 8, 2026 |
| AO (Accepted) | Marcus T. Hargrove | MedCore Health Systems | April 10, 2026 |

---

*All names, organizations, findings, and system details are fictional. Created for cybersecurity portfolio demonstration purposes only.*
