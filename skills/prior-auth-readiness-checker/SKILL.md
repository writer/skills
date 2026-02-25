---
name: prior-auth-readiness-checker
description: Validate prior authorization request completeness against payer-specific requirements including clinical documentation, medical necessity criteria, and submission standards. Use when preparing prior auth submissions, checking PA readiness before submission, identifying missing documentation, or streamlining the authorization workflow.

metadata:
  display_name: "Prior Auth Readiness Checker"
  short_description: "Check prior authorization submission readiness and gaps"
  default_prompt: "Check my prior auth for gaps risks and required fixes"
  version: "1.0.0"
  tags:
    - healthcare
  icon_path: "assets/icon.png"
---

# Prior Authorization Readiness Checker

## Overview

Evaluate prior authorization (PA) requests for completeness and compliance with payer-specific requirements before submission. This skill validates that all required clinical documentation, medical necessity criteria, demographic information, and supporting evidence are present — reducing PA denials, rework, and delays in patient care by ensuring first-pass approval readiness.

## When to Use

- Preparing a prior authorization request for submission
- Checking if all payer-required elements are present before sending
- Identifying missing documentation that could cause PA denial
- Validating medical necessity justification against payer criteria
- Training staff on PA submission requirements
- Auditing PA workflows for process improvement

## Required Inputs

| Input | Description | Format |
|-------|-------------|--------|
| Requested service | CPT/HCPCS code, service description, quantity | Structured object |
| Patient information | Demographics, insurance, member ID, group number | Structured object |
| Provider information | NPI, taxonomy, rendering and ordering provider | Structured object |
| Clinical documentation | Relevant notes, test results, prior treatment history | Document references |
| Payer and plan | Payer name, plan type, PA requirements | Structured object |
| Diagnosis codes | ICD-10 codes justifying medical necessity | Array |

## Methodology

### Step 1: PA Requirement Verification

Determine if prior authorization is required for this service/payer combination:

**PA Requirement Factors:**
- Service type (surgical procedures, advanced imaging, DME, specialty drugs, genetic testing)
- Place of service (outpatient, inpatient, ASC, office)
- Payer and plan type (commercial, Medicare Advantage, Medicaid managed care)
- Network status (in-network vs. out-of-network may have different PA requirements)
- Dollar threshold (some plans require PA above certain cost thresholds)

**Common Services Requiring PA:**
- Advanced imaging (MRI, CT, PET)
- Elective surgeries and procedures
- Specialty pharmaceuticals (biologics, chemotherapy, gene therapy)
- Durable medical equipment (DME) over cost threshold
- Inpatient admissions (planned)
- Out-of-network referrals
- Behavioral health services (some plans)
- Home health and post-acute services

### Step 2: Documentation Completeness Check

Validate that all required elements are present:

**Administrative Elements:**
- [ ] Patient demographics (name, DOB, member ID, group number)
- [ ] Subscriber information (if different from patient)
- [ ] Ordering/requesting provider (name, NPI, taxonomy code, contact)
- [ ] Rendering/servicing provider (name, NPI, address)
- [ ] Facility information (name, NPI, place of service code)
- [ ] Requested service (CPT/HCPCS, units, start date, duration)
- [ ] Primary and secondary diagnosis codes (ICD-10-CM)

**Clinical Documentation:**
- [ ] History and physical or relevant clinical note
- [ ] Diagnosis-specific clinical findings supporting medical necessity
- [ ] Prior treatments attempted and their outcomes (step therapy)
- [ ] Relevant lab results, imaging reports, or pathology
- [ ] Specialist consultation notes (if applicable)
- [ ] Functional status assessment (for DME, rehab, home health)
- [ ] Medication history (for pharmacy PAs — prior trials and failures)

### Step 3: Medical Necessity Validation

Assess whether the clinical documentation supports medical necessity:

**Medical Necessity Criteria (General Framework):**
1. Service is appropriate for the diagnosis (ICD-10 supports CPT)
2. Service is not elective or cosmetic (unless documented medical indication)
3. Conservative or first-line treatments have been tried or are contraindicated
4. Service is expected to improve, maintain, or prevent decline in patient condition
5. Service is provided at the appropriate level and setting
6. Service frequency and duration are within accepted guidelines

**Payer-Specific Criteria Sources:**
- InterQual criteria (inpatient, procedures, imaging)
- Milliman Care Guidelines (level of care, length of stay)
- CMS National Coverage Determinations (NCDs) for Medicare
- Local Coverage Determinations (LCDs) for Medicare
- Payer-specific clinical policies and medical policies
- Drug-specific utilization management criteria (for pharmacy PAs)

### Step 4: Step Therapy and Prior Treatment Verification

Validate that required prior treatments have been documented:

**Step Therapy Requirements:**
- First-line treatment attempted and duration documented
- Clinical response or failure documented with specifics
- Adverse reactions documented with severity
- Contraindications to first-line therapy documented with clinical rationale
- Progressive treatment ladder followed per payer policy

### Step 5: Readiness Scoring and Gap Report

Generate a readiness assessment:

**Readiness Score Calculation:**
- Administrative completeness: 0-100 (weighted 25%)
- Clinical documentation adequacy: 0-100 (weighted 40%)
- Medical necessity justification strength: 0-100 (weighted 25%)
- Step therapy/prior treatment documentation: 0-100 (weighted 10%)
- Composite readiness score: weighted average

**Readiness Tiers:**

| Tier | Score | Recommendation |
|------|-------|---------------|
| Ready to submit | 90-100 | Submit PA request |
| Near-ready | 75-89 | Address minor gaps, then submit |
| Significant gaps | 50-74 | Obtain missing documentation before submission |
| Not ready | Below 50 | Major documentation deficiencies, do not submit |

## Output Specification

The output includes:

**pa_requirement_status**: pa_required (yes/no), basis (payer policy, service type), exceptions

**administrative_checklist**: each required administrative element with status (present/missing/incomplete), and corrective action if missing

**clinical_documentation_checklist**: each required clinical element with status, source document reference, and gap description if missing

**medical_necessity_assessment**: criteria_met count, criteria_total, strength (strong/moderate/weak/insufficient), supporting_evidence, gaps in justification

**step_therapy_verification**: required (yes/no), steps_documented, steps_required, gap_detail

**readiness_score**: composite score, component scores, readiness tier, submission recommendation

**gap_report**: prioritized list of gaps with required_element, gap_description, required_action, responsible_party, urgency

**submission_guidance**: recommended submission method (portal/fax/phone), expected turnaround, escalation timeline

## Analysis Framework

### PA Denial Prevention

Most common reasons for PA denials and how to prevent them:

| Denial Reason | Prevention | Readiness Check |
|--------------|------------|-----------------|
| Insufficient clinical information | Ensure H&P and supporting docs attached | Clinical documentation checklist |
| Medical necessity not established | Document failed prior treatments, clinical rationale | Medical necessity assessment |
| Missing demographic/insurance info | Verify eligibility and demographics pre-submission | Administrative checklist |
| Wrong procedure or diagnosis code | Validate CPT-ICD linkage before submission | Code validation |
| Step therapy not followed | Document prior treatments with outcomes | Step therapy verification |
| Expired or wrong auth | Verify auth validity period and service match | Administrative checklist |

### Turnaround Time Expectations

| Request Type | Standard | Urgent/Expedited |
|-------------|----------|-----------------|
| Commercial payer | 5-15 business days | 24-72 hours |
| Medicare Advantage | 14 calendar days (standard), 7 days (expedited) | 72 hours |
| Medicaid managed care | Varies by state, typically 14 days | 24-72 hours |
| Pharmacy PA | 5-10 business days | 24-48 hours |

## Examples

**Input**: PA request for lumbar MRI (CPT 72148) for 55-year-old with low back pain (M54.5). Payer: Aetna commercial. No prior imaging on file. Physical therapy notes mention 4 weeks of PT with minimal improvement.

**Readiness Assessment**:
- Administrative: 95% — all elements present except rendering provider taxonomy code
- Clinical documentation: 70% — PT notes document conservative treatment, but need office visit note documenting neurological findings; no documentation of duration/onset of symptoms
- Medical necessity: 65% — Conservative treatment (PT) documented, but payer requires 6 weeks before advanced imaging (only 4 documented). Need documentation of red flag symptoms or neurological deficits to justify earlier imaging
- Step therapy: 60% — PT documented but duration insufficient per payer policy
- Composite readiness: 72% — SIGNIFICANT GAPS
- Recommendation: Do not submit yet. Obtain provider office note with neurological exam findings. If neurological deficits present, document as justification for earlier imaging. Otherwise, continue PT for 2 additional weeks before resubmitting.

## Guidelines

1. **Always verify PA requirements** — requirements change frequently; do not assume
2. **Check payer-specific criteria** — generic medical necessity is not sufficient; match to payer policies
3. **Document step therapy thoroughly** — include dates, durations, and specific outcomes of prior treatments
4. **Submit complete packages** — incomplete submissions are the number one cause of PA delays and denials
5. **Track PA status proactively** — do not wait for denial; follow up within expected turnaround windows

## Validation Checklist

- [ ] PA requirement is confirmed for this service/payer combination
- [ ] All administrative elements are present and accurate
- [ ] Clinical documentation supports the requested service
- [ ] Medical necessity criteria are addressed with specific clinical evidence
- [ ] Step therapy requirements are met or exemption is documented
- [ ] Readiness score is calculated with component breakdown
- [ ] Gap report includes specific corrective actions with responsible parties
- [ ] Submission method and expected turnaround are documented

## HIPAA Compliance Notes

- PA requests contain extensive PHI including diagnoses, treatment history, and clinical documentation
- Transmit PA requests via secure methods (encrypted portal, secure fax, encrypted email)
- Store PA tracking data in BAA-covered systems with role-based access controls
- Clinical documentation shared with payers must be limited to information relevant to the PA decision (minimum necessary)
- Maintain audit trails for all PA submissions, status checks, and communications
- Patient authorization may be required for sharing certain sensitive information (substance abuse, HIV, mental health) depending on state law
