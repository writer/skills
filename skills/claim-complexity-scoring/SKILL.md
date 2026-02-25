---
name: claim-complexity-scoring
description: Score healthcare claim complexity for work queue prioritization by evaluating coding difficulty, payer rules, documentation requirements, denial risk, and financial impact. Use when triaging claims for billing review, assigning claims to staff by expertise level, predicting denial probability, or optimizing revenue cycle workflow efficiency.

metadata:
  display_name: "Claim Complexity Scoring"
  short_description: "Score healthcare claim complexity for work queue triage"
  default_prompt: "Score my claim complexity and explain what to improve"
  version: "1.0.0"
  tags:
    - healthcare
  icon_path: "assets/icon.png"
---

# Claim Complexity Scoring

## Overview

Assign a standardized complexity score to healthcare claims to enable intelligent work queue prioritization, staff assignment by competency level, and proactive intervention on high-risk claims before submission. Claims range from straightforward single-code outpatient encounters to multi-service surgical episodes with complex modifier requirements, bundling rules, and payer-specific documentation thresholds. This skill evaluates multiple dimensions of claim complexity — coding, documentation, payer rules, financial value, and historical denial risk — to produce a composite score that optimizes revenue cycle throughput while concentrating expert attention on claims that need it most.

## When to Use

- Triaging claim work queues for daily billing operations
- Assigning claims to coders or billers based on skill level
- Identifying claims requiring pre-submission audit or review
- Predicting denial probability for proactive intervention
- Optimizing claim submission timing and sequencing
- Evaluating revenue cycle staff training needs based on complexity patterns
- Supporting workload balancing across billing team members
- Quantifying operational complexity for staffing models and productivity benchmarks

## Required Inputs

| Input | Description | Format |
|-------|-------------|--------|
| `claim_data` | CPT/HCPCS codes, ICD-10 diagnoses, modifiers, units, charges | Structured claim object |
| `encounter_context` | Place of service, provider type, date of service, patient type | Structured object |
| `payer_info` | Payer name, plan type, contract status, known billing rules | Structured object |
| `documentation_status` | Clinical documentation availability and completeness indicators | Structured object |
| `historical_denial_data` | Denial rates by CPT/payer combination from organization history | Lookup table |
| `ncci_edits` | Applicable CCI edit pairs and MUE limits for billed codes | Reference data |
| `financial_thresholds` | Organizational thresholds for high-value claim review | Configuration object |

## Methodology

### Step 1: Coding Complexity Assessment

Evaluate the intrinsic coding complexity of the claim:

**Code Volume and Diversity:**
- Single CPT code: Base complexity = 1
- 2-5 CPT codes: Base complexity = 2
- 6-10 CPT codes: Base complexity = 3
- 11+ CPT codes: Base complexity = 5

**Code Type Weighting:**

| Code Type | Complexity Weight | Rationale |
|-----------|------------------|-----------|
| E/M (99201-99499) | 1.0 | Standard, well-defined documentation requirements |
| Surgery (10000-69999) | 2.5 | Bundling rules, modifier requirements, global periods |
| Radiology (70000-79999) | 1.5 | Component billing, professional/technical splits |
| Pathology (80000-89999) | 1.5 | Panel rules, specimen requirements |
| Medicine (90000-99199) | 1.5 | Diverse rules, infusion hierarchies |
| HCPCS Level II (A-V) | 2.0 | DME coverage rules, NDC requirements for drugs |
| Category III / Unlisted | 3.5 | Requires special reports, pricing by report |

**Modifier Complexity:**
- No modifiers: +0
- Standard modifiers (25, 59, 76): +0.5 each
- High-complexity modifiers (22, 62, 66, multiple surgery modifiers): +1.5 each
- Bilateral, multiple procedure discount implications: +1.0

### Step 2: Bundling and Edit Analysis

Assess the risk of NCCI and payer-specific edit failures:

- **NCCI Column 1/Column 2 edits**: Identify code pairs subject to bundling; check modifier indicator
- **Medically Unlikely Edits (MUE)**: Verify units billed do not exceed MUE limits
- **Payer-specific edits**: Known proprietary edits beyond NCCI (e.g., UHC Claim Edit System, Anthem iExchange edits)
- **Global period conflicts**: Check if procedures fall within another procedure's global surgical period
- **Add-on code validation**: Verify add-on codes are billed with appropriate primary codes

**Edit Risk Scoring:**
- No applicable edits: +0
- Edits present with appropriate modifiers: +1
- Edits present, modifier appropriateness uncertain: +3
- Known payer-specific edit history for this code combination: +4

### Step 3: Payer Rule Complexity

Score the payer-specific billing requirements:

| Payer Factor | Low (1 pt) | Medium (2 pts) | High (3 pts) |
|-------------|------------|-----------------|---------------|
| Prior auth | Not required | Standard auth obtained | Complex auth, multi-service |
| Medical necessity | Standard LCD | Restrictive LCD with specific criteria | No LCD, coverage uncertain |
| Timely filing | 180+ days remaining | 90-180 days | Under 90 days |
| Contract status | In-network, standard | In-network, complex contract | Out-of-network or SCA |
| Known denial history | Under 5% for this code | 5-15% | Over 15% |
| Coordination of benefits | Primary only | Secondary, known primary EOB | Tertiary or COB disputes |

### Step 4: Documentation Risk Assessment

Evaluate whether the supporting clinical documentation will withstand payer scrutiny:

- **E/M documentation**: Does the note support the billed level? (Audit score comparison)
- **Surgical documentation**: Does the operative report describe all billed procedures distinctly?
- **Medical necessity**: Does the documentation support the diagnosis-to-procedure medical necessity linkage?
- **Signature and authentication**: Are all required signatures, dates, and attestations present?
- **Addenda risk**: Were late addenda added that might raise payer suspicion?

**Documentation Risk Score:**
- Complete, well-documented, supports all codes: +0
- Minor gaps, likely supportable: +1
- Moderate gaps, may require query or addendum: +3
- Significant gaps, documentation does not clearly support codes: +5

### Step 5: Financial Impact Weighting

Incorporate the financial significance of the claim:

| Charge Range | Weight Multiplier | Review Trigger |
|-------------|-------------------|----------------|
| Under $500 | 0.5x | Standard processing |
| $500 - $2,500 | 1.0x | Standard processing |
| $2,500 - $10,000 | 1.5x | Recommended pre-bill review |
| $10,000 - $50,000 | 2.0x | Required pre-bill review |
| Over $50,000 | 3.0x | Senior coder/auditor review required |

### Step 6: Composite Score Calculation

Calculate the final complexity score:

```
raw_score = (coding_complexity × code_weight)
          + edit_risk_score
          + payer_rule_score
          + documentation_risk_score

composite_score = raw_score × financial_multiplier
```

**Complexity Tiers:**

| Score Range | Tier | Routing | Expected Processing Time |
|-------------|------|---------|--------------------------|
| 0-5 | Tier 1 - Simple | Auto-submission or junior biller | Under 5 minutes |
| 6-12 | Tier 2 - Standard | Experienced biller | 5-15 minutes |
| 13-20 | Tier 3 - Complex | Senior coder review | 15-30 minutes |
| 21-30 | Tier 4 - High Complexity | Coding specialist or auditor | 30-60 minutes |
| 31+ | Tier 5 - Critical | Senior auditor + supervisor review | 60+ minutes |

### Step 7: Work Queue Assignment

Route claims to appropriate staff and queues based on complexity tier:

- **Auto-adjudication candidates** (Tier 1): Claims with established patterns, clean history, low financial risk
- **Standard queue** (Tier 2): Routine claims processed by experienced billing staff
- **Specialist queue** (Tier 3-4): Complex claims requiring coding expertise, edit resolution, or pre-bill audit
- **Escalation queue** (Tier 5): High-risk, high-value claims requiring multidisciplinary review
- **Rush queue** (any tier): Claims approaching timely filing deadlines, regardless of complexity

## Output Specification

```yaml
claim_complexity_assessment:
  claim_id: string
  date_of_service: string
  total_charges: number
  complexity_score: number
  complexity_tier: string  # Tier 1-5
  routing_recommendation: string
  scoring_breakdown:
    coding_complexity: number
    edit_risk: number
    payer_rule_complexity: number
    documentation_risk: number
    financial_multiplier: number
  risk_flags:
    - flag: string
      severity: string  # low, medium, high, critical
      description: string
      recommended_action: string
  denial_probability: number  # percentage
  estimated_processing_time: string
  staff_assignment:
    required_skill_level: string
    queue: string
    priority: number
  pre_submission_actions:
    - action: string
      reason: string
      deadline: string
```

## Analysis Framework

### Denial Probability Model

Map complexity scores to expected denial rates based on historical data:

| Complexity Tier | Historical Denial Rate | Preventable Denial Rate |
|----------------|----------------------|------------------------|
| Tier 1 | 1-3% | Under 1% |
| Tier 2 | 3-8% | 1-3% |
| Tier 3 | 8-15% | 3-7% |
| Tier 4 | 15-25% | 5-12% |
| Tier 5 | 25-40% | 10-20% |

### Productivity Benchmarking

Align complexity scoring with revenue cycle productivity standards:

- **Tier 1 claims**: Target 30-40 claims per hour per biller
- **Tier 2 claims**: Target 15-25 claims per hour per biller
- **Tier 3 claims**: Target 6-12 claims per hour per coder
- **Tier 4 claims**: Target 3-6 claims per hour per specialist
- **Tier 5 claims**: Target 1-3 claims per hour per auditor

## Examples

**Example: Multi-level Spine Surgery Claim**

- CPT codes: 22612, 22614 x2, 63047, 63048, 22840, 20930
- Modifiers: 51, 59, 62 (co-surgery)
- Payer: Aetna Commercial PPO
- Total charges: $185,000
- Coding complexity: 5 (11+ lines) + surgery weight (2.5) = 12.5
- Edit risk: NCCI edits between fusion and decompression codes, modifier 59 required (+3)
- Payer complexity: Prior auth obtained, but co-surgery requires separate auth verification (+2)
- Documentation risk: Complex operative note, must describe each level distinctly (+2)
- Financial multiplier: 3.0x (over $50,000)
- Composite score: (12.5 + 3 + 2 + 2) × 3.0 = 58.5 → Tier 5 (Critical)
- Routing: Senior auditor review required, operative note audit, auth verification before submission

## Guidelines

1. **Recalibrate scoring models quarterly** — adjust weights based on actual denial outcomes
2. **Incorporate payer-specific historical data** — generic scoring is less accurate than payer-specific models
3. **Use complexity scores for staffing models** — translate scores to time estimates for FTE planning
4. **Flag outlier scores** — unusually high or low scores may indicate data quality issues
5. **Integrate with clearinghouse edits** — pre-submission editing catches errors before payer adjudication
6. **Review auto-submission thresholds regularly** — ensure Tier 1 auto-submission does not generate excessive denials
7. **Train staff on complexity tiers** — align training curriculum to the complexity levels staff are assigned

## Validation Checklist

- [ ] Coding complexity assessed with code volume, type weighting, and modifier analysis
- [ ] NCCI and MUE edits evaluated with modifier appropriateness determined
- [ ] Payer-specific rules scored including authorization, medical necessity, and filing deadlines
- [ ] Documentation risk assessed against coding and medical necessity requirements
- [ ] Financial impact multiplier applied based on total claim value
- [ ] Composite score maps to defined complexity tier with routing recommendation
- [ ] Denial probability estimated based on historical data for similar claims
- [ ] Pre-submission actions identified for Tier 3+ claims
- [ ] Work queue assignment matches staff competency levels
- [ ] Scoring model validated against actual denial outcomes

## HIPAA Compliance Notes

- Claim complexity scoring involves processing PHI including diagnoses, procedures, and provider information (45 CFR 164.501)
- Scoring algorithms accessing patient-level claim data require role-based access controls (45 CFR 164.312(a))
- Work queue displays containing patient information must be secured per workstation security standards (45 CFR 164.310(c))
- Aggregate complexity analytics used for staffing and benchmarking should be de-identified where possible
- Maintain audit logs for all claim access and routing decisions (45 CFR 164.312(b))
- Third-party scoring tools must have Business Associate Agreements in place (45 CFR 164.502(e))
