---
name: underwriting-consistency-checker
description: Detect underwriting bias, inconsistency, and disparate treatment across loan decisions. Use when performing fair lending audits, reviewing underwriter discretion patterns, analyzing exception-to-policy rates, or preparing for regulatory examinations under ECOA, HMDA, and fair lending frameworks.

metadata:
  display_name: "Underwriting Consistency Checker"
  short_description: "Check loan underwriting for bias, consistency, and fairness"
  default_prompt: "Check my underwriting consistency for gaps risks and required fixes"
  version: "1.0.0"
  tags:
    - financial-services
  icon_path: "assets/icon.png"
---

# Underwriting Consistency Checker

## Overview

Systematically analyze underwriting decisions to detect inconsistency, potential bias, and disparate treatment. This skill compares decisions across similarly situated borrowers, evaluates exception-to-policy rates by demographic segments, and identifies underwriter-level patterns that may indicate conscious or unconscious bias. Outputs support fair lending examination preparedness, HMDA analysis, and internal audit remediation.

## When to Use

- Conducting periodic fair lending reviews and self-assessments
- Preparing for regulatory examinations (OCC, CFPB, state AG)
- Analyzing underwriter override and exception patterns
- Reviewing HMDA data for disparate impact indicators
- Investigating complaints of discriminatory lending practices
- Benchmarking consistency across branches, regions, or channels

## Required Inputs

| Input | Description | Format |
|-------|-------------|--------|
| Decision log | Complete application decisions with timestamps | Database extract or CSV |
| Borrower profiles | Credit, income, collateral, demographics (HMDA fields) | Structured data |
| Underwriter IDs | Anonymized underwriter identifiers | Keyed to decisions |
| Policy rules | Current credit policy with overlays | Policy document |
| Exception log | All exception-to-policy approvals with justification | Exception tracking system |
| HMDA LAR | Loan Application Register with required fields | HMDA-format data |

## Methodology

### Step 1 — Construct Similarly Situated Borrower Groups

Define comparison groups using objective, non-prohibited credit factors:

- **Credit score bands**: 580–619, 620–659, 660–699, 700–739, 740–779, 780+
- **DTI buckets**: <30%, 30–36%, 36–43%, 43–50%, >50%
- **LTV tiers**: <60%, 60–75%, 75–80%, 80–90%, 90–95%, >95%
- **Product type**: Conventional, FHA, VA, USDA, jumbo, non-QM
- **Loan purpose**: Purchase, rate/term refinance, cash-out refinance

Group borrowers who share the same band across all objective factors. These are "similarly situated" for comparison purposes.

### Step 2 — Compute Outcome Disparities

Within each similarly situated group, calculate:

- **Approval rate differential** by race/ethnicity, sex, age cohort
- **Pricing differential** (rate spread) by demographic segments
- **Condition frequency** — additional conditions imposed by segment
- **Time-to-decision** variance by segment
- **Withdrawal/incomplete rates** by segment (potential steering indicator)

Apply statistical significance tests (Fisher's exact test for small samples, chi-squared for larger) and practical significance thresholds (>2 percentage points or odds ratio >1.5).

### Step 3 — Analyze Exception-to-Policy Patterns

Examine exceptions across dimensions:

- Exception rate by underwriter (identify outliers > 2 standard deviations)
- Exception rate by borrower demographic segment
- Exception type distribution (DTI waiver, LTV waiver, credit score waiver)
- Exception justification quality (documented compensating factors vs. vague rationale)
- Favorable vs. unfavorable exception distribution by demographic

Flag any pattern where a protected class receives systematically fewer favorable exceptions or more unfavorable exceptions than similarly situated non-protected class applicants.

### Step 4 — Underwriter-Level Consistency Scoring

For each underwriter, calculate:

- **Decision concordance rate** — agreement with model recommendation
- **Override direction bias** — ratio of approve-overrides to deny-overrides
- **Condition severity index** — average burden of conditions imposed
- **Demographic consistency score** — variance in outcomes across protected classes for similarly situated applicants
- **Peer benchmarking** — deviation from median underwriter behavior

Generate an underwriter consistency scorecard ranking individuals by risk of inconsistent treatment.

### Step 5 — Regression-Based Disparate Impact Testing

Run logistic regression on approval/denial outcomes:

- **Dependent variable**: Binary approval outcome
- **Control variables**: FICO, DTI, LTV, reserves, employment tenure, loan amount
- **Test variables**: Race/ethnicity, sex, age (prohibited basis factors)

If any prohibited basis variable is statistically significant (p < 0.05) after controlling for legitimate credit factors, flag for disparate impact investigation. Report marginal effects and odds ratios.

### Step 6 — Matched-Pair Analysis

Select specific case pairs for deep review:

- Identify denied minority applicants and approved non-minority applicants with comparable or weaker credit profiles
- Document the specific factors that differentiated the two decisions
- Assess whether the differentiation is supported by legitimate, documented business reasons
- Prepare case narratives for regulatory examination defense or remediation

### Step 7 — Generate Findings and Remediation Plan

Compile findings into a structured report with:

- Executive summary of consistency metrics
- Specific disparities identified with statistical support
- Underwriter-level remediation recommendations
- Policy modification suggestions to reduce discretionary inconsistency
- Training recommendations for identified gaps
- Monitoring framework for ongoing surveillance

## Output Specification

```
## Underwriting Consistency Analysis Report

### Executive Summary
- Analysis period: [Date range]
- Applications reviewed: [N]
- Underwriters assessed: [N]
- Overall consistency score: [X/100]

### Disparate Treatment Indicators
| Metric | Control Group | Test Group | Differential | Significance |
|--------|--------------|------------|--------------|--------------|
| Approval rate | XX% | XX% | X pp | p = X.XXX |
| Avg rate spread | X.XX% | X.XX% | X bps | p = X.XXX |
| Exception rate | XX% | XX% | X pp | p = X.XXX |
| Avg conditions | X.X | X.X | X.X | p = X.XXX |

### Exception Analysis
- Total exceptions: [N] ([X]% of decisions)
- Favorable exception disparity: [Finding]
- Underwriters with outlier exception rates: [List]

### Underwriter Consistency Scorecards
| Underwriter | Concordance | Override Bias | Demographic Score | Risk Tier |
|-------------|-------------|---------------|-------------------|-----------|
| [ID] | XX% | X.XX | XX/100 | [Low/Med/High] |

### Regression Results
- Prohibited basis variables significant: [Yes/No — details]
- Marginal effects: [Table of coefficients]

### Matched-Pair Cases
- Pairs identified: [N]
- Pairs requiring remediation: [N]
- [Case narrative summaries]

### Remediation Recommendations
1. [Specific action item with responsible party and deadline]
2. [Specific action item with responsible party and deadline]
```

## Analysis Framework

Apply the **DICE** framework:

- **D**isparities — Quantify outcome differences across protected classes
- **I**nconsistencies — Identify underwriter-level behavioral outliers
- **C**ontrols — Ensure legitimate credit factors are properly controlled
- **E**vidence — Support every finding with statistical and case-level evidence

## Examples

**Example 1 — Branch-Level Disparity Detection**

Finding: Branch 14 approves Hispanic applicants at 62% vs. 78% for non-Hispanic White applicants in the 680–719 FICO band with comparable DTI/LTV profiles. Fisher's exact test p = 0.003. Exception rate for Hispanic applicants is 4% vs. 12% for non-Hispanic White. Recommendation: Mandatory second-look program, underwriter retraining, policy overlay review.

**Example 2 — Underwriter Override Pattern**

Finding: Underwriter UW-207 overrides model denials to approve at 22% rate (peer median: 8%). Override beneficiaries are 91% non-minority. Approve-override justifications cite "strong compensating factors" but documentation is sparse in 65% of cases. Recommendation: Enhanced documentation requirements, supervisory review for all UW-207 overrides pending investigation.

## Guidelines

- Use anonymized underwriter IDs in all reports to maintain objectivity
- Apply both statistical significance (p < 0.05) and practical significance (>2pp or OR >1.5)
- Control for all legitimate credit factors before drawing disparate impact conclusions
- Document the regression model specification, variable definitions, and exclusion criteria
- Maintain matched-pair files in a format suitable for regulatory examination production
- Update the analysis quarterly and immediately after policy changes
- Coordinate findings with Legal and Compliance before external distribution
- Preserve all underlying data and workpapers for the full regulatory retention period

## Validation Checklist

- [ ] Similarly situated groups are defined using only legitimate credit factors
- [ ] Sample sizes are sufficient for statistical testing in each comparison cell
- [ ] Regression controls include all material credit variables available
- [ ] Exception analysis covers both favorable and unfavorable exceptions
- [ ] Underwriter scorecards use consistent methodology across all individuals
- [ ] Matched-pair narratives document specific decision-differentiating factors
- [ ] Findings distinguish statistical significance from practical significance
- [ ] Remediation recommendations are specific, actionable, and time-bound
- [ ] Report has been reviewed by Legal/Compliance before distribution
- [ ] Monitoring cadence is established for ongoing surveillance
