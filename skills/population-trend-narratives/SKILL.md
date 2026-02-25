---
name: population-trend-narratives
description: Generate plain-language narratives explaining population health trends from clinical, utilization, and cost data. Use when translating statistical trends into stakeholder-ready explanations, writing population health reports, or presenting epidemiological findings to non-technical audiences.

metadata:
  display_name: "Population Trend Narratives"
  short_description: "Narrate population health trends in plain language"
  default_prompt: "Summarize my population trend with key findings and next steps"
  version: "1.0.0"
  tags:
    - healthcare
  icon_path: "assets/icon.png"
---

# Population Trend Narratives

## Overview

This skill transforms quantitative population health metrics — prevalence rates, utilization trends, cost trajectories, and quality scores — into clear, contextualized narratives for clinical leaders, plan administrators, and external stakeholders. It applies epidemiological framing, statistical significance testing, and benchmark contextualization to produce explanations that are accurate, actionable, and accessible.

## When to Use

- Writing quarterly or annual population health status reports
- Explaining year-over-year changes in disease prevalence, utilization, or cost
- Translating dashboard metrics into narrative summaries for leadership briefings
- Contextualizing anomalous trends (spikes, drops, or plateaus) with root-cause hypotheses
- Preparing population health sections for regulatory filings or accreditation submissions

## Required Inputs

| Input | Description | Format |
|-------|-------------|--------|
| Trend metrics | Time-series data for prevalence, utilization, cost, quality | Tabular with timestamps |
| Population denominators | Member counts by period, LOB, geography | Enrollment summaries |
| Benchmark data | HEDIS percentiles, CDC prevalence, CMS Star Ratings | Reference tables |
| Intervention timeline | Program launches, policy changes, provider network changes | Event log |
| Demographic breakdowns | Metrics stratified by age, sex, race/ethnicity, geography | Stratified tables |

## Methodology

### Step 1 — Validate Data Quality and Completeness

Before generating narratives, assess data integrity:

- Check for claims lag impact on recent periods (typically 60-90 day run-out)
- Verify denominator stability (enrollment changes vs. real trend changes)
- Identify data source changes (new EHR integration, claims system migration)
- Flag periods affected by known disruptions (COVID-19, system outages, plan transitions)
- Confirm statistical power: minimum cohort sizes for reliable trend detection

### Step 2 — Calculate Trend Statistics

Apply appropriate statistical methods:

- **Absolute change**: Metric(t) - Metric(t-1)
- **Relative change**: (Metric(t) - Metric(t-1)) / Metric(t-1) × 100
- **Annualized rate**: Normalize partial-year data to annual equivalents
- **Statistical significance**: Chi-square for rate comparisons, t-test for means, confidence intervals
- **Trend direction**: Linear regression slope for multi-period trends, p-value for trend significance

### Step 3 — Contextualize Against Benchmarks

Position observed trends against external references:

- **National benchmarks**: CDC WONDER, BRFSS, NHIS for prevalence; CMS BPCI/MSSP for utilization
- **HEDIS percentiles**: Compare quality measures against NCQA national percentile distributions
- **Peer comparison**: Similar plan size, LOB, and geographic market
- **Internal targets**: Organizational strategic plan goals, VBC contract thresholds
- **Historical context**: 3-5 year trend lines to distinguish signal from noise

### Step 4 — Generate Root-Cause Hypotheses

For each significant trend, develop structured explanations:

- **Programmatic factors**: New care management program, screening campaign, formulary change
- **Demographic shifts**: Aging population, enrollment mix changes, member migration
- **Provider factors**: Network changes, practice pattern variation, staffing changes
- **External factors**: Seasonal variation, public health events, regulatory changes
- **Data artifacts**: Coding practice changes, claims system updates, measurement methodology shifts

Rank hypotheses by evidence strength: confirmed (data-supported), probable (consistent with patterns), possible (plausible but unverified).

### Step 5 — Compose Narrative Sections

Structure narratives using the following framework:

1. **Lead statement**: One sentence summarizing the trend and its significance
2. **Quantification**: Specific numbers with appropriate precision and confidence
3. **Context**: How the trend compares to benchmarks and expectations
4. **Explanation**: Most likely drivers with evidence citations
5. **Implication**: What this means for patient outcomes, costs, or strategic goals
6. **Recommendation**: Suggested actions or areas for further investigation

### Step 6 — Apply Audience-Appropriate Language

Adapt complexity to target audience:

| Audience | Complexity | Jargon Level | Detail Level |
|----------|------------|--------------|--------------|
| Board/executives | Low | Minimal; define all acronyms | High-level with financial impact |
| Clinical leaders | Medium | Clinical terms acceptable | Measure-specific with benchmarks |
| Operational staff | Medium | Operational terms acceptable | Actionable with process detail |
| Regulatory/external | High | Technical precision required | Full methodology documentation |

### Step 7 — Review and Quality-Check Narratives

Before finalizing:

- Verify every number in the narrative matches the source data
- Ensure causal language is appropriately hedged ("associated with" vs. "caused by")
- Confirm denominators and time periods are clearly stated
- Check that trends are not over-interpreted (avoid reading significance into noise)
- Validate that recommended actions logically follow from the evidence presented

## Output Specification

```
Population Trend Narrative:
├── Executive Summary (3-5 key takeaways)
├── Population Overview (size, composition, changes)
├── Prevalence Trends (chronic conditions, emerging patterns)
├── Utilization Trends (inpatient, ED, outpatient, pharmacy)
├── Cost Trends (PMPM, total cost, cost drivers)
├── Quality Trends (HEDIS, Stars, patient experience)
├── Disparity Findings (equity-relevant trend differences)
├── Outlook and Recommendations
└── Methodology and Data Notes
```

## Analysis Framework

### Trend Significance Thresholds

| Metric Type | Minimum Change to Narrate | Statistical Test |
|-------------|---------------------------|------------------|
| Prevalence rate | ≥ 0.5 percentage points | Chi-square, p < 0.05 |
| PMPM cost | ≥ 3% relative change | t-test with CI |
| Utilization rate | ≥ 5% relative change | Poisson regression |
| Quality measure | ≥ 2 percentage points | Proportion test |

### Narrative Quality Rubric

- **Accuracy**: All numbers verified, appropriate precision, no conflation of correlation and causation
- **Completeness**: Trend, context, explanation, and implication all addressed
- **Clarity**: Readable by target audience, no undefined acronyms, logical flow
- **Actionability**: Clear next steps or investigation recommendations

## Examples

**Example 1 — Quarterly Diabetes Prevalence Narrative**
"Type 2 diabetes prevalence in our Medicare Advantage population increased from 14.2% to 15.1% between Q1 and Q4 2025, representing 540 additional diagnosed members. This 0.9 percentage-point increase exceeds the CDC national annual growth rate of 0.3 points, suggesting our enhanced screening program launched in March 2025 is successfully identifying previously undiagnosed cases rather than reflecting true incidence growth. The newly identified cohort skews toward early-stage disease (68% HbA1c 6.5-7.5%), supporting this interpretation. We recommend expanding the screening program to the three clinic sites not yet participating."

**Example 2 — ED Utilization Trend**
"Emergency department visit rates declined 12% year-over-year (from 482 to 424 visits per 1,000 members), with the sharpest decline among CHF patients enrolled in our remote monitoring program (−23%). This reduction is statistically significant (p < 0.001) and outpaces the regional average decline of 4%. The program's 850 enrolled CHF patients accounted for 44% of the total ED reduction, strongly suggesting program attribution."

## Guidelines

- Never present trends without denominator context — a rising count may reflect enrollment growth, not rate increase
- Always report confidence intervals or statistical significance for key trend claims
- Distinguish between clinically meaningful and statistically significant changes
- Use consistent time periods for comparisons; clearly label seasonal vs. annualized data
- Disclose known data limitations (claims lag, incomplete capture, coding changes) in methodology notes

## Validation Checklist

- [ ] All numerical values cross-referenced against source data
- [ ] Time periods clearly stated and consistent across all comparisons
- [ ] Causal claims are evidence-supported and appropriately hedged
- [ ] Target audience complexity level is appropriate
- [ ] Benchmarks are current and sourced
- [ ] Denominator changes are accounted for in trend interpretation
- [ ] Data limitations and caveats are disclosed

## HIPAA Compliance

This skill generates aggregate population-level narratives and should not include individual patient identifiers. All outputs must comply with HIPAA Privacy and Security Rules. Apply minimum cell-size suppression (n ≥ 11) for any sub-group statistics that could enable re-identification. When narratives reference specific patient cohorts or geographic areas, ensure the level of specificity does not permit identification of individuals. De-identify all outputs per 45 CFR §164.514 before external distribution.
