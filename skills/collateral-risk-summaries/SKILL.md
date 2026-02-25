---
name: collateral-risk-summaries
description: Assess and summarize collateral risk for secured lending decisions including real estate, equipment, inventory, and receivables. Use when evaluating collateral adequacy, preparing collateral risk sections for credit memos, monitoring collateral value deterioration, reviewing appraisals, or assessing liquidation recovery scenarios.

metadata:
  display_name: "Collateral Risk Summaries"
  short_description: "Assess collateral risk and recovery for secured lending"
  default_prompt: "Summarize my collateral risk with key findings and next steps"
  version: "1.0.0"
  tags:
    - financial-services
  icon_path: "assets/icon.png"
---

# Collateral Risk Summaries

## Overview

Produce comprehensive collateral risk assessments for secured lending transactions. This skill evaluates collateral type, valuation methodology, marketability, environmental risk, lien position, and expected liquidation recovery to generate structured risk summaries suitable for credit memoranda, loan committee presentations, and ongoing portfolio monitoring. Assessments incorporate advance rate frameworks, collateral-specific depreciation models, and stress-tested recovery scenarios.

## When to Use

- Evaluating collateral adequacy for new loan originations or renewals
- Preparing the collateral section of credit memoranda for loan committee
- Reviewing appraisal reports for completeness and reasonableness
- Monitoring collateral value changes during the loan life (annual reviews, impairment triggers)
- Assessing liquidation scenarios for distressed or workout situations
- Determining appropriate advance rates for asset-based lending facilities

## Required Inputs

| Input | Description | Format |
|-------|-------------|--------|
| Collateral description | Type, location, condition, specifications | Structured data |
| Valuation report | Appraisal, BPO, desktop valuation, or internal assessment | Appraisal document |
| Loan terms | Amount, LTV, advance rate, lien position | Loan structure |
| Market data | Comparable sales, market trends, vacancy rates | Market analysis |
| Environmental reports | Phase I/II ESA results, known contamination | Environmental docs |
| Insurance coverage | Hazard, flood, liability coverage amounts | Insurance certs |
| Legal review | Title, lien search, UCC filing status | Legal documents |

## Methodology

### Step 1 — Collateral Classification and Eligibility

Classify the collateral and determine eligibility under the lending program:

- **Real estate**: Commercial (office, retail, industrial, multifamily, special purpose), residential (1–4 family, condo, manufactured)
- **Equipment**: General purpose vs. special purpose, mobile vs. fixed, age and remaining useful life
- **Inventory**: Raw materials, work-in-process, finished goods — eligible vs. ineligible categories
- **Receivables**: Eligible A/R (age < 90 days, no concentration > 25%, no intercompany, no government without assignment)
- **Securities**: Marketable vs. restricted, margin requirements, custodial arrangements
- **Other**: Intellectual property, business enterprise value, personal guarantees, life insurance CSV

Determine ineligible collateral components: environmentally contaminated, contested title, uninsurable, cross-collateralized with senior liens exceeding value.

### Step 2 — Valuation Assessment and Reconciliation

Evaluate the collateral valuation for completeness and reasonableness:

- **Appraisal methodology review**: Confirm appropriate approach used
  - Income approach: Cap rate supported by market data, NOI calculated correctly, vacancy and expense assumptions reasonable
  - Sales comparison: Comparables are truly comparable (location, size, age, condition, timing)
  - Cost approach: Replacement cost accurate, depreciation reasonable, land value supported
- **Reconciliation**: If multiple approaches used, verify reconciliation logic and final value
- **Red flag identification**:
  - Value significantly above recent purchase price without justification
  - Cap rates below market norms for the property type and submarket
  - Unsupported adjustments to comparables exceeding 25%
  - Appraisal ordered by borrower rather than lender
  - Appraiser unfamiliar with the local market or property type
- **Mark-to-market adjustments**: Apply index-based adjustments for existing collateral (HPI for residential, NCREIF/CoStar for commercial)

### Step 3 — Advance Rate Determination

Apply appropriate advance rates based on collateral type and quality:

| Collateral Type | Standard Advance Rate | Stressed Advance Rate | Notes |
|----------------|----------------------|----------------------|-------|
| 1–4 Family Residential | 75%–80% | 60%–65% | Higher for owner-occupied |
| Commercial RE (stabilized) | 70%–75% | 55%–65% | Varies by property type |
| Commercial RE (construction) | 60%–65% | 45%–55% | Based on costs-to-date |
| Equipment (general purpose) | 70%–80% | 50%–60% | Orderly liquidation value |
| Equipment (special purpose) | 40%–60% | 25%–40% | Forced liquidation value |
| Eligible A/R | 80%–85% | 65%–75% | Net of dilution and disputes |
| Eligible Inventory | 50%–65% | 30%–45% | Depends on marketability |
| Marketable Securities | 50%–70% | 35%–50% | Margin loan requirements |

Adjust advance rates downward for: illiquid markets, deferred maintenance, environmental concerns, declining market trends, or special-purpose properties.

### Step 4 — Risk Factor Analysis

Assess specific risk factors affecting collateral value stability:

- **Market risk**: Local market supply/demand dynamics, absorption rates, development pipeline
- **Obsolescence risk**: Functional obsolescence (floor plan, ceiling height), economic obsolescence (market shifts)
- **Environmental risk**: Phase I findings requiring Phase II, known contamination, proximity to industrial sites
- **Regulatory risk**: Zoning changes, rent control, building code compliance, ADA requirements
- **Concentration risk**: Over-reliance on single tenant, geographic area, or property type
- **Physical condition**: Deferred maintenance, remaining useful life of major systems (roof, HVAC, elevator)
- **Insurance adequacy**: Coverage amount vs. replacement cost, flood zone determination, earthquake exposure

### Step 5 — Liquidation Recovery Scenario Analysis

Model recovery under multiple liquidation scenarios:

- **Orderly liquidation (12–18 months)**: Market-rate disposition with reasonable marketing period
  - Apply 10%–15% discount to current appraised value
  - Deduct: broker commissions (5%–6%), closing costs (2%–3%), carrying costs (interest, taxes, insurance, maintenance during marketing period)
- **Forced liquidation (3–6 months)**: Accelerated sale under distressed conditions
  - Apply 25%–40% discount to current appraised value
  - Deduct: Same cost categories plus potential auction/receiver fees
- **Net recovery calculation**:

```
Net Recovery = Liquidation Value
             - Senior liens (if any)
             - Selling costs
             - Carrying costs during liquidation
             - Environmental remediation costs (if applicable)
             - Legal/foreclosure costs
```

### Step 6 — Lien Position and Legal Perfection Review

Verify collateral security and perfection:

- **Title search**: Confirm clear title with no unexpected liens, judgments, or encumbrances
- **Lien position**: Verify the institution holds the intended priority position
- **UCC filings**: Confirm UCC-1 filed in correct jurisdiction with accurate debtor/collateral description
- **Insurance**: Named as loss payee/additional insured on all required policies
- **Flood determination**: FEMA flood zone check; flood insurance if in SFHA
- **Property taxes**: Current status — delinquent taxes create superior liens
- **Guarantees**: Personal guarantee and guarantor financial capacity assessment

### Step 7 — Generate Collateral Risk Summary

Compile all analysis into a structured summary for credit documentation:

## Output Specification

```
## Collateral Risk Summary

### Collateral Overview
- Type: [Classification]
- Description: [Property/asset description]
- Location: [Address/jurisdiction]
- Appraised/assessed value: $[X]
- Valuation date: [Date]
- Valuation method: [Income/Sales/Cost/Combination]

### Valuation Assessment
- Methodology: [Appropriate/Concerns noted]
- Red flags: [None/Identified — description]
- Mark-to-market adjustment: [X]% → Adjusted value: $[X]

### Advance Rate Analysis
| Metric | Value |
|--------|-------|
| Loan amount | $[X] |
| Appraised value | $[X] |
| Standard advance rate | XX% |
| Proposed LTV | XX% |
| LTV vs. advance rate | [Within / Exceeds — by X%] |

### Risk Factors
| Factor | Rating | Commentary |
|--------|--------|-----------|
| Market conditions | [Low/Med/High] | [Detail] |
| Environmental | [Low/Med/High] | [Detail] |
| Physical condition | [Low/Med/High] | [Detail] |
| Obsolescence | [Low/Med/High] | [Detail] |
| Insurance adequacy | [Adequate/Deficient] | [Detail] |

### Liquidation Recovery Analysis
| Scenario | Gross Value | Costs | Net Recovery | Recovery % |
|----------|------------|-------|-------------|-----------|
| Orderly (12–18 mo) | $[X] | $[X] | $[X] | XX% |
| Forced (3–6 mo) | $[X] | $[X] | $[X] | XX% |

### Legal Perfection
- Title: [Clear/Exceptions noted]
- Lien position: [1st/2nd — confirmed/unconfirmed]
- UCC status: [Filed/Pending]
- Insurance: [Adequate/Deficient]

### Overall Collateral Risk Rating: [Low / Moderate / Elevated / High]
### Recommendation: [Accept / Accept with conditions / Decline]
```

## Analysis Framework

Apply the **VALUE** framework:

- **V**aluation — Assess the quality and reasonableness of the collateral valuation
- **A**dvance rate — Determine the appropriate advance rate for the collateral type and quality
- **L**iquidation — Model recovery scenarios under orderly and forced disposition
- **U**nderlying risks — Identify environmental, market, physical, and legal risk factors
- **E**nforceability — Verify lien perfection, insurance, and legal access to collateral

## Examples

**Example 1 — Multifamily Property**

72-unit apartment complex, Class B, built 1998. Appraised at $9.8M using 5.8% cap rate on $568K NOI. Comparables support cap rate. Occupancy 94% (market 96%). Deferred maintenance: $180K (roof, parking lot). Phase I: No RECs. Flood zone: X (no flood insurance required). Proposed loan: $6.86M (70% LTV). Orderly liquidation recovery: $7.9M net of costs. Forced liquidation: $5.7M. Risk rating: Moderate — manageable deferred maintenance, stable market fundamentals. Recommendation: Accept with condition that deferred maintenance be addressed within 12 months, escrowed from loan proceeds.

**Example 2 — Special-Purpose Equipment**

CNC machining center, 2019 vintage, original cost $1.2M. Orderly liquidation value (OLV) per equipment appraiser: $720K (60% of cost). Forced liquidation value: $420K (35% of cost). Equipment is bolted to foundation — removal cost estimated at $45K. Proposed advance: $500K (69% of OLV). Market for used CNC equipment is active with multiple dealer channels. Risk rating: Moderate — active secondary market but high removal/transport costs. Recommendation: Accept at 65% of OLV ($468K) to provide cushion for removal and transport costs.

## Guidelines

- Require independent appraisals for all real estate collateral above de minimis thresholds ($500K)
- Use OLV (orderly liquidation value) rather than FMV for equipment advance rate calculations
- Apply haircuts to inventory advance rates for perishable, fashion-sensitive, or technology items
- Update collateral valuations at minimum annually for criticized assets, every 3 years for pass
- Require Phase I ESA for all commercial real estate; Phase II if Phase I identifies RECs
- Verify insurance annually and immediately upon any casualty loss notification
- Cross-reference property tax records to confirm no delinquencies creating senior liens
- Document all appraisal review findings per FIRREA and interagency appraisal guidelines

## Validation Checklist

- [ ] Collateral correctly classified and eligible under the lending program
- [ ] Valuation methodology is appropriate for the collateral type
- [ ] Appraisal red flags identified and addressed or escalated
- [ ] Advance rate is consistent with policy for the collateral type and quality
- [ ] All material risk factors documented with ratings and commentary
- [ ] Liquidation recovery modeled under both orderly and forced scenarios
- [ ] Liquidation costs are realistic (commissions, carrying costs, legal fees)
- [ ] Lien position confirmed through title search or UCC search
- [ ] Insurance coverage adequate and institution named as loss payee
- [ ] Environmental risk appropriately assessed (Phase I at minimum for CRE)
