---
name: outcomes-attribution
description: Attribute health outcomes to specific clinical interventions, programs, or policy changes using causal inference methods. Use when determining which interventions drove observed improvements, allocating credit across concurrent programs, or defending outcome claims to payers and regulators.

metadata:
  display_name: "Outcomes Attribution"
  short_description: "Attribute health outcomes to clinical interventions"
  default_prompt: "Analyze my outcomes attribution and recommend clear next actions"
  version: "1.0.0"
  tags:
    - healthcare
  icon_path: "assets/icon.png"
---

# Outcomes Attribution

## Overview

This skill applies causal inference and attribution methodologies to determine whether observed health outcome changes can be credibly linked to specific interventions. It employs difference-in-differences, instrumental variables, interrupted time series, and multi-touch attribution models adapted from epidemiology and health services research to produce defensible attribution conclusions.

## When to Use

- Determining which program or intervention caused an observed outcome improvement
- Allocating credit when multiple concurrent interventions could explain results
- Building evidence for value-based care contract performance narratives
- Defending outcome claims in RADV, MSSP, or quality program audits
- Deciding resource allocation among competing programs based on attributed impact

## Required Inputs

| Input | Description | Format |
|-------|-------------|--------|
| Outcome metrics | Time-series outcome data (admissions, costs, quality scores) | Panel data |
| Intervention timeline | Start/end dates, scope, intensity of each intervention | Event log |
| Patient exposure | Which patients were exposed to which interventions and when | Enrollment/assignment |
| Covariates | Demographics, comorbidity, SES, provider characteristics | Patient-level data |
| External factors | Policy changes, seasonal patterns, market events | Context log |
| Comparison data | Outcomes for unexposed or differently-exposed populations | Claims/outcomes |

## Methodology

### Step 1 — Map the Intervention Landscape

Create a comprehensive timeline of all interventions active during the evaluation period:

- Program launches, modifications, and terminations with exact dates
- Policy or formulary changes affecting the population
- Provider network additions or losses
- External events (public health emergencies, competitor market entry)
- Gradual rollouts vs. abrupt implementations (matters for method selection)

Classify each intervention by: target population, mechanism of action (clinical, behavioral, financial, structural), and expected outcome pathway.

### Step 2 — Select Attribution Method

Choose the appropriate causal inference approach based on data structure and intervention characteristics:

| Method | When to Use | Requirements |
|--------|-------------|--------------|
| Difference-in-differences (DID) | Clear treatment/control groups, pre/post data | Parallel trends assumption |
| Interrupted time series (ITS) | Single population, abrupt intervention start | ≥ 8 pre-intervention time points |
| Propensity score matching (PSM) | Observational data, selection bias concerns | Rich covariate data |
| Instrumental variables (IV) | Unmeasured confounding suspected | Valid instrument available |
| Regression discontinuity (RD) | Assignment based on a threshold variable | Sharp/fuzzy assignment cutoff |
| Multi-touch attribution | Multiple concurrent interventions | Patient-level exposure data |

### Step 3 — Test Causal Assumptions

Validate the assumptions underlying the chosen method:

- **DID**: Test parallel trends in pre-intervention period; plot pre-trends visually and test with placebo DID
- **ITS**: Test for autocorrelation (Durbin-Watson), seasonality, and non-stationarity
- **PSM**: Verify covariate balance (SMD < 0.1), common support, and no unmeasured confounders
- **IV**: Test instrument relevance (F-statistic > 10) and exclusion restriction
- Document assumption violations and their potential impact on conclusions

### Step 4 — Estimate Treatment Effects

Calculate the causal effect of each intervention:

- **Average Treatment Effect on the Treated (ATT)**: Impact on patients who actually received the intervention
- **Intent-to-Treat (ITT)**: Impact on all assigned patients regardless of engagement
- **Local Average Treatment Effect (LATE)**: Impact on patients whose behavior was changed by the instrument
- Report point estimates with 95% confidence intervals and p-values
- Calculate effect sizes (Cohen's d, risk ratios, NNT) for clinical interpretability

### Step 5 — Decompose Multi-Intervention Attribution

When multiple programs operate simultaneously, allocate outcome changes:

- **Sequential decomposition**: Attribute based on temporal ordering of intervention starts
- **Shapley value attribution**: Game-theoretic fair allocation across all intervention combinations
- **Mediation analysis**: Trace outcome through intermediate pathways specific to each intervention
- **Exposure-weighted attribution**: Weight by patient-level dose/engagement across programs
- Sum attributed effects and compare to total observed change; report unexplained residual

### Step 6 — Conduct Sensitivity and Robustness Checks

Stress-test attribution conclusions:

- Vary measurement windows (6, 12, 18-month post-intervention)
- Test alternative comparison groups or matching specifications
- Run placebo tests (apply method to periods/populations with no intervention)
- Conduct E-value analysis for unmeasured confounding (how strong would a confounder need to be to nullify results?)
- Report Rosenbaum bounds for PSM sensitivity

### Step 7 — Produce Attribution Report

Structure conclusions with appropriate certainty language:

- **Strong attribution** (multiple methods converge, assumptions validated): "The evidence strongly supports that Program X caused a Y% reduction in Z"
- **Moderate attribution** (single method, assumptions reasonable): "Program X is likely associated with a Y% reduction in Z, though residual confounding cannot be fully excluded"
- **Weak attribution** (assumption violations, limited data): "Program X may have contributed to the observed Y% reduction in Z, but definitive causal claims are not supported by available evidence"

## Output Specification

```
Attribution Report:
├── Intervention Timeline (visual map of all active interventions)
├── Method Selection Rationale (chosen approach with justification)
├── Assumption Validation (test results for causal assumptions)
├── Treatment Effect Estimates (ATT, ITT with CI and p-values)
├── Multi-Intervention Decomposition (attributed share per program)
├── Sensitivity Analysis Results (robustness across specifications)
├── Attribution Confidence Assessment (strong/moderate/weak per claim)
├── Unexplained Residual Analysis (portion not attributed to known interventions)
└── Recommendations (resource allocation implications)
```

## Analysis Framework

### Attribution Confidence Scoring

| Factor | Weak (1) | Moderate (2) | Strong (3) |
|--------|----------|--------------|------------|
| Study design | Pre-post only | Quasi-experimental | Randomized or natural experiment |
| Comparison group | None | Historical or unmatched | Well-matched concurrent |
| Assumption validity | Violations detected | Assumptions plausible | Assumptions verified |
| Effect consistency | Single specification | Consistent across some | Robust across all |
| Biological plausibility | Unclear mechanism | Plausible pathway | Established causal pathway |

Total score: 5-8 = weak, 9-12 = moderate, 13-15 = strong attribution confidence.

### Common Attribution Pitfalls

- **Regression to the mean**: High-cost patients selected into programs naturally regress, mimicking program effect
- **Selection bias**: Patients who enroll/engage differ systematically from those who don't
- **Secular trends**: Background improvements (declining smoking, better medications) mistaken for program impact
- **Contamination**: Control group partially exposed to intervention components
- **Hawthorne effect**: Observation itself changes behavior

## Examples

**Example 1 — Care Management Program Attribution**
A health system runs a CHF care management program alongside a new cardiology telehealth initiative. CHF admissions dropped 25%. ITS analysis on care management (launched 6 months earlier) attributes 18% reduction (95% CI: 12-24%). DID analysis adding telehealth as a second intervention attributes an additional 5% (95% CI: 1-9%). Residual 2% consistent with background trend. Shapley decomposition: 72% care management, 20% telehealth, 8% secular.

**Example 2 — VBC Contract Performance Defense**
An ACO must demonstrate that its 8% total cost reduction is attributable to its interventions (not market changes) for shared savings. Apply DID against non-ACO-attributed patients in the same market. Estimate ATT of 6.2% (p=0.003). Remaining 1.8% explained by regional utilization trend. E-value analysis shows an unmeasured confounder would need RR > 2.8 to nullify, supporting robust attribution.

## Guidelines

- Always prefer quasi-experimental methods over simple pre-post comparisons
- Report ITT as primary analysis; per-protocol as secondary (avoids healthy-participant bias)
- Never claim causation from correlation — clearly state the method and its limitations
- When multiple programs operate concurrently, attribution must sum to ≤ 100% of observed change
- Document all analytical choices (method, specification, comparison group) to enable replication

## Validation Checklist

- [ ] Causal method is appropriate for the data structure and intervention type
- [ ] Key assumptions are explicitly tested and reported
- [ ] Confidence intervals are reported for all effect estimates
- [ ] Sensitivity analyses cover at least 3 alternative specifications
- [ ] Attribution claims use appropriate certainty language
- [ ] Unexplained residual is reported and interpreted
- [ ] Report is structured for peer review or audit scrutiny

## HIPAA Compliance

This skill processes Protected Health Information (PHI) for health care operations including program evaluation and quality improvement. All analyses must comply with HIPAA Privacy and Security Rules. Apply minimum necessary data access standards. Patient-level exposure and outcome data must be stored in access-controlled environments. Report aggregate attribution results only; apply minimum cell-size suppression (n ≥ 11) for sub-group analyses. De-identify data per 45 CFR §164.514 before sharing with external evaluators or auditors.
