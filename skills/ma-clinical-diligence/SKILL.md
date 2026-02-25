---
name: ma-clinical-diligence
description: Conduct clinical due diligence for healthcare mergers, acquisitions, partnerships, and joint ventures. Use when evaluating acquisition targets' clinical quality, operational performance, regulatory compliance, and integration risks as part of M&A transactions.

metadata:
  display_name: "Ma Clinical Diligence"
  short_description: "Run clinical due diligence for healthcare M&A targets"
  default_prompt: "Analyze my ma clinical diligence and recommend clear next actions"
  version: "1.0.0"
  tags:
    - healthcare
  icon_path: "assets/icon.png"
---

# M&A Clinical Diligence

## Overview

This skill provides a structured framework for evaluating the clinical and operational dimensions of healthcare M&A transactions — hospital acquisitions, physician practice purchases, home health/hospice acquisitions, and health plan mergers. It covers quality of care assessment, regulatory compliance review, medical staff evaluation, clinical integration planning, and risk identification to support informed transaction decisions and post-merger integration.

## When to Use

- Conducting buy-side clinical due diligence on an acquisition target
- Evaluating clinical assets as part of a sell-side preparation
- Assessing clinical integration feasibility for a proposed merger or partnership
- Identifying clinical risks that could affect deal valuation or structure
- Developing post-merger clinical integration plans
- Supporting board-level investment decisions with clinical risk assessments

## Required Inputs

| Input | Description | Format |
|-------|-------------|--------|
| Quality data | Target's quality measures, Star Ratings, accreditation status | Quality reports |
| Financial data | Revenue, cost by service line, payer mix, medical loss ratio | Financial statements |
| Regulatory history | Survey deficiencies, CMS citations, state actions, sanctions | Regulatory records |
| Medical staff data | Provider roster, specialties, employment models, productivity | Staff reports |
| Patient data | Volume, case mix, market share, patient satisfaction | Operational data |
| Legal/compliance | Litigation, compliance investigations, whistleblower actions | Legal records |
| Technology | EHR system, clinical decision support, telehealth capabilities | IT inventory |

## Methodology

### Step 1 — Assess Clinical Quality Profile

Evaluate the target's clinical quality position:

**Quality Metrics Review**:
- CMS Star Ratings (overall and domain-level) with 3-year trend
- HEDIS performance vs. NCQA national percentiles
- Hospital Compare / Care Compare ratings and scores
- Leapfrog Hospital Safety Grade
- AHRQ Patient Safety Indicators (PSI) and Inpatient Quality Indicators (IQI)
- Condition-specific outcomes (mortality, readmission, complication rates)
- Patient experience (HCAHPS/CAHPS scores and percentiles)

**Quality Infrastructure Assessment**:
- Quality department staffing and leadership
- Clinical governance committee structure and effectiveness
- Peer review and credentialing processes
- Clinical protocols, pathways, and order sets
- Quality improvement methodology (Lean, Six Sigma, IHI Model for Improvement)

### Step 2 — Review Regulatory and Compliance Standing

Examine regulatory risk exposure:

- **CMS survey history**: Deficiency citations, condition-level deficiencies, CMPs, immediate jeopardy findings
- **State survey results**: State licensing survey outcomes, Plans of Correction compliance
- **Accreditation status**: Joint Commission, NCQA, URAC, CARF — current status, recent findings
- **OIG/DOJ investigations**: Open or resolved False Claims Act, Anti-Kickback, Stark Law matters
- **EMTALA compliance**: Emergency department compliance history
- **Excluded persons screening**: LEIE/SAM database compliance for all providers and staff
- **Consent decree or corporate integrity agreements**: Active or historical oversight arrangements

### Step 3 — Evaluate Medical Staff and Provider Assets

Assess the clinical workforce:

- **Provider inventory**: Count, specialty mix, board certification rates, average age
- **Employment model**: Employed vs. independent; contract terms, non-compete clauses
- **Productivity benchmarks**: wRVU per provider vs. MGMA medians by specialty
- **Compensation analysis**: Total comp per wRVU vs. market rates (MGMA, SullivanCotter)
- **Retention risk**: Tenure distribution, turnover history, key-person dependencies
- **Recruitment pipeline**: Open positions, recruitment difficulty, J-1/H-1B visa dependencies
- **Credentialing and privileging**: Active credential files, privileging delineation, NPDB query compliance
- **Cultural assessment**: Physician satisfaction, governance participation, alignment with acquirer's model

### Step 4 — Analyze Clinical Operations

Evaluate operational performance:

- **Utilization metrics**: Occupancy, OR utilization, clinic visit capacity, ED throughput
- **Length of stay**: Observed vs. expected by service line, case mix adjusted
- **Operating efficiency**: Cost per case/visit, staffing ratios, supply cost benchmarks
- **Care delivery model**: Care management programs, population health infrastructure, VBC participation
- **Technology platform**: EHR system (platform, version, customization), interoperability capability, clinical decision support maturity
- **Referral patterns**: Inbound/outbound referral volumes, leakage rates, network integrity

### Step 5 — Identify Clinical Integration Risks

Assess integration complexity and risk:

| Risk Category | Factors to Evaluate |
|--------------|---------------------|
| EHR integration | Platform compatibility, data migration complexity, workflow differences |
| Clinical standardization | Protocol alignment, formulary harmonization, order set unification |
| Provider retention | Key physician flight risk, non-compete enforceability, compensation model changes |
| Quality convergence | Time to align quality metrics, cultural differences in quality expectations |
| Regulatory integration | License transfers, CON implications, CMS enrollment updates |
| Patient migration | Patient retention during transition, referral pattern disruption |

Estimate timeline and cost for each integration workstream. Identify deal-breaker risks that could prevent successful integration.

### Step 6 — Quantify Clinical Value and Risk Impact on Valuation

Translate clinical findings into financial implications:

- **Quality premium/discount**: Strong quality → higher Star Ratings → quality bonus revenue potential
- **Regulatory remediation costs**: Estimated investment to resolve deficiencies or compliance gaps
- **Provider retention costs**: Retention bonuses, compensation adjustments to prevent key physician departures
- **Integration costs**: EHR conversion, clinical standardization, training, workflow redesign
- **Revenue synergies**: Cross-referral opportunities, service line complementarity, network completeness
- **Risk provisions**: Malpractice tail coverage, open litigation reserves, compliance remediation

### Step 7 — Produce Diligence Report and Recommendations

Structure the clinical due diligence findings:

- **Overall clinical risk rating**: Low, moderate, high, or critical
- **Key findings**: Top 5 strengths and top 5 risks
- **Deal impact assessment**: Findings that should affect valuation, deal structure, or go/no-go decision
- **Integration planning requirements**: Critical Day 1 items vs. 100-day plan vs. long-term integration
- **Representations and warranties recommendations**: Clinical-specific R&W for the purchase agreement
- **Post-closing monitoring plan**: KPIs and milestones for clinical integration success measurement

## Output Specification

```
Clinical Due Diligence Report:
├── Executive Summary (clinical risk rating, key findings, recommendation)
├── Quality Assessment (metrics, trends, benchmarks, infrastructure)
├── Regulatory and Compliance Review (survey history, open matters, risk rating)
├── Medical Staff Analysis (inventory, productivity, retention risk, compensation)
├── Clinical Operations Review (utilization, efficiency, technology, care model)
├── Integration Risk Assessment (complexity, timeline, cost by workstream)
├── Financial Impact of Clinical Findings (valuation adjustments, synergies, costs)
├── R&W and Indemnification Recommendations
├── Post-Closing Integration Plan (Day 1, 100-day, Year 1 milestones)
└── Clinical Diligence Data Room Index (documents reviewed)
```

## Analysis Framework

### Clinical Risk Rating

| Rating | Criteria | Deal Implication |
|--------|----------|------------------|
| Low | Quality above median, clean regulatory, stable staff | Proceed with standard terms |
| Moderate | Some quality gaps, minor regulatory issues, manageable staff risk | Adjust valuation, add clinical reps |
| High | Below-median quality, significant regulatory findings, retention risk | Material valuation adjustment, enhanced indemnification |
| Critical | Active regulatory action, systemic quality failures, provider exodus | Re-evaluate deal viability |

### Integration Complexity Scoring

| Dimension | Simple (1) | Moderate (2) | Complex (3) |
|-----------|-----------|--------------|-------------|
| EHR | Same platform | Different but compatible | Incompatible, full migration needed |
| Clinical model | Similar protocols | Some differences | Fundamentally different approach |
| Provider model | Same employment type | Mixed but compatible | Conflicting compensation models |
| Geography | Adjacent / overlapping | Same region, different area | Different state / regulatory regime |

## Examples

**Example 1 — Hospital Acquisition Diligence**
Evaluate a 200-bed community hospital acquisition target. Quality: CMS 3-star, HCAHPS below state average, readmission rate 16.2% (national 15.5%). Regulatory: 2 state survey deficiencies (medication management, infection control) corrected within 90 days. Medical staff: 120 credentialed physicians, 3 high-revenue specialists approaching retirement. Clinical risk rating: Moderate. Valuation impact: recommend $3.5M quality improvement investment over 24 months, $1.2M retention package for key specialists, EHR migration cost $8M over 3 years.

**Example 2 — Physician Practice Acquisition**
Due diligence on a 25-provider multi-specialty practice. wRVU productivity: 60th MGMA percentile (strong). Compensation: 75th percentile (slightly above market). Quality: HEDIS measures above 75th percentile. Risk: 3 physicians express uncertainty about employment model transition, 2 have restrictive non-competes expiring within 18 months. Recommend: retention agreements with 2-year cliff vesting, cultural integration plan prioritizing physician governance participation.

## Guidelines

- Request at minimum 3 years of quality data to assess trends, not just point-in-time performance
- Verify regulatory information directly with CMS and state agencies — don't rely solely on target's representations
- Interview key clinical leaders and physicians directly when possible — written data misses cultural dynamics
- Coordinate clinical diligence findings with financial, legal, and operational workstreams
- Identify "Day 1 readiness" items that must be resolved before transaction close (licensure, CMS enrollment, malpractice coverage)
- Consider engaging independent clinical consultants for specialized areas (infection control, pharmacy, behavioral health)

## Validation Checklist

- [ ] Quality data verified against public sources (CMS Care Compare, state databases)
- [ ] Regulatory history checked with primary sources (CMS, state health department, OIG)
- [ ] Provider credentials and licenses independently verified
- [ ] Financial impact estimates are conservative and documented
- [ ] Integration cost estimates include both one-time and ongoing expenses
- [ ] Key person risks identified with specific mitigation plans
- [ ] Report reviewed by clinical, legal, and financial diligence leads for consistency

## HIPAA Compliance

Clinical due diligence involves accessing the target organization's quality, operational, and potentially patient-level data. Pre-transaction access to PHI requires appropriate data use agreements or pre-LOI confidentiality agreements with HIPAA provisions. Post-transaction data access falls under the successor entity's HIPAA obligations. All PHI accessed during diligence must be used under minimum necessary standards, stored in secure data rooms with audit logging, and destroyed or returned per agreement terms if the transaction does not close. Diligence reports must not contain individual patient identifiers; all examples and case references must be de-identified per 45 CFR §164.514.
