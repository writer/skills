---
name: on-call-load-optimization
description: Balance on-call schedules fairly across providers by analyzing call burden distribution, frequency equity, weekend/holiday allocation, response volume patterns, and impact on provider well-being and productivity. Use when creating or evaluating call schedules, addressing provider complaints about call equity, optimizing coverage for patient safety, or assessing call compensation models against workload.

metadata:
  display_name: "On Call Load Optimization"
  short_description: "Optimize provider on-call schedule equity and fairness"
  default_prompt: "Optimize my on call load and suggest the best next steps"
  version: "1.0.0"
  tags:
    - healthcare
  icon_path: "assets/icon.png"
---

# On-Call Load Optimization

## Overview

Optimize on-call scheduling to achieve equitable distribution of call burden across providers while maintaining continuous patient coverage and minimizing the impact on provider well-being and next-day clinical productivity. On-call responsibilities contribute significantly to physician burnout (cited by 40-50% of physicians as a major dissatisfaction factor), and inequitable distribution amplifies this effect. This skill analyzes historical call patterns, quantifies true call burden (beyond simple shift counts), models equitable distribution algorithms, and evaluates the relationship between call load and provider performance, patient safety, and retention.

## When to Use

- Creating or revising on-call rotation schedules
- Investigating provider complaints about call inequity
- Evaluating the impact of call on provider productivity and burnout
- Modeling staffing scenarios for new coverage requirements
- Assessing call compensation adequacy against workload data
- Optimizing call coverage during holidays and vacation seasons
- Planning for call schedule changes due to provider departures or additions
- Analyzing post-call clinical performance for patient safety

## Required Inputs

| Input | Description | Format |
|-------|-------------|--------|
| `provider_roster` | Eligible providers with specialty, FTE, seniority, contract call obligations | Structured array |
| `call_schedule_history` | Past 12+ months of call assignments with dates and shift types | Array of records |
| `call_activity_data` | Actual call volume: pages, calls received, ED consults, admissions, surgeries during call | Array of events |
| `coverage_requirements` | Required coverage hours, locations, and specialties per time period | Configuration object |
| `provider_preferences` | Preferred/blocked dates, swap requests, personal constraints | Structured object |
| `post_call_data` | Next-day productivity, patient safety events, errors after call shifts | Structured object |
| `compensation_data` | Call pay rates, stipends, and incentive structures | Structured object |

## Methodology

### Step 1: Call Burden Quantification

Move beyond simple shift counts to measure true call burden:

**Burden Dimensions:**

| Dimension | Metric | Weight | Data Source |
|-----------|--------|--------|------------|
| Frequency | Number of call shifts per month | 20% | Schedule data |
| Intensity | Average pages/calls/consults per shift | 25% | Call activity logs |
| Disruption | Percentage of shifts with overnight activity (sleep disruption) | 20% | Call activity timestamps |
| Duration | Total hours spent on call-related clinical activity | 15% | Activity duration logs |
| Recovery impact | Post-call productivity decrease (wRVU comparison) | 10% | Billing data |
| Undesirability | Weekend, holiday, and consecutive-day call penalties | 10% | Schedule data |

**Composite Burden Score Calculation:**
```
burden_score = (frequency_score × 0.20)
             + (intensity_score × 0.25)
             + (disruption_score × 0.20)
             + (duration_score × 0.15)
             + (recovery_score × 0.10)
             + (undesirability_score × 0.10)
```

Each dimension normalized to 0-100 scale based on group distribution.

### Step 2: Equity Analysis

Assess current distribution fairness:

**Equity Metrics:**
- **Gini coefficient**: Measure of inequality in burden distribution (0 = perfect equality, 1 = maximum inequality). Target below 0.15.
- **Max/min ratio**: Ratio of highest to lowest individual burden score. Target below 1.5.
- **Weekend/holiday equity**: Standard deviation of weekend/holiday assignments per provider. Target SD below 1.0.
- **Consecutive call**: Maximum consecutive call days assigned to any provider. Recommended max of 3 for overnight; 7 for pager-only.
- **Rest interval**: Minimum hours between end of call and next clinical session. Recommended minimum 8-12 hours post-active call.

**Stratified Equity Assessment:**
- Compare burden by provider seniority (junior vs. senior)
- Compare by FTE status (full-time vs. part-time — should be proportional)
- Compare by gender (documented gender disparities in call burden exist in literature)
- Compare by practice site (multi-site systems may have location-based inequity)

### Step 3: Coverage Optimization

Model optimal coverage to minimize total burden while maintaining safety:

**Coverage Requirements Analysis:**
- Map historical call volume by hour, day of week, and season
- Identify high-volume periods requiring enhanced coverage (e.g., Monday AM, holiday weekends)
- Identify low-volume periods where reduced coverage may be safe (weekend daytime with low census)
- Model backup/escalation tiers to avoid single-provider overload

**Staffing Models:**

| Model | Description | Best For |
|-------|-------------|----------|
| Fixed rotation | Set rotation cycle (every Nth day) | Small groups, equal FTE |
| Block scheduling | Week-long call blocks with recovery time | Surgical specialties |
| Night float | Dedicated nighttime provider rotation | Large groups, high nocturnal volume |
| Tiered call | Primary + backup with escalation protocols | Complex coverage needs |
| Hospitalist partnership | Shared call with hospital medicine | Primary care groups |

### Step 4: Schedule Generation

Generate optimized schedules using constraint-based algorithms:

**Hard Constraints (must satisfy):**
- Every required coverage slot is filled
- No provider exceeds maximum consecutive call days
- Minimum rest interval between call and clinic is maintained
- Provider contractual call limits are respected
- Blocked dates and approved leave are honored
- Providers are only scheduled for call types within their scope and credentials

**Soft Constraints (optimize toward):**
- Minimize variance in total burden scores across providers
- Distribute weekends and holidays as evenly as possible
- Honor provider preferences when possible
- Avoid scheduling call immediately before high-productivity clinic days
- Separate call shifts for the same provider by maximum interval
- Balance seasonal distribution (no provider consistently assigned holiday periods)

**Optimization Approach:**
- Generate feasible schedules satisfying all hard constraints
- Score each schedule by equity metrics and preference satisfaction
- Select the schedule with the lowest Gini coefficient and highest preference score
- Present top 3 candidate schedules for group review and selection

### Step 5: Impact Assessment

Evaluate the effect of call on provider performance and well-being:

**Productivity Impact:**
- Compare wRVUs on post-call days vs. non-post-call days for each provider
- Calculate aggregate productivity loss attributable to call burden
- Typical finding: 15-30% wRVU reduction on post-call clinic days

**Patient Safety Analysis:**
- Review incident reports and near-misses associated with post-call shifts
- Analyze complication rates for procedures performed post-call
- Assess handoff quality at end-of-call transitions
- Reference ACGME duty hour principles as a framework (though not all providers are subject to ACGME)

**Well-Being Indicators:**
- Track burnout survey scores (Maslach Burnout Inventory) correlated with call burden
- Monitor provider turnover rates by call burden quartile
- Assess absenteeism patterns following heavy call periods
- Review call-swap request frequency as a dissatisfaction proxy

### Step 6: Compensation Alignment

Evaluate whether call compensation matches actual burden:

- **Per-shift stipend analysis**: Compare stipend to actual work hours during call (effective hourly rate)
- **Market benchmarking**: Compare call compensation to MGMA and SullivanCotter call pay benchmarks
- **Burden-adjusted compensation**: Do higher-burden shifts receive proportionally higher compensation?
- **Productivity credit**: Should post-call wRVU targets be adjusted to account for call impact?
- **Call buy-out options**: Model financial implications of allowing providers to buy out of call shifts

### Step 7: Continuous Monitoring and Adjustment

Implement ongoing schedule optimization:

- Monthly burden score dashboard with equity metrics
- Quarterly schedule fairness review with provider input
- Real-time swap management system with equity impact assessment
- Annual comprehensive call model evaluation
- Trigger-based schedule adjustment: if any provider's burden exceeds 1.5x the group median, automatic rebalancing

## Output Specification

```yaml
call_optimization_report:
  reporting_period: string
  provider_count: number
  total_call_shifts: number
  equity_metrics:
    gini_coefficient: number
    max_min_ratio: number
    weekend_holiday_sd: number
    max_consecutive_days: number
  provider_detail:
    - provider_id: string
      total_shifts: number
      weekend_shifts: number
      holiday_shifts: number
      burden_score: number
      burden_percentile: number
      post_call_productivity_impact: number
  coverage_analysis:
    gaps_identified: array
    over_coverage_periods: array
    volume_pattern: object
  optimized_schedule:
    schedule_id: string
    equity_improvement: number
    constraint_violations: array
    preference_satisfaction_rate: number
  compensation_analysis:
    effective_hourly_rate_range: string
    market_benchmark_comparison: string
    recommendations: array
  well_being_indicators:
    burnout_correlation: number
    turnover_risk_flags: array
```

## Analysis Framework

### Call Burden Equity Matrix

| Equity Level | Gini Coefficient | Max/Min Ratio | Action Required |
|-------------|-----------------|---------------|-----------------|
| Excellent | Under 0.05 | Under 1.2 | Maintain current model |
| Good | 0.05-0.10 | 1.2-1.3 | Minor adjustments |
| Fair | 0.10-0.15 | 1.3-1.5 | Schedule restructuring recommended |
| Poor | 0.15-0.25 | 1.5-2.0 | Significant intervention needed |
| Critical | Over 0.25 | Over 2.0 | Immediate restructuring required |

## Examples

**Example: 12-Provider General Surgery Call Optimization**

- Current model: Simple rotation, every 12th day, fixed cycle
- Problem: 3 providers consistently get Friday/weekend calls due to cycle alignment; holiday distribution inequitable
- Current Gini coefficient: 0.19 (poor) when measuring composite burden
- Call volume analysis: Friday overnight and Sunday daytime are highest volume (3x weekday average)
- Post-call impact: 23% average wRVU reduction on post-call clinic days
- Optimized schedule: Constraint-based algorithm with weekend/holiday equity targets
- Result: Gini coefficient reduced to 0.07, weekend SD from 2.3 to 0.8
- Compensation recommendation: Tiered call pay (weeknight $800, weekend day $1,200, weekend overnight $1,500) based on burden analysis
- Productivity adjustment: Reduce post-call clinic template by 25% to maintain quality

## Guidelines

1. **Measure burden, not just frequency** — shift counts alone miss intensity and disruption differences
2. **Involve providers in schedule design** — imposed schedules generate more dissatisfaction
3. **Protect post-call recovery** — schedule lighter clinical loads following active call shifts
4. **Review equity quarterly** — small imbalances compound over time
5. **Document call obligations in contracts** — clear expectations prevent disputes
6. **Monitor for disparities** — ensure call is not disproportionately assigned by gender, seniority, or minority status
7. **Consider patient safety** — fatigued providers make more errors; prioritize adequate rest

## Validation Checklist

- [ ] Call burden measured across multiple dimensions (not just shift count)
- [ ] Composite burden score calculated with transparent weighting
- [ ] Equity assessed using Gini coefficient and max/min ratio
- [ ] Weekend and holiday distribution analyzed separately
- [ ] Coverage requirements mapped against historical volume patterns
- [ ] Optimized schedule satisfies all hard constraints
- [ ] Post-call productivity impact quantified with wRVU data
- [ ] Compensation alignment evaluated against market benchmarks
- [ ] Provider well-being indicators tracked and correlated with call burden
- [ ] Continuous monitoring plan established with trigger-based rebalancing

## HIPAA Compliance Notes

- Call activity data may include patient identifiers when logging consults and admissions (45 CFR 164.501)
- Patient safety event analysis linked to post-call shifts involves PHI review
- De-identify patient data when analyzing call volume patterns for scheduling purposes
- Provider performance data (post-call productivity) should be handled under peer review confidentiality where applicable
- Call system logs containing patient callback numbers require secure storage (45 CFR 164.312(a))
- Maintain minimum necessary access for staff managing call schedules who may see patient-related activity data (45 CFR 164.502(b))
