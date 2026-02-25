---
name: Schedule Optimization Advisor
description: Optimize provider scheduling templates using demand pattern analysis, appointment type modeling, buffer optimization, and patient access analytics to maximize throughput, reduce wait times, and improve provider satisfaction.

metadata:
  display_name: "Schedule Optimization Advisor"
  short_description: "Optimize provider scheduling templates and patient access"
  default_prompt: "Optimize my provider scheduling templates and patient access and suggest the best next steps"
  version: "1.0.0"
  tags:
    - healthcare
  icon_path: "assets/icon.png"
---

# Schedule Optimization Advisor

## Overview

This skill analyzes and optimizes provider scheduling templates by modeling patient demand patterns, appointment type distributions, visit duration variability, and no-show behavior to create evidence-based schedule designs. Optimal scheduling balances patient access (short wait times), provider productivity (appropriate utilization), care quality (adequate visit time), and clinician well-being (manageable pace). Poor scheduling is a top driver of both patient access complaints and provider burnout. This skill applies operations research techniques and healthcare-specific constraints to generate implementable template recommendations.

## When to Use

- Redesigning provider scheduling templates for new or existing practices
- Addressing chronic access problems (long wait times, poor third-next-available)
- Reducing patient in-clinic wait times and cycle times
- Improving provider schedule utilization rates (target: 85-95% after no-shows)
- Implementing open access or advanced access scheduling models
- Balancing provider workload equity across a department or group
- Optimizing appointment mix (new vs. follow-up, in-person vs. telehealth)

## Required Inputs

| Input | Description | Format |
|-------|-------------|--------|
| `current_templates` | Existing schedule templates by provider with slot types and durations | JSON array |
| `appointment_data` | 12+ months of scheduling data with types, durations, outcomes | De-identified JSON |
| `demand_patterns` | Appointment request volumes by day, time, type, and urgency | JSON object |
| `no_show_data` | No-show and cancellation rates by day, time, type, and patient segment | JSON object |
| `cycle_time_data` | Check-in to check-out times, provider face time, room turnaround | JSON object |
| `provider_preferences` | Provider schedule preferences and constraints | JSON object |
| `access_targets` | Organizational access goals (TNAA, wait time, utilization) | JSON object |

## Methodology

### Step 1: Current State Analysis
- Profile current scheduling performance:
  - Template utilization rate: (filled slots / available slots) by provider, day, and time
  - Effective utilization: (completed visits / available slots) accounting for no-shows
  - Third-next-available appointment (TNAA) by provider and visit type
  - Same-day and urgent request fulfillment rate
  - Patient cycle time: arrival to rooming, rooming to provider, provider to checkout
  - Schedule variance: actual visit duration vs. allotted time by appointment type
  - Overbooking frequency and impact on wait times
- Identify scheduling pattern problems:
  - Demand-supply mismatch by day of week and time of day
  - Appointment type mismatch (wrong slot types offered vs. demand)
  - No-show clustering patterns
  - End-of-day overtime and start-of-day underutilization

### Step 2: Demand Pattern Modeling
- Analyze appointment demand across dimensions:
  - Day-of-week demand curves (typically: Monday highest, Friday/Wednesday variable)
  - Time-of-day preferences (morning vs. afternoon demand by patient segment)
  - Seasonal patterns (flu season, back-to-school, year-end insurance utilization)
  - Urgent vs. routine demand ratio (target: 25-35% same-day/urgent capacity)
  - New patient vs. follow-up ratio by specialty
  - Telehealth demand by visit type and patient segment
- Forecast demand using time series analysis with seasonal adjustment
- Model demand elasticity: how does supply change affect demand capture?

### Step 3: Visit Duration Optimization
- Analyze actual visit durations by appointment type:
  - Calculate mean, median, standard deviation, and 90th percentile
  - Identify visit types with high duration variance (candidates for template differentiation)
  - Separate provider face time from total cycle time
- Recommend appointment slot durations:
  - Set slot duration at 75th-85th percentile of actual duration (balances throughput with overrun risk)
  - Create differentiated slot types for visit complexity:
    - Brief follow-up: 10-15 minutes
    - Standard follow-up: 15-20 minutes
    - Complex visit or new patient: 30-40 minutes
    - Procedure: procedure-specific duration + setup and recovery buffer
  - Build in transition time between appointments (3-5 minutes for documentation)

### Step 4: Template Design
- Construct optimized scheduling templates:
  - **Demand-matched supply**: Align available slots to demand curves (more morning slots if demand peaks AM)
  - **Mixed appointment types**: Interleave complex and simple visits to manage provider cognitive load
  - **Same-day access blocks**: Reserve 15-25% of daily capacity for same-day/urgent (vary by specialty)
  - **Telehealth blocks**: Dedicate blocks for virtual visits (reduce room turnaround constraints)
  - **Administrative time**: Protected time for inbox, charting, peer review (minimum 1 hour/day)
  - **Buffer slots**: Strategic empty slots at predictable bottleneck times
  - **New patient clustering**: Schedule new patients early in session when provider is freshest
- Apply constraints:
  - Provider preferences (teaching days, OR days, meeting schedules)
  - Room and equipment availability
  - Support staff scheduling alignment
  - Regulatory requirements (supervising provider presence for APPs)

### Step 5: No-Show and Cancellation Management
- Integrate no-show predictions into template design:
  - Calculate expected show rate by slot (day, time, type, patient segment)
  - Apply smart overbooking: overbook in high no-show slots, not universally
  - Overbooking formula: overbook_count = floor(slot_count x predicted_no_show_rate x 0.7)
  - Implement waitlist management: auto-offer cancelled slots to waitlisted patients
  - Design cancellation backfill workflow with maximum fill-time targets
- Monitor overbooking impact:
  - Patient wait time should not increase more than 10 minutes on overbooked days
  - Provider overtime should not exceed 30 minutes on overbooked days

### Step 6: Performance Monitoring and Iteration
- Establish ongoing monitoring dashboard:
  - Daily: utilization rate, no-show rate, overtime hours
  - Weekly: TNAA by provider, same-day fill rate, cycle time averages
  - Monthly: access target achievement, patient satisfaction impact, provider satisfaction
- Create feedback loop:
  - Quarterly template review with providers
  - Statistical process control on key metrics
  - A/B testing of template changes (pilot with subset of providers before rollout)

## Output Specification

```yaml
schedule_optimization:
  current_state:
    avg_utilization: number
    avg_effective_utilization: number
    avg_tnaa_days: number
    avg_cycle_time_minutes: number
    same_day_fill_rate: number
  optimized_template:
    - provider_type: string
      sessions_per_week: number
      slots_per_session: number
      slot_mix:
        - type: string
          duration_minutes: number
          count_per_session: number
      same_day_reserve_pct: number
      telehealth_block_pct: number
      admin_time_minutes_per_day: number
      overbooking_strategy:
        slots_to_overbook: number
        criteria: string
  projected_improvements:
    utilization_increase: string
    tnaa_reduction: string
    same_day_capacity_change: string
    overtime_impact: string
    patient_wait_time_impact: string
  implementation_plan:
    phases: array
    pilot_providers: array
    rollout_timeline: string
    monitoring_metrics: array
```

## Analysis Framework

Apply **Lean Healthcare Scheduling** principles combined with operations research:
1. **Demand leveling**: Match supply to demand patterns rather than arbitrary equal distribution
2. **Flow optimization**: Minimize bottlenecks and waiting through smart sequencing
3. **Pull scheduling**: Reserve capacity for same-day demand rather than front-loading
4. **Variation reduction**: Standardize visit durations and workflows to reduce schedule disruption
5. **Continuous improvement**: Monitor, measure, and iterate based on performance data

## Examples

**Example: Primary Care Practice (6 Providers)**
- Current state: 73% effective utilization, TNAA 12 days, 22% no-show rate
- Optimized template changes:
  - Shifted from uniform 20-min slots to differentiated (10/15/20/30 min)
  - Added 20% same-day reserve (released at 3 PM day prior if unfilled)
  - Implemented demand-matched templates (heavier AM Monday/Tuesday, lighter Friday PM)
  - Smart overbooking in high no-show slots (2 per session max)
  - Added 30 min protected admin time mid-morning and mid-afternoon
- Projected results: Effective utilization 86%, TNAA 4 days, patient wait time reduced 8 minutes, provider overtime reduced 40%

## Guidelines

- **HIPAA Compliance**: Scheduling analytics use appointment data that may contain PHI (patient identifiers, diagnoses). Ensure all analytical data is de-identified. Aggregate reporting by slot type and time, not by individual patient.
- **Provider Engagement**: Template changes must be co-designed with providers. Imposed schedule changes without input drive dissatisfaction and turnover. Use shared governance model for template decisions.
- **Patient Access Equity**: Ensure same-day access is available across all locations, not concentrated in select sites. Monitor access metric equity across patient insurance types.
- **Work-Life Balance**: Schedule optimization must not eliminate protected time or increase total clinical hours. Efficiency gains should benefit both access and provider well-being.
- **Gradual Implementation**: Roll out template changes incrementally (1-2 providers as pilot for 4-6 weeks before broader deployment). Measure impact before scaling.

## Validation Checklist

- [ ] Current state analysis completed with utilization, TNAA, and cycle time baselines
- [ ] Demand patterns modeled across day, time, season, and visit type
- [ ] Visit duration analysis based on actual data, not assumptions
- [ ] Template design includes same-day access, admin time, and telehealth
- [ ] No-show management integrated with smart overbooking strategy
- [ ] Provider preferences and constraints incorporated
- [ ] Projected improvements quantified with realistic assumptions
- [ ] Pilot plan designed with measurable success criteria
- [ ] Monitoring dashboard specified with daily, weekly, and monthly metrics
- [ ] Provider engagement and co-design process documented
- [ ] Patient access equity analysis included
- [ ] HIPAA compliance verified for scheduling data usage
