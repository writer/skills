---
name: value-based-care-readiness
description: Assess organizational readiness for value-based care contracts including shared savings, bundled payments, capitation, and global risk arrangements. Use when evaluating VBC contract opportunities, identifying capability gaps, building VBC transition roadmaps, or benchmarking VBC maturity.

metadata:
  display_name: "Value Based Care Readiness"
  short_description: "Assess organizational readiness for value-based care deals"
  default_prompt: "Optimize my value based care and suggest the best next steps"
  version: "1.0.0"
  tags:
    - healthcare
  icon_path: "assets/icon.png"
---

# Value-Based Care Readiness

## Overview

This skill evaluates an organization's preparedness to enter or advance in value-based care (VBC) arrangements by assessing capabilities across clinical operations, data infrastructure, financial risk management, provider network, and governance. It applies VBC maturity models, financial scenario analysis, and industry readiness frameworks to produce actionable assessments with prioritized gap-closure roadmaps.

## When to Use

- Evaluating whether to enter a new VBC contract (MSSP, MA, commercial shared savings, bundled payments)
- Assessing readiness to move from upside-only to downside-risk arrangements
- Identifying capability gaps that must be addressed before assuming additional financial risk
- Benchmarking VBC maturity against industry peers
- Building a multi-year VBC transition roadmap for strategic planning

## Required Inputs

| Input | Description | Format |
|-------|-------------|--------|
| Current contracts | Existing VBC arrangements, terms, performance history | Contract summaries |
| Quality performance | HEDIS, Star Ratings, MSSP quality scores | Quality dashboard |
| Financial data | PMPM costs, MLR, medical cost trend, claims data | Financial tables |
| Infrastructure inventory | Care management platforms, analytics, HIE connectivity | Capability assessment |
| Provider network | Panel sizes, specialty coverage, referral patterns | Network data |
| Governance structure | VBC leadership, committees, physician engagement | Organizational data |

## Methodology

### Step 1 — Assess Current VBC Position

Map the organization on the VBC continuum:

| Stage | Model | Risk Level | Characteristics |
|-------|-------|------------|-----------------|
| 1 — Fee-for-Service | Traditional FFS | None | Volume-based, no quality linkage |
| 2 — Pay-for-Performance | FFS + quality bonuses | Minimal | Quality incentives layered on FFS |
| 3 — Shared Savings (upside) | MSSP Track 1, commercial SS | Low-moderate | Savings sharing, no downside |
| 4 — Shared Risk | MSSP Enhanced, commercial | Moderate | Both upside and downside exposure |
| 5 — Bundled Payments | BPCI-A, CJR | Moderate-high | Episode-based accountability |
| 6 — Full/Global Capitation | MA, global risk | High | Full premium risk, PMPM payment |

Document: current stage, revenue under VBC (% of total), contract performance history, and trend.

### Step 2 — Evaluate Readiness Across Five Domains

Score each domain on a 1-5 maturity scale:

**Domain 1 — Clinical Capability (Weight: 25%)**
- Care management programs (disease management, transitional care, complex care)
- Clinical protocols and pathways for high-cost conditions
- Patient engagement and activation tools
- SDOH screening and community resource integration
- Behavioral health integration
- Population health analytics (risk stratification, predictive models)

**Domain 2 — Data and Analytics (Weight: 25%)**
- Claims and clinical data integration (multi-payer, EHR, labs, pharmacy, HIE)
- Real-time analytics, risk stratification, and predictive modeling capability
- Quality measure calculation engine and financial/actuarial modeling

**Domain 3 — Financial Readiness (Weight: 20%)**
- Total cost of care and PMPM economics understanding with actuarial capability (IBNR, reserves)
- Stop-loss/reinsurance strategy, adequate capital reserves for downside exposure
- MLR management and experience with claims payment or delegated functions

**Domain 4 — Network and Provider Engagement (Weight: 20%)**
- Provider network adequacy for covered population
- Specialist referral management (narrow network, preferred specialists)
- Provider performance transparency and variation reduction
- Physician compensation aligned with VBC goals
- Provider education and engagement in quality improvement
- Care compact agreements with high-value partners

**Domain 5 — Governance and Leadership (Weight: 10%)**
- Dedicated VBC leadership (CMO, VP of population health) and board-level oversight
- Cross-functional VBC steering committee with payer relationship management
- Change management capability and legal/compliance expertise in risk arrangements

### Step 3 — Conduct Financial Scenario Modeling

Model the financial impact of proposed VBC contracts:

- **Total cost of care analysis**: Calculate current PMPM by service category for target population
- **Benchmark comparison**: Compare against CMS benchmarks, regional averages, or contract-specified targets
- **Savings potential**: Estimate addressable medical cost reduction (utilization management, care management, network optimization)
- **Downside exposure**: Model worst-case loss scenarios under proposed risk corridors
- **Break-even analysis**: Calculate minimum savings percentage needed to avoid losses
- **Sensitivity testing**: Vary assumptions on enrollment, trend, and savings capture rate

### Step 4 — Identify Critical Gaps

For each domain scoring below target maturity:

- Specify the gap (what's missing or insufficient)
- Assess the gap's impact on VBC success (critical, important, or nice-to-have)
- Estimate time and investment to close the gap
- Identify dependencies between gaps (data infrastructure enables care management)
- Prioritize by: risk-to-contract-performance, cost-to-close, time-to-close

### Step 5 — Build VBC Readiness Roadmap

Create a phased transition plan:

| Phase | Timeline | Focus | Milestone |
|-------|----------|-------|-----------|
| Foundation | 0-12 months | Data integration, care management standup, provider education | Analytics platform live, CM program enrolled |
| Launch | 12-24 months | Enter upside-only contracts, pilot programs | First shared savings contract signed |
| Acceleration | 24-36 months | Assume downside risk, expand programs | Positive shared savings earned |
| Optimization | 36-48 months | Full risk / capitation readiness | Global risk contract feasibility confirmed |

### Step 6 — Benchmark Against Peers

Compare readiness against industry VBC adoption benchmarks:

- Percentage of revenue under VBC (HCPLAN framework categories)
- Peer organization maturity scores (similar size, market, patient mix)
- Industry leaders' capability profiles as aspirational targets
- Market-specific factors (state Medicaid VBC mandates, employer demands, MA penetration)

### Step 7 — Present Readiness Assessment

Produce a structured recommendation:

- Overall readiness score (composite of domain scores, weighted)
- Go/no-go recommendation for specific contract types
- Critical path items that must be addressed before contract execution
- Investment budget for gap closure activities
- Expected timeline to target VBC maturity stage

## Output Specification

```
VBC Readiness Assessment:
├── Executive Summary (current state, readiness score, recommendation)
├── VBC Continuum Position (current stage with benchmarks)
├── Domain Maturity Scores (radar chart across 5 domains)
├── Financial Scenario Analysis (PMPM, savings potential, risk exposure)
├── Gap Inventory (prioritized by impact and urgency)
├── Readiness Roadmap (phased plan with milestones and investment)
├── Peer Benchmarking (maturity comparison)
├── Contract-Specific Readiness (go/no-go for each contract type)
└── Investment Budget and Resource Requirements
```

## Analysis Framework

### VBC Maturity Scoring

| Score | Maturity Level | Description |
|-------|---------------|-------------|
| 1 | Initial | No formal capability; ad hoc processes |
| 2 | Developing | Basic capability exists but inconsistent |
| 3 | Defined | Standardized processes, moderate effectiveness |
| 4 | Managed | Data-driven, continuously measured and improved |
| 5 | Optimized | Best-in-class, predictive, fully integrated |

### Contract-Type Readiness Thresholds

| Contract Type | Minimum Overall Score | Critical Domain Thresholds |
|---------------|----------------------|---------------------------|
| P4P | 2.0 | Quality ≥ 2 |
| Upside-only shared savings | 2.5 | Data ≥ 3, Clinical ≥ 2 |
| Two-sided shared savings | 3.0 | All domains ≥ 2, Financial ≥ 3 |
| Bundled payments | 3.0 | Clinical ≥ 3, Data ≥ 3 |
| Global capitation | 4.0 | All domains ≥ 3, Financial ≥ 4 |

## Examples

**Example 1 — MSSP Track Advancement**
Assess a 200-physician ACO currently in MSSP BASIC Track for readiness to move to ENHANCED Track (downside risk). Domain scores: Clinical 3.2, Data 2.8, Financial 2.4, Network 3.0, Governance 3.5. Overall: 2.96. Gap: Financial readiness below threshold — lacks actuarial capability and stop-loss strategy. Recommendation: Engage actuarial consultant, secure stop-loss reinsurance, and delay Enhanced Track entry by 12 months.

**Example 2 — MA Global Risk Feasibility**
Evaluate a health system's readiness to accept MA global capitation for 30,000 lives. Overall score: 3.4. Strengths: clinical programs (4.1), governance (3.8). Gaps: data integration (2.9 — lacking real-time claims feed), financial risk management (2.7 — no catastrophic reserve). Model shows $4.2M downside exposure in worst-case scenario, requiring $6M reserve fund. Recommend 18-month preparation phase.

## Guidelines

- Readiness is population-specific — an organization may be ready for VBC with one population but not another
- Financial modeling must include catastrophic risk scenarios, not just average-case
- Provider engagement is often the rate-limiting factor — assess physician buy-in realistically
- VBC readiness assessment should be updated annually as capabilities evolve
- Distinguish between capability presence and capability effectiveness — having a care management program is different from having an effective one

## Validation Checklist

- [ ] All five domains assessed with specific evidence for each score
- [ ] Financial scenarios include pessimistic, base, and optimistic cases
- [ ] Domain scores are validated by operational leaders (not self-assessed by VBC team alone)
- [ ] Gap priorities reflect actual contract requirements, not generic best practices
- [ ] Roadmap timelines are realistic given organizational change capacity
- [ ] Peer benchmarks are from comparable organizations
- [ ] Investment estimates include both capital and operating costs

## HIPAA Compliance

VBC readiness assessments may involve analysis of claims data, quality measures, and patient-level utilization patterns. All data processing must comply with HIPAA Privacy and Security Rules. Financial modeling using claims data requires minimum necessary access. Readiness reports shared with potential VBC partners or consultants must use de-identified or aggregate data, or require executed Business Associate Agreements. Quality performance data shared externally must comply with applicable state and federal reporting requirements.
