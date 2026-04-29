# System Security Plan (SSP)
## MedCore Electronic Health Records Platform (EHRP) v4.2.1
### Step 3: Implement Security Controls

---

**Organization:** MedCore Health Systems
**System Name:** MedCore Electronic Health Records Platform (EHRP)
**System Version:** v4.2.1
**Overall System Categorization:** HIGH (C=HIGH, I=HIGH, A=HIGH)
**Applicable Baseline:** NIST SP 800-53 Rev 5 HIGH Baseline (272 controls after tailoring)
**SSP Version:** 1.0
**Classification:** SENSITIVE FOR OFFICIAL USE ONLY
**Date:** February 28, 2026
**Prepared By:** Amara Osei, ISSO
**Reviewed By:** Jonathan E. Steele, CISO
**Approved By:** Marcus T. Hargrove, Authorizing Official

---

## PART I: SYSTEM IDENTIFICATION

### 1.1 System Overview

MedCore Electronic Health Records Platform (EHRP) v4.2.1 is the primary clinical information system for MedCore Health Systems, a regional healthcare provider based in Atlanta, Georgia. The EHRP manages the complete lifecycle of patient electronic health records across all MedCore facilities, supporting approximately 1,847 authorized users including physicians, nurses, clinical staff, and administrative personnel.

The system operates in a hybrid cloud/on-premises architecture. Primary workloads run in AWS GovCloud (us-gov-east-1) with on-premises components supporting legacy HL7 integration and laboratory equipment interfaces. The system processes, stores, and transmits electronic Protected Health Information (ePHI) and Personally Identifiable Information (PII) for approximately 340,000 active patient records.

### 1.2 System Components

**Cloud Infrastructure (AWS GovCloud):**
- API Gateway (OIDC/Auth) — TLS 1.3 termination and request routing
- Patient Management Service — CRUD operations for patient demographics and registration
- Clinical Records Service — EHR documentation, notes, orders, and clinical workflow
- Scheduling Service — Appointment management and resource scheduling
- Billing and Claims Service — Insurance claims processing and revenue cycle management
- Message Broker (Kafka/RabbitMQ) — Asynchronous event processing between services
- Clinical Database (PostgreSQL RDS) — Primary persistent data store for all ePHI
- Medical Imaging Store (S3 with server-side encryption) — DICOM and imaging data storage
- Session Cache (ElastiCache/Redis) — Session management and temporary data caching
- AWS KMS — Key management for all encryption keys
- AWS CloudTrail — API activity logging across all EHRP AWS resources
- AWS CloudWatch — Metrics, alarms, and log aggregation
- AWS Security Hub — Unified security posture management
- Amazon GuardDuty — Threat detection and anomaly detection
- AWS Config — Configuration compliance monitoring
- Amazon Macie — ePHI detection and data classification in S3

**On-Premises Components:**
- Legacy HL7 Interface Engine (IBM MQ Series) — HL7 v2 message processing for legacy integrations
- Local Gateway — Protocol translation and secure tunnel management
- Lab Equipment Integration Points — Laboratory analyzer interfaces

**External Interconnections:**
- External Health Information Exchange (HIE) via HL7/FHIR
- Insurance Payer connections via EDI/X12
- Surescripts e-Rx via certified connection
- Identity Provider (OAuth2/OIDC) for federated authentication

### 1.3 Key Personnel

| Role | Name | Contact |
|------|------|---------|
| Authorizing Official (AO) | Marcus T. Hargrove, CEO | mhargrove@medcorehealthsystems.org |
| Chief Information Security Officer (CISO) | Jonathan E. Steele | jsteele@medcorehealthsystems.org |
| Information System Security Officer (ISSO) | Amara Osei | aosei@medcorehealthsystems.org |
| Chief Information Officer (CIO) / System Owner | Dr. Priya Nambiar | pnambiar@medcorehealthsystems.org |
| Privacy Officer | Dr. Rachel Feinberg | rfeinberg@medcorehealthsystems.org |
| Senior Systems Administrator | Thomas J. Bridwell | tbridwell@medcorehealthsystems.org |
| Cloud Security Engineer | Keisha M. Robertson | krobertson@medcorehealthsystems.org |
| IAM Administrator | Carlos Vega | cvega@medcorehealthsystems.org |
| Network Engineer | Patrick O. Sullivan | psullivan@medcorehealthsystems.org |

---

## PART II: SECURITY CONTROL IMPLEMENTATIONS

### ACCESS CONTROL (AC)

---

**AC-1 — Access Control Policy and Procedures**

**Implementation Status:** Implemented

**Implementation Description:**
MedCore Health Systems maintains a formal Access Control Policy (MedCore-POL-AC-001, Version 3.2, effective January 2026) that establishes the scope, objectives, and requirements for access control across all information systems including the EHRP. The policy addresses purpose, scope, roles, responsibilities, management commitment, coordination among organizational entities, and compliance.

Supporting procedures are documented in the EHRP Access Control Procedures document (MedCore-PROC-AC-001, Version 2.1). The ISSO reviews and updates the policy and procedures annually and whenever significant changes occur. The most recent review was completed January 15, 2026.

**Responsible Role:** ISSO, IAM Administrator
**Review Frequency:** Annual

---

**AC-2 — Account Management**

**Implementation Status:** Implemented

**Implementation Description:**
The EHRP employs a lifecycle account management process covering creation, modification, review, disablement, and removal of all account types. All accounts are provisioned through a formal access request workflow requiring manager approval and ISSO review for privileged access.

Account types include: individual named user accounts, service accounts (non-interactive), shared emergency break-glass accounts (4 total, stored in physical lockbox), and temporary contractor accounts (90-day maximum duration).

The IAM Administrator conducts monthly reviews of privileged accounts and quarterly recertification of all standard accounts. Accounts for terminated users are disabled within 24 hours of HR notification (1 hour for high-risk terminations per AC-2(13)). Service account passwords rotate on a 90-day schedule via AWS Secrets Manager.

Okta serves as the central Identity Provider for all EHRP user authentication, integrating with AWS IAM Identity Center for cloud resource access and Active Directory for on-premises components.

**Responsible Role:** IAM Administrator, ISSO
**Review Frequency:** Monthly (privileged), Quarterly (all accounts)

---

**AC-3 — Access Enforcement**

**Implementation Status:** Implemented

**Implementation Description:**
The EHRP enforces access control policies at multiple layers:

- **Application Layer:** Role-Based Access Control (RBAC) implemented within the EHRP application. Defined roles include: Physician, Registered Nurse, Medical Assistant, Scheduling Staff, Billing Specialist, IT Administrator, ISSO, Read-Only Auditor, and Break-Glass Emergency.
- **API Layer:** AWS API Gateway enforces OAuth2 token validation before any request reaches backend services. All API calls require a valid, unexpired JWT with appropriate scope claims.
- **Database Layer:** PostgreSQL row-level security (RLS) restricts query results to records within the user's authorized patient panel (treating providers) or organization-wide access (administrators).
- **Cloud Layer:** AWS IAM policies with least-privilege controls govern all access to AWS resources by both human users and service accounts.

**Responsible Role:** Systems Administrator, Cloud Security Engineer
**Review Frequency:** Quarterly (access rights review)

---

**AC-6 — Least Privilege**

**Implementation Status:** Implemented

**Implementation Description:**
MedCore EHRP enforces least privilege through the following mechanisms:

All user roles are defined with the minimum permissions required to perform assigned job functions. The EHRP RBAC model was reviewed and approved by the System Owner and Privacy Officer. No role has blanket administrative access; even IT administrators operate under role-limited accounts for daily tasks, with separate privileged accounts used only when elevated access is required.

AWS IAM policies follow least-privilege principles: all policies are deny-by-default with explicit allow statements scoped to specific resources and actions. IAM permission boundaries are applied to all developer and operator roles to prevent privilege escalation.

Privileged access to production systems requires the use of dedicated privileged accounts (separate from daily-use accounts) and is logged through a Privileged Access Management (PAM) solution. All privileged sessions are recorded.

**Responsible Role:** IAM Administrator, Cloud Security Engineer
**Review Frequency:** Quarterly

---

**AC-7 — Unsuccessful Logon Attempts**

**Implementation Status:** Implemented

**Implementation Description:**
Okta enforces account lockout after 5 consecutive unsuccessful authentication attempts. After lockout, accounts remain locked for 30 minutes before automatic unlock, or may be immediately unlocked by the IAM Administrator.

For workstations in patient-facing areas (exam rooms, nursing stations), Windows Group Policy enforces a 3-attempt lockout with immediate administrator notification, due to the higher risk of unauthorized ePHI access in shared clinical environments.

Lockout events are forwarded to the SIEM (Splunk) and generate an alert to the ISSO if a single account exceeds 3 lockout events within a 24-hour period, which may indicate a brute-force attack or account compromise attempt.

**Responsible Role:** IAM Administrator, Systems Administrator
**Review Frequency:** Monthly (SIEM review)

---

### AUDIT AND ACCOUNTABILITY (AU)

---

**AU-2 — Event Logging**

**Implementation Status:** Implemented

**Implementation Description:**
The EHRP logs the following security-relevant events across all system components:

- User authentication events (success, failure, MFA challenge, lockout)
- Privileged user actions and administrative operations
- ePHI access events (view, create, modify, delete of patient records)
- System configuration changes
- Account lifecycle events (creation, modification, disablement, deletion)
- Security control failures and alerts
- Network connection events (VPN, remote access, firewall denials)
- API calls to all AWS services (via CloudTrail)
- Database query events for ePHI tables (PostgreSQL audit extension)
- Application error events and exception logs

The ISSO reviewed and approved the audit event list in coordination with the Privacy Officer to ensure HIPAA audit logging requirements (45 CFR 164.312(b)) are fully satisfied.

**Responsible Role:** Systems Administrator, Cloud Security Engineer, SOC Analyst
**Review Frequency:** Weekly (automated review); Monthly (ISSO review)

---

**AU-9 — Protection of Audit Information**

**Implementation Status:** Implemented with Enhancement AU-9(3)

**Implementation Description:**
Audit records are protected from unauthorized access and modification through the following controls:

- SIEM (Splunk) access is restricted to SOC analysts (read-only) and the ISSO (read/write for configuration). No production system can modify or delete Splunk log data.
- AWS CloudTrail logs are delivered to a dedicated S3 bucket with Object Lock enabled (WORM — Write Once, Read Many) for a minimum retention period of 7 years per AU-11.
- S3 bucket policies deny all deletion operations, including from the root account.
- HMAC-SHA-256 cryptographic protection (AU-9(3)) is applied to all log records at ingestion into Splunk, creating a verifiable chain of integrity.
- Log forwarding pipelines are monitored; any failure to receive expected log volume triggers an immediate alert to the ISSO within 15 minutes per AU-5 parameter values.

**Responsible Role:** Cloud Security Engineer, SOC Analyst
**Review Frequency:** Monthly integrity verification

---

**AU-11 — Audit Record Retention**

**Implementation Status:** Implemented

**Implementation Description:**
All EHRP audit records are retained for a minimum of 7 years in accordance with MedCore's Records Retention Schedule (MedCore-POL-RM-001). This exceeds the HIPAA minimum requirement of 6 years and satisfies MedCore's legal hold requirements.

Active audit records are maintained in Splunk for the current year plus one preceding year (approximately 2 years of immediately searchable data). Records older than 2 years are archived to AWS S3 Glacier Instant Retrieval with a documented retrieval SLA of 4 hours, and are available for legal, regulatory, or incident investigation purposes.

**Responsible Role:** Cloud Security Engineer, ISSO
**Review Frequency:** Annual (retention validation)

---

### CONFIGURATION MANAGEMENT (CM)

---

**CM-2 — Baseline Configuration**

**Implementation Status:** Implemented

**Implementation Description:**
MedCore maintains a documented baseline configuration for all EHRP components. The EHRP Security Baseline v2.1 (current as of January 2026) documents approved configurations for all servers, network devices, and application components within the authorization boundary.

Baseline configurations are derived from: CIS Level 2 Benchmarks for all Linux and Windows servers; DISA STIG guidance for applicable components; and MedCore-specific security requirements documented in the application configuration standards.

Baseline configurations are stored in a version-controlled repository (AWS CodeCommit) with access restricted to the Systems Administrator and Cloud Security Engineer. All changes to baseline configurations require change management approval per CM-3.

**Responsible Role:** Systems Administrator, Cloud Security Engineer
**Review Frequency:** Annual; upon any significant change

---

**CM-6 — Configuration Settings**

**Implementation Status:** Implemented

**Implementation Description:**
Security configuration settings are enforced through the following mechanisms:

- **Linux Servers:** CIS Level 2 Benchmark for RHEL 8/9 applied via Ansible automation playbooks. Compliance is verified monthly using Tenable.sc SCAP scanning. Current compliance score: 91%.
- **Windows Servers (on-premises):** CIS Level 2 Benchmark for Windows Server 2019/2022 enforced via Group Policy Objects (GPOs). Monthly compliance verification via Tenable.sc.
- **AWS Resources:** AWS Config Rules enforce MedCore's cloud security baseline (based on CIS AWS Foundations Benchmark Level 2). Current AWS Config compliance: 94%.
- **Databases:** CIS PostgreSQL Benchmark enforced and verified quarterly.
- **Network Devices:** Firewall rules reviewed and validated quarterly by the Network Engineer.

Deviations from baseline settings require documented exception approval from the ISSO and are tracked in the configuration management exception register.

**Responsible Role:** Systems Administrator, Cloud Security Engineer
**Review Frequency:** Monthly (automated scans); Annual (full review)

---

**CM-8 — System Component Inventory**

**Implementation Status:** Implemented

**Implementation Description:**
MedCore maintains a comprehensive inventory of all EHRP system components in the CMDB (ServiceNow). The inventory includes: hardware assets (servers, network devices, lab equipment), software components (OS versions, application versions, third-party libraries), cloud resources (AWS resource IDs, types, regions), and data flows.

The inventory is updated monthly by the Systems Administrator and reviewed by the ISSO. AWS Config continuously discovers and tracks cloud resource inventory; any deviation between AWS Config inventory and the CMDB is flagged for reconciliation within 5 business days.

**Responsible Role:** Systems Administrator, Cloud Security Engineer
**Review Frequency:** Monthly

---

### IDENTIFICATION AND AUTHENTICATION (IA)

---

**IA-2 — Identification and Authentication (Organizational Users)**

**Implementation Status:** Implemented with Enhancement IA-2(12)

**Implementation Description:**
All EHRP users are uniquely identified and authenticated before gaining access to any system component. Authentication is managed through Okta Identity Cloud as the primary Identity Provider, integrated with AWS IAM Identity Center for cloud resource access.

All accounts require Multi-Factor Authentication (MFA). Standard user accounts use TOTP-based authenticators (Okta Verify mobile app). Privileged and administrative accounts use FIDO2/WebAuthn hardware security keys (YubiKey 5 Series) as the primary authenticator per IA-2(12).

Shared or group accounts are prohibited with the exception of the four documented break-glass emergency accounts, which have specific procedural controls per AC-2.

**Responsible Role:** IAM Administrator
**Review Frequency:** Monthly (MFA compliance audit)

---

**IA-5 — Authenticator Management**

**Implementation Status:** Implemented

**Implementation Description:**
Authenticator management for EHRP accounts follows MedCore's Authenticator Management Procedures (MedCore-PROC-IA-001):

- **Passwords:** Minimum 14 characters; complexity requirements (uppercase, lowercase, number, special character); last 24 passwords cannot be reused; no mandatory expiration for accounts with active MFA (aligned with NIST SP 800-63B guidance).
- **Hardware Security Keys:** Registered in Okta; associated with a single named user account; inventory tracked in the IAM Administrator's asset register; replaced immediately upon reported loss or suspected compromise.
- **Service Account Credentials:** All service account secrets stored in AWS Secrets Manager with automatic 90-day rotation enabled. No hard-coded credentials in any EHRP application code (verified via GitLeaks pre-commit scanning and AWS Macie).

**Responsible Role:** IAM Administrator
**Review Frequency:** Annual (authenticator policy review)

---

### INCIDENT RESPONSE (IR)

---

**IR-4 — Incident Handling**

**Implementation Status:** Implemented

**Implementation Description:**
MedCore maintains a documented Incident Response Plan (MedCore-IRP-001, Version 4.1, reviewed January 2026) covering preparation, detection, analysis, containment, eradication, recovery, and post-incident activity.

The incident response capability includes: 24/7 SIEM monitoring by MedCore's Security Operations Center (SOC); defined escalation paths from SOC Analyst to ISSO to CISO to AO; documented playbooks for the most likely incident scenarios including ransomware, ePHI breach, unauthorized access, and DDoS.

Incident reporting timelines are: ISSO notification within 1 hour; CISO notification within 4 hours; AO notification within 24 hours of confirmed incident. For breaches of unsecured ePHI affecting 500 or more individuals, HHS OCR notification is required within 60 days of discovery per HIPAA Breach Notification Rule.

**Responsible Role:** ISSO, SOC Team
**Review Frequency:** Annual; after each significant incident

---

**IR-3 — Incident Response Testing**

**Implementation Status:** Implemented

**Implementation Description:**
MedCore conducts an annual incident response tabletop exercise involving the ISSO, CISO, CIO, Privacy Officer, and SOC leadership. The most recent tabletop exercise was conducted November 2025 and focused on a simulated ransomware scenario affecting the EHRP. After-action findings are documented and incorporated into POA&M items as applicable.

**Responsible Role:** ISSO
**Review Frequency:** Annual

---

### RISK ASSESSMENT (RA)

---

**RA-3 — Risk Assessment**

**Implementation Status:** Implemented

**Implementation Description:**
MedCore conducted a formal risk assessment of the EHRP in accordance with NIST SP 800-30 Rev 1 as part of the initial RMF process. The risk assessment identified threats, vulnerabilities, and potential adverse impacts to operations, assets, and individuals.

The risk assessment is reviewed and updated at least annually by the ISSO and whenever significant changes occur to the system, threat environment, or organizational environment. The current risk assessment was completed February 1, 2026 and is on file with the ISSO.

**Responsible Role:** ISSO, CISO
**Review Frequency:** Annual; upon significant change

---

**RA-5 — Vulnerability Monitoring and Scanning**

**Implementation Status:** Implemented

**Implementation Description:**
Vulnerability scanning for the EHRP is performed using Qualys Vulnerability Management (authenticated scans) on a weekly schedule covering all in-scope IP ranges. AWS Inspector performs continuous vulnerability assessment of EC2 instances and container images within the AWS GovCloud environment.

Findings are imported into the SIEM and cross-referenced with the POA&M. Remediation SLAs are: Critical — 15 days; High — 30 days; Moderate — 90 days; Low — 180 days. The ISSO reviews scan results monthly and reports status in the ConMon monthly report.

**Responsible Role:** Security Operations, Systems Administrator
**Review Frequency:** Weekly (automated scans); Monthly (ISSO review)

---

### SYSTEM AND COMMUNICATIONS PROTECTION (SC)

---

**SC-7 — Boundary Protection**

**Implementation Status:** Implemented

**Implementation Description:**
The EHRP authorization boundary is enforced through layered network controls:

**Cloud Boundary:**
- AWS Virtual Private Cloud (VPC) with public/private subnet architecture
- Internet-facing resources limited to the API Gateway only
- AWS WAF on API Gateway for application-layer protection
- Security Groups with deny-by-default and explicit allow rules for all inter-service communication
- VPC Flow Logs enabled and forwarded to Splunk for analysis

**On-Premises to Cloud:**
- Site-to-site VPN (IPSec/IKEv2) with AES-256 encryption
- No direct internet access from on-premises EHRP components
- All traffic to/from cloud routes through the VPN tunnel

**External Connections:**
- All external connections (HIE, EDI, e-Rx) are via encrypted, authenticated channels
- Connection agreements documented as Interconnection Security Agreements (ISAs)

**Responsible Role:** Network Engineer, Cloud Security Engineer
**Review Frequency:** Quarterly (rule review); Monthly (flow log analysis)

---

**SC-8 — Transmission Confidentiality and Integrity**

**Implementation Status:** Implemented with Enhancement SC-8(3)

**Implementation Description:**
All EHRP data transmissions are protected using TLS 1.3 (minimum TLS 1.2 for legacy integration partners with documented exception). The EHRP enforces strong cipher suites only; weak ciphers (RC4, DES, 3DES, export ciphers) are disabled.

ePHI transmitted to external parties uses end-to-end encryption with FIPS 140-2 validated cryptographic modules. Message externals (headers, addressing information) are also protected per SC-8(3) to prevent metadata-based patient identification.

TLS certificates are managed through AWS Certificate Manager (ACM) with automatic rotation. Certificate expiration monitoring is configured in CloudWatch with 30-day advance alerts.

**Responsible Role:** Cloud Security Engineer, Network Engineer
**Review Frequency:** Quarterly (TLS configuration review)

---

**SC-28 — Protection of Information at Rest**

**Implementation Status:** Implemented (with compensating control for Legacy HL7 engine — see Tailoring Decisions)

**Implementation Description:**
All EHRP data at rest is encrypted using AES-256:

- **Clinical Database (PostgreSQL RDS):** Encryption at rest enabled using AWS KMS customer-managed key (CMK)
- **Medical Imaging (S3):** Server-side encryption using AWS KMS CMK (SSE-KMS)
- **Session Cache (Redis):** ElastiCache encryption at rest enabled with AWS KMS
- **EBS Volumes:** All EC2 instance volumes encrypted with AWS KMS CMK
- **Backup Storage:** All RDS automated backups and S3 backup copies encrypted with the same KMS CMK
- **On-Premises Servers:** Full disk encryption using BitLocker with TPM 2.0

All KMS keys are customer-managed with documented key rotation policies (annual rotation) and key usage logging to CloudTrail.

**Responsible Role:** Cloud Security Engineer, Systems Administrator
**Review Frequency:** Annual (encryption key review)

---

### SYSTEM AND INFORMATION INTEGRITY (SI)

---

**SI-2 — Flaw Remediation**

**Implementation Status:** Implemented

**Implementation Description:**
MedCore maintains a formal patch management process for the EHRP (MedCore-PROC-CM-002, Version 2.3). Patches are evaluated, tested in the staging environment, and deployed to production according to the following schedule and SLAs: Critical — 15 days; High — 30 days; Moderate — 90 days; Low — 180 days.

AWS Systems Manager Patch Manager automates patching for EC2 instances in the AWS GovCloud environment during approved maintenance windows (Sundays 2:00-5:00 AM EST). On-premises server patching is managed manually by the Systems Administrator during the same maintenance window.

Emergency patches for actively exploited vulnerabilities are deployed outside the standard schedule following emergency change management approval.

**Responsible Role:** Systems Administrator, Cloud Security Engineer
**Review Frequency:** Monthly (patch compliance review)

---

**SI-4 — System Monitoring**

**Implementation Status:** Implemented with Enhancement SI-4(23)

**Implementation Description:**
MedCore operates a comprehensive system monitoring capability for the EHRP:

- **SIEM (Splunk Enterprise):** Centralized log aggregation and correlation from all EHRP components. 24/7 monitoring by SOC analysts. Use cases aligned with HIPAA security event requirements and MITRE ATT&CK framework for healthcare.
- **AWS Security Hub:** Aggregates findings from GuardDuty, Inspector, Config, and Macie into a unified security posture dashboard reviewed by the Cloud Security Engineer daily and by the ISSO weekly.
- **Amazon GuardDuty:** Continuous threat detection using ML-based analysis of CloudTrail, VPC Flow Logs, and DNS logs.
- **Host-Based EDR — CrowdStrike Falcon (SI-4(23)):** Deployed on all EHRP servers (cloud and on-premises). Provides real-time endpoint detection, behavioral analysis, and automated response capabilities.
- **Network Traffic Analysis:** VPC Flow Logs and Splunk network analytics detect anomalous traffic patterns, unauthorized connections, and data exfiltration attempts.

**Responsible Role:** SOC Team, Cloud Security Engineer, ISSO
**Review Frequency:** Continuous (automated); Weekly (ISSO review)

---

## PART III: AUTHORIZATION STATEMENT

This System Security Plan accurately describes the security controls implemented or planned for the MedCore Electronic Health Records Platform (EHRP) v4.2.1. The ISSO, CISO, and System Owner have reviewed and approved this plan, and the Authorizing Official has accepted the residual risk associated with operating this system under the controls described herein.

| Role | Name | Signature | Date |
|------|------|-----------|------|
| ISSO | Amara Osei | [Signed] | February 28, 2026 |
| CISO | Jonathan E. Steele | [Signed] | February 28, 2026 |
| System Owner / CIO | Dr. Priya Nambiar | [Signed] | February 28, 2026 |
| Privacy Officer | Dr. Rachel Feinberg | [Signed] | February 28, 2026 |
| Authorizing Official | Marcus T. Hargrove | [Signed] | March 1, 2026 |

---

*MedCore Health Systems - SENSITIVE / FOR OFFICIAL USE ONLY*
*Document: SSP-EHRP-v1.0 | February 2026*
*NOTE: This SSP documents key control implementations. The complete SSP includes all 272 controls across 20 families. Additional control family implementations are maintained in supplemental SSP volumes.*
