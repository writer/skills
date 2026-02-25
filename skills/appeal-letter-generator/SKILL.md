---
name: appeal-letter-generator
description: Generate professionally structured, evidence-based appeal letters for claim denials, prior authorization overturns, and payment disputes with payer-specific formatting and clinical justification. Use when appealing denied claims, overturning prior auth denials, disputing underpayments, or preparing external review submissions.

metadata:
  display_name: "Appeal Letter Generator"
  short_description: "Draft evidence-based healthcare claim denial appeal letters"
  default_prompt: "Generate appeal letter for my case with clear next steps"
  version: "1.0.0"
  tags:
    - healthcare
  icon_path: "assets/icon.png"
---

# Appeal Letter Generator

## Overview

Generate comprehensive, professionally structured appeal letters for healthcare claim denials, prior authorization denials, and payment disputes. This skill produces appeal correspondence that includes proper formatting, clinical justification, regulatory citations, contractual references, and supporting evidence organization — maximizing the probability of successful appeal outcomes.

## When to Use

- Appealing a denied healthcare claim (clinical or administrative)
- Overturning a prior authorization denial
- Disputing an underpayment or incorrect payment
- Preparing for external review or independent review organization (IRO) submissions
- Drafting physician peer-to-peer preparation letters
- Generating batch appeal templates for systemic denial patterns

## Required Inputs

| Input | Description | Format |
|-------|-------------|--------|
| Denial details | CARC/RARC codes, denial reason, denied amount | Structured object |
| Original claim | CPT, ICD-10, dates of service, billed amount | Claim object |
| Clinical documentation | Supporting notes, test results, medical records | Document references |
| Payer information | Payer name, appeals address, plan type, appeal level | Structured object |
| Patient information | Name, member ID, DOB, group number | Structured object |
| Provider information | Name, NPI, credentials, specialty | Structured object |

## Methodology

### Step 1: Denial Analysis

Analyze the denial to determine the appropriate appeal strategy:

**Denial Type Classification:**

| Type | Appeal Strategy | Key Arguments |
|------|----------------|---------------|
| Medical necessity | Clinical justification with guidelines | Peer-reviewed evidence, clinical criteria met |
| Authorization | Retroactive auth or auth correction | Emergency exception, retroactive auth policy |
| Coding/billing | Corrected claim or coding justification | CPT guidelines, NCCI modifier rules |
| Timely filing | Proof of timely submission | Electronic confirmation, mail receipt, prior submissions |
| Eligibility | Eligibility verification evidence | Enrollment records, retroactive eligibility |
| Contractual | Contract term citation | Fee schedule, contract provisions |
| Bundling/NCCI | Distinct service documentation | Modifier justification, separate site/session |

### Step 2: Appeal Level Determination

Identify the correct appeal level and requirements:

**Standard Appeal Levels:**

1. **Level 1 - Internal Reconsideration**: Informal review with additional information. Deadline: typically 60-180 days from denial
2. **Level 2 - Formal Internal Appeal**: Review by physician not involved in original decision. Deadline: 180 days from Level 1 decision
3. **Level 3 - External Review (IRO)**: Independent review by external organization. Deadline: typically 60 days from Level 2 exhaustion
4. **Level 4 - State/Federal Review**: State insurance department or CMS appeal. Deadline: varies by jurisdiction

**Medicare-Specific Appeals:**
1. Redetermination (MAC) — 120 days
2. Reconsideration (QIC) — 180 days
3. ALJ Hearing — 60 days, must meet amount in controversy threshold
4. Medicare Appeals Council — 60 days
5. Federal District Court — 60 days, must meet amount threshold

### Step 3: Evidence Assembly

Organize supporting evidence for maximum impact:

**Required Evidence Checklist:**
- Original claim form and remittance
- Clinical documentation supporting the service
- Relevant lab results, imaging, and test reports
- Physician letter of medical necessity
- Published clinical guidelines supporting the treatment
- Peer-reviewed literature (if applicable)
- Prior authorization documentation (if obtained)
- Payer policy with relevant sections highlighted
- Corrected claim form (if coding appeal)

### Step 4: Letter Construction

Build the appeal letter with these required sections:

**Appeal Letter Structure:**

**Header:**
- Date
- Provider/facility name, address, NPI
- Payer appeals department address
- RE: Appeal for [patient name], Member ID, Claim number, DOS

**Opening Paragraph:**
- State the purpose: appeal of claim denial
- Reference the denial date and CARC/RARC codes
- State the specific relief requested (pay the claim, approve the service, correct the payment)

**Patient Summary (2-3 sentences):**
- Relevant diagnoses and clinical context
- Why the service was needed

**Denial Rebuttal (core of the letter):**
- Address each stated denial reason specifically
- Provide evidence contradicting the denial rationale
- Cite clinical guidelines and medical literature
- Reference payer policy provisions that support coverage
- Include contractual language if payment dispute

**Medical Necessity Argument (if applicable):**
- Patient-specific clinical factors requiring the service
- Prior treatments attempted and their outcomes
- Consequences of not providing the service
- Alignment with evidence-based guidelines (cite specific guidelines)
- Clinical criteria met (InterQual, Milliman, or applicable criteria)

**Regulatory and Legal References:**
- State prompt payment laws
- ERISA requirements (for self-funded plans)
- Mental Health Parity Act (if behavioral health)
- No Surprises Act provisions (if applicable)
- State external review rights

**Closing:**
- Restate the requested action
- Provide contact information for follow-up
- Note appeal deadline compliance
- Request written response within statutory timeframe

**Enclosures List:**
- Itemized list of all supporting documents enclosed

### Step 5: Quality Review

Review the completed letter against success criteria:

- All denial reasons are specifically addressed
- Clinical justification is supported by cited evidence
- Tone is professional and objective (not adversarial)
- Regulatory references are accurate and applicable
- Appeal is submitted within the required deadline
- Correct appeal level and recipient address

## Output Specification

The output includes:

**appeal_metadata**: appeal_level, deadline, submission_method (mail/fax/portal), payer_appeals_address

**appeal_letter**: fully formatted letter text with all required sections

**evidence_checklist**: list of required supporting documents with status (attached/needed/not applicable)

**success_probability**: estimated based on denial type, evidence strength, and historical outcomes

**follow_up_plan**: follow_up_date, escalation_triggers, next_appeal_level_if_denied

## Analysis Framework

### Appeal Success Factors

| Factor | Impact on Success | How to Maximize |
|--------|------------------|-----------------|
| Clinical documentation strength | HIGH | Include detailed notes with specific findings |
| Guideline citation | HIGH | Reference specific guideline sections and recommendations |
| Specificity of rebuttal | HIGH | Address each denial reason individually |
| Timeliness | CRITICAL | File well before deadline |
| Correct appeal level | MEDIUM | Ensure proper sequencing of appeal levels |
| Peer-reviewed literature | MEDIUM | Include relevant studies for novel or disputed treatments |
| Provider credentials | MEDIUM | Include treating physician letter with relevant specialty |
| Payer policy reference | HIGH | Cite the payer's own policy supporting coverage |

### Appeal Success Rates by Denial Type

| Denial Type | Typical Success Rate | Key Success Factor |
|-------------|---------------------|-------------------|
| Medical necessity | 40-60% | Strong clinical documentation + guidelines |
| Authorization (retro) | 50-70% | Urgency documentation, good-cause exception |
| Coding correction | 60-80% | Clear CPT guidelines reference |
| Timely filing | 20-40% | Proof of prior timely submission |
| Payment dispute | 50-65% | Contract terms clearly cited |

## Examples

**Input**: Denial of inpatient admission for CHF exacerbation. CARC 50 (medical necessity). Payer states observation level was appropriate. Patient had 3-day stay with IV diuresis, respiratory distress, and cardiology consult.

**Appeal Letter (abbreviated)**:

RE: Appeal - Medical Necessity for Inpatient Admission
Patient: [Name], Member ID: [ID], DOS: [dates], Claim: [number]

Dear Appeals Committee,

We are writing to appeal the denial of inpatient admission for the above-referenced patient, denied under CARC 50 (not deemed medically necessary). We respectfully request that this determination be reversed and the claim processed for inpatient-level reimbursement.

[Patient] is a 72-year-old with systolic heart failure (EF 25%, ICD-10 I50.22) who presented with acute decompensation including dyspnea at rest, bilateral lower extremity edema, and elevated BNP of 2,450 pg/mL. The clinical presentation met InterQual criteria for inpatient admission...

The patient required continuous IV diuretic therapy (furosemide 80mg IV q8h), continuous telemetry monitoring, and cardiology consultation. The attending physician expected a stay spanning at least two midnights, consistent with CMS Two-Midnight Rule guidance...

Per AHA/ACC Heart Failure Guidelines (2022), patients with acute decompensated heart failure requiring IV diuretics and hemodynamic monitoring warrant inpatient-level care (Class I, Level B recommendation)...

## Guidelines

1. **Be specific, not generic** — generic appeal letters have low success rates
2. **Address each denial reason individually** — do not ignore any stated reason
3. **Let evidence speak** — cite guidelines, literature, and payer policies rather than opinion
4. **Maintain professional tone** — adversarial language reduces credibility
5. **Meet all deadlines** — untimely appeals are dismissed regardless of merit

## Validation Checklist

- [ ] All denial reasons (CARC/RARC) are specifically addressed in the letter
- [ ] Clinical justification is supported by cited evidence-based guidelines
- [ ] Patient-specific clinical details are included (not generic language)
- [ ] Regulatory references are accurate and applicable to the payer type
- [ ] Appeal is within the filing deadline for the applicable appeal level
- [ ] Enclosure list matches the actually attached documentation
- [ ] Contact information and return address are correct
- [ ] Letter is signed by appropriate party (provider, billing manager, patient)

## HIPAA Compliance Notes

- Appeal letters contain extensive PHI and must be transmitted securely
- Use secure fax, encrypted email, or payer portal for submission
- Retain copies of appeals and responses in the patient's billing record
- Clinical documentation shared with payers in appeals is permitted under TPO
- When using third-party appeal services, ensure BAA is in place
- Patient authorization may be needed if the appeal includes sensitive diagnoses (42 CFR Part 2, state mental health laws)
