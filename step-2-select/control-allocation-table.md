# Step 2 — Select: Security Control Allocation Table
## MedCore EHRP | NIST SP 800-53 Rev 5 High Baseline

**Document Type:** Control Allocation Table | **Version:** 1.0 | **Date:** April 2026
**Baseline:** NIST SP 800-53 Rev 5 — HIGH Baseline (265 controls)

---

## Overview

This document identifies the security control baseline selected for the MedCore EHRP and allocates each control as System-Specific, Common (Inherited), or Hybrid. This allocation determines which controls the System Owner is responsible for implementing vs. which are inherited from the Common Control Provider.

**Total Controls Selected: 265**
- System-Specific Controls: 198
- Common (Inherited) Controls: 42
- Hybrid Controls: 25

---

## Baseline Selection Rationale

The MedCore EHRP received a HIGH overall security categorization under FIPS 199 (Confidentiality=HIGH, Integrity=HIGH, Availability=HIGH). Per FIPS 200 and NIST SP 800-53 Rev 5, a HIGH-impact system must implement the HIGH security control baseline as the minimum set of controls.

**Selected Baseline:** NIST SP 800-53 Rev 5 — HIGH Baseline
**Tailoring:** Controls have been tailored based on system-specific conditions, mission/business needs, and the operational environment (healthcare, cloud/on-premises hybrid). See [tailoring-decisions.md](./tailoring-decisions.md).

---

## Control Allocation by Family

| Family ID | Family Name | Total Controls | System-Specific | Common (Inherited) | Hybrid |
|-----------|------------|:--------------:|:---------------:|:------------------:|:------:|
| AC | Access Control | 25 | 22 | 0 | 3 |
| AT | Awareness & Training | 6 | 0 | 6 | 0 |
| AU | Audit & Accountability | 16 | 13 | 0 | 3 |
| CA | Assessment, Authorization & Monitoring | 9 | 7 | 0 | 2 |
| CM | Configuration Management | 14 | 12 | 0 | 2 |
| CP | Contingency Planning | 13 | 10 | 0 | 3 |
| IA | Identification & Authentication | 13 | 11 | 0 | 2 |
| IR | Incident Response | 10 | 2 | 7 | 1 |
| MA | Maintenance | 6 | 5 | 0 | 1 |
| MP | Media Protection | 8 | 6 | 0 | 2 |
| PE | Physical & Environmental | 23 | 0 | 23 | 0 |
| PL | Planning | 11 | 9 | 0 | 2 |
| PM | Program Management | 32 | 28 | 0 | 4 |
| PS | Personnel Security | 9 | 0 | 9 | 0 |
| PT | PII Processing & Transparency | 8 | 6 | 0 | 2 |
| RA | Risk Assessment | 10 | 8 | 0 | 2 |
| SA | System & Services Acquisition | 23 | 20 | 0 | 3 |
| SC | System & Communications Protection | 51 | 47 | 0 | 4 |
| SI | System & Information Integrity | 23 | 20 | 0 | 3 |
| SR | Supply Chain Risk Management | 12 | 10 | 0 | 2 |
| **TOTAL** | | **265** | **198** | **45** | **42** |

---

## Key Control Allocations — Detail

### Fully Inherited (Common) Controls

The following control families are **fully inherited** from the MedCore IT Infrastructure team (Common Control Provider):

**Physical and Environmental Protection (PE) — All controls inherited**
- PE-1 through PE-23 are implemented at the organizational level for all MedCore data center facilities
- The MedCore data center implements badge access, CCTV, environmental monitoring, and power redundancy
- Evidence: Physical security assessment reports provided by Facilities Security team

**Personnel Security (PS) — All controls inherited**
- PS-1 through PS-9 are implemented organization-wide through Human Resources
- Background investigations conducted at hire and every 5 years for privileged users
- Evidence: HR policy documentation, background check vendor contracts

**Awareness & Training (AT) — All controls inherited**
- AT-1 through AT-6 implemented organization-wide via the MedCore Security Awareness Program
- All staff complete annual security awareness training; privileged users complete role-based training
- Evidence: Training completion records from LMS (Learning Management System)

**Incident Response (IR) — Majority inherited**
- IR-1, IR-2, IR-4, IR-5, IR-6, IR-7, IR-8 are inherited from the Enterprise SOC
- EHRP-specific incident response procedures (IR-3 Testing, IR-9 Spillage) are system-specific
- Evidence: Enterprise Incident Response Plan, SOC operations procedures

---

### System-Specific Controls — Selected Examples

| Control | Name | Allocation | Implementation Approach |
|---------|------|-----------|------------------------|
| AC-2 | Account Management | System-Specific | Active Directory + Azure AD role-based access for EHRP |
| AC-3 | Access Enforcement | System-Specific | EHRP application-layer RBAC enforcing least privilege |
| AC-17 | Remote Access | System-Specific | Cisco AnyConnect VPN with MFA required for remote EHRP access |
| AU-2 | Event Logging | System-Specific | EHRP audit events forwarded to Splunk SIEM |
| AU-9 | Protection of Audit Information | System-Specific | Audit logs stored in immutable S3 bucket (WORM) |
| CM-7 | Least Functionality | System-Specific | EHRP servers hardened per CIS Benchmarks |
| IA-2 | Multi-Factor Authentication | System-Specific | MFA enforced for all EHRP users via Azure AD Conditional Access |
| IA-5 | Authenticator Management | System-Specific | Password policy enforced: 16 char min, 90-day rotation for privileged |
| SC-8 | Transmission Confidentiality | System-Specific | TLS 1.3 enforced for all EHRP data in transit |
| SC-28 | Protection at Rest | System-Specific | AES-256 encryption for all PHI in RDS (PostgreSQL) |
| SI-3 | Malware Protection | System-Specific | CrowdStrike Falcon EDR deployed on all EHRP endpoints |
| SI-7 | Software Integrity Verification | System-Specific | Code signing and SBOM for all EHRP application deployments |
| SC-12 | Cryptographic Key Management | System-Specific | AWS KMS with HSM-backed keys for PHI encryption |

---

### Hybrid Controls — Selected Examples

| Control | Name | System-Specific Portion | Inherited Portion |
|---------|------|------------------------|------------------|
| CA-2 | Control Assessments | EHRP-specific assessment scope | Enterprise assessment methodology |
| CA-7 | Continuous Monitoring | EHRP-specific ConMon metrics | Enterprise ConMon program governance |
| AU-6 | Audit Record Review | EHRP-specific log review procedures | Enterprise SIEM (Splunk) platform |
| CP-9 | System Backup | EHRP-specific backup schedule and RPO/RTO | Enterprise backup infrastructure |
| CM-6 | Configuration Settings | EHRP application config baselines | Enterprise hardening standards |

---

## Tailoring Decisions Summary

See [tailoring-decisions.md](./tailoring-decisions.md) for the complete tailoring rationale. Key decisions include:

| Decision | Control(s) | Rationale |
|---------|-----------|----------|
| Added control | SC-8(1) Cryptographic Protection | All PHI transmissions must use approved cryptography per HIPAA |
| Added control | AC-2(1) Automated Account Management | HIGH-impact system requires automation for account lifecycle |
| Added control | IA-2(1)(2)(12) MFA for All Access | PHI access requires MFA per HIPAA Security Rule |
| Added control | AU-2(3) Review of Events | PHI systems require enhanced audit event categories |
| Added control | SI-12 Memory Protection | HIGH-impact systems require memory protection controls |
| Scoped out | PE family (all) | Fully inherited from Common Control Provider |
| Scoped out | AT family (all) | Fully inherited from Common Control Provider |

---

*Document Owner: ISSO — Amara Osei | Next Review: April 2027*
*MedCore Health Systems is fictional. Created for cybersecurity portfolio demonstration purposes only.*
