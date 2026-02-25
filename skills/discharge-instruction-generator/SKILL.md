---
name: Discharge Instruction Generator
description: Generate CMS-compliant, health-literacy-appropriate discharge instruction sets covering medication reconciliation, follow-up care, warning signs, activity restrictions, and patient-specific self-management plans with teach-back verification.

metadata:
  display_name: "Discharge Instruction Generator"
  short_description: "Generate CMS-compliant patient discharge instructions"
  default_prompt: "Generate discharge instruction for my case with clear next steps"
  version: "1.0.0"
  tags:
    - healthcare
  icon_path: "assets/icon.png"
---

# Discharge Instruction Generator

## Overview

This skill generates structured, patient-centered discharge instructions that comply with CMS Conditions of Participation (CoP) for discharge planning (42 CFR 482.43), Joint Commission National Patient Safety Goals, and health literacy best practices. Effective discharge instructions are critical to reducing 30-day readmission rates, currently penalized under the Hospital Readmissions Reduction Program (HRRP). Studies show that patients who do not understand their discharge instructions are 30% more likely to be readmitted or visit the ED within 30 days.

## When to Use

- Generating standardized discharge instruction templates for clinical service lines
- Creating patient-specific discharge summaries from clinical encounter data
- Redesigning discharge workflows to reduce readmission risk
- Preparing for Joint Commission survey readiness on discharge communication standards
- Adapting instructions for special populations (low literacy, LEP, elderly, pediatric caregivers)
- Supporting care transitions programs (Project RED, BOOST, TCM)

## Required Inputs

| Input | Description | Format |
|-------|-------------|--------|
| `encounter_summary` | Clinical encounter details (diagnosis, procedures, complications) | JSON object |
| `medication_list` | Discharge medications with changes from admission | JSON array |
| `follow_up_plan` | Scheduled and recommended follow-up appointments | JSON array |
| `patient_profile` | Age, health literacy level, language, SDoH factors, caregiver availability | JSON object |
| `condition_protocols` | Evidence-based self-management protocols for discharge diagnoses | JSON array |
| `hospital_resources` | Nurse line number, pharmacy contacts, community resources | JSON object |
| `readmission_risk_score` | LACE or HOSPITAL score if available | JSON object |

## Methodology

### Step 1: Clinical Content Assembly
- Extract and organize clinical information into discharge instruction domains per CMS CoP:
  - **Diagnosis Summary**: What happened and what was found (in plain language)
  - **Procedures Performed**: What was done, with expected recovery timeline
  - **Medication Reconciliation**: Complete list with changes clearly marked (NEW, CHANGED, STOPPED, UNCHANGED)
  - **Activity Restrictions**: Specific, time-bound limitations (lifting, driving, bathing, work return)
  - **Diet Instructions**: Specific dietary guidance relevant to condition
  - **Wound/Site Care**: Step-by-step care instructions if applicable
  - **Follow-Up Appointments**: Provider, date/time, location, purpose, preparation needed
  - **Warning Signs**: Red-flag symptoms requiring immediate medical attention
  - **Contact Information**: Who to call and when (nurse line, provider office, 911 criteria)

### Step 2: Medication Reconciliation Section
- Apply Joint Commission NPSG.03.06.01 medication reconciliation requirements:
  - List every discharge medication with: name (generic and brand), dose, route, frequency, purpose, duration
  - Clearly mark changes from preadmission medication list:
    - NEW: "This is a new medicine" with explanation of why it was added
    - CHANGED: "This dose is different" with explanation of what changed and why
    - STOPPED: "Stop taking this medicine" with explanation of why and what replaces it
    - UNCHANGED: "Keep taking this as before"
  - Highlight high-alert medications (anticoagulants, insulin, opioids) with specific safety instructions
  - Include medication timing schedule (visual grid for complex regimens)
  - Flag potential interactions and foods or activities to avoid

### Step 3: Warning Signs (Return Precautions)
- Generate condition-specific red-flag symptom lists:
  - Cardiac: chest pain, severe shortness of breath, rapid heart rate, sudden weight gain above 3 lbs/day
  - Surgical: fever above 101.5F, wound redness or drainage, uncontrolled pain, inability to eat or drink
  - Neurological: sudden severe headache, vision changes, weakness on one side, confusion
  - Infectious: worsening fever, new rash, spreading redness, altered mental status
- Format as clear action triggers: "Go to the Emergency Room RIGHT AWAY if you have..."
- Distinguish between "Call your doctor office" vs. "Call 911 or go to the ER"

### Step 4: Health Literacy Adaptation
- Adjust all content to target reading level (default: 6th grade):
  - Apply Flesch-Kincaid scoring (target 6.0 or lower)
  - Use plain-language medical term substitutions
  - Limit sentences to 15-20 words
  - Use active voice and second person ("you")
  - One instruction per bullet point
- Apply visual design principles:
  - Headers for each section with consistent formatting
  - Numbered steps for sequential instructions
  - Bold or highlight critical safety information
  - White space for notes and questions
  - Consider pictographic medication schedules for very low literacy

### Step 5: Personalization and SDoH Adaptation
- Adapt instructions based on patient-specific factors:
  - **Transportation barriers**: Include telehealth follow-up options, pharmacy delivery info
  - **Food insecurity**: Provide low-cost dietary alternatives, food assistance resources
  - **Caregiver involvement**: Add caregiver-specific instructions and role clarity
  - **Living situation**: Adapt activity restrictions to home environment (stairs, bathroom access)
  - **Insurance/cost concerns**: Include medication assistance programs, generic alternatives, financial counseling
- Incorporate community resources from 2-1-1 or local resource directories

### Step 6: Teach-Back Integration
- Generate teach-back verification prompts for each critical section:
  - Medications: "Can you tell me which medicines are new and when to take them?"
  - Warning signs: "What symptoms should make you call us or go to the ER?"
  - Follow-up: "When is your next appointment and how will you get there?"
  - Self-care: "Can you show me how you will care for your wound or check your blood sugar?"
- Include documentation template for teach-back completion status
- Flag sections where teach-back was not achieved for nursing follow-up

## Output Specification

```yaml
discharge_instructions:
  patient_identifier: string
  encounter_type: string
  discharge_date: date
  readability_scores:
    flesch_kincaid_grade: number
    flesch_reading_ease: number
  sections:
    diagnosis_summary:
      plain_language: string
      clinical_reference: string
    medications:
      - name: string
        dose: string
        frequency: string
        purpose: string
        change_status: string
        special_instructions: string
        high_alert: boolean
    activity_restrictions:
      - restriction: string
        duration: string
        rationale: string
    diet_instructions: string
    wound_care: string
    warning_signs:
      call_doctor: array
      go_to_er: array
    follow_up:
      - provider: string
        date: date
        purpose: string
        preparation: string
    contact_information:
      nurse_line: string
      provider_office: string
      pharmacy: string
      emergency: string
    community_resources: array
  teach_back:
    prompts:
      - section: string
        question: string
        achieved: boolean
    overall_comprehension: string
  cms_compliance:
    discharge_planning_elements_met: array
    gaps_identified: array
```

## Analysis Framework

Apply the **Project RED (Re-Engineered Discharge)** framework with 12 components:
1. Ascertain need for and obtain language assistance
2. Make appointments for follow-up care
3. Plan for follow-up of results pending at discharge
4. Organize post-discharge outpatient services and equipment
5. Identify the correct medicines and a medication management plan
6. Reconcile the discharge plan with national guidelines
7. Teach a written discharge plan the patient understands
8. Educate the patient about their diagnosis and self-management
9. Review what to do if a problem arises (warning signs)
10. Assess the degree of understanding via teach-back
11. Expedite transmission of the discharge summary to follow-up providers
12. Provide telephone reinforcement within 72 hours of discharge

## Examples

**Example: CHF Discharge Instructions**
- Diagnosis summary: "You came to the hospital because your heart was not pumping well enough and fluid built up in your body. This is called heart failure."
- New medication: "Furosemide (Lasix) 40mg. Take 1 tablet every morning. This is a water pill that helps remove extra fluid. You may need to use the bathroom more often."
- Warning signs: "Go to the ER RIGHT AWAY if: You gain more than 3 pounds in one day. You cannot breathe when lying down. You have chest pain that does not go away."
- Follow-up: "See Dr. Smith (your heart doctor) on March 15 at 10:00 AM at the Heart Clinic, 2nd floor. Bring your medicine list and weight log."
- Readability: FK Grade 5.4, Reading Ease 74, Teach-back prompts: 5 sections covered

## Guidelines

- **HIPAA Compliance**: Discharge instructions contain PHI and must be handled with appropriate safeguards. Electronic transmission must use encrypted channels. Templates or examples for quality improvement must be de-identified.
- **CMS Compliance**: Instructions must meet CoP discharge planning requirements (42 CFR 482.43) including medication reconciliation, follow-up plan, and patient/caregiver education documentation.
- **Joint Commission Alignment**: Address NPSG.03.06.01 (medication reconciliation), PC.04.01.05 (discharge instructions), and PC.04.02.01 (care transitions).
- **Readmission Prevention**: For patients with LACE score of 10 or higher or HOSPITAL score of 7 or higher, flag for enhanced discharge planning including 48-hour follow-up call and care transition nurse assignment.
- **Legal Considerations**: Discharge instructions serve as legal documentation that patient education occurred. Ensure teach-back completion is documented in the medical record.

## Validation Checklist

- [ ] All CMS CoP discharge planning elements addressed
- [ ] Medication reconciliation complete with change status for each medication
- [ ] High-alert medications have specific safety instructions
- [ ] Warning signs differentiate "call doctor" from "go to ER" from "call 911"
- [ ] Follow-up appointments include date, time, location, provider, and purpose
- [ ] Readability score at or below 6th grade (Flesch-Kincaid)
- [ ] Teach-back questions generated for every critical section
- [ ] SDoH adaptations applied based on patient profile
- [ ] Community resources included for identified social needs
- [ ] Contact information complete (nurse line, office, pharmacy, emergency)
- [ ] Clinical accuracy review documented
- [ ] HIPAA safeguards applied to all output containing PHI
- [ ] Documentation meets Joint Commission survey readiness standards
