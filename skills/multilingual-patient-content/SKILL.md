---
name: Multilingual Patient Content
description: Generate and validate language-safe healthcare communications for Limited English Proficiency (LEP) populations following Section 1557, CMS language access requirements, and culturally appropriate health communication standards.

metadata:
  display_name: "Multilingual Patient Content"
  short_description: "Create multilingual healthcare content for LEP patients"
  default_prompt: "Analyze my multilingual patient content and recommend clear next actions"
  version: "1.0.0"
  tags:
    - healthcare
  icon_path: "assets/icon.png"
---

# Multilingual Patient Content

## Overview

This skill produces and validates multilingual patient-facing healthcare content that meets federal language access requirements under Section 1557 of the ACA, Title VI of the Civil Rights Act, and CMS Meaningful Access provisions. It addresses the full lifecycle of multilingual content: translation readiness assessment, cultural adaptation beyond literal translation, quality validation, and compliance documentation. Approximately 25.7 million people in the U.S. are LEP, and language barriers are associated with longer hospital stays, higher readmission rates, and increased adverse events.

## When to Use

- Translating patient education materials, consent forms, or discharge instructions into non-English languages
- Establishing language access programs or evaluating existing translation workflows
- Preparing for OCR (Office for Civil Rights) compliance reviews on language access
- Adapting content for culturally distinct populations beyond simple translation
- Implementing multilingual patient portal or digital health content
- Training staff on LEP communication requirements and best practices

## Required Inputs

| Input | Description | Format |
|-------|-------------|--------|
| `source_content` | English-language source material to be translated/adapted | String |
| `target_languages` | List of target languages with dialect specificity (e.g., "Spanish-MX", "Chinese-Traditional") | JSON array |
| `content_type` | Material type: consent_form, discharge_instructions, education, correspondence, signage | String |
| `patient_population` | Demographics of target language population (country of origin, literacy level, cultural context) | JSON object |
| `regulatory_context` | Applicable requirements (Section 1557, state Medicaid, Joint Commission) | JSON array |
| `existing_translations` | Previously translated materials for consistency review (optional) | JSON array |

## Methodology

### Step 1: Translation Readiness Assessment
- Evaluate source content for translation suitability:
  - Reading level of source (target 6th grade or below per best practice)
  - Idioms, colloquialisms, or culturally specific references that will not translate literally
  - Sentence complexity and passive voice usage
  - Medical terminology density
  - Visual elements with embedded text requiring separate translation
- Simplify source content before translation when reading level exceeds 8th grade
- Create a terminology glossary for consistent translation of key medical terms

### Step 2: Language Threshold Analysis
- Determine which languages require translated materials per federal standards:
  - Section 1557: Translate vital documents for language groups constituting 5% or 1,000 individuals (whichever is less) of the eligible population or likely affected population
  - CMS Medicaid Managed Care (42 CFR 438.10): Translate materials when a language is spoken by 5% or more of the enrollee population in a service area
  - State-specific thresholds may be more stringent
- Document language prevalence data sources (ACS, state Medicaid enrollment, facility registration data)
- Prioritize languages by population size, clinical risk, and complaint history

### Step 3: Cultural Adaptation (Transcreation)
- Go beyond literal translation to cultural adaptation:
  - Adjust health concepts that differ across cultures (pain scales, mental health terminology, dietary guidance)
  - Adapt visual elements (skin tone representation, family structure, food imagery)
  - Consider health beliefs and traditional medicine interactions
  - Adjust formality level based on cultural norms (formal "usted" vs. informal "tu" in Spanish)
  - Verify numerical formatting (date formats, measurement units, decimal separators)
- Engage community health workers or cultural liaisons for validation
- Document cultural adaptations with rationale

### Step 4: Translation Quality Standards
- Apply quality standards aligned with ATA (American Translators Association) framework:
  - Use qualified medical translators (not bilingual staff without translation credentials)
  - Require back-translation for critical documents (consent forms, medication instructions, surgical prep)
  - Implement dual-review process: linguistic review + clinical accuracy review
  - Assess translated readability using target-language readability tools where available
- Quality scoring rubric:
  - Accuracy: Medical concepts correctly conveyed (no omissions, additions, or distortions)
  - Fluency: Natural-sounding in target language (not "translationese")
  - Terminology consistency: Key terms match approved glossary
  - Cultural appropriateness: Content resonates with target audience

### Step 5: Compliance Documentation
- Generate compliance documentation package:
  - Language access plan with threshold analysis
  - Translation log (source, target language, translator credentials, review status, date)
  - Tagline requirements: Include required taglines in top 15 languages (per Section 1557)
  - Nondiscrimination notice in appropriate languages
  - Interpreter services availability notice
- Document process for updating translations when source content changes

### Step 6: Distribution and Access Verification
- Ensure multilingual materials are accessible at point of care:
  - EHR integration for language-matched discharge instructions
  - Patient portal multilingual content availability
  - Printed materials inventory management by language
  - Signage in threshold languages at all patient access points
  - Staff training on how to access and provide translated materials
- Monitor utilization rates by language to identify gaps

## Output Specification

```yaml
multilingual_content:
  source_document:
    title: string
    reading_level: number
    translation_readiness_score: number
  language_threshold_analysis:
    - language: string
      population_percentage: number
      population_count: number
      threshold_met: boolean
      regulatory_basis: string
  translations:
    - language: string
      dialect: string
      translator_credentials: string
      back_translation_completed: boolean
      cultural_adaptations:
        - original_element: string
          adapted_element: string
          rationale: string
      quality_scores:
        accuracy: number
        fluency: number
        terminology_consistency: number
        cultural_appropriateness: number
      clinical_review_status: string
  compliance_package:
    taglines_included: boolean
    nondiscrimination_notice: boolean
    language_access_plan_reference: string
  distribution_plan:
    channels: array
    ehr_integration: boolean
    portal_availability: boolean
```

## Analysis Framework

Apply the **CLAS Standards** (Culturally and Linguistically Appropriate Services) as the overarching framework:
- **Principal Standard**: Provide effective, equitable, understandable, and respectful quality care
- **Governance/Leadership**: Advance CLAS through organizational policies and practices
- **Communication and Language Assistance**: Offer language assistance at no cost, in a timely manner
- **Engagement, Continuous Improvement, Accountability**: Collect and maintain data on language needs, implement improvements

## Examples

**Example: Diabetes Self-Management Education (Spanish)**
- Source: 8th grade English, 12 pages with embedded medication schedule graphics
- Pre-translation simplification reduced to 6th grade, graphics separated for independent translation
- Cultural adaptations: dietary examples changed from generic "whole grains" to "arroz integral, frijoles"; family-centered care model emphasized per Hispanic cultural values; "usted" formality used
- Back-translation completed, 2 medication terms flagged and corrected
- Quality scores: Accuracy 96%, Fluency 92%, Terminology 98%, Cultural Appropriateness 94%

## Guidelines

- **HIPAA Compliance**: Translated materials containing PHI must maintain all HIPAA safeguards. Translators handling PHI must have BAA (Business Associate Agreement) in place. De-identify any materials used for translator training or quality audits.
- **Section 1557 Compliance**: Vital documents must be translated for threshold languages. Taglines in top 15 languages must appear on significant publications. Ensure nondiscrimination notices are posted and distributed.
- **Interpreter vs. Translation**: This skill addresses written translation. For oral interpretation, ensure qualified medical interpreters (not family members or untrained bilingual staff) per Joint Commission PC.02.01.21.
- **Quality Assurance**: Never rely on machine translation alone for patient safety documents. Machine translation may be used as a first draft followed by qualified human review and editing.
- **Continuous Updates**: Establish version control for translated materials. When source content is updated, flag all translations for corresponding updates.

## Validation Checklist

- [ ] Source content simplified to appropriate reading level before translation
- [ ] Language threshold analysis completed with documented data sources
- [ ] Qualified medical translators used (credentials documented)
- [ ] Back-translation completed for critical safety documents
- [ ] Cultural adaptations documented with rationale
- [ ] Quality scoring completed across all four dimensions
- [ ] Clinical accuracy review completed by bilingual clinician
- [ ] Section 1557 taglines included in required languages
- [ ] Nondiscrimination notice included
- [ ] HIPAA safeguards maintained for PHI-containing translations
- [ ] Distribution plan covers all patient access channels
- [ ] Version control established for translation updates
