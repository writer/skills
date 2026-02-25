---
name: SDoH Risk Identifier
description: Identify and assess social determinants of health risks using validated screening tools (PRAPARE, AHC-HRSN) to enable targeted resource linkage, care plan adaptation, and health equity improvement across patient populations.

metadata:
  display_name: "Sdoh Risk Identifier"
  short_description: "Screen for social determinants of health risk factors"
  default_prompt: "Review my sdoh risk and highlight top risks and next actions"
  version: "1.0.0"
  tags:
    - healthcare
  icon_path: "assets/icon.png"
---

# SDoH Risk Identifier

## Overview

This skill identifies social determinants of health (SDoH) risks that impact patient health outcomes, care adherence, and experience. It applies validated screening instruments including the PRAPARE (Protocol for Responding to and Assessing Patients Assets, Risks, and Experiences) and the AHC-HRSN (Accountable Health Communities Health-Related Social Needs) screening tool to systematically assess domains such as housing instability, food insecurity, transportation barriers, interpersonal violence, and financial strain. SDoH account for 30-55% of health outcomes (WHO), making identification and intervention essential for value-based care, health equity, and population health management.

## When to Use

- Implementing or enhancing SDoH screening programs in clinical settings
- Analyzing population-level SDoH risk profiles for community health needs assessments (CHNA)
- Adapting care plans and discharge plans based on identified social needs
- Supporting CMS quality programs that incorporate SDoH (SDOH Z-codes, HEDIS measures)
- Evaluating health equity and disparities across patient populations
- Connecting patients to community-based organizations and social services
- Meeting Joint Commission requirements for assessing social determinants

## Required Inputs

| Input | Description | Format |
|-------|-------------|--------|
| `screening_responses` | Patient responses to validated SDoH screening tools | JSON object |
| `patient_demographics` | Age, race, ethnicity, language, insurance type, zip code | JSON object |
| `clinical_data` | Diagnoses, medications, utilization history (de-identified) | JSON object |
| `community_resources` | Available social services by geography and domain | JSON array |
| `screening_tool` | Which tool was used: PRAPARE, AHC_HRSN, custom | String |
| `area_level_data` | Census, ADI, food desert, HPSA designations for patient area | JSON object |

## Methodology

### Step 1: Screening Tool Administration
- Select and administer validated SDoH screening tool:
  - **PRAPARE** (21 core questions across 4 domains):
    - Personal Characteristics: Race, ethnicity, farmworker status, veteran status, language
    - Family and Home: Housing status, housing concerns, address duration
    - Money and Resources: Education, employment, insurance, income, material security, transportation, social support
    - Social and Emotional Health: Stress, safety, refugee status
  - **AHC-HRSN** (10 core screening questions):
    - Housing instability (2 questions)
    - Food insecurity (2 questions)
    - Transportation problems (1 question)
    - Utility help needs (1 question)
    - Interpersonal safety (1 question)
    - Plus supplemental questions on financial strain, employment, family/community support, education, physical activity, substance use, mental health, disabilities
- Ensure screening is conducted in patient preferred language
- Use trauma-informed approach: explain purpose, normalize, ensure confidentiality

### Step 2: Risk Domain Assessment
- Score each SDoH domain based on screening responses:
  - **Housing instability**: Homeless, at risk of eviction, substandard conditions, frequent moves
  - **Food insecurity**: Insufficient food, poor nutrition, reliance on food assistance
  - **Transportation barriers**: Cannot get to appointments, pharmacy, or essential services
  - **Financial strain**: Cannot afford medications, copays, basic needs; medical debt
  - **Interpersonal violence**: Domestic violence, elder abuse, unsafe living situation
  - **Social isolation**: Limited social support, loneliness, caregiver burden
  - **Education/literacy**: Low educational attainment, limited health literacy, digital exclusion
  - **Employment**: Unemployment, underemployment, job insecurity, hazardous work
  - **Legal needs**: Immigration concerns, disability benefits, housing rights
  - **Utilities**: Risk of utility shutoff, inability to maintain safe temperature
- Assign severity per domain: No risk, Low risk, Moderate risk, High risk, Urgent risk

### Step 3: Clinical Impact Correlation
- Map identified SDoH risks to clinical impact indicators:
  - Housing instability: higher ED utilization, medication storage challenges, infection risk
  - Food insecurity: diabetes management failure, malnutrition, growth delay (pediatric)
  - Transportation: no-shows, delayed care, medication non-adherence
  - Financial strain: prescription abandonment, deferred preventive care, late-stage diagnoses
  - Interpersonal violence: injury patterns, mental health impact, non-disclosure of symptoms
- Flag high-risk clinical interactions:
  - Patient with food insecurity plus diabetes: care plan must address nutrition access
  - Patient with housing instability plus COPD: medication storage and environmental triggers
  - Patient with transportation barriers plus chronic disease: telehealth prioritization

### Step 4: ICD-10-CM Z-Code Mapping
- Map identified risks to appropriate ICD-10-CM Z-codes for documentation:
  - Z59.0: Homelessness
  - Z59.1: Inadequate housing
  - Z59.4: Lack of adequate food
  - Z59.7: Insufficient social insurance and welfare support
  - Z60.2: Problems related to living alone
  - Z63.0: Problems in relationship with spouse or partner
  - Z56: Problems related to employment and unemployment
  - Z55: Problems related to education and literacy
  - Z75.3: Unavailability of health-care facilities
- Document Z-codes in clinical record to support population health reporting and reimbursement

### Step 5: Resource Linkage
- Match identified needs to community resources:
  - Query community resource databases (2-1-1, findhelp/Aunt Bertha, Unite Us)
  - Filter by: patient zip code, eligibility criteria, language availability, capacity
  - Prioritize resources with closed-loop referral capability
- Generate resource recommendations per domain:
  - Housing: shelters, rapid rehousing programs, housing authorities, legal aid
  - Food: food banks, SNAP enrollment, WIC, Meals on Wheels, medically tailored meals
  - Transportation: Medicaid non-emergency transport, ride-share programs, volunteer driver programs
  - Financial: charity care enrollment, medication assistance programs, benefit enrollment (SSI, SSDI)
  - Safety: domestic violence hotlines, safe housing, legal protection orders
- Track referral completion (closed-loop referral) and outcome

### Step 6: Population-Level Analysis
- Aggregate individual screening data for population health insights:
  - Prevalence of each SDoH risk by geography, demographics, and clinical cohort
  - Heat maps of SDoH risk concentration by zip code or census tract
  - Correlation analysis: SDoH risk prevalence vs. clinical outcomes (readmissions, ED visits, A1c)
  - Resource gap analysis: where identified needs exceed available community resources
- Support CHNA reporting and community benefit planning
- Inform health equity dashboards and disparity reduction strategies

## Output Specification

```yaml
sdoh_assessment:
  screening_tool_used: string
  screening_date: date
  risk_summary:
    - domain: string
      severity: string
      screening_responses: object
      clinical_impact: array
      z_code: string
  overall_risk_level: string
  resource_recommendations:
    - domain: string
      resources:
        - name: string
          type: string
          contact: string
          eligibility: string
          language_available: array
          referral_status: string
  care_plan_adaptations:
    - clinical_concern: string
      sdoh_interaction: string
      adapted_recommendation: string
  population_analysis:
    total_screened: number
    risk_prevalence:
      - domain: string
        percentage: number
    geographic_hotspots: array
    resource_gaps: array
```

## Analysis Framework

Apply the **WHO Social Determinants Framework** adapted for clinical operationalization:
1. **Structural determinants**: Socioeconomic position, governance, policy (context for understanding)
2. **Intermediary determinants**: Material circumstances, behaviors, biological and psychosocial factors (screening targets)
3. **Health system**: Access, quality, equity of care (intervention points)
4. **Health outcomes**: Morbidity, mortality, functional status, well-being (measurement)

Combine with the **CMS Accountable Health Communities Model** intervention tiers:
- Tier 1: Awareness (screen and inform)
- Tier 2: Assistance (screen, inform, and assist with resource connection)
- Tier 3: Alignment (screen, assist, and align community resources with health system)

## Examples

**Example: Primary Care SDoH Screening Program**
- Population: 2,400 patients screened using AHC-HRSN over 6 months
- Prevalence: Food insecurity 18%, transportation 12%, housing 9%, financial strain 31%, social isolation 14%
- Clinical correlation: Food-insecure diabetic patients had mean A1c 1.4 points higher than food-secure
- Resource linkage: 67% of identified needs received referral, 41% confirmed resource connection (closed-loop)
- Z-code documentation: Increased from 3% to 47% of eligible encounters after implementation
- Geographic hotspot: 3 zip codes accounted for 58% of housing instability identifications

## Guidelines

- **HIPAA Compliance**: SDoH data is part of the medical record and subject to HIPAA protections. Ensure screening responses are stored in EHR with appropriate access controls. Aggregate population data must meet minimum cell sizes for reporting. Never share individual SDoH screening results with non-covered entities without patient authorization.
- **42 CFR Part 2**: If screening identifies substance use, Part 2 protections apply to that information. Ensure proper consent mechanisms.
- **Trauma-Informed Approach**: Train screeners in trauma-informed communication. Never require patients to answer SDoH questions. Explain purpose, ensure confidentiality, and normalize the screening process.
- **Equity Focus**: Analyze screening completion rates by demographics to identify who is and is not being screened. Ensure screening tools are available in threshold languages.
- **Actionability**: Never screen without having resources to offer. Screening that identifies needs without connecting to help can erode patient trust and cause harm.
- **Workflow Integration**: Embed screening in existing clinical workflows (annual wellness visits, intake, care transitions) rather than creating stand-alone processes.

## Validation Checklist

- [ ] Validated screening tool selected and properly administered
- [ ] Screening available in patient preferred languages
- [ ] All SDoH domains assessed with severity scoring
- [ ] Clinical impact correlations documented
- [ ] ICD-10-CM Z-codes mapped and documented
- [ ] Community resources matched to identified needs
- [ ] Closed-loop referral tracking implemented
- [ ] Population-level analysis completed with geographic mapping
- [ ] HIPAA compliance verified for data storage and sharing
- [ ] Trauma-informed screening approach documented and staff trained
- [ ] Screening completion rates analyzed for equity
- [ ] Care plan adaptations generated for clinical-SDoH interactions
