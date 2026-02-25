---
name: authorization-timeline-predictor
description: Predict prior authorization processing timelines and identify delay risk factors by analyzing payer response patterns, service complexity, clinical documentation completeness, and historical approval data. Use when estimating authorization turnaround for scheduling, identifying at-risk authorizations, optimizing submission timing, or managing patient expectations for prior auth dependent services.

metadata:
  display_name: "Authorization Timeline Predictor"
  short_description: "Forecast prior authorization timelines and delay risks"
  default_prompt: "Review my authorization timeline and highlight top risks and next actions"
  version: "1.0.0"
  tags:
    - healthcare
  icon_path: "assets/icon.png"
---

# Authorization Timeline Predictor

## Overview

Predict the expected processing time for prior authorization requests by analyzing historical payer response patterns, service-specific approval complexity, documentation completeness, and submission channel efficiency. Prior authorization delays are a leading cause of care delays, with an average of 14 business days for standard requests and frequent extensions beyond 30 days for complex services. This skill enables proactive scheduling, identifies submissions at high risk of delay, and recommends interventions to accelerate approvals — reducing patient wait times and preventing revenue loss from abandoned or expired authorizations.

## When to Use

- Estimating turnaround time for a new prior authorization submission
- Identifying authorization requests at risk of delay or denial
- Optimizing submission timing and channel selection for faster processing
- Managing patient and provider expectations for authorization-dependent services
- Prioritizing authorization work queues based on predicted processing time
- Analyzing payer-specific authorization performance for contract negotiations
- Forecasting staffing needs for the prior authorization team
- Tracking authorization cycle time against CMS and state regulatory requirements

## Required Inputs

| Input | Description | Format |
|-------|-------------|--------|
| `auth_request` | Service requiring authorization: CPT/HCPCS, diagnosis, provider, facility | Structured object |
| `payer_info` | Payer name, plan type, state, submission channel | Structured object |
| `clinical_documentation` | Submitted clinical notes, letters of medical necessity | Document references |
| `historical_auth_data` | Past authorization requests with submission dates, decision dates, outcomes | Array of records |
| `submission_details` | Submission date, method (portal/fax/phone), completeness status | Structured object |
| `urgency_level` | Standard, expedited, or retrospective review type | String |

## Methodology

### Step 1: Baseline Timeline Estimation

Establish the baseline expected processing time using historical data and regulatory requirements:

**Regulatory Maximums:**

| Review Type | Medicare Advantage | Medicaid (Federal) | Commercial (State Varies) |
|-------------|-------------------|-------------------|--------------------------|
| Standard (non-urgent) | 14 calendar days (extendable to 28) | 14 calendar days | 15-30 business days (state-dependent) |
| Expedited/Urgent | 72 hours | 72 hours | 48-72 hours |
| Retrospective | 30 calendar days | 30 calendar days | 30-60 calendar days |
| Extension allowed | 14 additional days | 14 additional days | Varies by state |

**CMS Interoperability Rule (CMS-0057-F):** Medicare Advantage and Medicaid managed care plans must provide prior auth decisions within 72 hours (expedited) or 7 calendar days (standard) for most services, effective January 2026.

- Calculate payer-specific median processing time from historical data
- Segment by service category (imaging, surgery, DME, medications, specialist referrals)
- Establish baseline prediction: median historical days for same payer + service category

### Step 2: Delay Risk Factor Assessment

Score each authorization request against known delay risk factors:

**High-Risk Factors (add 5-10 days each):**
- Service requires peer-to-peer clinical review (complex surgeries, advanced imaging, high-cost drugs)
- Incomplete clinical documentation at initial submission
- Non-formulary or experimental/investigational service
- Out-of-network provider requiring single-case agreement
- History of additional information requests from this payer for this service type

**Moderate-Risk Factors (add 2-5 days each):**
- Fax submission (vs. electronic portal submission)
- Submission on Friday or before holiday
- Payer currently experiencing known processing backlogs
- Multiple concurrent authorization requests for same patient
- Service requires coordination with pharmacy benefit (medical vs. pharmacy benefit determination)

**Low-Risk Factors (add 1-2 days each):**
- First-time authorization for this patient with this payer
- Minor documentation formatting issues
- High payer volume period (January, open enrollment aftermath)

### Step 3: Documentation Completeness Scoring

Evaluate the submitted documentation for completeness against payer-specific requirements:

| Documentation Element | Weight | Status |
|----------------------|--------|--------|
| Letter of medical necessity from ordering provider | Critical | Present/Absent |
| Relevant clinical notes (last 90 days) | Critical | Present/Absent |
| Diagnostic test results supporting medical necessity | High | Present/Absent |
| Conservative treatment history (if applicable) | High | Present/Absent/N/A |
| Peer-reviewed literature (for experimental services) | Medium | Present/Absent/N/A |
| Correct CPT/HCPCS and ICD-10 codes | Critical | Present/Incorrect |
| Provider credentials and network status | Medium | Verified/Unverified |

- **Completeness score above 90%**: Minimal delay risk from documentation
- **Completeness score 70-90%**: Moderate risk of additional information request (adds 7-14 days)
- **Completeness score below 70%**: High risk of delay or denial; recommend resubmission before proceeding

### Step 4: Predictive Timeline Calculation

Combine baseline, risk factors, and documentation scoring:

```
predicted_days = baseline_median
              + sum(risk_factor_adjustments)
              + documentation_delay_estimate
              + seasonal_adjustment
              + channel_adjustment
```

**Confidence Intervals:**
- Provide 50th percentile (expected), 75th percentile (likely worst case), and 95th percentile (extreme delay)
- Flag requests where predicted timeline exceeds the patient's clinical urgency window

**Seasonal Adjustments:**
- January: +2-3 days (new benefit year, eligibility changes)
- Q4: +1-2 days (year-end processing volumes)
- Holiday weeks: +3-5 days (reduced payer staffing)

### Step 5: Acceleration Recommendations

For authorizations predicted to exceed acceptable timelines, recommend interventions:

- **Expedited review request**: If clinical criteria for urgency are met (serious jeopardy to life, health, or ability to regain maximum function)
- **Peer-to-peer scheduling**: Proactively schedule physician-to-physician review rather than waiting for payer to request
- **Portal submission**: Convert fax submissions to electronic portal for faster intake
- **Documentation pre-check**: Complete documentation gap analysis before submission
- **Concurrent submission**: For services requiring both medical and pharmacy authorization, submit simultaneously
- **Escalation pathways**: State insurance department complaints for violations of turnaround requirements
- **Gold card programs**: Identify if the provider qualifies for payer's expedited or auto-approval programs

### Step 6: Monitoring and Alert Framework

Track authorization progress against predicted timelines:

- **Day 3 check**: Confirm payer received and acknowledged the request
- **Day 7 check**: Verify no additional information request is pending
- **Day 10 alert**: If no decision, escalate or request status update
- **Regulatory deadline alert**: 2 business days before regulatory maximum, escalate
- **Expiration tracking**: Monitor authorization validity period and initiate renewal 30 days before expiration
- **Abandonment detection**: Flag authorizations with no activity for 10+ business days

### Step 7: Payer Performance Analytics

Aggregate authorization data for payer performance benchmarking:

- Median and mean processing days by payer, service category, and submission channel
- Denial rate at initial submission vs. after peer-to-peer review
- Additional information request rate (indicator of documentation standard clarity)
- Regulatory compliance rate (percentage of decisions within required timeframes)
- Trend analysis: improving or deteriorating payer performance over time
- Use for payer contract negotiations and value-based arrangement discussions

## Output Specification

```yaml
authorization_timeline_prediction:
  auth_request_id: string
  service: string
  payer: string
  plan_type: string
  submission_date: string
  predicted_decision_date:
    p50: string  # expected
    p75: string  # likely worst case
    p95: string  # extreme delay
  predicted_days:
    p50: number
    p75: number
    p95: number
  risk_score: number  # 0-100
  risk_factors:
    - factor: string
      impact_days: number
      mitigable: boolean
  documentation_completeness: number  # percentage
  documentation_gaps:
    - element: string
      criticality: string
      recommendation: string
  acceleration_recommendations:
    - action: string
      expected_time_savings: number
      effort_level: string
  regulatory_deadline: string
  regulatory_deadline_days_remaining: number
  monitoring_schedule:
    - check_date: string
      action: string
  clinical_urgency_flag: boolean
  payer_historical_performance:
    median_days: number
    approval_rate: number
    additional_info_request_rate: number
```

## Analysis Framework

### Authorization Complexity Tiers

| Tier | Service Types | Typical Timeline | Denial Risk |
|------|--------------|------------------|-------------|
| Tier 1 - Routine | Standard imaging, PT/OT eval, DME | 3-7 days | Low (under 10%) |
| Tier 2 - Moderate | Advanced imaging, outpatient surgery, specialty drugs | 7-14 days | Moderate (10-25%) |
| Tier 3 - Complex | Inpatient procedures, high-cost biologics, transplant | 14-30 days | High (25-40%) |
| Tier 4 - Exceptional | Experimental treatments, out-of-network, rare disease | 30-60+ days | Very high (40%+) |

### Submission Channel Impact

| Channel | Avg. Processing Time | Recommended For |
|---------|---------------------|-----------------|
| Electronic portal | Fastest (baseline) | All submissions when available |
| EDI/electronic submission | Baseline + 1 day | High-volume automated submissions |
| Fax | Baseline + 3-5 days | Only when portal unavailable |
| Phone | Baseline + 1-2 days | Urgent/expedited requests with immediate decision |

## Examples

**Example: Lumbar Fusion Surgery Authorization**

- Service: CPT 22612 (Lumbar interbody fusion), CPT 22614 (each additional level)
- Payer: UnitedHealthcare Commercial PPO
- Submission: Electronic portal, complete documentation including 12 weeks conservative therapy records, MRI, and surgeon letter of necessity
- Historical median for this payer + service: 12 business days
- Risk factors: Multi-level fusion (+3 days), likely peer-to-peer required (+5 days)
- Documentation completeness: 95%
- Predicted timeline: P50 = 15 business days, P75 = 22 days, P95 = 35 days
- Acceleration: Proactively schedule peer-to-peer for day 7; could reduce by 3-5 days
- Patient guidance: Schedule surgery tentatively for 4 weeks out; confirm after authorization received

## Guidelines

1. **Always check regulatory requirements** — payer turnaround obligations vary by state and plan type
2. **Document submission timestamps** — essential for regulatory complaints and appeals
3. **Prioritize clinical urgency** — expedited review is legally required when delay could cause serious harm
4. **Track authorization expiration dates** — most authorizations expire 60-90 days after approval
5. **Monitor CMS Interoperability Rule compliance** — new federal standards for electronic prior auth effective 2026
6. **Never delay clinically urgent care** — provide service and pursue retrospective authorization when appropriate
7. **Build payer scorecards** — aggregate data drives contract negotiation leverage

## Validation Checklist

- [ ] Baseline timeline calculated from historical data for matching payer and service category
- [ ] All applicable delay risk factors identified and scored
- [ ] Documentation completeness evaluated against payer-specific requirements
- [ ] Predicted timeline includes confidence intervals (P50, P75, P95)
- [ ] Acceleration recommendations are actionable and linked to expected time savings
- [ ] Regulatory deadline identified and monitoring schedule established
- [ ] Clinical urgency assessed and expedited review triggered when appropriate
- [ ] Payer performance benchmarked against regulatory and industry standards
- [ ] Authorization expiration tracking included in output

## HIPAA Compliance Notes

- Authorization requests contain PHI including diagnoses, treatment plans, and provider information (45 CFR 164.501)
- Electronic authorization submissions must use encrypted channels per 45 CFR 164.312(e)
- Historical authorization data used for predictive modeling must be access-controlled per 45 CFR 164.312(a)
- Payer performance analytics should use de-identified or aggregated data when shared outside the covered entity
- Authorization tracking systems must maintain audit logs per 45 CFR 164.312(b)
- Staff accessing authorization data require appropriate HIPAA training and role-based access controls
