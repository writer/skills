---
name: Provider Capacity Forecasting
description: Predict provider capacity shortages and surpluses using demand modeling, wRVU productivity analysis, panel-size optimization, and workforce pipeline analytics to inform strategic recruitment and scheduling decisions.

metadata:
  display_name: "Provider Capacity Forecasting"
  short_description: "Forecast provider capacity shortages and surpluses"
  default_prompt: "Optimize my provider capacity forecasting and suggest the best next steps"
  version: "1.0.0"
  tags:
    - healthcare
  icon_path: "assets/icon.png"
---

# Provider Capacity Forecasting

## Overview

This skill forecasts provider capacity supply and demand across specialties and service lines using wRVU (work Relative Value Unit) productivity analysis, patient panel modeling, demographic demand projections, and workforce pipeline data. It enables health systems to anticipate shortages 6-24 months ahead, optimize existing capacity allocation, and make evidence-based recruitment and expansion decisions. The AAMC projects a physician shortage of 37,800 to 124,000 by 2034, making proactive capacity planning essential for ensuring access and financial sustainability.

## When to Use

- Annual strategic workforce planning and recruitment prioritization
- Evaluating capacity impact of new service lines, facility expansions, or acquisitions
- Assessing impact of provider retirements, departures, or leave on access
- Optimizing provider-to-patient panel ratios across primary care sites
- Preparing for value-based care population health management requirements
- Responding to access complaints or growing appointment wait times
- Informing GME program development and advanced practice provider deployment

## Required Inputs

| Input | Description | Format |
|-------|-------------|--------|
| `provider_roster` | Current providers by specialty, FTE, location, contract end date, age | JSON array |
| `wrvu_data` | Historical wRVU production by provider and specialty (12-24 months) | JSON object |
| `appointment_data` | Scheduling data with wait times, fill rates, demand indicators | JSON object |
| `patient_demographics` | Service area population by age, sex, insurance, growth projections | JSON object |
| `utilization_rates` | Historical and projected utilization rates by specialty | JSON object |
| `pipeline_data` | Recruitment pipeline, residency completion dates, APP onboarding | JSON array |
| `financial_data` | Revenue per wRVU, compensation benchmarks, contribution margin | JSON object |

## Methodology

### Step 1: Current Capacity Inventory
- Enumerate current provider capacity by specialty:
  - Total FTE by specialty and location
  - Clinical FTE (adjusted for administrative, research, teaching, and leadership time)
  - wRVU production per clinical FTE vs. MGMA/AMGA benchmarks:
    - Family Medicine median: 4,200-4,800 wRVU/yr
    - Internal Medicine median: 4,500-5,200 wRVU/yr
    - Cardiology median: 7,000-8,500 wRVU/yr
    - Orthopedic Surgery median: 8,000-10,000 wRVU/yr
    - Psychiatry median: 3,800-4,500 wRVU/yr
  - Panel size per primary care provider (target: 1,800-2,500 empaneled patients per 1.0 FTE)
  - Advanced practice provider (APP) capacity as physician-equivalent FTE (typically 0.6-0.8)
- Identify capacity at risk:
  - Providers within 5 years of typical retirement age (65)
  - Contract expirations within 12 months
  - Known leave plans (parental, sabbatical, medical)
  - Burnout risk indicators (cross-reference with burnout detection skill)

### Step 2: Demand Modeling
- Project patient demand by specialty:
  - **Demographic demand**: Apply age-sex utilization rates to population projections
    - Use CMS utilization data or proprietary actuarial tables
    - Account for aging population effects (65+ population growing 3.2% annually)
    - Incorporate migration and growth patterns from census and planning data
  - **Epidemiological demand**: Disease prevalence trends affecting specialty need
    - Obesity, diabetes, behavioral health prevalence trajectories
    - Post-pandemic behavioral health demand surge
  - **Market demand**: Competitive landscape and market share assumptions
    - New entrants, competitor expansions, payer network changes
  - **Programmatic demand**: Planned service line expansions, new contracts, VBC populations
  - **Regulatory demand**: Changing screening guidelines, quality measure requirements
- Express demand in required wRVU capacity and required FTE by specialty

### Step 3: Supply-Demand Gap Analysis
- Calculate gap for each specialty and location:
  - Gap = Projected Demand FTE - (Current FTE - Attrition + Pipeline)
  - Positive gap = shortage (need more providers)
  - Negative gap = surplus (potential for redeployment or growth absorption)
- Project gaps at 6-month, 12-month, 18-month, and 24-month horizons
- Sensitivity analysis: model optimistic, baseline, and pessimistic scenarios
  - Optimistic: low attrition, strong recruitment, moderate demand growth
  - Baseline: historical attrition, expected recruitment, projected demand
  - Pessimistic: high attrition, limited recruitment, accelerated demand

### Step 4: Financial Impact Assessment
- Quantify financial impact of capacity gaps:
  - Revenue at risk from unfilled demand (wRVU gap x revenue per wRVU)
  - Recruitment cost per specialty (MGMA benchmark: 25K-50K per physician)
  - Ramp-up time to full productivity (typically 12-18 months for new physicians)
  - Locum tenens cost for interim coverage vs. permanent hire
  - Lost downstream revenue from referral leakage due to access constraints
- Calculate ROI for recruitment investments and APP expansion

### Step 5: Optimization Strategies
- Generate capacity optimization recommendations before new recruitment:
  - **Schedule optimization**: Reduce no-shows, optimize template utilization
  - **APP deployment**: Expand APP scope for routine visits, freeing physician capacity
  - **Telehealth expansion**: Convert appropriate visit types to virtual (typically 20-30% eligible)
  - **Team-based care**: Implement collaborative practice models (RN care management, pharmacist MTM)
  - **Panel rebalancing**: Redistribute patients across providers to equalize workload
  - **Efficiency improvements**: Reduce EHR burden, streamline workflows, add scribes
- Estimate FTE equivalents recovered from each optimization strategy

### Step 6: Recruitment Priority Ranking
- Rank specialties for recruitment priority using weighted scoring:
  - Access gap severity (wait time above benchmark): 25% weight
  - Revenue impact: 20% weight
  - Strategic alignment (VBC, service line growth): 20% weight
  - Attrition risk: 15% weight
  - Community need (HPSA designation, CHNA findings): 10% weight
  - Competitive vulnerability: 10% weight
- Generate recruitment timeline with realistic onboarding assumptions

## Output Specification

```yaml
capacity_forecast:
  forecast_date: date
  forecast_horizon_months: number
  specialty_analysis:
    - specialty: string
      current_fte: number
      clinical_fte: number
      current_wrvu_per_fte: number
      benchmark_wrvu: number
      productivity_percentile: number
      attrition_risk_fte: number
      pipeline_fte: number
      projected_demand_fte:
        6_month: number
        12_month: number
        24_month: number
      gap:
        6_month: number
        12_month: number
        24_month: number
      revenue_at_risk: number
      recruitment_priority_score: number
  optimization_opportunities:
    - strategy: string
      estimated_fte_equivalent: number
      implementation_timeline: string
      investment_required: number
  recruitment_plan:
    - specialty: string
      positions_needed: number
      priority_rank: number
      target_start_date: date
      estimated_recruitment_cost: number
      ramp_to_full_productivity_months: number
  scenario_analysis:
    optimistic: object
    baseline: object
    pessimistic: object
```

## Analysis Framework

Apply the **AAMC Workforce Planning Model** adapted for health system use:
1. **Supply modeling**: Current inventory + pipeline - projected attrition
2. **Demand modeling**: Population demographics x utilization rates + programmatic demand
3. **Gap analysis**: Supply - demand = shortage or surplus
4. **Intervention modeling**: Optimization, recruitment, and scope expansion strategies
5. **Financial modeling**: Revenue impact, investment requirements, ROI

## Examples

**Example: Regional Health System Workforce Forecast**
- System: 8 hospitals, 120 ambulatory sites, 1,200 providers
- Critical shortages identified (24-month): Psychiatry (gap: 8.2 FTE), Gastroenterology (gap: 4.5 FTE), Primary Care (gap: 12.0 FTE)
- Surplus identified: General Surgery (surplus: 2.1 FTE, absorbed by new trauma center)
- Optimization potential: Telehealth expansion in primary care = 3.5 FTE equivalent, APP deployment in GI = 2.0 FTE equivalent
- Net recruitment need: Psychiatry 6 positions, GI 2 positions, Primary Care 8 positions
- Revenue at risk without action: 14.2M annually from primary care leakage alone
- Recruitment investment: 2.1M estimated with 18-month ROI

## Guidelines

- **HIPAA Compliance**: Workforce analytics do not typically involve PHI but may reference patient volumes. Ensure any patient data used in demand modeling is aggregated and de-identified. Provider productivity data should be handled per employment confidentiality policies.
- **Data Quality**: wRVU data must account for provider ramp-up periods, leave, and part-time status. Normalize productivity to clinical FTE, not total FTE. Validate data against billing system and EHR independently.
- **Market Sensitivity**: Recruitment priority rankings and compensation benchmarks are competitively sensitive. Restrict distribution to strategic planning leadership.
- **Equity Lens**: Evaluate whether capacity gaps disproportionately affect underserved communities (HPSA, MUA designations). Prioritize recruitment that addresses health equity gaps.
- **Scenario Planning**: Never present a single forecast as definitive. Always provide scenario ranges with explicit assumptions documented.

## Validation Checklist

- [ ] Current capacity inventory complete with clinical FTE adjustments
- [ ] wRVU productivity benchmarked against MGMA or equivalent data source
- [ ] Demand model incorporates demographic, epidemiological, and programmatic factors
- [ ] Attrition projections account for retirement, burnout risk, and contract timelines
- [ ] Supply-demand gaps calculated at multiple time horizons
- [ ] Financial impact quantified with revenue-at-risk analysis
- [ ] Optimization strategies evaluated before defaulting to recruitment
- [ ] Recruitment priorities ranked with transparent weighted scoring
- [ ] Scenario analysis includes optimistic, baseline, and pessimistic projections
- [ ] Pipeline data validated and onboarding timelines realistic
- [ ] Equity impact assessed for underserved population access
- [ ] Forecast assumptions documented for leadership review
