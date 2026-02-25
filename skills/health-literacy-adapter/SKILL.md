---
name: Health Literacy Adapter
description: Dynamically adjust healthcare content readability and presentation based on assessed health literacy levels using validated instruments (REALM, NVS, TOFHLA) and adaptive content transformation strategies aligned with universal precautions approach.

metadata:
  display_name: "Health Literacy Adapter"
  short_description: "Adapt healthcare content to patient literacy levels"
  default_prompt: "Generate health literacy for my case with clear next steps"
  version: "1.0.0"
  tags:
    - healthcare
  icon_path: "assets/icon.png"
---

# Health Literacy Adapter

## Overview

This skill adapts healthcare content to match individual or population health literacy levels using a systematic, evidence-based approach. It employs validated health literacy assessment instruments (REALM-SF, Newest Vital Sign, TOFHLA) to determine comprehension capacity, then applies graduated content transformation strategies ranging from minor adjustments for adequate literacy to comprehensive restructuring for limited literacy. The skill follows the Universal Precautions approach recommended by AHRQ: assume all patients may have difficulty comprehending health information and design communications accordingly, while providing additional adaptations for those with identified limitations.

## When to Use

- Adapting EHR-generated patient instructions to appropriate literacy levels
- Creating tiered versions of education materials for diverse patient populations
- Designing intake forms, consent documents, or portal content with literacy considerations
- Training clinical staff on health literacy communication techniques
- Evaluating existing patient materials against literacy standards
- Implementing AHRQ Health Literacy Universal Precautions Toolkit recommendations
- Supporting Promoting Interoperability requirements for patient-accessible content

## Required Inputs

| Input | Description | Format |
|-------|-------------|--------|
| `source_content` | Healthcare content to be adapted | String |
| `literacy_level` | Assessed or estimated health literacy level: limited, marginal, adequate | String |
| `assessment_instrument` | Tool used for assessment: REALM_SF, NVS, TOFHLA, estimated | String |
| `content_purpose` | Purpose: education, instruction, consent, notification, self_management | String |
| `modality` | Delivery channel: print, digital, verbal_script, video_script, sms | String |
| `clinical_context` | Condition, care setting, urgency level | JSON object |
| `audience_characteristics` | Age range, primary language, visual/cognitive considerations | JSON object |

## Methodology

### Step 1: Health Literacy Level Determination
- Apply or interpret validated health literacy assessment:
  - **REALM-SF** (Rapid Estimate of Adult Literacy in Medicine - Short Form):
    - 7 medical words, patient reads aloud, score 0-7
    - 0-3: limited literacy (3rd grade and below)
    - 4-6: marginal literacy (4th-6th grade)
    - 7: adequate literacy (7th grade and above)
  - **Newest Vital Sign (NVS)**:
    - 6 questions about a nutrition label, score 0-6
    - 0-1: high likelihood of limited literacy
    - 2-3: possibility of limited literacy
    - 4-6: adequate literacy
  - **TOFHLA** (Test of Functional Health Literacy in Adults):
    - Reading comprehension (50 items) + numeracy (17 items)
    - 0-53: inadequate health literacy
    - 54-66: marginal health literacy
    - 67-100: adequate health literacy
- When formal assessment is not available, use proxy indicators:
  - Education level (not always predictive but provides baseline)
  - Patient portal engagement level
  - Teach-back performance history
  - Primary language and LEP status
  - Age (literacy challenges increase in elderly populations)

### Step 2: Content Analysis and Gap Assessment
- Analyze source content characteristics:
  - Current reading grade level (Flesch-Kincaid, SMOG)
  - Medical terminology density (terms per 100 words)
  - Sentence complexity (average length, clause count)
  - Numeracy demands (dosage calculations, percentages, risk ratios)
  - Visual support (present/absent, quality, relevance)
  - Action clarity (specific, vague, assumed knowledge)
- Calculate literacy gap: difference between content level and patient literacy level
- Determine transformation intensity:
  - Gap of 0-2 grade levels: Light adaptation
  - Gap of 3-5 grade levels: Moderate adaptation
  - Gap of 6+ grade levels: Intensive adaptation

### Step 3: Graduated Content Transformation
- **Light Adaptation** (adequate literacy, minor gaps):
  - Replace technical terms with plain-language equivalents where possible
  - Shorten sentences exceeding 25 words
  - Add section headers for navigation
  - Bold key action items
  - Verify numerical information is clearly contextualized
- **Moderate Adaptation** (marginal literacy):
  - Reduce reading level to 6th grade target
  - Restructure to inverted pyramid (most important first)
  - Replace all medical jargon or define in context
  - Add visual aids (icons, simple diagrams, pictographs)
  - Convert complex lists to numbered sequential steps
  - Use concrete examples instead of abstract concepts
  - Add teach-back prompts after each major section
- **Intensive Adaptation** (limited literacy):
  - Reduce reading level to 3rd-4th grade target
  - Use very short sentences (8-10 words maximum)
  - One concept per page or screen
  - Heavy visual support (pictographic instructions, photo sequences)
  - Audio/video supplement recommendation
  - Medication schedule as visual grid with pill images
  - Eliminate or drastically simplify all numerical content
  - Use icon-based warning signs instead of text-heavy lists
  - Recommend in-person education with teach-back

### Step 4: Numeracy Adaptation
- Assess and adapt numerical content:
  - **Adequate numeracy**: Present numbers with context ("3 out of 100 people")
  - **Limited numeracy**: Use simple frequency ("very rare") or visual representations
  - Medication dosing: Use visual aids (pill images with clock times)
  - Risk communication: Use icon arrays or pictographs instead of percentages
  - Lab values: Use simple ranges ("normal", "too high", "too low") with color coding
  - Appointment times: Use 12-hour clock with AM/PM, include day of week
- Never assume patients can interpret fractions, decimals, or percentages without support

### Step 5: Modality-Specific Optimization
- **Print materials**: Layout, font, spacing, visual hierarchy per SAM criteria
- **Digital/portal**: Progressive disclosure, chunked content, accessible design (WCAG 2.1)
- **Verbal scripts**: Staff talking points with embedded teach-back, pause points
- **Video scripts**: Scene-by-scene storyboard, reading level of narration, visual support notes
- **SMS/text**: Character-limited messages with single action per message, link to detailed content
- Each modality adaptation maintains consistent key messages across channels

### Step 6: Effectiveness Verification
- Apply validation measures:
  - Readability scoring (Flesch-Kincaid target achieved)
  - SAM assessment (target Superior: 70-100%)
  - CDC Clear Communication Index (target 90+)
  - Cognitive load assessment (Miller Law: 7 plus or minus 2 information chunks)
  - Usability testing with representative patients (recommended)
- Generate teach-back assessment protocol for staff use
- Create feedback mechanism for ongoing content improvement

## Output Specification

```yaml
adapted_content:
  literacy_assessment:
    instrument: string
    score: number
    level: string
  source_analysis:
    original_grade_level: number
    terminology_density: number
    numeracy_demands: string
    literacy_gap: number
    transformation_intensity: string
  adapted_output:
    target_grade_level: number
    achieved_grade_level: number
    modality: string
    sections:
      - heading: string
        content: string
        visual_support: string
        teach_back_prompt: string
    numeracy_adaptations:
      - original: string
        adapted: string
        method: string
  quality_scores:
    flesch_kincaid: number
    sam_score: number
    cci_score: number
    cognitive_load_chunks: number
  recommendations:
    supplemental_modalities: array
    staff_communication_tips: array
    follow_up_education: array
```

## Analysis Framework

Apply the **AHRQ Health Literacy Universal Precautions Toolkit** framework:
1. **Awareness**: Build organizational awareness that health literacy is everyone's responsibility
2. **Written communication**: Apply plain language, appropriate readability, effective design
3. **Verbal communication**: Use teach-back, chunk and check, patient-friendly language
4. **Self-management support**: Simplify action plans, use visual aids, set achievable goals
5. **Supportive systems**: Design systems that reduce literacy demands (simplified forms, navigation aids)

## Examples

**Example: Warfarin Self-Management Instructions**
- Patient: 72-year-old, REALM-SF score 3 (limited literacy), Spanish-speaking
- Source: 11th grade clinic handout with INR ranges, food interaction tables, dose adjustment algorithms
- Adaptation level: Intensive
- Adapted output:
  - 3rd grade reading level in Spanish
  - Visual pill calendar with color-coded doses
  - Traffic light system for foods: green (safe), yellow (small amounts), red (avoid)
  - Photo-based bleeding warning signs instead of text descriptions
  - Single action per page: "Take your blood thinner pill every day at the same time"
  - Audio companion recommended in addition to print
  - Teach-back: "Show me on this calendar when you take your pill"
- Scores: FK Grade 3.2, SAM 88% (Superior), CCI 94

## Guidelines

- **HIPAA Compliance**: Health literacy assessments are part of the medical record and subject to HIPAA protections. De-identify all literacy assessment data used for program evaluation or quality improvement. Never label patients externally as "low literacy."
- **Stigma Prevention**: Use Universal Precautions approach publicly. Targeted adaptations should be delivered naturally without drawing attention to literacy level. Avoid phrases like "simplified version" in patient-facing labels.
- **Clinical Accuracy**: Adaptations must not sacrifice medical accuracy for simplicity. When simplification creates ambiguity, retain the precise term with an embedded plain-language definition.
- **Cultural Responsiveness**: Literacy adaptation must be culturally appropriate. Health literacy varies independently from education and language. Avoid assumptions based on demographics.
- **ADA Compliance**: Ensure adapted materials meet accessibility requirements for visual impairment (large print, screen reader compatible), hearing impairment (captioned video), and cognitive disability.
- **Continuous Assessment**: Health literacy is not static. Reassess when patients have new conditions, new medications, or demonstrate changed comprehension through teach-back.

## Validation Checklist

- [ ] Health literacy level assessed or estimated using validated approach
- [ ] Literacy gap calculated and transformation intensity determined
- [ ] Content adapted to target reading level for assessed literacy
- [ ] Medical terminology replaced or defined in context
- [ ] Numeracy content adapted with visual support where needed
- [ ] Modality-specific optimizations applied
- [ ] SAM assessment completed with Superior rating target
- [ ] Teach-back prompts included for each critical section
- [ ] Clinical accuracy preserved through adaptation
- [ ] Cultural appropriateness verified
- [ ] Accessibility requirements met (ADA, WCAG)
- [ ] HIPAA compliance maintained for literacy assessment data
- [ ] Stigma-free delivery approach documented
