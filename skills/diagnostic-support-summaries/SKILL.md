---
name: diagnostic-support-summaries
description: Generate evidence-based diagnostic summaries by synthesizing clinical findings, test results, and differential diagnoses with supporting literature and diagnostic criteria. Use when building differential diagnosis lists, summarizing diagnostic workups, preparing case presentations, or supporting clinical reasoning with evidence synthesis.

metadata:
  display_name: "Diagnostic Support Summaries"
  short_description: "Synthesize clinical findings into diagnostic summaries"
  default_prompt: "Help me with synthesize clinical findings into diagnostic and give clear next steps"
  version: "1.0.0"
  tags:
    - healthcare
  icon_path: "assets/icon.png"
---

# Diagnostic Support Summaries

## Overview

Generate comprehensive, evidence-based diagnostic summaries that synthesize a patient's clinical presentation, examination findings, and test results into structured differential diagnoses with supporting evidence. This skill applies validated diagnostic criteria, Bayesian clinical reasoning, and evidence-based medicine principles to support — not replace — physician diagnostic decision-making.

## When to Use

- Synthesizing complex clinical presentations into structured differentials
- Preparing diagnostic case summaries for conferences or consultations
- Summarizing diagnostic workup progress with next-step recommendations
- Supporting clinical reasoning with evidence-based diagnostic criteria
- Generating teaching case summaries for medical education
- Documenting diagnostic reasoning for medical-legal purposes

## Required Inputs

| Input | Description | Format |
|-------|-------------|--------|
| Clinical presentation | Symptoms, duration, progression, associated features | Structured HPI |
| Physical exam findings | Pertinent positives and negatives by system | Structured exam |
| Diagnostic test results | Labs, imaging, pathology, special tests | Structured results with reference ranges |
| Patient context | Age, sex, comorbidities, medications, risk factors | Structured demographics |
| Clinical question | Specific diagnostic question being addressed | Free text |

## Methodology

### Step 1: Clinical Data Organization

Structure the clinical information using a systematic framework:

**Presenting Syndrome Identification:**
- Identify the primary presenting syndrome (e.g., acute chest pain, chronic cough, unexplained weight loss)
- Classify by organ system, acuity (acute/subacute/chronic), and severity
- Note temporal pattern (sudden, gradual, intermittent, progressive)

**Pertinent Feature Extraction:**
- Pertinent positives: findings that support specific diagnoses
- Pertinent negatives: findings that argue against specific diagnoses
- Red flags: findings suggesting dangerous or emergent conditions
- Pattern recognition: classic presentation patterns (e.g., pleuritic chest pain + dyspnea + recent immobilization = PE concern)

### Step 2: Differential Diagnosis Generation

Build a prioritized differential using anatomic, pathophysiologic, and probabilistic reasoning:

**Framework: "VINDICATE + P"**
- **V**ascular: thrombotic, embolic, hemorrhagic, vasculitic
- **I**nfectious: bacterial, viral, fungal, parasitic
- **N**eoplastic: primary, metastatic, paraneoplastic
- **D**egenerative: wear-and-tear, aging-related
- **I**atrogenic/Intoxication: drug-related, procedure-related
- **C**ongenital: genetic, developmental
- **A**utoimmune/Allergic: systemic autoimmune, organ-specific
- **T**raumatic: acute injury, repetitive stress
- **E**ndocrine/Metabolic: hormonal, electrolyte, metabolic
- **P**sychogenic: functional, somatoform, psychiatric

### Step 3: Evidence Mapping

For each differential diagnosis, map the supporting and refuting evidence:

**Diagnostic Criteria Application:**
- Apply validated diagnostic criteria where available (e.g., Duke criteria for endocarditis, SLICC criteria for SLE, Light criteria for pleural effusion)
- Calculate pre-test probability using clinical prediction rules where applicable (Wells score for PE, CHA2DS2-VASc for stroke risk)
- Note sensitivity and specificity of key findings for each diagnosis

**Evidence Strength for Each Diagnosis:**
- Strong support: pathognomonic finding or multiple concordant features
- Moderate support: several consistent features, some expected features absent
- Weak support: possible but fewer consistent features
- Against: key expected features absent or contradictory findings present

### Step 4: Workup Assessment

Evaluate the current diagnostic workup status:

- **Completed tests**: results and their diagnostic implications
- **Pending tests**: expected timeline and what they will clarify
- **Recommended next tests**: prioritized by diagnostic yield and clinical urgency
- **Test characteristics**: sensitivity, specificity, likelihood ratios for recommended tests

### Step 5: Summary Generation

Produce the diagnostic support summary:

**Summary Components:**
1. One-sentence clinical synopsis
2. Ranked differential with probability estimates and evidence basis
3. Key supporting/refuting evidence for top 3 diagnoses
4. Current workup status with pending and recommended tests
5. Clinical reasoning narrative connecting evidence to diagnoses
6. Urgency assessment for time-sensitive diagnoses

## Output Specification

The output includes:

**clinical_synopsis**: one-sentence summary of the case

**presenting_syndrome**: syndrome name, organ_system, acuity, severity

**differential_diagnoses** (ranked list): diagnosis name, icd10, probability_estimate (high/moderate/low/unlikely), supporting_evidence list, refuting_evidence list, diagnostic_criteria_met (criteria name, elements met, elements total), key_discriminating_tests

**workup_status**: completed_tests (test, result, interpretation, diagnostic_implication), pending_tests (test, expected_turnaround, diagnostic_question), recommended_tests (test, rationale, sensitivity, specificity, urgency)

**clinical_reasoning_narrative**: prose explaining the diagnostic logic

**urgency_flags**: time-sensitive diagnoses requiring immediate action

**evidence_references**: guideline or literature citations supporting the analysis

## Analysis Framework

### Diagnostic Probability Stratification

| Probability Tier | Estimated Likelihood | Action |
|-----------------|---------------------|--------|
| Must not miss | Any probability, high severity | Rule out immediately regardless of probability |
| High probability | Greater than 50% | Primary working diagnosis, confirm |
| Moderate probability | 15-50% | Active differential, targeted testing |
| Low probability | 5-15% | Consider if initial workup negative |
| Unlikely | Less than 5% | Do not pursue unless red flags emerge |

### Pre-Test to Post-Test Probability

Apply likelihood ratios to update diagnostic probabilities:

- LR+ greater than 10: Strong rule-in (large increase in probability)
- LR+ 5-10: Moderate rule-in
- LR+ 2-5: Small increase in probability
- LR- 0.2-0.5: Small decrease in probability
- LR- 0.1-0.2: Moderate rule-out
- LR- less than 0.1: Strong rule-out (large decrease in probability)

## Examples

**Input**: 45-year-old female presenting with 3 weeks of progressive fatigue, joint pain (MCPs and wrists bilateral), morning stiffness lasting over 60 minutes, and new malar rash. ANA positive 1:640, dsDNA positive, C3/C4 low, CBC shows mild leukopenia.

**Diagnostic Summary (abbreviated)**:
- Synopsis: 45F with polyarthritis, malar rash, and serologic findings concerning for systemic lupus erythematosus
- Top Differential:
  1. SLE (HIGH) — meets 4+ SLICC criteria (arthritis, malar rash, ANA+, dsDNA+, low complement, leukopenia). Criteria: 4/11 ACR or 4/17 SLICC met
  2. Mixed connective tissue disease (LOW) — overlapping features but anti-U1 RNP not tested
  3. Rheumatoid arthritis (LOW) — symmetric small joint arthritis fits, but rash and serology favor SLE
- Recommended: anti-Smith antibody, anti-U1 RNP, urinalysis with microscopy (lupus nephritis screening), anti-CCP (RA differentiation), complement levels trending
- Urgency: Renal involvement screening is time-sensitive

## Guidelines

1. **This is decision support, not diagnosis** — all output requires physician review and clinical judgment
2. **Must-not-miss diagnoses always appear** regardless of probability (e.g., PE in chest pain, SAH in headache)
3. **Apply Occam's razor judiciously** — prefer one unifying diagnosis but acknowledge when multiple diagnoses are more likely
4. **Cite diagnostic criteria explicitly** — specify which criteria are met and which are not
5. **Quantify uncertainty** — use probability tiers rather than definitive statements

## Validation Checklist

- [ ] All pertinent positives and negatives from the input are addressed
- [ ] Differential diagnoses are prioritized by probability and severity
- [ ] Must-not-miss diagnoses are included regardless of probability
- [ ] Diagnostic criteria are applied correctly with elements enumerated
- [ ] Recommended tests are prioritized by diagnostic yield and urgency
- [ ] Clinical reasoning narrative is logically coherent
- [ ] No diagnostic conclusions are stated as definitive — all framed as supportive

## HIPAA Compliance Notes

- Diagnostic summaries contain sensitive PHI including diagnoses and test results
- When used for teaching or case conferences, fully de-identify per Safe Harbor (remove all 18 identifiers)
- Store diagnostic support outputs in the medical record system under appropriate access controls
- Ensure AI-generated diagnostic summaries are clearly labeled as decision support, not final diagnoses
- Maintain audit trails for all diagnostic summary generation and access
