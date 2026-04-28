# NIST Risk Management Framework (RMF) Implementation
## Applied to MedCore Electronic Health Records Platform (EHRP)

**Framework:** NIST SP 800-37 Rev 2 — Risk Management Framework for Information Systems and Organizations
**System:** MedCore EHRP | MedCore Health Systems (Fictional)
**Security Categorization:** HIGH (FIPS 199)
**Control Baseline:** NIST SP 800-53 Rev 5 — Moderate Baseline (tailored to HIGH)
**Status:** In Progress

> **Disclaimer:** All content in this repository is fictional and created for cybersecurity portfolio demonstration purposes. MedCore Health Systems, its personnel, systems, and data do not exist. No real organizational, patient, or government information is used.
>
> ---
>
> ## What Is the NIST RMF?
>
> The NIST Risk Management Framework (RMF) is a structured, flexible process that integrates security and privacy risk management activities into the system development life cycle. It provides a disciplined, structured, and flexible process for managing security and privacy risk. The RMF is mandatory for all U.S. federal information systems and is widely adopted in healthcare, defense, and enterprise environments.
>
> The RMF consists of seven steps (Step 0 through Step 6), each producing specific artifacts that collectively form the authorization package required to obtain an Authorization to Operate (ATO).
>
> ---
>
> ## RMF Steps — Document Index
>
> | Step | Name | Key Activity | Primary Artifact | Status |
> |------|------|-------------|-----------------|--------|
> | [Step 0](./step-0-prepare/) | Prepare | Establish organizational context and roles | Risk Management Strategy | Complete |
> | [Step 1](./step-1-categorize/) | Categorize | Classify system impact using FIPS 199 | FIPS 199 Worksheet | Complete |
> | [Step 2](./step-2-select/) | Select | Choose and tailor NIST SP 800-53 control baseline | Control Selection Table | Complete |
> | [Step 3](./step-3-implement/) | Implement | Document security control implementations | System Security Plan (SSP) | Complete |
> | [Step 4](./step-4-assess/) | Assess | Test and evaluate control effectiveness | Security Assessment Report (SAR) | Complete |
> | [Step 5](./step-5-authorize/) | Authorize | Authorizing Official reviews risk and issues decision | Authorization to Operate (ATO) Memo | Complete |
> | [Step 6](./step-6-monitor/) | Monitor | Continuously monitor controls and report status | ConMon Strategy & POA&M | Complete |
>
> ---
>
> ## Repository Structure
>
> ```
> nist-rmf-implementation/
> ├── README.md                              ← This document — RMF overview and index
> │
> ├── step-0-prepare/
> │   ├── README.md                          ← Step 0 overview and objectives
> │   ├── roles-and-responsibilities.md      ← RMF team: AO, ISSO, SCA, System Owner
> │   ├── risk-management-strategy.md        ← Organizational risk tolerance and approach
> │   └── common-control-identification.md   ← Inherited vs. system-specific controls
> │
> ├── step-1-categorize/
> │   ├── README.md                          ← Step 1 overview and objectives
> │   ├── fips-199-worksheet.md              ← Security categorization (C/I/A impact levels)
> │   ├── nist-800-60-information-types.md   ← Information type mapping and impact values
> │   └── categorization-decision-memo.md    ← Official categorization determination memo
> │
> ├── step-2-select/
> │   ├── README.md                          ← Step 2 overview and objectives
> │   ├── baseline-selection-rationale.md    ← Why Moderate baseline was selected
> │   ├── tailoring-decisions.md             ← Control additions, removals, compensating controls
> │   └── control-allocation-table.md        ← System-specific vs. common vs. hybrid controls
> │
> ├── step-3-implement/
> │   ├── README.md                          ← Step 3 overview and objectives
> │   ├── system-security-plan.md            ← Full SSP — all 20 control families implemented
> │   └── implementation-evidence-guide.md   ← Guide for collecting control evidence
> │
> ├── step-4-assess/
> │   ├── README.md                          ← Step 4 overview and objectives
> │   ├── security-assessment-plan.md        ← SAP — methodology, scope, schedule
> │   ├── security-assessment-report.md      ← SAR — findings, risk ratings, recommendations
> │   └── assessment-findings-tracker.md     ← Individual control findings with risk levels
> │
> ├── step-5-authorize/
> │   ├── README.md                          ← Step 5 overview and objectives
> │   ├── authorization-package-summary.md   ← Executive summary for AO review
> │   ├── risk-acceptance-statement.md       ← AO residual risk acceptance decision
> │   └── authorization-to-operate-memo.md   ← Official ATO decision letter
> │
> └── step-6-monitor/
>     ├── README.md                          ← Step 6 overview and objectives
>     ├── continuous-monitoring-strategy.md  ← ConMon program overview and schedule
>     ├── poam-tracker.md                    ← Plan of Action and Milestones
>     ├── monthly-reporting-template.md      ← Monthly status report format
>     └── annual-assessment-schedule.md      ← Ongoing assessment and review calendar
> ```
>
> ---
>
> ## The RMF Lifecycle Applied to MedCore EHRP
>
> ```
> PREPARE (Step 0)
>     Establish roles, governance, and organizational risk context
>          |
>          v
> CATEGORIZE (Step 1)
>     FIPS 199: Confidentiality=HIGH, Integrity=HIGH, Availability=HIGH
>     Overall Categorization: HIGH
>          |
>          v
> SELECT (Step 2)
>     NIST SP 800-53 Rev 5 Moderate Baseline
>     Tailored upward to HIGH for PHI/clinical systems
>     265 controls selected across 20 families
>          |
>          v
> IMPLEMENT (Step 3)
>     System Security Plan (SSP) — all 265 controls documented
>     Control implementation statements for each applicable control
>          |
>          v
> ASSESS (Step 4)
>     Independent Security Control Assessment
>     Security Assessment Plan (SAP) → Security Assessment Report (SAR)
>     Findings categorized: High / Moderate / Low / Informational
>          |
>          v
> AUTHORIZE (Step 5)
>     Authorization Package submitted to Authorizing Official (AO)
>     Residual risk accepted → Authorization to Operate (ATO) issued
>          |
>          v
> MONITOR (Step 6)
>     Continuous monitoring program active
>     Monthly reporting, POA&M management, annual assessments
>     Ongoing ConMon → feeds back into Categorize/Select as needed
> ```
>
> ---
>
> ## Key Reference Documents
>
> | Document | Authority | Purpose |
> |----------|-----------|---------|
> | NIST SP 800-37 Rev 2 | NIST | RMF process guidance |
> | NIST SP 800-53 Rev 5 | NIST | Security control catalog |
> | NIST SP 800-53A Rev 5 | NIST | Control assessment procedures |
> | NIST SP 800-60 Vol I & II | NIST | Information type categorization |
> | FIPS 199 | NIST/OMB | Security categorization standards |
> | FIPS 200 | NIST/OMB | Minimum security requirements |
> | NIST SP 800-18 Rev 1 | NIST | SSP guidance |
| NIST SP 800-30 Rev 1 | NIST | Risk assessment guidance |
> | NIST SP 800-137 | NIST | Information security continuous monitoring |
>
> ---
>
> ## Related Repositories
>
> | Repository | Relationship |
> |-----------|-------------|
> | [medcore-health-systems](https://github.com/kcrozz55/medcore-health-systems) | Baseline system this RMF applies to |
> | [ato-security-package](https://github.com/kcrozz55/ato-security-package) | Full ATO package incorporating all RMF outputs |
> | [cybersecurity-portfolio](https://github.com/kcrozz55/cybersecurity-portfolio) | Master portfolio index |
> | [vulnerability-management-program](https://github.com/kcrozz55/vulnerability-management-program) | Feeds vulnerability findings into Step 4 SAR and Step 6 POA&M |
> | [security-policies-procedures](https://github.com/kcrozz55/security-policies-procedures) | Policies referenced in Step 3 SSP implementations |
>
> ---
>
> *All content is fictional and created for cybersecurity portfolio demonstration purposes only.*
