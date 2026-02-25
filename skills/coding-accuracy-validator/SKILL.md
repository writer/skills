---
name: coding-accuracy-validator
description: Validate ICD-10-CM diagnosis and CPT/HCPCS procedure code accuracy against clinical documentation, NCCI edits, LCD/NCD policies, and coding guidelines. Use when auditing coded claims, validating code assignments before submission, performing coding compliance reviews, or training coders on accurate code selection.

metadata:
  display_name: "Coding Accuracy Validator"
  short_description: "Validate ICD-10 and CPT code accuracy against documentation"
  default_prompt: "Check my coding accuracy for gaps risks and required fixes"
  version: "1.0.0"
  tags:
    - healthcare
  icon_path: "assets/icon.png"
---

# Coding Accuracy Validator

## Overview

Validate the accuracy of ICD-10-CM diagnosis codes and CPT/HCPCS procedure codes against clinical documentation, official coding guidelines, NCCI (National Correct Coding Initiative) edits, payer-specific policies, and medical necessity requirements. This skill supports coding compliance, reduces claim denials from coding errors, and ensures optimal reimbursement through accurate code capture.

## When to Use

- Auditing coded claims before submission for accuracy
- Validating diagnosis-procedure code linkages (medical necessity)
- Checking for NCCI edit violations (bundling/unbundling)
- Reviewing coding specificity and compliance with Official Coding Guidelines
- Performing retrospective coding audits for compliance programs
- Supporting coder education with detailed code validation feedback

## Required Inputs

| Input | Description | Format |
|-------|-------------|--------|
| Assigned codes | ICD-10-CM and CPT/HCPCS codes with modifiers | Structured array |
| Clinical documentation | Encounter note supporting the codes | Text or structured note |
| Encounter type | Inpatient, outpatient, professional, facility | Enum string |
| Provider specialty | Specialty of the rendering provider | String |
| Payer | Payer for LCD/NCD validation | String |

## Methodology

### Step 1: ICD-10-CM Diagnosis Code Validation

Validate each assigned diagnosis code:

**Specificity Check:**
- Is the code at the highest level of specificity supported by documentation?
- Are required 4th, 5th, 6th, and 7th characters present?
- Is laterality captured where applicable?
- Are episode-of-care characters correct (A=initial, D=subsequent, S=sequela)?
- Are combination codes used where available (e.g., E11.65 for DM2 with hyperglycemia)?

**Documentation Support:**
- Does the clinical note explicitly document the condition coded?
- Is the diagnosis stated by the physician (or qualified provider)?
- Are signs/symptoms coded only when no definitive diagnosis exists?
- For inpatient: Is the principal diagnosis the condition established after study to be chiefly responsible for the admission?

**Coding Guideline Compliance:**
- ICD-10-CM Official Guidelines for Coding and Reporting compliance
- Chapter-specific guidelines (e.g., Chapter 4 endocrine, Chapter 9 circulatory)
- Selection of principal diagnosis guidelines for inpatient
- Present on admission (POA) indicator accuracy for inpatient claims
- External cause codes where applicable (V, W, X, Y codes)

### Step 2: CPT/HCPCS Procedure Code Validation

Validate each assigned procedure code:

**Code Selection Accuracy:**
- Does the CPT code description match the documented procedure or service?
- Is the correct code range selected (e.g., excision vs. destruction vs. shaving)?
- Are time-based codes supported by documented time?
- For E/M codes: Does the MDM level match the documentation?

**Modifier Validation:**
- Are required modifiers present (25, 59, 76, 77, LT/RT, etc.)?
- Is modifier 25 (significant, separately identifiable E/M) justified with documentation?
- Are modifiers used correctly (not to bypass edits inappropriately)?
- Are anatomic modifiers correct (LT/RT, F1-F9, T1-T9)?

**Units and Frequency:**
- Are units billed consistent with documentation?
- For time-based services, do units match documented time (e.g., 97110 per 15-min increments)?
- Does the frequency of service align with medical necessity?

### Step 3: NCCI Edit Validation

Check for National Correct Coding Initiative violations:

**Column 1/Column 2 Edits:**
- Identify code pairs where one procedure is a component of another
- Verify if modifier bypass is permitted (modifier indicator 1 = modifier allowed)
- Confirm documentation supports separate and distinct services when modifier used

**Medically Unlikely Edits (MUEs):**
- Verify units billed do not exceed MUE limits for each CPT code
- MUE adjudication: claim line (1), date of service (2), or per day (3)
- If exceeding MUE, verify documentation supports the units

**Add-On Code Validation:**
- Add-on codes must be billed with the primary procedure
- Verify the correct primary procedure is present
- Add-on codes cannot be billed standalone

### Step 4: Medical Necessity Linkage

Validate diagnosis-procedure linkage:

**ICD-10 to CPT Linkage:**
- Does the diagnosis code medically justify the procedure?
- Check against LCD/NCD covered diagnoses lists
- Verify the clinical scenario supports the service ordered
- Flag procedures without supporting diagnosis justification

**Frequency and Setting Appropriateness:**
- Is the service frequency within payer guidelines?
- Is the place of service appropriate for the procedure?
- Are duplicate services on the same date appropriately modified or justified?

### Step 5: Validation Report Generation

Produce the comprehensive validation report:

**Severity Classifications:**
- CRITICAL: Code will likely result in denial, audit risk, or compliance violation
- WARNING: Code may be questioned; additional documentation recommended
- ADVISORY: Best practice suggestion for coding optimization
- PASS: Code is accurate and well-supported

## Output Specification

The output includes:

**validation_summary**: total_codes_reviewed, critical_issues, warnings, advisories, passes, overall_accuracy_score (0-100%)

**diagnosis_code_validation**: for each ICD-10 code — code, description, validation_status, specificity_assessment, documentation_support (supported/partial/unsupported), guideline_compliance_issues, recommended_code (if different), rationale

**procedure_code_validation**: for each CPT/HCPCS code — code, description, validation_status, modifier_assessment, units_assessment, documentation_support, recommended_code (if different), rationale

**ncci_edit_results**: code_pair, edit_type (column1-column2/MUE/add-on), modifier_indicator, violation_status, recommendation

**medical_necessity_linkage**: procedure_code, linked_diagnosis, linkage_valid (yes/no), lcd_ncd_reference, coverage_status

**compliance_risk_assessment**: overall_risk_level (low/moderate/high), specific_risks, documentation_recommendations, coder_education_points

## Analysis Framework

### Common Coding Errors by Category

| Error Category | Example | Risk Level |
|---------------|---------|------------|
| Upcoding | E/M 99215 billed without supporting MDM | Critical — compliance/fraud risk |
| Undercoding | E/M 99213 billed when documentation supports 99214 | Warning — revenue loss |
| Unbundling | Billing component codes separately when a comprehensive code exists | Critical — compliance risk |
| Missing specificity | E11.9 (DM2 unspecified) when complications documented | Warning — may trigger query |
| Wrong laterality | Right knee procedure coded without RT modifier | Critical — denial risk |
| Missing modifier | Two distinct E/M services without modifier 25 | Critical — denial risk |
| Diagnosis-procedure mismatch | Screening mammography coded with breast cancer diagnosis | Critical — medical necessity |

### E/M Code Level Validation (2021+ MDM-Based)

| E/M Level | Problem Complexity | Data Complexity | Risk |
|-----------|-------------------|-----------------|------|
| 99212/99202 | Straightforward | Minimal or none | Minimal |
| 99213/99203 | Low | Limited | Low |
| 99214/99204 | Moderate | Moderate | Moderate |
| 99215/99205 | High | Extensive | High |

Two of three MDM elements must meet the level billed.

## Examples

**Input**: Outpatient visit coded with 99214 (E/M moderate), ICD-10: E11.9 (DM2 unspecified), 83036 (HbA1c), 99214-25, 36415 (venipuncture).

**Validation Results**:
1. E11.9 — WARNING: DM2 coded as unspecified. Note documents diabetic neuropathy and retinopathy. Recommend E11.40 (DM2 with diabetic neuropathy unspecified) and E11.319 (DM2 with unspecified diabetic retinopathy without macular edema) for full capture
2. 99214 — PASS: MDM moderate level supported (multiple chronic conditions, medication management, prescription drug management risk)
3. 99214-25 — PASS: Modifier 25 appropriate since separately identifiable E/M with lab draw
4. 83036 — PASS: HbA1c medically necessary for DM2 monitoring, LCD covered
5. 36415 — ADVISORY: Venipuncture is typically included in the office visit unless performed by a separate lab; verify billing arrangement

## Guidelines

1. **Code only what is documented** — never assign codes based on clinical assumptions
2. **Specificity matters** — always code to the highest level of specificity supported by documentation
3. **Query before assuming** — when documentation is ambiguous, issue a physician query rather than guessing
4. **Follow Official Guidelines** — ICD-10-CM Official Guidelines are the authoritative reference
5. **Keep NCCI edits current** — CMS updates NCCI edits quarterly

## Validation Checklist

- [ ] All ICD-10 codes are at the highest specificity level supported by documentation
- [ ] All CPT codes accurately reflect the documented procedures/services
- [ ] Required modifiers are present and correctly applied
- [ ] NCCI column 1/column 2 edits have been checked
- [ ] MUE limits are not exceeded without justification
- [ ] Add-on codes are paired with valid primary codes
- [ ] Diagnosis-procedure linkage supports medical necessity
- [ ] E/M level is supported by documented MDM elements

## HIPAA Compliance Notes

- Coding validation involves access to clinical documentation containing PHI
- Coding audit results must be stored securely with appropriate access controls
- External coding auditors must operate under a BAA
- Coding validation findings used for education should be de-identified
- Maintain audit trails for all coding reviews for compliance program documentation
- False Claims Act implications: knowingly submitting inaccurate codes constitutes potential fraud
