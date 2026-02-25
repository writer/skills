---
name: data-access-governance
description: Enforce data access policies and rules for protected health information by defining role-based access controls, monitoring access patterns, detecting unauthorized access, and ensuring minimum necessary compliance under HIPAA. Use when designing access control frameworks, investigating potential unauthorized access, conducting access audits, implementing break-the-glass procedures, managing workforce access changes, or preparing for OCR access control compliance reviews.

metadata:
  display_name: "Data Access Governance"
  short_description: "Enforce HIPAA data access policies and controls for PHI"
  default_prompt: "Check my data access governance for gaps risks and required fixes"
  version: "1.0.0"
  tags:
    - healthcare
  icon_path: "assets/icon.png"
---

# Data Access Governance

## Overview

Establish and enforce comprehensive data access governance for protected health information (PHI) across electronic systems by implementing role-based access control (RBAC), minimum necessary standards, audit logging, anomaly detection, and break-the-glass procedures. HIPAA's Security Rule (45 CFR 164.312(a)) requires access controls as a technical safeguard, and the Privacy Rule (45 CFR 164.502(b)) mandates minimum necessary use and disclosure. This skill operationalizes these requirements into a practical governance framework that balances robust PHI protection with the clinical workflow efficiency needed for patient care delivery.

## When to Use

- Designing or reviewing role-based access control frameworks for EHR and clinical systems
- Conducting periodic user access reviews and recertification
- Investigating suspected unauthorized access to patient records (snooping)
- Implementing minimum necessary standards for PHI access
- Designing break-the-glass procedures for emergency access
- Responding to OCR audit findings related to access controls
- Managing access changes for new hires, role changes, and terminations
- Evaluating access control capabilities during system selection or implementation

## Required Inputs

| Input | Description | Format |
|-------|-------------|--------|
| `system_inventory` | Systems containing PHI with access control capabilities | Structured inventory |
| `role_definitions` | Organizational roles and their PHI access requirements | Structured role matrix |
| `workforce_roster` | Current workforce members with assigned roles and system access | Structured array |
| `access_logs` | System audit logs showing user access to PHI records | Log data |
| `policies` | Access control, minimum necessary, and workforce security policies | Document references |
| `incident_data` | Prior unauthorized access incidents and investigation outcomes | Array of records |
| `regulatory_requirements` | Applicable HIPAA, state privacy law, and accreditation requirements | Reference configuration |

## Methodology

### Step 1: Access Control Framework Design

Establish the organizational access control architecture:

**Role-Based Access Control (RBAC) Model:**

| Role Category | PHI Access Scope | Access Type | Example Roles |
|--------------|-----------------|-------------|---------------|
| Direct care provider | Own patients (treatment relationship) | Read/Write clinical data | Attending physician, bedside nurse, therapist |
| Care team member | Unit/department patients | Read clinical data, limited write | Charge nurse, care coordinator, social worker |
| Clinical support | Task-specific access | Limited read per function | Lab tech, radiology tech, dietary |
| Administrative | Billing/scheduling relevant data | Read billing/demographic data | Scheduler, registration, billing staff |
| Quality/compliance | Aggregated or audited data | Read with purpose limitation | Quality analyst, compliance officer, auditor |
| IT/technical | System administration | Administrative access with audit | System admin, security analyst |
| Research | Consented/IRB-approved data | Read with protocol limitations | Research coordinator, PI |
| Executive | Aggregate/de-identified data | Dashboard/report access | C-suite, VP operations |

**Minimum Necessary Matrix:**
- For each role, define the minimum PHI data elements needed to perform the job function
- Restrict access to only the data categories required (demographics, clinical notes, labs, imaging, medications, billing)
- Implement view restrictions by patient population (own patients, department, facility, system-wide)
- Define temporal restrictions (how far back historical records are accessible)

### Step 2: Access Provisioning Procedures

Define the lifecycle of access from request through revocation:

**Access Lifecycle Management:**

| Stage | Process | Timeline | Verification |
|-------|---------|----------|-------------|
| Request | Manager submits access request with role justification | At hiring or role change | Role-based template |
| Approval | Data owner or security team reviews and approves | Within 2 business days | Approval documentation |
| Provisioning | IT grants access per approved role template | Within 1 business day of approval | Access confirmation |
| Activation | User acknowledges acceptable use policy and completes training | Before first access | Signed acknowledgment |
| Modification | Role change triggers access review and adjustment | Within 2 business days of role change | Re-certification |
| Suspension | Leave of absence or investigation triggers temporary suspension | Same day as trigger event | Suspension documentation |
| Termination | Employment end triggers immediate access revocation | Within 4 hours of separation (same day) | Revocation confirmation |

**Access Request Approval Authority:**
- Standard access (within role template): Direct supervisor approval
- Elevated access (beyond role template): Department director + Security Officer approval
- Emergency access (break-the-glass): Automatic with retroactive review within 24 hours
- Research access: IRB approval + Privacy Officer review

### Step 3: Minimum Necessary Implementation

Operationalize HIPAA's minimum necessary standard (45 CFR 164.502(b)):

**Minimum Necessary Categories:**
- **Treatment**: Minimum necessary does not apply to disclosures for treatment purposes between providers (45 CFR 164.502(b)(2)(i)) — but organizations may still implement reasonable restrictions
- **Payment**: Limit to data elements needed for the specific payment activity
- **Healthcare operations**: Limit to data needed for the specific operational purpose
- **Workforce access**: Implement role-based restrictions that provide only the data needed for the job function
- **Routine disclosures**: Define standard protocols for recurring disclosure types (e.g., subpoena response, public health reporting)
- **Non-routine disclosures**: Individual review for each non-routine disclosure request

**Implementation Approaches:**
- EHR role templates restricting chart sections by role (e.g., nurses cannot view psychotherapy notes)
- Data element filtering in reports and extracts (include only requested/needed fields)
- Patient population restrictions (providers access only their assigned patients or department)
- Time-based restrictions (access limited to patients with encounters within a defined period)
- Purpose-based access (user must specify reason for accessing record outside their assigned patients)

### Step 4: Audit Logging and Monitoring

Implement comprehensive access monitoring:

**Required Audit Log Elements (45 CFR 164.312(b)):**
- User ID and role at time of access
- Date and time of access
- Patient record accessed (patient identifier)
- Action performed (view, create, modify, print, export, delete)
- System or application accessed
- Access location (workstation ID, IP address, remote/on-site)

**Proactive Monitoring Program:**

| Monitoring Type | Frequency | Trigger Criteria | Response |
|----------------|-----------|-----------------|----------|
| Routine audit log review | Monthly | Random sample of access records | Verify access appropriateness |
| High-profile patient monitoring | Real-time | Access to VIP, employee, or flagged patient records | Immediate alert and review |
| Volume anomaly detection | Daily | User accessing significantly more records than peer average | Investigation trigger |
| After-hours access review | Weekly | Access outside assigned work hours | Verification of clinical justification |
| Relationship verification | Continuous | Access to records without treatment relationship | Alert and justification request |
| Break-the-glass review | Within 24 hours | Every emergency access override | Mandatory justification review |
| Terminated user monitoring | Real-time | Any access attempt by terminated user | Immediate security alert |

### Step 5: Unauthorized Access Detection and Investigation

Detect and investigate potential unauthorized access (snooping):

**Detection Indicators:**
- Accessing records of family members, neighbors, celebrities, or co-workers without treatment relationship
- Accessing own medical record through clinical system (rather than patient portal)
- Accessing records after treatment relationship has ended without legitimate purpose
- Accessing records from unusual locations or at unusual times
- Accessing records flagged for heightened monitoring (VIP, employee health)
- Pattern of accessing records matching news events (accident victims, crime victims)

**Investigation Process:**
1. Preserve audit log evidence
2. Identify the accessed records and the accessor
3. Determine if a treatment relationship or legitimate business purpose existed
4. Interview the accessor to understand the reason for access
5. Review organizational policy and HIPAA requirements
6. Determine if a privacy violation occurred
7. If violation confirmed: apply sanctions per sanction policy, determine if breach notification is required
8. Document the investigation and outcome

**Sanction Policy Application:**
- First offense, no harm: Verbal warning and re-education
- Repeat offense or minor harm: Written warning and remedial training
- Intentional or significant: Suspension, termination, and potential referral to OCR
- All violations: Documented in employee file per organizational sanction policy (required by 45 CFR 164.308(a)(1)(ii)(C))

### Step 6: Break-the-Glass Procedures

Design emergency access override protocols:

**When Break-the-Glass Applies:**
- Medical emergency requiring immediate access to patient information not normally accessible to the user
- System failure preventing normal access for active patient care
- Disaster or mass casualty event requiring expanded access

**Break-the-Glass Requirements:**
- User must acknowledge emergency access is being activated
- System logs the break-the-glass event with enhanced detail
- User must provide justification within 24 hours
- Privacy/Security Officer reviews every break-the-glass event
- Inappropriate use of break-the-glass is subject to sanctions
- Break-the-glass rates are monitored (high rates may indicate role template inadequacy)

### Step 7: Periodic Access Review and Recertification

Conduct regular reviews of access appropriateness:

**Review Schedule:**

| Review Type | Frequency | Scope | Reviewer |
|------------|-----------|-------|----------|
| New user access | 30 days after provisioning | Individual access vs. role template | Direct supervisor |
| Department access review | Quarterly | All users in department vs. role templates | Department director |
| Privileged access | Monthly | Admin, IT, and elevated access users | Security Officer |
| Comprehensive recertification | Semi-annual | All users across all systems | Department director + Security |
| Terminated user audit | Monthly | Verify all terminated users have been revoked | HR + IT Security |
| Vendor/BA access review | Quarterly | All external access accounts | Security Officer + Vendor Manager |

**Recertification Process:**
- Generate access report showing each user's current access rights
- Manager certifies that each user's access is appropriate for current role
- Identify and remove excess access (access creep from prior roles)
- Document recertification completion with manager attestation
- Escalate unresolved excess access to Security Officer

## Output Specification

```yaml
data_access_governance_report:
  assessment_date: string
  systems_in_scope: number
  total_users: number
  rbac_framework:
    roles_defined: number
    users_per_role: object
    minimum_necessary_implemented: boolean
  access_provisioning:
    avg_provisioning_time: string
    avg_termination_revocation_time: string
    orphaned_accounts_found: number
  monitoring_summary:
    audit_log_coverage: number  # percentage of systems
    anomalies_detected: number
    investigations_conducted: number
    violations_confirmed: number
    break_the_glass_events: number
    break_the_glass_justified: number
  recertification:
    last_completed: string
    completion_rate: number
    excess_access_removed: number
  findings:
    - finding: string
      hipaa_reference: string
      risk_level: string
      remediation: string
  compliance_score: number
```

## Analysis Framework

### Access Control Maturity Model

| Level | Description | Characteristics |
|-------|-------------|-----------------|
| Level 1 — Ad Hoc | Access granted without structured framework | No role definitions, broad access, no monitoring |
| Level 2 — Defined | RBAC framework exists with basic provisioning | Role templates, manual reviews, limited monitoring |
| Level 3 — Managed | Active monitoring and periodic recertification | Audit log review, anomaly alerts, quarterly recertification |
| Level 4 — Optimized | Automated governance with continuous monitoring | Real-time anomaly detection, automated provisioning/deprovisioning, break-the-glass analytics |

## Examples

**Example: Hospital EHR Access Governance Audit**

- Scope: 2,500 EHR users across 450-bed hospital
- RBAC assessment: 28 role templates defined; 92% of users aligned to templates; 8% (200 users) have customized access requiring review
- Minimum necessary: Clinical notes restricted by role; billing staff cannot view psychotherapy notes — compliant
- Provisioning: Average provisioning time 1.2 days (compliant); average termination revocation 6.8 hours (within 4-hour target for 85% of terminations)
- Critical finding: 12 orphaned accounts from employees terminated 30+ days ago still active — immediate revocation required
- Monitoring: 1,847 anomaly alerts in past quarter; 23 investigations initiated; 3 confirmed unauthorized access (2 employee record access, 1 celebrity patient)
- Break-the-glass: 45 events in quarter; 42 justified; 3 inappropriate (sanctions applied)
- Recommendation: Implement automated account deactivation triggered by HR termination record; reduce orphaned account gap to zero

## Guidelines

1. **Access is a privilege, not a right** — all PHI access must be justified by job function
2. **Implement least privilege** — default to minimum access; add only when justified
3. **Automate provisioning and deprovisioning** — manual processes are error-prone and slow
4. **Monitor continuously** — periodic audits alone are insufficient; implement real-time anomaly detection
5. **Apply sanctions consistently** — inconsistent enforcement undermines the entire governance program
6. **Review break-the-glass events promptly** — within 24 hours of every occurrence
7. **Address access creep** — users who change roles accumulate excess access unless actively managed

## Validation Checklist

- [ ] RBAC framework defined with role templates covering all workforce categories
- [ ] Minimum necessary standard implemented with data element and population restrictions
- [ ] Access provisioning lifecycle documented from request through termination
- [ ] Audit logging enabled across all PHI-containing systems with required data elements
- [ ] Proactive monitoring program implemented with defined triggers and response procedures
- [ ] Unauthorized access investigation process documented with sanction policy
- [ ] Break-the-glass procedures designed with mandatory retroactive review
- [ ] Periodic access recertification schedule established and documented
- [ ] Orphaned account detection and remediation process in place
- [ ] Compliance with 45 CFR 164.312(a) access controls and 164.312(b) audit controls verified

## HIPAA Compliance Notes

- Access controls are a required technical safeguard under the HIPAA Security Rule (45 CFR 164.312(a)(1))
- Unique user identification is required (45 CFR 164.312(a)(2)(i)) — shared accounts violate this standard
- Emergency access procedures must be established (45 CFR 164.312(a)(2)(ii))
- Automatic logoff must be implemented (45 CFR 164.312(a)(2)(iii))
- Audit controls must be implemented to record and examine PHI access (45 CFR 164.312(b))
- Minimum necessary standard applies to all uses and disclosures except treatment (45 CFR 164.502(b))
- Sanction policy is a required administrative safeguard (45 CFR 164.308(a)(1)(ii)(C))
- Workforce security procedures are required (45 CFR 164.308(a)(3))
- Access authorization policies are required (45 CFR 164.308(a)(4))
- Documentation must be retained for 6 years (45 CFR 164.316(b)(2)(i))
