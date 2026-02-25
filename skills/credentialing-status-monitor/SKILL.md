---
name: Credentialing Status Monitor
description: Track and manage provider credentialing and privileging lifecycles using CAQH workflow standards, NCQA credentialing requirements, and CMS enrollment timelines to prevent coverage gaps, billing disruptions, and compliance violations.

metadata:
  display_name: "Credentialing Status Monitor"
  short_description: "Track provider credentialing and privileging status"
  default_prompt: "Review my credentialing status and highlight top risks and next actions"
  version: "1.0.0"
  tags:
    - healthcare
  icon_path: "assets/icon.png"
---

# Credentialing Status Monitor

## Overview

This skill monitors the complete provider credentialing and privileging lifecycle across health plans, facilities, and regulatory bodies to prevent lapses that result in billing disruptions, coverage gaps, compliance violations, and patient safety risks. It tracks primary source verification timelines, CAQH ProView profile status, payer enrollment deadlines, facility privileging cycles, and state licensure renewals. The average credentialing process takes 90-150 days, and errors or delays can cost health systems 10K-50K per provider per month in lost revenue. NCQA credentialing standards (CR Standards) require initial credentialing within 180 days and re-credentialing every 36 months.

## When to Use

- Monitoring credentialing pipeline for new provider onboarding
- Tracking re-credentialing deadlines across multiple facilities and plans
- Identifying providers at risk of credentialing lapses or expired privileges
- Auditing credentialing files for NCQA, Joint Commission, or CMS survey readiness
- Managing CAQH ProView profile completeness and attestation currency
- Coordinating multi-state licensure for telehealth providers
- Investigating billing denials related to credentialing or enrollment status

## Required Inputs

| Input | Description | Format |
|-------|-------------|--------|
| `provider_roster` | All providers requiring credentialing with demographics and start dates | JSON array |
| `caqh_data` | CAQH ProView profile status, attestation dates, data completeness | JSON object |
| `payer_enrollment` | Enrollment status by payer with effective dates and re-enrollment schedules | JSON array |
| `facility_privileges` | Hospital and facility privileging status with expiration dates | JSON array |
| `licensure_data` | State medical licenses, DEA registrations, board certifications with expiration dates | JSON array |
| `verification_status` | Primary source verification completion status for each credential element | JSON object |
| `credentialing_timeline` | Target dates for onboarding milestones | JSON object |

## Methodology

### Step 1: Credential Element Inventory
- Track all required credential elements per provider per NCQA CR standards:
  - **Licensure**: State medical license (all practice states), current and unrestricted
  - **DEA Registration**: Current DEA certificate for prescribing providers
  - **Board Certification**: Specialty board certification or eligibility documentation
  - **Education and Training**: Medical school, residency, fellowship verification
  - **Work History**: Minimum 5-year work history with gap explanations
  - **Malpractice Insurance**: Current coverage meeting minimum requirements (typically 1M/3M)
  - **Malpractice History**: NPDB query for claims history (initial and every 36 months)
  - **Sanctions**: OIG/GSA exclusion list check, state sanctions, Medicare/Medicaid sanctions
  - **Hospital Privileges**: Current privileges at affiliated hospitals
  - **CDS Certificate**: State-level controlled substance registration where required
  - **ECFMG Certification**: For international medical graduates
- Flag missing or expiring elements with days-to-expiration countdown

### Step 2: CAQH ProView Management
- Monitor CAQH ProView profile status:
  - Profile completeness percentage (target: 100%)
  - Attestation currency (must re-attest every 120 days per CAQH requirement)
  - Data accuracy validation against organizational records
  - Authorization status for plan-specific data access
- Flag issues:
  - Attestation expiring within 30 days
  - Incomplete profile sections blocking payer enrollment
  - Discrepancies between CAQH data and organizational records
  - Missing practice locations or plan affiliations
- Generate CAQH re-attestation reminders and track completion

### Step 3: Payer Enrollment Tracking
- Track enrollment status across all contracted payers:
  - Application submission date and status (submitted, in process, approved, denied)
  - Effective date of enrollment (critical for billing commencement)
  - Provider number or NPI linkage per payer
  - Re-enrollment and re-credentialing cycle dates (typically every 36 months)
  - Retroactive billing eligibility and limitations
- Calculate revenue at risk for delayed enrollment:
  - Services rendered before enrollment effective date may be non-billable
  - Estimate daily revenue impact per provider per payer
- Track Medicare and Medicaid enrollment separately (CMS-855 forms, PECOS status)

### Step 4: Facility Privileging Monitoring
- Track hospital and facility privileging lifecycle:
  - Initial privileging application status and timeline
  - Privilege categories granted (core, specific procedures, temporary)
  - Focused Professional Practice Evaluation (FPPE) status for new privileges
  - Ongoing Professional Practice Evaluation (OPPE) completion status
  - Re-privileging cycle (typically every 24 months per Joint Commission MS.06.01.03)
  - Temporary privileges status and expiration (120 days max per Joint Commission)
- Flag privilege-related risks:
  - Privileges expiring within 90 days without re-application initiated
  - FPPE milestones approaching without completion documentation
  - OPPE data collection gaps for required metrics
  - Adverse privilege actions requiring reporting

### Step 5: Risk Dashboard and Alerting
- Calculate credentialing risk score per provider:
  - **Low risk**: All elements current, next expiration more than 90 days away
  - **Moderate risk**: Element expiring within 60-90 days, renewal in progress
  - **High risk**: Element expiring within 30-60 days, renewal not yet initiated
  - **Critical risk**: Element expired or expiring within 30 days
- Generate automated alerts:
  - 120 days before license expiration: initiate renewal
  - 90 days before re-credentialing due: begin re-credentialing process
  - 30 days before CAQH attestation expiration: re-attestation reminder
  - Immediate: any expired credential element, OIG exclusion hit, adverse action
- Dashboard showing at-a-glance status for all providers

### Step 6: Compliance Audit Readiness
- Prepare credentialing files for audit:
  - Verify all NCQA CR standard elements documented with primary source verification
  - Ensure credentialing committee minutes document all decisions
  - Validate that initial credentialing completed within 180 calendar days of application
  - Confirm re-credentialing completed within 36 months of previous cycle
  - Verify peer review and clinical competence assessments current
  - Document clean claims file for each provider
- Generate audit readiness score per provider and per organization
- Identify files requiring remediation before scheduled audits

## Output Specification

```yaml
credentialing_status:
  total_providers: number
  risk_distribution:
    low: number
    moderate: number
    high: number
    critical: number
  provider_details:
    - provider_id: string
      name: string
      specialty: string
      overall_risk: string
      credential_elements:
        - element: string
          status: string
          expiration_date: date
          days_to_expiration: number
          psv_completed: boolean
          action_needed: string
      caqh_status:
        completeness_pct: number
        attestation_date: date
        days_to_re_attestation: number
      payer_enrollment:
        - payer: string
          status: string
          effective_date: date
          recredential_due: date
      facility_privileges:
        - facility: string
          status: string
          expiration_date: date
          fppe_status: string
          oppe_status: string
  alerts:
    - provider_id: string
      alert_type: string
      severity: string
      element: string
      action_required: string
      deadline: date
  revenue_at_risk:
    delayed_enrollment: number
    lapsed_credentials: number
  audit_readiness:
    overall_score: number
    files_requiring_remediation: number
    ncqa_compliance_pct: number
```

## Analysis Framework

Apply the **NCQA Credentialing and Re-credentialing Standards** (CR Standards):

| Standard | Requirement | Monitoring Approach |
|----------|------------|-------------------|
| CR 1 | Credentialing policies and procedures | Policy review and update tracking |
| CR 2 | Credentialing committee oversight | Committee meeting and decision documentation |
| CR 3 | Initial credentialing process | Application-to-decision timeline monitoring |
| CR 4 | Re-credentialing process | 36-month cycle compliance tracking |
| CR 5 | Ongoing monitoring between cycles | Monthly OIG/SAM checks, sanction monitoring |
| CR 6 | Delegation oversight | Delegated credentialing audit and reporting |

## Examples

**Example: 400-Provider Medical Group Credentialing Dashboard**
- Total providers: 400 (320 physicians, 80 APPs)
- Risk distribution: Low 72%, Moderate 18%, High 7%, Critical 3%
- Critical alerts: 12 providers with licenses expiring within 30 days, 3 with expired CAQH attestations
- Revenue at risk: 340K/month from 8 providers with delayed payer enrollments
- CAQH compliance: 89% profiles complete (target: 100%), 23 providers need re-attestation
- Payer enrollment gaps: 15 providers pending Medicare enrollment (average delay: 47 days)
- Audit readiness score: 84% (target: 95%), 64 files need documentation remediation
- OPPE gaps: 28 providers missing current OPPE data for upcoming re-privileging

## Guidelines

- **HIPAA Compliance**: Provider credentialing data includes sensitive personal information (SSN, DOB, malpractice history) that must be protected per organizational data security policies. While not PHI, this data requires equivalent safeguards. Restrict access to credentialing staff and authorized leadership.
- **NPDB Reporting**: Adverse privilege actions must be reported to the National Practitioner Data Bank within 30 days per HCQIA. Ensure monitoring captures reportable events.
- **State Variation**: Licensure requirements, supervised practice rules, and credentialing timelines vary by state. Multi-state organizations must track state-specific requirements, especially for telehealth across state lines.
- **Delegation Oversight**: If credentialing is delegated to another entity, NCQA requires annual audits and pre-approval of credentialing decisions. Track delegation agreements and audit schedules.
- **Timeliness Standards**: CMS requires Medicare enrollment applications to be processed within specific timelines. Track CMS processing separately from commercial payer enrollment.

## Validation Checklist

- [ ] All credential elements inventoried for each provider
- [ ] Expiration dates tracked with automated countdown alerts
- [ ] CAQH ProView profiles monitored for completeness and attestation currency
- [ ] Payer enrollment tracked across all contracted plans
- [ ] Facility privileges monitored with FPPE and OPPE status
- [ ] OIG/SAM exclusion checks performed monthly
- [ ] Risk scoring applied with clear severity criteria
- [ ] Revenue at risk calculated for enrollment delays
- [ ] Audit readiness assessed against NCQA CR standards
- [ ] State-specific requirements documented and tracked
- [ ] Provider data security safeguards implemented
- [ ] Credentialing committee documentation current
