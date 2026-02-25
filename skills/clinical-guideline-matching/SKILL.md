---
name: clinical-guideline-matching
description: Match patient cases to applicable evidence-based clinical guidelines and protocols with gap analysis and recommendation generation. Use when evaluating treatment plans against clinical standards, performing guideline adherence reviews, supporting clinical decision-making, or identifying evidence-based treatment options.

metadata:
  display_name: "Clinical Guideline Matching"
  short_description: "Match patients to evidence-based clinical guidelines"
  default_prompt: "Optimize my clinical guideline matching and suggest the best next steps"
  version: "1.0.0"
  tags:
    - healthcare
  icon_path: "assets/icon.png"
---

# Clinical Guideline Matching

## Overview

Systematically match patient clinical profiles to applicable evidence-based guidelines (AHA/ACC, NCCN, ADA, USPSTF, IDSA, etc.), identify applicable recommendations, assess adherence, and highlight deviations with clinical rationale. This skill supports clinical decision support, quality reporting, peer review, and care standardization initiatives.

## When to Use

- Evaluating a treatment plan against current clinical guidelines
- Identifying which guidelines apply to a patient condition set
- Performing guideline adherence audits for quality programs (MIPS, HEDIS)
- Generating clinical decision support alerts
- Supporting peer-to-peer reviews with evidence-based references
- Preparing clinical justification documentation

## Required Inputs

| Input | Description | Format |
|-------|-------------|--------|
| Patient clinical profile | Diagnoses, demographics, labs, vitals | Structured object |
| Active treatment plan | Current medications, procedures, referrals | Structured list |
| Guideline scope | Specific guideline set or "all applicable" | String or array |
| Review context | CDS alert, quality review, peer review | Enum string |

## Methodology

### Step 1: Guideline Identification

Match patient conditions to applicable guideline sets:

1. Map each active ICD-10 diagnosis to guideline-covered conditions
2. Consider patient demographics (age, sex, comorbidities) for guideline applicability
3. Rank guidelines by relevance and recency (prefer most current edition)
4. Identify overlapping or conflicting guidelines and note prioritization

Guideline Source Priority:
1. Specialty society guidelines (AHA, NCCN, ADA, etc.)
2. USPSTF recommendations (preventive services)
3. CMS National Coverage Determinations (NCDs)
4. Local Coverage Determinations (LCDs)
5. Institutional protocols

### Step 2: Recommendation Extraction

For each applicable guideline, extract relevant recommendations:

- **Class of Recommendation** (CoR): I (strong), IIa (moderate), IIb (weak), III (no benefit/harm)
- **Level of Evidence** (LoE): A (multiple RCTs), B-R (randomized), B-NR (non-randomized), C-LD (limited data), C-EO (expert opinion)
- **Specific action items**: diagnostics, therapeutics, monitoring, referrals
- **Contraindications and precautions**: patient-specific factors that modify recommendations

### Step 3: Adherence Assessment

Compare current treatment plan against guideline recommendations:

Adherence Classification:
- ADHERENT: Current plan aligns with guideline recommendation
- PARTIAL: Some elements present, others missing
- NON-ADHERENT: Plan deviates from guideline without documented rationale
- NOT APPLICABLE: Guideline recommendation excluded by patient factors
- CONTRAINDICATED: Guideline recommendation inappropriate for this patient

### Step 4: Gap Analysis

Identify unaddressed guideline recommendations:

- Recommended diagnostics not ordered
- First-line therapies not initiated or attempted
- Monitoring intervals not met
- Recommended referrals not placed
- Preventive measures not addressed

### Step 5: Recommendation Generation

Produce actionable clinical recommendations:

- Prioritize by clinical urgency and evidence strength
- Include specific medication names, doses, and frequencies where guideline-specified
- Note patient-specific modifications (renal dosing, drug interactions, allergies)
- Provide guideline citation with section reference for each recommendation

## Output Specification

The output report includes:

**applicable_guidelines**: guideline_name, issuing_body, edition_year, applicability_reason, and a list of recommendations each containing recommendation_id, text, class (I/IIa/IIb/III), level_of_evidence (A/B-R/B-NR/C-LD/C-EO), adherence_status, current_plan_evidence, gap_detail, and suggested_action

**gap_summary**: total_recommendations_evaluated, counts by adherence status, adherence_rate percentage, and priority_gaps with gap description, guideline_source, evidence_strength, clinical_urgency (high/medium/low), and suggested_intervention

**conflicts**: when multiple guidelines apply, list the conflicting guidelines, describe the issue, and provide a resolution_approach

## Analysis Framework

### Guideline-Condition Mapping (Common)

| Condition Category | Primary Guidelines |
|---|---|
| Heart failure | AHA/ACC HF Guidelines, HFSA |
| Diabetes mellitus | ADA Standards of Care, AACE |
| Hypertension | AHA/ACC HTN Guideline |
| Cancer (by type) | NCCN Clinical Practice Guidelines |
| Infectious disease | IDSA Practice Guidelines |
| Preventive care | USPSTF A/B Recommendations |
| Chronic kidney disease | KDIGO Guidelines |
| COPD / Asthma | GOLD, GINA Guidelines |

### Evidence Strength Hierarchy

Recommendations with higher class and evidence level take priority in gap analysis:

1. Class I, Level A — strongest (must-do based on robust evidence)
2. Class I, Level B-R — strong with good evidence
3. Class IIa, Level A/B — reasonable with supporting evidence
4. Class IIb — may be considered
5. Class III — not recommended (harm or no benefit)

## Examples

**Input**: 65-year-old male, HFrEF (EF 25%), DM2, CKD Stage 3b, on lisinopril 20mg, metoprolol succinate 50mg, metformin 1000mg BID.

**Guideline Match (abbreviated)**:
- AHA/ACC HF Guideline (2022): Class I recommendation for ARNI (sacubitril/valsartan) over ACEi in HFrEF — NON-ADHERENT (patient on ACEi, not ARNI). Suggested: Switch lisinopril to sacubitril/valsartan with 36-hour washout
- AHA/ACC HF: Class I for SGLT2i in HFrEF — NON-ADHERENT. Suggested: Add dapagliflozin 10mg (also benefits CKD per KDIGO)
- ADA Standards 2025: Metformin caution with eGFR <30, monitor renal function — ADHERENT (CKD 3b, eGFR likely 30-44, metformin acceptable with monitoring)
- AHA/ACC HF: Target dose beta-blocker — PARTIAL (metoprolol 50mg, target 200mg). Suggested: Uptitrate as tolerated

## Guidelines

1. **Use the most current guideline edition** — always specify the year to avoid outdated recommendations
2. **Never override clinical judgment** — present guidelines as decision support, not mandates
3. **Account for multimorbidity** — when guidelines conflict due to comorbidities, flag for physician resolution
4. **Document rationale for non-adherence** — acceptable reasons include patient preference, contraindications, and clinical judgment
5. **Distinguish screening from diagnostic guidelines** — different applicability criteria

## Validation Checklist

- [ ] All active diagnoses have been evaluated for applicable guidelines
- [ ] Each recommendation includes class and level of evidence
- [ ] Adherence status is assessed for every extracted recommendation
- [ ] Patient-specific contraindications are accounted for in adherence assessment
- [ ] Guideline conflicts are identified and documented
- [ ] Suggested actions are specific and clinically actionable
- [ ] Guideline citations include issuing body, title, and year

## HIPAA Compliance Notes

- Clinical profiles used for guideline matching must be accessed under minimum necessary principles
- Guideline match reports containing PHI must be stored in BAA-covered systems
- When used for population-level quality analysis, de-identify per HIPAA Safe Harbor or Expert Determination
- Audit trail required for all guideline match operations involving identifiable patient data
- Ensure guideline recommendations are not confused with clinical orders — they require physician review and authorization
