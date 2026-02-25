---
name: Patient Communication Simplifier
description: Transform complex clinical and administrative healthcare communications into plain-language content calibrated to target health literacy levels using Flesch-Kincaid, SMOG, and SAM scoring with teach-back verification frameworks.

metadata:
  display_name: "Patient Communication Simplifier"
  short_description: "Simplify clinical communications for patient readability"
  default_prompt: "Generate patient communication for my case with clear next steps"
  version: "1.0.0"
  tags:
    - healthcare
  icon_path: "assets/icon.png"
---

# Patient Communication Simplifier

## Overview

This skill transforms complex medical communications (clinical notes, consent forms, discharge instructions, benefit explanations, care plans) into plain-language content accessible to patients at varying health literacy levels. It applies validated readability assessment instruments (Flesch-Kincaid, SMOG, Fry Readability Graph) and suitability evaluation tools (Suitability Assessment of Materials, SAM) to ensure output meets national health literacy standards. The CDC recommends patient materials target a 6th-8th grade reading level; nearly 36% of U.S. adults have basic or below-basic health literacy (NAAL).

## When to Use

- Converting clinical documentation into patient-facing after-visit summaries
- Simplifying consent forms, advance directives, or financial agreements
- Rewriting patient education materials for lower literacy audiences
- Preparing content for patient portals that must meet Meaningful Use plain-language requirements
- Adapting communications for specific populations (elderly, pediatric caregivers, LEP post-translation)
- Responding to CMS or Joint Commission findings on patient communication adequacy

## Required Inputs

| Input | Description | Format |
|-------|-------------|--------|
| `source_content` | Original clinical or administrative text to simplify | String |
| `content_type` | Category: discharge_instructions, consent_form, care_plan, education_material, correspondence | String |
| `target_reading_level` | Desired grade level (default: 6th grade) | Number |
| `patient_context` | Target audience characteristics (age range, condition, cultural considerations) | JSON object |
| `clinical_accuracy_reviewer` | Identifier for clinical SME who will validate accuracy | String |
| `output_format` | Desired format: plain_text, html, structured_json | String |

## Methodology

### Step 1: Source Content Analysis
- Compute baseline readability metrics on the source document:
  - **Flesch-Kincaid Grade Level**: 0.39 x (total words/total sentences) + 11.8 x (total syllables/total words) - 15.59
  - **SMOG Index**: 3 + sqrt(polysyllable count x 30/total sentences)
  - **Flesch Reading Ease**: 206.835 - 1.015 x (words/sentences) - 84.6 x (syllables/words), target 60 or above
- Identify clinical jargon, abbreviations, acronyms, and complex sentence structures
- Flag sentences exceeding 20 words (recommended maximum for patient materials)
- Catalogue multi-syllabic medical terms requiring simplification or definition

### Step 2: Terminology Simplification
- Replace medical jargon with plain-language equivalents using validated substitution lists:
  - "hypertension" becomes "high blood pressure"
  - "myocardial infarction" becomes "heart attack"
  - "bilateral" becomes "on both sides"
  - "contraindicated" becomes "should not be used"
  - "prophylaxis" becomes "prevention"
  - "etiology" becomes "cause"
  - "benign" becomes "not cancer" or "not harmful"
  - "prognosis" becomes "what we expect to happen"
- When a medical term must be retained (medication names, diagnosis for insurance), introduce it with its plain-language equivalent: "metformin (your diabetes medicine)"
- Preserve clinical precision: simplification must not introduce ambiguity or inaccuracy

### Step 3: Structural Simplification
- Apply plain-language writing principles (per PlainLanguage.gov and NIH Clear Communication):
  - Use active voice ("Take your medicine at 8 AM" not "Medicine should be taken at 8 AM")
  - Use second person ("you/your") to address the patient directly
  - Limit sentences to 15-20 words maximum
  - One idea per sentence, one topic per paragraph
  - Use headers and bullet points to organize information
  - Lead with the most important information (inverted pyramid)
  - Use concrete numbers instead of vague terms ("every 4 hours" not "frequently")
- Apply chunking: group related instructions under clear action-oriented headers
  - "What to Do at Home"
  - "When to Call Your Doctor"
  - "Your Medicines"
  - "Your Next Appointment"

### Step 4: Visual and Layout Optimization
- Recommend design elements that improve comprehension:
  - White space: 1-inch margins minimum, 1.15 line spacing minimum
  - Font: Sans-serif, 12pt minimum (14pt for elderly audiences)
  - Contrast: Dark text on light background (WCAG AA minimum)
  - Visuals: Simple illustrations or icons to reinforce key concepts
  - Highlight critical safety information (warning signs, emergency instructions)
- Structure content for SAM evaluation targeting "superior" rating (70-100%)

### Step 5: Readability Verification
- Recompute readability scores on simplified output:
  - Flesch-Kincaid Grade Level at or below target (default: 6.0)
  - SMOG Index at or below target + 1 grade level
  - Flesch Reading Ease of 60 or above (70 or above preferred)
- Apply SAM assessment across six domains:
  - Content (purpose, scope, summary)
  - Literacy demand (reading level, vocabulary, context, sentence construction)
  - Graphics (cover, type, relevance, captions)
  - Layout and Typography (subheadings, cues, whitespace)
  - Learning stimulation (interaction, modeling, motivation)
  - Cultural appropriateness (match to audience experience and imagery)
- Score: Not Suitable (0-39%), Adequate (40-69%), Superior (70-100%)

### Step 6: Teach-Back Verification Framework
- Generate 3-5 teach-back questions for each content section:
  - "In your own words, what should you do if [symptom] happens?"
  - "Can you show me how you would take your medicine based on these instructions?"
  - "What is the most important thing to watch for after you go home?"
- Design questions to verify comprehension of critical safety information
- Include suggested scripts for staff administering teach-back

## Output Specification

```yaml
simplified_content:
  original_metrics:
    flesch_kincaid_grade: number
    smog_index: number
    flesch_reading_ease: number
    word_count: number
    avg_sentence_length: number
  simplified_metrics:
    flesch_kincaid_grade: number
    smog_index: number
    flesch_reading_ease: number
    word_count: number
    avg_sentence_length: number
    sam_score_percent: number
    sam_rating: string
  content:
    sections:
      - heading: string
        body: string
        critical_safety: boolean
  terminology_changes:
    - original_term: string
      simplified_term: string
      context: string
  teach_back_questions:
    - section: string
      question: string
      expected_response_elements: array
  design_recommendations:
    font: string
    font_size: string
    layout_notes: array
  clinical_review_status: string
```

## Analysis Framework

Apply the **CDC Clear Communication Index** (CCI) as the primary evaluation framework:
1. **Main message**: Is the main message obvious and stated early?
2. **Language**: Are words common and sentences short?
3. **Information design**: Is the layout clean with clear visual hierarchy?
4. **State of the science**: Is the information accurate and evidence-based?
5. **Behavioral recommendations**: Are actions specific and achievable?
6. **Numbers**: Are numbers simple, necessary, and explained?
7. **Risk**: Are risks and benefits presented clearly and without bias?

Target CCI score: 90 out of 100 or higher.

## Examples

**Example: Discharge Instructions for Heart Failure**
- Original (Grade 12.4): "Patient is advised to adhere to a sodium-restricted diet of less than 2000mg daily, monitor daily weight fluctuations, and report any acute dyspnea, peripheral edema, or weight gain exceeding 3 pounds in 24 hours to the prescribing cardiologist."
- Simplified (Grade 5.8): "Eat less salt. Try to have less than 2,000 mg of salt each day. Weigh yourself every morning before eating. Call your heart doctor right away if: you gain more than 3 pounds in one day, your feet or legs swell up, or you have trouble breathing."
- FK Grade reduction: 12.4 to 5.8; Flesch Reading Ease: 34 to 72; SAM: Superior (82%)

## Guidelines

- **HIPAA Compliance**: Simplified content must not introduce PHI not present in the source. If source contains PHI, maintain same access controls on output. De-identify any examples used for training or quality improvement.
- **Clinical Accuracy**: Every simplification must be reviewed by a clinical SME before patient distribution. Simplification must never sacrifice accuracy for readability.
- **Cultural Sensitivity**: Avoid idioms, metaphors, and culturally specific references that may not translate across populations. Use person-first language ("person with diabetes" not "diabetic").
- **Regulatory Compliance**: Meet Promoting Interoperability requirements for patient-accessible clinical information. Comply with ACA Section 1557 requirements for accessible communications.
- **Accessibility**: Ensure output is screen-reader compatible. Provide alt-text recommendations for any visual elements. Follow WCAG 2.1 AA standards.

## Validation Checklist

- [ ] Baseline readability scores computed on source content
- [ ] Target reading level achieved (Flesch-Kincaid at or below target grade)
- [ ] SMOG Index within 1 grade level of target
- [ ] Flesch Reading Ease of 60 or above
- [ ] SAM assessment completed with score of 70% or above (Superior)
- [ ] All medical jargon replaced or defined in context
- [ ] Sentence length 20 words or fewer on average
- [ ] Active voice used throughout
- [ ] Teach-back questions generated for each content section
- [ ] Clinical accuracy review assigned and tracked
- [ ] Cultural sensitivity review completed
- [ ] HIPAA compliance verified: no unintended PHI exposure
- [ ] Design recommendations included for print and digital formatting
