---
name: model-risk-documentation
description: Document and explain model risk management decisions aligned with SR 11-7 and OCC 2011-12 supervisory guidance. Use when creating model validation reports, model inventory documentation, model risk assessments, ongoing monitoring plans, or responding to MRM examination findings.

metadata:
  display_name: "Model Risk Documentation"
  short_description: "Document model risk management per SR 11-7 guidelines"
  default_prompt: "Review my risk documentation and highlight top risks and next actions"
  version: "1.0.0"
  tags:
    - financial-services
  icon_path: "assets/icon.png"
---

# Model Risk Documentation

## Overview

This skill produces comprehensive model risk management (MRM) documentation aligned with SR 11-7 (Fed) and OCC Bulletin 2011-12 requirements. It covers model development documentation, independent validation reports, model risk assessments, ongoing performance monitoring, and model governance artifacts. The output meets examiner expectations for model risk management programs at supervised financial institutions.

## When to Use

- Drafting model development documentation for new or materially changed models
- Writing independent model validation reports
- Completing model risk tier assessments and model inventory entries
- Documenting ongoing monitoring results and performance degradation analysis
- Preparing model risk findings responses for examiners
- Supporting model governance committee materials
- Documenting model limitations, assumptions, and compensating controls

## Required Inputs

| Input | Description | Format |
|-------|-------------|--------|
| Model description | Purpose, methodology, inputs, outputs | Technical documentation |
| Model type | Quantitative, qualitative, hybrid, vendor, challenger | Classification |
| Model use | Business application, regulatory filing, risk limit | Use case definition |
| Validation results | Back-testing, benchmarking, sensitivity, stability | Test output |
| Performance metrics | Accuracy, discrimination, calibration, stability | Statistical results |
| Model tier | Tier 1 (critical), Tier 2 (significant), Tier 3 (limited) | Risk assessment |
| Regulatory context | Capital, CECL, stress testing, pricing, BSA | Regulatory use |

## Methodology

### Step 1: Classify the Model

Determine the SR 11-7 model definition applicability:

**SR 11-7 Model Definition**: "A quantitative method, system, or approach that applies statistical, economic, financial, or mathematical theories, techniques, and assumptions to process input data into quantitative estimates."

Classify by:
- **Model type**: Statistical/econometric, machine learning, expert judgment, scorecard, spreadsheet-based, vendor (black-box or transparent)
- **Risk tier**: Based on materiality of outputs, regulatory use, and complexity
- **Model lifecycle stage**: Development, implementation, production, retirement

| Tier | Criteria | Validation Frequency | Documentation Standard |
|------|----------|---------------------|----------------------|
| **Tier 1** | Regulatory capital, CCAR/DFAST, large loss exposure | Annual full validation | Comprehensive |
| **Tier 2** | Pricing, limit setting, management reporting | 18-month validation cycle | Standard |
| **Tier 3** | Low-materiality, decision support, non-regulatory | 24-month validation cycle | Streamlined |

### Step 2: Document Model Development

Create development documentation covering these required elements:

**Conceptual Soundness**:
- Theoretical basis and academic/industry foundation
- Appropriateness of methodology for intended use
- Key assumptions with justification and sensitivity analysis
- Variable selection rationale (economic intuition, statistical significance, regulatory expectation)
- Alternative approaches considered and reasons for rejection

**Data Quality and Representativeness**:
- Development data source, extraction criteria, and time period
- Sample size and composition (in-sample, out-of-sample, out-of-time)
- Data exclusions with documented rationale
- Missing data treatment methodology
- Data representativeness assessment (does the development sample reflect current portfolio?)

**Implementation**:
- Model implementation platform and version
- Numerical precision and computational considerations
- Override rules and manual adjustment protocols
- Integration with upstream (data feeds) and downstream (reporting, decisioning) systems

### Step 3: Document Validation Activities

Structure the validation report using the three SR 11-7 validation pillars:

**Pillar 1 — Conceptual Soundness Review**:
- Theory and methodology assessment
- Assumption reasonableness evaluation
- Benchmark comparison against alternative methodologies
- Literature review for industry best practices
- Regulatory guidance compliance check

**Pillar 2 — Outcomes Analysis (Back-testing)**:
- Predicted vs. actual comparison over multiple time periods
- Statistical tests: binomial test, traffic light approach, Hosmer-Lemeshow, chi-square
- Discrimination metrics: Gini coefficient, KS statistic, AUROC, accuracy ratio
- Calibration assessment: PD vs. observed default rates by grade
- Stability analysis: Population Stability Index (PSI), Characteristic Stability Index (CSI)

**Pillar 3 — Ongoing Monitoring**:
- Performance metric tracking against established thresholds
- Early warning indicators for model degradation
- Override analysis: frequency, direction, magnitude, and appropriateness
- Trigger events requiring ad hoc validation

### Step 4: Assess Model Limitations

Document all known limitations with compensating controls:

```markdown
| Limitation | Impact | Severity | Compensating Control |
|-----------|--------|----------|---------------------|
| [Limitation 1] | [Impact description] | [High/Med/Low] | [Control description] |
| [Limitation 2] | [Impact description] | [High/Med/Low] | [Control description] |
```

Common limitation categories:
- Data limitations (insufficient history, survivorship bias, regime changes)
- Methodology limitations (linearity assumptions, distributional assumptions)
- Implementation limitations (approximations, rounding, system constraints)
- Scope limitations (populations not covered, tail risk inadequacy)

### Step 5: Produce the Model Risk Assessment

Quantify model risk across dimensions:

| Dimension | Weight | Rating (1-5) | Weighted Score |
|-----------|--------|--------------|----------------|
| Materiality of use | 25% | [Rating] | [Score] |
| Complexity | 20% | [Rating] | [Score] |
| Data quality | 15% | [Rating] | [Score] |
| Performance stability | 15% | [Rating] | [Score] |
| Vendor dependence | 10% | [Rating] | [Score] |
| Regulatory scrutiny | 15% | [Rating] | [Score] |
| **Total** | 100% | | **[Total]** |

Map total score to risk tier: 1.0-2.0 = Tier 3, 2.1-3.5 = Tier 2, 3.6-5.0 = Tier 1

### Step 6: Document Findings and Recommendations

Classify validation findings by severity:

| Severity | Definition | Remediation Timeline |
|----------|-----------|---------------------|
| **Critical** | Model produces materially inaccurate results; immediate business impact | 30 days; interim compensating controls required |
| **Significant** | Model weakness that could become material; requires methodological change | 90 days |
| **Moderate** | Documentation gap or minor performance issue | 180 days |
| **Advisory** | Best practice recommendation; no immediate risk | Next model refresh cycle |

### Step 7: Establish Ongoing Monitoring Framework

Define the monitoring plan:
- Monthly/quarterly performance metrics with RAG thresholds
- Trigger events requiring ad hoc review (portfolio composition change, macro regime shift, M&A)
- Annual attestation requirements
- Model owner responsibilities vs. validation team responsibilities
- Escalation procedures for threshold breaches

## Output Specification

```markdown
# Model Risk Documentation: [Model Name]

## Model Identification
- **Model ID**: [Inventory ID]
- **Model Name**: [Name]
- **Model Owner**: [Business unit and individual]
- **Model Developer**: [Internal/Vendor]
- **Risk Tier**: [Tier 1/2/3]
- **Last Validation**: [Date]
- **Next Validation Due**: [Date]

## Purpose and Use
[Description of what the model does and how its outputs are used in business decisions]

## Methodology Summary
[High-level description of the modeling approach, key variables, and output interpretation]

## Validation Summary
### Conceptual Soundness: [Satisfactory / Needs Improvement / Unsatisfactory]
[Key findings from conceptual review]

### Outcomes Analysis: [Satisfactory / Needs Improvement / Unsatisfactory]
| Metric | Value | Threshold | Status |
|--------|-------|-----------|--------|
| Gini Coefficient | [X.XX] | [>0.XX] | [Pass/Fail] |
| PSI | [X.XX] | [<0.25] | [Pass/Fail] |
| KS Statistic | [X.XX] | [>0.XX] | [Pass/Fail] |

### Ongoing Monitoring: [Satisfactory / Needs Improvement / Unsatisfactory]
[Monitoring results and trend assessment]

## Findings
| # | Severity | Finding | Remediation | Due Date | Status |
|---|----------|---------|-------------|----------|--------|
| 1 | [Severity] | [Finding] | [Action] | [Date] | [Open/Closed] |

## Limitations and Compensating Controls
[Documented limitations with corresponding controls]

## Overall Assessment
- **Model Risk Rating**: [Low / Moderate / High / Critical]
- **Recommendation**: [Approve / Conditional Approve / Reject / Retire]
- **Conditions (if applicable)**: [Conditions for continued use]
```

## Analysis Framework

### Performance Degradation Assessment

When model performance metrics breach thresholds:
1. Identify which metrics degraded and by how much
2. Determine root cause (data drift, population shift, regime change, coding error)
3. Assess materiality of degradation on model outputs and business decisions
4. Recommend remediation: recalibration, redevelopment, overlay, or retirement
5. Define interim compensating controls during remediation

### Vendor Model Assessment

For vendor (third-party) models, additional documentation requirements:
- Vendor due diligence and ongoing monitoring evidence
- Contractual provisions for data access, model transparency, and audit rights
- Customization and configuration documentation
- Vendor model change management process
- Fallback procedures if vendor model becomes unavailable

## Examples

**Example 1 — Validation Finding**:
"Finding #3 (Significant): The commercial real estate PD model (Model ID: CR-PD-004) exhibits PSI of 0.31 for the office property segment, exceeding the 0.25 threshold indicating significant population shift. The development sample (2015-2019) does not reflect post-pandemic office vacancy dynamics. The model underpredicts PD for office properties by an average of 85 basis points relative to observed defaults. Recommendation: Apply a 100bp PD overlay for office segment pending model redevelopment targeting Q2 2026. Interim compensating control: manual review of all office CRE exposures exceeding $5M."

**Example 2 — Model Inventory Entry**:
"Model: CECL Lifetime Loss Model (ID: ACL-LTL-001). Tier 1 — Used for CECL allowance calculation reported in 10-K/10-Q and Call Report Schedule RC-R. Methodology: Vintage-level loss rate projection using Moody's macroeconomic scenarios with 8-quarter reasonable and supportable forecast period and 4-quarter straight-line reversion. Last validated: 2025-06-30 (Satisfactory with 2 Moderate findings). Model owner: Chief Credit Officer. Next validation due: 2026-06-30."

## Guidelines

- All models meeting the SR 11-7 definition must be in the model inventory, including spreadsheets and end-user computing tools
- Effective challenge requires validators independent from model development and use
- Document the model's intended use; usage outside documented scope constitutes an unapproved model
- Performance thresholds must be pre-defined, not set after observing results
- Vendor model opacity does not exempt the institution from validation obligations
- Track finding remediation to closure with evidence of implementation
- Model risk aggregation: assess the combined effect of model limitations across interconnected models
- Maintain version control for all model documentation
- Ensure model governance committee minutes reflect challenge and approval decisions

## Validation Checklist

- [ ] Model meets SR 11-7 definition and is registered in model inventory
- [ ] Risk tier assessment is completed and documented with scoring rationale
- [ ] Development documentation covers conceptual soundness, data, and implementation
- [ ] Validation addresses all three pillars (conceptual, outcomes, monitoring)
- [ ] Performance metrics are compared against pre-defined thresholds
- [ ] All findings have severity classification, remediation plan, and due dates
- [ ] Limitations are documented with corresponding compensating controls
- [ ] Overall model risk rating and recommendation are stated
- [ ] Ongoing monitoring plan defines metrics, frequencies, and escalation procedures
- [ ] Documentation supports examiner review without requiring verbal explanation
