# Step 0 — Prepare: Roles and Responsibilities
## MedCore EHRP | NIST SP 800-37 Rev 2

**Document Type:** RMF Preparation Artifact | **Version:** 1.0 | **Date:** April 2026

---

## Purpose

Per NIST SP 800-37 Rev 2, the Prepare step requires organizations to establish a risk management hierarchy, assign key roles, and ensure all RMF participants understand their authorities before the RMF lifecycle begins.

---

## RMF Role Assignments

| Role | Name | Title |
|------|------|-------|
| Authorizing Official (AO) | Marcus T. Hargrove | CEO, MedCore Health Systems |
| AO Designated Representative (AODR) | Dr. Priya Nambiar | Chief Information Officer |
| System Owner | Jonathan E. Steele | Chief Information Security Officer |
| ISSO | Amara Osei | Director of Cybersecurity and Compliance |
| Security Control Assessor (SCA) | CyberProof Solutions | Independent Third-Party Assessor |
| Common Control Provider | Luis Castillo | Director of IT Infrastructure |
| Information Owner | Dr. Rachel Feinberg | Privacy Officer |

---

## Key Responsibilities

### Authorizing Official (AO)
- Accept organizational risk and issue the ATO, IATO, or DATO
- Review the authorization package (SSP, SAR, POA&M)
- Ensure adequate resources are allocated for security control implementation
- Review significant changes to determine if re-authorization is required

### ISSO
- Serve as the day-to-day RMF point of contact for MedCore EHRP
- Maintain the SSP to reflect current control implementations
- Conduct continuous monitoring and prepare monthly status reports
- Manage the POA&M and track finding remediation
- Coordinate with the independent SCA during assessments

### System Owner
- Develop and submit the System Security Plan (SSP)
- Coordinate control implementation with system administrators
- Report system changes that may affect the authorization boundary

### Security Control Assessor (SCA)
- Independently assess all SSP security controls per NIST SP 800-53A Rev 5
- Develop the Security Assessment Plan (SAP)
- Produce the Security Assessment Report (SAR) with findings and recommendations
- **Independence:** Organizationally separate from MedCore IT operations

### Common Control Provider
Inherited controls provided to MedCore EHRP:
- PE (Physical and Environmental Protection) — Data center physical security
- PS (Personnel Security) — Background investigations and termination procedures
- AT (Awareness and Training) — Organization-wide security awareness program
- IR (Incident Response) — Enterprise SOC and SIEM (Splunk) operations

---

## RACI Matrix

| RMF Activity | AO | AODR | System Owner | ISSO | SCA |
|-------------|:--:|:----:|:------------:|:----:|:---:|
| Establish risk management strategy | A | C | R | C | I |
| Categorize system (FIPS 199) | A | C | R | R | I |
| Select security controls | A | C | R | R | C |
| Implement security controls | I | I | A | R | I |
| Develop System Security Plan | A | C | R | R | I |
| Conduct security assessment | I | C | C | C | A |
| Develop Security Assessment Report | I | C | C | R | A |
| Issue ATO / DATO | A | R | C | C | I |
| Manage POA&M | I | I | A | R | I |
| Conduct continuous monitoring | I | C | A | R | I |

**R** = Responsible | **A** = Accountable | **C** = Consulted | **I** = Informed

---

*Document Owner: ISSO — Amara Osei | Review: Annual | Next Review: April 2027*
*MedCore Health Systems is fictional. Created for cybersecurity portfolio demonstration purposes only.*
