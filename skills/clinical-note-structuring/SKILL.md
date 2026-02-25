---
name: clinical-note-structuring
description: Structure unstructured clinical notes into standardized SOAP format with coded diagnoses, procedure mappings, and quality documentation markers. Use when processing free-text clinical notes, physician dictations, EHR narratives, or when the user needs to convert raw clinical documentation into structured, queryable formats.

metadata:
  display_name: "Clinical Note Structuring"
  short_description: "Convert free-text clinical notes into structured SOAP format"
  default_prompt: "Generate clinical note for my case with clear next steps"
  version: "1.0.0"
  tags:
    - healthcare
  icon_path: "assets/icon.png"
---

# Clinical Note Structuring

## Overview

Transform unstructured clinical documentation — free-text physician notes, dictated reports, nursing assessments, and EHR narratives — into standardized, structured formats aligned with SOAP (Subjective, Objective, Assessment, Plan) methodology. The skill extracts clinical entities, maps to ICD-10-CM/CPT codes, identifies documentation gaps, and produces output suitable for downstream billing, quality reporting, and clinical decision support.

## When to Use

- Converting free-text clinical notes into structured SOAP format
- Extracting diagnoses, procedures, medications, and allergies from narratives
- Preparing notes for coding and billing workflows
- Identifying documentation deficiencies before claim submission
- Supporting clinical documentation improvement (CDI) programs
- Processing batch clinical notes for analytics pipelines

## Required Inputs

| Input | Description | Format |
|-------|-------------|--------|
| Raw clinical note | Unstructured text from EHR, dictation, or handoff | Plain text or HL7 MDM segment |
| Encounter type | Outpatient, inpatient, ED, telehealth | Enum string |
| Provider specialty | Specialty context for code mapping | String (e.g., "cardiology") |
| Note type | Progress note, H&P, discharge summary, consult | Enum string |

## Methodology

### Step 1: Note Segmentation

Parse the raw note into logical sections using NLP boundary detection:

1. Identify section headers (explicit: "Assessment:", implicit: contextual shifts)
2. Segment into SOAP components:
   - **Subjective**: Chief complaint (CC), history of present illness (HPI), review of systems (ROS), past medical/surgical/family/social history (PMH/PSH/FH/SH)
   - **Objective**: Vitals, physical exam findings, lab/imaging results
   - **Assessment**: Diagnoses, clinical impressions, differential diagnoses
   - **Plan**: Treatment orders, medications, referrals, follow-up
3. Handle non-standard note formats (narrative-only, problem-oriented) by inferring SOAP mapping

### Step 2: Clinical Entity Extraction

Extract and normalize clinical entities from each section:

- **Diagnoses**: Map to ICD-10-CM codes with specificity level (3-7 characters)
- **Procedures**: Map to CPT/HCPCS codes
- **Medications**: Normalize to RxNorm CUIs with dose, route, frequency
- **Labs**: Map to LOINC codes with values and reference ranges
- **Allergies**: Classify by type (drug, food, environmental) and severity

### Step 3: Documentation Quality Assessment

Evaluate note completeness against E/M documentation requirements:

Documentation Scoring Matrix:
- HPI elements (location, quality, severity, duration, timing, context, modifying factors, associated signs): Count present out of 8
- ROS systems reviewed: Count out of 14
- Exam elements by body area or organ system: Count documented
- Medical decision-making complexity: Straightforward, Low, Moderate, or High
- E/M level supported: 99211-99215 (established) or 99201-99205 (new)

### Step 4: Gap Identification

Flag documentation deficiencies:

- Missing specificity for diagnosis codes (e.g., "diabetes" without type/complication)
- Laterality not documented where required
- Insufficient HPI elements for the billed E/M level
- Missing linkage between assessment and plan items
- Absent or incomplete ROS for the complexity level

### Step 5: Structured Output Assembly

Produce the final structured note with:

- SOAP sections with labeled subsections
- Coded entities with confidence scores
- Documentation quality score
- Gap list with remediation suggestions
- Mapping to applicable quality measures (HEDIS, MIPS)

## Output Specification

The structured output includes the following top-level sections:

**encounter_metadata**: date, provider, specialty, encounter_type, note_type

**subjective**: chief_complaint, hpi (elements_present, narrative), ros (systems_reviewed, pertinent_positives, pertinent_negatives), history (pmh, psh, medications, allergies, family_history, social_history)

**objective**: vitals (bp, hr, rr, temp, spo2, weight, bmi), physical_exam (system, findings, normal_abnormal), results (test, loinc, value, unit, reference_range, flag)

**assessment**: diagnoses (description, icd10, rank, status, confidence), differentials (description, icd10, likelihood)

**plan**: items (action, linked_diagnosis_icd10, category), medications_ordered (name, rxnorm, dose, route, frequency, duration), referrals (specialty, urgency, reason), follow_up (timeframe, conditions)

**quality**: documentation_score (0-100), em_level_supported, gaps (field, issue, recommendation, severity), quality_measures_addressed (measure_id, measure_name, status)

## Analysis Framework

### Documentation Completeness Tiers

| Tier | Score | Description |
|------|-------|-------------|
| Complete | 90-100 | All required elements present, high specificity |
| Adequate | 70-89 | Minor gaps, sufficient for billing |
| Deficient | 50-69 | Significant gaps, risk of downcoding |
| Insufficient | below 50 | Major documentation failures, claim risk |

### E/M Level Determination (2021+ Guidelines)

Apply MDM-based leveling using three elements:

1. **Number and complexity of problems addressed** — minimal, low, moderate, high
2. **Amount and complexity of data reviewed** — minimal/none, limited, moderate, extensive
3. **Risk of complications/morbidity/mortality** — minimal, low, moderate, high

Two of three elements at a given level determine the E/M code.

## Examples

**Input**: "Pt presents with chest pain x 2 days, worse with exertion. Hx of HTN, DM2. BP 148/92, HR 88. EKG shows ST depression V4-V6. Troponin pending. Start heparin drip, cardiology consult, admit to telemetry."

**Structured Output (abbreviated)**:
- Subjective: CC is Chest pain; HPI includes location (chest), duration (2 days), modifying factor (exertion)
- Objective: Vitals are BP 148/92, HR 88; Results show EKG ST depression V4-V6
- Assessment: Acute chest pain (R07.9), HTN (I10), DM2 (E11.9) — flag: DM needs complication specificity
- Plan: Heparin drip, cardiology consult, telemetry admission
- Gaps: DM2 lacks complication detail; troponin result pending; ROS not documented

## Guidelines

1. **Preserve clinical intent** — never alter the clinical meaning of documentation; structure only
2. **Default to lower specificity** when code assignment is ambiguous; flag for clinician review
3. **Apply "if not documented, it was not done"** — do not infer clinical actions not explicitly stated
4. **Map every assessment item to at least one plan item** to ensure medical necessity linkage
5. **Flag sensitive diagnoses** (HIV, substance abuse, mental health) for additional privacy handling

## Validation Checklist

- [ ] Every diagnosis in the assessment has a valid ICD-10-CM code
- [ ] HPI element count matches the documented narrative
- [ ] E/M level is supported by the documentation elements present
- [ ] All medications include dose, route, and frequency
- [ ] No PHI appears in output fields beyond what is clinically necessary
- [ ] Documentation gaps include actionable remediation suggestions
- [ ] SOAP sections contain no cross-contaminated content (e.g., plan items in assessment)

## HIPAA Compliance Notes

- All processing must occur within a BAA-covered environment
- De-identify output when used for analytics or training purposes per Safe Harbor or Expert Determination methods
- Minimum necessary standard: only extract and expose PHI elements required for the specific use case
- Audit log all access to structured notes containing PHI
- Ensure encryption at rest (AES-256) and in transit (TLS 1.2+) for all note data
