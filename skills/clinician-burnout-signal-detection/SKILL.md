---
name: Clinician Burnout Signal Detection
description: Identify early warning signals of clinician burnout using Maslach Burnout Inventory dimensions, operational proxy metrics, and workforce analytics to enable proactive intervention and retention strategies.

metadata:
  display_name: "Clinician Burnout Signal Detection"
  short_description: "Detect early warning signs of clinician burnout and fatigue"
  default_prompt: "Review my clinician burnout signal and highlight top risks and next actions"
  version: "1.0.0"
  tags:
    - healthcare
  icon_path: "assets/icon.png"
---

# Clinician Burnout Signal Detection

## Overview

This skill detects early indicators of clinician burnout by analyzing operational data, workforce patterns, and wellness survey signals across the three dimensions of the Maslach Burnout Inventory (MBI): emotional exhaustion, depersonalization, and reduced personal accomplishment. Clinician burnout affects 42-54% of U.S. physicians (National Academy of Medicine) and is associated with increased medical errors, higher turnover costs (estimated at 500K-1M per physician departure), reduced patient satisfaction, and poorer clinical outcomes. Early detection enables targeted wellness interventions, workload adjustments, and systemic improvements before burnout leads to attrition.

## When to Use

- Monitoring workforce wellness metrics as part of ongoing operational dashboards
- Investigating drivers behind increasing provider turnover or early retirement
- Assessing impact of operational changes on clinician well-being (EHR transitions, coverage model changes)
- Preparing for or responding to workforce surveys (AMA Organizational Biopsy, Mini-Z)
- Evaluating effectiveness of wellness programs and burnout prevention initiatives
- Supporting Quadruple Aim objectives (adding clinician well-being to Triple Aim)

## Required Inputs

| Input | Description | Format |
|-------|-------------|--------|
| `ehr_usage_data` | Time in EHR, after-hours charting (pajama time), inbox volume, note length | De-identified JSON |
| `scheduling_data` | Panel size, visits per session, overtime hours, PTO utilization, call frequency | JSON object |
| `workforce_survey` | MBI scores or Mini-Z/well-being survey results (if available) | JSON object |
| `turnover_data` | Departures, retirement announcements, transfer requests, contract non-renewals | JSON array |
| `quality_metrics` | Patient satisfaction scores, safety event reports, complaint rates per provider | JSON object |
| `peer_benchmarks` | Specialty-specific workload and productivity benchmarks | JSON object |

## Methodology

### Step 1: Maslach Burnout Inventory Framework Application
- Assess signals across all three MBI dimensions:
  - **Emotional Exhaustion (EE)**: Feeling emotionally drained, overwhelmed, and depleted
    - Proxy signals: Rising after-hours EHR time, declining PTO usage (presenteeism), increased sick calls, shortened visit durations suggesting rushing
  - **Depersonalization (DP)**: Detachment, cynicism, treating patients as objects
    - Proxy signals: Increasing patient complaints about empathy, declining patient satisfaction scores, copy-forward note patterns, decreased use of patient names in documentation
  - **Reduced Personal Accomplishment (PA)**: Feeling ineffective, questioning competence
    - Proxy signals: Declining CME engagement, reduced committee participation, withdrawal from teaching and mentoring, declining quality metrics
- Score each dimension on a Low/Moderate/High burnout risk scale
- Note: Direct MBI survey data is preferred but operational proxies provide continuous monitoring between surveys

### Step 2: Operational Workload Analysis
- Analyze workload intensity metrics:
  - **Clinical volume**: Visits per session vs. benchmark, panel size vs. specialty target
    - Primary care panel benchmark: 1,800-2,500 patients per 1.0 FTE
    - Specialty benchmarks vary (reference MGMA or AMGA data)
  - **EHR burden**: Total EHR time per clinical hour (benchmark: less than 2:1 ratio)
    - After-hours charting ("pajama time"): flag if exceeding 30 min/day average
    - Inbox messages per day: flag if exceeding 50 messages/day
    - Note length trend: increasing length may indicate compliance anxiety
  - **Schedule compression**: Double-bookings, add-on frequency, lunch break erosion
  - **On-call load**: Call nights per month, overnight disruption frequency
  - **Administrative burden**: Prior authorization time, peer review, committee load

### Step 3: Temporal Pattern Detection
- Analyze signals over time to detect deteriorating trends:
  - Rolling 90-day trend analysis for key metrics
  - Compare individual provider trends against department and peer group baselines
  - Identify inflection points (sudden changes suggesting acute stressors)
  - Seasonal patterns (flu season, year-end, open enrollment periods)
- Apply statistical process control: flag metrics exceeding 2 sigma from personal baseline
- Detect clustering: multiple signals shifting simultaneously suggests burnout progression

### Step 4: Risk Stratification
- Assign overall burnout risk tier:
  - **Low risk** (0-2 signals): Continue monitoring, reinforce protective factors
  - **Moderate risk** (3-5 signals): Proactive check-in, workload review, wellness resources
  - **High risk** (6-8 signals): Urgent leadership attention, schedule modification, peer support
  - **Critical risk** (9+ signals or turnover intent indicator): Immediate intervention required
- Weight signals by evidence strength:
  - Strong evidence: Direct MBI/Mini-Z scores, turnover announcement, patient safety event
  - Moderate evidence: After-hours EHR trend, declining satisfaction scores, PTO patterns
  - Weak evidence (contextual): Meeting attendance, CME engagement, email responsiveness

### Step 5: Driver Analysis
- Identify primary burnout drivers for targeted intervention:
  - **Workload drivers**: Volume, complexity, administrative burden, EHR friction
  - **Control drivers**: Autonomy erosion, rigid scheduling, micromanagement
  - **Community drivers**: Team dysfunction, isolation, lack of peer support
  - **Fairness drivers**: Compensation inequity, unequal call distribution, favoritism
  - **Values alignment**: Mission drift, ethical distress, inability to provide desired care
  - **Reward drivers**: Lack of recognition, stagnant advancement, declining reimbursement
- Map to Maslach and Leiter Six Areas of Worklife model for intervention targeting

### Step 6: Intervention Recommendations
- Generate prioritized interventions based on identified drivers:
  - **Workload interventions**: Scribe support, advanced practice provider pairing, panel right-sizing, inbox management protocols
  - **Efficiency interventions**: EHR optimization, smart phrases, team-based documentation
  - **Autonomy interventions**: Schedule flexibility, telehealth options, reduced meeting burden
  - **Community interventions**: Peer support programs, Schwartz Rounds, team building
  - **Individual interventions**: Coaching referral, EAP connection, resilience programs (as supplement to systemic changes, not replacement)
  - **System interventions**: Workflow redesign, staffing ratios, leadership development
- Track intervention adoption and effectiveness over 90-day cycles

## Output Specification

```yaml
burnout_signal_report:
  analysis_period: string
  population_analyzed: string
  aggregate_risk_distribution:
    low: number
    moderate: number
    high: number
    critical: number
  mbi_dimension_signals:
    emotional_exhaustion:
      proxy_signals: array
      risk_level: string
    depersonalization:
      proxy_signals: array
      risk_level: string
    personal_accomplishment:
      proxy_signals: array
      risk_level: string
  workload_metrics:
    avg_visits_per_session: number
    avg_ehr_time_ratio: number
    avg_after_hours_minutes: number
    avg_inbox_messages_per_day: number
    pto_utilization_rate: number
  high_risk_signals:
    - signal: string
      dimension: string
      trend: string
      affected_count: number
      severity: string
  primary_drivers:
    - driver: string
      category: string
      evidence: string
      affected_percentage: number
  interventions:
    - intervention: string
      target_driver: string
      priority: string
      timeline: string
      expected_impact: string
      responsible_owner: string
```

## Analysis Framework

Apply the **National Academy of Medicine Systems Model** for clinician burnout:
1. **External environment**: Regulatory burden, payment models, technology requirements
2. **Healthcare organization**: Culture, values, leadership, resources
3. **Work unit**: Practice efficiency, workload, teamwork, supervision
4. **Individual**: Personal resilience, coping, life events (least emphasis per NAM)

Key principle: Burnout is primarily a system problem, not an individual failing. Interventions must prioritize organizational and work-unit changes over individual resilience programs.

## Examples

**Example: 150-Provider Multi-Specialty Group Analysis**
- Survey: Mini-Z administered, 72% response rate
- Risk distribution: 18% low, 34% moderate, 31% high, 17% critical
- Top EE signal: After-hours EHR time averaging 52 min/day (benchmark: less than 30)
- Top DP signal: Primary care patient satisfaction declined 8 percentile points over 6 months
- Top PA signal: CME completion rate dropped from 94% to 71% year-over-year
- Primary drivers: EHR inbox volume (72% cited), call schedule inequity (54%), administrative prior auth burden (48%)
- Priority interventions: Implement team-based inbox management (reduce physician inbox by 40%), equalize call distribution algorithm, add PA support for prior auth processing
- Estimated retention impact: 12% reduction in voluntary turnover based on peer benchmarks

## Guidelines

- **HIPAA Compliance**: Individual provider burnout data is sensitive employment information, not patient PHI, but must be handled with appropriate confidentiality protections. Aggregate analysis only for organizational reporting. Individual risk assessments shared only with the provider and designated wellness leadership.
- **Privacy and Trust**: Provider wellness data must never be used punitively. Establish clear data governance policies before implementing surveillance-based burnout detection. Obtain informed consent for monitoring programs.
- **Stigma Reduction**: Frame burnout detection as organizational health monitoring, not individual weakness identification. Normalize the conversation around burnout as occupational hazard.
- **Evidence Hierarchy**: Prioritize direct wellness survey data over operational proxies. Proxy-based detection should trigger check-ins, not conclusions.
- **Balanced Approach**: Always pair individual support with systemic interventions. Individual resilience programs without workload and systems changes are insufficient per NAM evidence.
- **Reporting Obligations**: Be aware of state-specific wellness program reporting requirements and medical board disclosure questions related to mental health treatment.

## Validation Checklist

- [ ] All three MBI dimensions assessed with proxy signals
- [ ] Operational workload metrics collected and benchmarked
- [ ] Temporal trend analysis completed (minimum 90-day window)
- [ ] Risk stratification applied with transparent criteria
- [ ] Driver analysis maps to Six Areas of Worklife model
- [ ] Interventions prioritize systemic over individual approaches
- [ ] Individual data protected with appropriate confidentiality
- [ ] Provider consent obtained for monitoring programs
- [ ] Aggregate reporting de-identified for organizational dashboards
- [ ] Intervention tracking established with 90-day review cycle
- [ ] Leadership accountability assigned for each intervention
- [ ] Connection to patient safety and quality outcomes documented
