---
name: market-expansion-analysis
description: Analyze viability of new clinic locations, facility expansions, or market entry for healthcare organizations. Use when evaluating geographic expansion opportunities, assessing market demand, performing competitive analysis, or building financial pro formas for new facilities.

metadata:
  display_name: "Market Expansion Analysis"
  short_description: "Evaluate healthcare facility expansion and market viability"
  default_prompt: "Analyze my market expansion and recommend clear next actions"
  version: "1.0.0"
  tags:
    - healthcare
  icon_path: "assets/icon.png"
---

# Market Expansion Analysis

## Overview

This skill evaluates the strategic and financial viability of healthcare market expansion — new clinic openings, satellite facility launches, geographic market entry, and de novo hospital development. It integrates demographic demand modeling, competitive landscape analysis, regulatory feasibility, and financial pro forma construction to produce comprehensive expansion recommendations.

## When to Use

- Evaluating potential locations for new ambulatory clinics or urgent care centers
- Assessing feasibility of entering a new geographic market
- Building a business case for facility expansion or service line addition
- Analyzing competitive dynamics and market share opportunity
- Supporting certificate-of-need (CON) applications
- Evaluating acquisition targets' market position and growth potential

## Required Inputs

| Input | Description | Format |
|-------|-------------|--------|
| Target market demographics | Population, age distribution, growth projections, income | Census/ACS data |
| Health demand indicators | Disease prevalence, utilization rates, unmet need | CDC/BRFSS/HCUP |
| Competitive landscape | Existing facilities, providers, bed counts, market share | Market intelligence |
| Payer mix | Insurance coverage distribution, employer-sponsored rates | Market data |
| Real estate data | Available sites, lease/purchase costs, zoning | Commercial RE data |
| Regulatory requirements | CON laws, licensure, zoning, credentialing timelines | Regulatory reference |
| Organization financials | Current margins, cost structure, capital availability | Internal finance |

## Methodology

### Step 1 — Define Target Market and Service Area

Establish the geographic scope of the expansion analysis:

- Define primary service area (PSA): geography from which 70-80% of patients will originate
- Define secondary service area (SSA): geography for remaining 20-30%
- Use drive-time analysis (15-minute for primary care, 30-minute for specialty, 60-minute for tertiary)
- Map zip codes and census tracts to service area boundaries
- Calculate total population and demographic composition within service area

Key demographic factors:
- Population size and density (minimum thresholds by service type)
- Age distribution (aging populations drive higher healthcare demand)
- Population growth projections (5- and 10-year census forecasts)
- Income levels and insurance coverage rates
- Housing development pipeline (new residential construction)

### Step 2 — Estimate Healthcare Demand

Quantify the addressable market:

- **Demand by service type**: Apply age/sex-specific utilization rates to target population
  - Primary care visits per 1,000 by age band
  - Specialty referral rates by prevalence and utilization norms
  - ED visits, IP admissions, surgical cases per 1,000
- **Unmet demand**: Identify populations currently traveling outside the area for care (leakage analysis)
- **Growth demand**: Project volume increases from population growth and aging
- **Pent-up demand**: Estimate demand from uninsured/underinsured populations gaining coverage

### Step 3 — Analyze Competitive Landscape

Map existing healthcare supply in the target market:

- **Inventory**: All hospitals, ambulatory centers, physician practices, urgent care, retail clinics within service area
- **Capacity metrics**: Bed counts, OR suites, provider FTEs, appointment availability
- **Market share**: Inpatient discharge share by hospital, outpatient visit share by system
- **Quality comparison**: Star Ratings, Leapfrog grades, patient satisfaction scores
- **Strategic positioning**: Competitors' announced expansion plans, capital projects, partnerships

Identify competitive gaps:
- Underserved specialties (no nearby provider for specific services)
- Capacity constraints (long wait times, full panels, high occupancy rates)
- Quality gaps (below-average performers creating switching opportunity)
- Geographic gaps (population pockets far from existing facilities)

### Step 4 — Assess Regulatory and Operational Feasibility

Evaluate non-financial barriers to entry:

- **Certificate of Need (CON)**: Does the state require CON? For which services? Application timeline and success probability
- **Licensure**: State licensing requirements for the facility type, timeline
- **Zoning and permitting**: Local zoning compatibility, variance requirements, community resistance
- **Credentialing**: Provider credentialing timelines for target payers
- **Payer contracting**: Ability to secure in-network contracts with major payers in the market
- **Workforce availability**: Local labor market for nurses, techs, administrative staff (vacancy rates, wage levels)

### Step 5 — Build Financial Pro Forma

Construct a 5-year financial projection:

| Component | Detail |
|-----------|--------|
| Capital investment | Facility build-out/lease improvements, equipment, IT, working capital |
| Revenue model | Volume ramp (typically 30% Y1, 60% Y2, 85% Y3, 100% Y4), payer mix, revenue per visit/case |
| Operating expenses | Physician and staff compensation, supplies, rent, insurance, marketing, administrative |
| Contribution margin | By year, by service, by payer |
| Break-even analysis | Months/years to monthly break-even, cumulative break-even |
| NPV and IRR | 5-year discounted cash flow at organizational WACC |

Apply sensitivity analysis on:
- Volume ramp (slower, base, faster)
- Payer mix (more/less favorable)
- Rate environment (reimbursement trends)
- Competition response (new entrant, price war)

### Step 6 — Score and Rank Opportunities

Apply a weighted scoring framework:

| Criterion | Weight | Scoring (1-5) |
|-----------|--------|---------------|
| Market demand / population growth | 25% | Based on demand analysis |
| Competitive position / gap opportunity | 20% | Based on competitive analysis |
| Financial attractiveness (NPV, IRR) | 25% | Based on pro forma |
| Strategic alignment | 15% | Fit with organizational mission and capabilities |
| Operational feasibility | 15% | Regulatory, workforce, timeline |

### Step 7 — Formulate Expansion Recommendation

Produce a go/no-go recommendation with supporting rationale:

- **Strong go**: High demand, limited competition, attractive financials, strategic alignment
- **Conditional go**: Favorable fundamentals but specific risks to mitigate (CON approval, payer contracting)
- **Defer**: Market is promising but timing is wrong (build capability first, wait for population growth)
- **No go**: Insufficient demand, saturated market, unattractive economics, or strategic misalignment

## Output Specification

```
Market Expansion Analysis:
├── Executive Summary (opportunity assessment, recommendation, key metrics)
├── Market Demographic Profile (population, growth, age, income, insurance)
├── Healthcare Demand Model (by service type, current and projected)
├── Competitive Landscape Map (facilities, market share, quality, gaps)
├── Regulatory Feasibility Assessment (CON, licensing, zoning, timeline)
├── Financial Pro Forma (5-year P&L, capital requirements, NPV, IRR)
├── Sensitivity Analysis (volume, payer mix, competition scenarios)
├── Opportunity Scoring Matrix (weighted criteria, ranked opportunities)
├── Implementation Timeline (milestones from decision to first patient)
└── Risk Register (key risks with mitigation strategies)
```

## Analysis Framework

### Market Attractiveness Matrix

| | Low Competition | High Competition |
|---|------|------|
| **High Demand** | Prime opportunity — move quickly | Selective entry — differentiate or niche |
| **Low Demand** | Niche opportunity — targeted services | Avoid — insufficient opportunity |

### Facility Type Decision Criteria

| Indicator | Primary Care Clinic | Multi-Specialty | Urgent Care | ASC | Hospital |
|-----------|-------------------|-----------------|-------------|-----|----------|
| Min population | 10,000 | 50,000 | 25,000 | 75,000 | 150,000+ |
| Capital range | $1-3M | $5-15M | $2-5M | $10-25M | $100M+ |
| Break-even | 12-18 mo | 24-36 mo | 6-12 mo | 18-24 mo | 36-60 mo |
| Typical margin | 5-15% | 15-25% | 15-25% | 30-45% | 5-12% |

## Examples

**Example 1 — Primary Care Clinic Expansion**
Evaluate 5 potential sites for new primary care clinics in a growing suburban market. Site A: 45,000 population within 10-min drive, 2 competing practices, 12% population growth projected. Site B: 60,000 population, 5 competing practices, 3% growth. Score and rank: Site A scores 4.2 (high demand, low competition, strong growth), Site B scores 2.8 (adequate demand but saturated). Recommend Site A with 3-provider clinic, projected break-even at 14 months, 5-year NPV $2.1M.

**Example 2 — Market Entry Feasibility**
Assess entering a new metropolitan market with a multi-specialty ambulatory center. Market: 350,000 population, 3 health systems with 82% combined market share, moderate growth (5% projected). Competitive gap identified in orthopedics (8-week wait times at existing systems) and cardiology (no outpatient cath lab). Model a 15-provider multi-specialty center with orthopedics and cardiology focus. Capital: $12M. 5-year NPV: $4.8M (base), −$1.2M (pessimistic if dominant system responds aggressively). Recommend conditional go with phased entry.

## Guidelines

- Use the most recent Census Bureau and ACS data for demographic projections
- Validate demand models against actual utilization data from comparable markets
- Always model competitive response scenarios — incumbents rarely ignore new entrants
- Include realistic volume ramp curves — new facilities rarely reach full capacity in Year 1
- Account for cannibalization of existing organizational facilities in the same market
- Factor in telehealth as both a complement to and substitute for physical facility expansion

## Validation Checklist

- [ ] Population and demographic data are from current, authoritative sources
- [ ] Demand model uses age/sex-adjusted utilization rates appropriate to the market
- [ ] All major competitors identified and mapped
- [ ] Regulatory requirements researched for the specific state and locality
- [ ] Pro forma assumptions are documented and stress-tested
- [ ] Workforce availability assessment includes local wage benchmarking
- [ ] Implementation timeline accounts for permitting, construction, credentialing, payer contracting

## HIPAA Compliance

Market expansion analysis primarily uses publicly available demographic and market data and does not typically involve PHI. However, if organizational patient origin data, utilization patterns, or member-level data is used for demand modeling or leakage analysis, all processing must comply with HIPAA Privacy and Security Rules. De-identify patient data before geographic mapping. Reports shared with external consultants, real estate advisors, or joint venture partners must not contain PHI and should be covered by appropriate confidentiality agreements.
