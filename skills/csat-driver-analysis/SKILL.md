---
name: CSAT Driver Analysis
description: Explain changes in Customer Satisfaction (CSAT) scores by decomposing them into contributing factors across service dimensions, identifying the operational and experiential drivers behind score movements with statistical rigor.

metadata:
  display_name: "Csat Driver Analysis"
  short_description: "Decompose CSAT score changes into operational root drivers"
  default_prompt: "Analyze my csat driver and recommend clear next actions"
  version: "1.0.0"
  tags:
    - cpg-retail
  icon_path: "assets/icon.png"
---

# CSAT Driver Analysis

## Overview

This skill diagnoses why Customer Satisfaction (CSAT) scores changed — whether improving or declining — by decomposing aggregate score movements into the specific operational and experiential factors driving them. It goes beyond reporting "CSAT dropped 3 points" to explain that "CSAT dropped 3 points, primarily driven by a 12-point decline in delivery speed satisfaction among BOPIS customers in the Northeast region, which correlates with the carrier transition completed in Week 42." This enables targeted, evidence-based corrective action rather than broad, unfocused CX programs.

## When to Use

- When CSAT scores show a statistically significant change (up or down) from the prior period
- During quarterly business reviews to explain CX performance to leadership
- When evaluating the impact of specific operational changes on customer satisfaction
- To identify which service dimensions offer the greatest CSAT improvement potential
- When CSAT scores diverge across segments, channels, or regions and the cause is unclear
- To build a data-driven case for CX investment prioritization

## Required Inputs

| Input | Description | Format |
|-------|-------------|--------|
| `csat_responses` | Individual survey responses with scores, timestamps, and customer identifiers | Tabular |
| `survey_dimensions` | Sub-scores by dimension (product quality, delivery, service, value, ease) | Included in survey data |
| `customer_attributes` | Segment, tenure, channel, region, order type for each respondent | Tabular |
| `operational_metrics` | Delivery times, wait times, first-contact resolution, stockout rates by period | Tabular |
| `verbatim_comments` | Open-ended survey text responses | Text field in survey data |
| `change_log` | Operational, policy, or system changes during the analysis period | Event log |
| `historical_csat` | At least 12 months of historical CSAT data for trend and seasonality analysis | Time series |

## Methodology

### Step 1 — Score Decomposition

Break the aggregate CSAT change into its mathematical components:

1. **Dimensional Decomposition**: If CSAT is computed from multiple sub-dimensions (e.g., product, service, delivery, value, ease), calculate each dimension's contribution to the overall score change using a weighted decomposition:
   - Contribution of Dimension D = (Score Change in D) x (Weight of D in overall CSAT formula).
   - If weights are derived from regression (importance weights), re-estimate periodically to account for shifting customer priorities.

2. **Segment Decomposition**: Decompose the overall CSAT change by customer segment:
   - Mix Effect: Did the responding population shift toward a segment with inherently lower/higher satisfaction?
   - Rate Effect: Did satisfaction change within segments?
   - Formula: Total Change = Sum of (segment weight change x base score) + Sum of (base weight x segment score change) + interaction terms.

3. **Channel Decomposition**: Repeat the decomposition by channel (in-store, online, mobile, contact center) to identify channel-specific drivers.

### Step 2 — Driver Identification via Key Driver Analysis (KDA)

Determine which factors most influence overall CSAT:

1. **Derived Importance**: Run a regression model with overall CSAT as the dependent variable and dimensional sub-scores as independent variables. Standardized coefficients reveal derived importance (what actually drives satisfaction, which may differ from stated importance).
2. **Stated Importance**: If available, compare with direct customer ratings of importance for each dimension.
3. **Priority Matrix Construction**: Plot each dimension on a 2x2 matrix:
   - **High Importance / Low Performance**: Priority improvement areas (primary action targets).
   - **High Importance / High Performance**: Strengths to maintain and protect.
   - **Low Importance / Low Performance**: Monitor but deprioritize.
   - **Low Importance / High Performance**: Potential over-investment — consider reallocation.

### Step 3 — Operational Correlation

Link satisfaction changes to specific operational metrics:

1. **Lag-Adjusted Correlation**: Calculate Pearson or Spearman correlation between operational metrics (delivery time, wait time, resolution rate) and CSAT sub-scores, applying appropriate time lags (survey responses reflect experiences from 1-14 days prior).
2. **Threshold Detection**: Identify non-linear relationships — satisfaction often has threshold effects (e.g., delivery up to 3 days has high satisfaction, 4-5 days moderate, 6+ days precipitous decline). Use piecewise regression or decision tree analysis to detect thresholds.
3. **Change Point Analysis**: Align operational metric changes with CSAT inflection points. When an operational metric crossed a threshold during the period, flag it as a probable driver.

### Step 4 — Verbatim Analysis

Mine open-ended comments for causal explanations:

1. **Theme Extraction**: Apply topic modeling to extract dominant themes from verbatim comments. Compare theme prevalence between the current and prior period.
2. **Sentiment Analysis**: Score verbatims by sentiment intensity. Identify themes with the most negative sentiment and the largest sentiment shift.
3. **Quote Selection**: Select representative verbatim quotes (anonymized) for each major driver to bring the data story to life in presentations.
4. **Emerging Issues**: Flag themes that appear in the current period but were absent in the prior period — these are new issues that need immediate attention.

### Step 5 — Synthesis and Recommendation

Produce the integrated driver narrative:

1. **Headline Finding**: One sentence stating the primary driver of CSAT change with quantification.
2. **Supporting Drivers**: 2-3 additional factors with their contribution magnitude.
3. **Offsetting Factors**: Areas that improved and partially offset declines (or vice versa).
4. **Recommended Actions**: Specific interventions targeting the primary and secondary drivers, with expected CSAT point impact estimated from historical sensitivity analysis.
5. **Monitoring Plan**: Which metrics to watch weekly to detect whether the driver is improving or worsening.

## Output Specification

Produce a driver analysis report containing:

- `period`: Analysis period and comparison period
- `overall_csat`: Current score, prior score, change, and statistical significance (p-value and confidence interval)
- `dimensional_contributions`: Array of dimensions, each with current score, prior score, change, weight, contribution to overall change, and derived importance rank
- `segment_decomposition`: Mix effects and rate effects by customer segment
- `channel_decomposition`: CSAT change broken out by channel with volume weights
- `key_drivers`: Array of operational factors, each with correlation to CSAT, threshold values, current performance relative to threshold, and estimated CSAT impact if improved
- `verbatim_themes`: Array of themes with prevalence, sentiment score, sentiment change, and representative anonymized quotes
- `priority_matrix`: Importance vs. performance classification for each dimension
- `recommendations`: Prioritized actions with target driver, expected CSAT point improvement, implementation complexity, and timeline
- `confidence_notes`: Sample size adequacy, response bias assessment, and analytical limitations

## Analysis Framework

Apply the **CSAT Diagnostic Hierarchy**:

1. **Level 1 — Is the change real?** Validate statistical significance. With typical retail survey sample sizes, a 1-2 point change may be noise. Apply confidence intervals and minimum sample thresholds (n >= 100 per segment for reliable subsegment analysis).
2. **Level 2 — Where is the change?** Decompose by dimension, segment, channel, and geography to localize the change.
3. **Level 3 — What caused the change?** Correlate localized changes with operational metrics and verbatim themes.
4. **Level 4 — What should we do?** Prioritize actions using the importance-performance priority matrix and estimated ROI.
5. **Level 5 — Is it working?** Define leading indicators to monitor weekly so that intervention effectiveness is visible before the next survey wave.

## Examples

**Example CSAT Driver Analysis**:

Overall CSAT declined from 82.4 to 79.1 (-3.3 points, p < 0.01, n=4,280).

Dimensional decomposition: Delivery satisfaction contributed -2.1 points (64% of decline), ease of returns contributed -0.8 points (24%), and product quality contributed -0.4 points (12%).

Segment analysis: The decline was concentrated in BOPIS customers (-7.2 points) while ship-to-home customers were stable (-0.3 points). BOPIS volume mix increased from 28% to 35% of orders, amplifying the impact.

Operational correlation: BOPIS wait time increased from an average of 4.2 minutes to 11.8 minutes during the period, crossing the 8-minute satisfaction threshold identified in historical analysis. This correlates with a warehouse management system migration in Week 42 that disrupted pick-and-stage workflows.

Recommendation: (1) Deploy temporary manual pick process for BOPIS orders to reduce wait time below 6 minutes while WMS issues are resolved (expected +1.5 CSAT points). (2) Proactively communicate wait time estimates via SMS to reduce perceived wait frustration (expected +0.5 CSAT points). (3) Expedite WMS fix with vendor, target completion Week 46.

## Guidelines

- Never report CSAT changes without statistical significance testing. Sample sizes below 30 per subgroup should be flagged as unreliable.
- Distinguish between CSAT scale types (1-5, 1-7, 1-10, top-box percentage) and ensure all comparisons use the same methodology.
- Beware of response bias — customers with extreme experiences (very positive or very negative) are overrepresented in survey responses. Note this limitation.
- Use derived importance (from regression) over stated importance (from direct questions) — customers consistently overstate the importance of price and understate the importance of convenience.
- Account for survey fatigue effects — CSAT scores collected at the end of long surveys tend to be lower than those collected in short, focused surveys.
- When correlating operational metrics with CSAT, test for confounding variables. Delivery speed and product availability may both correlate with CSAT but the true driver may be stockouts causing substitution dissatisfaction.
- Include confidence intervals on all point estimates and clearly state analytical limitations.
- Present findings with customer verbatim quotes to make the analysis emotionally resonant for decision-makers.

## Validation Checklist

- [ ] CSAT change tested for statistical significance with p-value and confidence interval reported
- [ ] Sample sizes verified as adequate for each subgroup analysis (minimum n=30, target n=100)
- [ ] Dimensional decomposition sums to the total change (residual under 0.5 points)
- [ ] Segment decomposition correctly separates mix effects from rate effects
- [ ] Key driver analysis uses derived importance (regression-based), not just stated importance
- [ ] Operational correlations account for appropriate time lags between experience and survey response
- [ ] Threshold effects identified using non-linear analysis, not just linear correlation
- [ ] Verbatim analysis uses representative, anonymized quotes — no cherry-picking
- [ ] Recommendations include estimated CSAT point impact based on historical sensitivity
- [ ] Response bias and survey methodology limitations are explicitly acknowledged
