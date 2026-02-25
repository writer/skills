---
name: new-product-launch-readiness
description: >
  Evaluates the launch readiness of new CPG or retail products by assessing market opportunity, competitive
  positioning, operational preparedness, and go-to-market strategy. Use when the user is planning a new product
  launch, wants to assess launch risk, evaluate market entry timing, or needs a structured readiness checklist.
  Triggers on requests about new product launch, product launch readiness, launch assessment, go-to-market
  evaluation, NPD readiness, or new item setup.

metadata:
  display_name: "New Product Launch Readiness"
  short_description: "Assess CPG new product launch readiness and go-to-market"
  default_prompt: "Optimize my new product launch and suggest the best next steps"
  version: "1.0.0"
  tags:
    - commerce-intelligence
    - new-product-launch-readiness
    - cpg-retail
  icon_path: "assets/icon.png"
---

# New Product Launch Readiness

## Overview

New Product Launch Readiness provides a comprehensive assessment framework for evaluating whether a new CPG or retail product is ready for market introduction. In the CPG industry, 70–80% of new product launches fail within the first year, with the primary causes being insufficient market understanding, poor differentiation, inadequate distribution, and weak execution. This skill systematically evaluates readiness across five dimensions—market, product, commercial, operational, and financial—to identify gaps before launch and maximize success probability.

This is not a concept screening tool; it assumes the product concept has been validated and focuses on execution readiness in the 90 days leading up to and 90 days following launch.

## When to Use

- 90–120 days before a planned product launch for readiness assessment
- Gate review in a Stage-Gate NPD process (specifically Gate 4: Launch Readiness)
- Post-launch performance evaluation (comparing results to pre-launch assumptions)
- Portfolio prioritization: comparing launch readiness across multiple pipeline items
- Retailer presentation preparation: demonstrating launch rigor to buyer
- User asks about launching a new product or evaluating launch preparedness

## Required Inputs

| Input | Required | Description |
|---|---|---|
| Product concept | Yes | Product description, positioning, target consumer, key claims |
| Category/market data | Yes | Category size, growth rate, competitive landscape |
| Product specs | Yes | Formulation/design, packaging, sizes, variants, UPC, shelf life |
| Pricing strategy | Yes | Suggested retail, margin structure, price positioning |
| Distribution plan | Recommended | Target retailers, channel strategy, expected distribution (% ACV) |
| Marketing plan | Recommended | Media spend, sampling, trade promotion, digital strategy |
| Supply chain readiness | Recommended | Manufacturing status, inventory availability, lead times |
| Financial projections | Recommended | Year 1 revenue forecast, P&L, break-even timeline |
| Competitive intelligence | Optional | Competitive product details, pricing, market share |
| Consumer research | Optional | Concept test scores, purchase intent data, usage test results |

## Methodology

### Step 1: Market Opportunity Assessment

Evaluate the market context for the launch:

**Category Attractiveness Score** (0–100):
| Factor | Weight | Scoring Criteria |
|---|---|---|
| Category size | 20% | > $1B = 100, $500M–$1B = 75, $100M–$500M = 50, < $100M = 25 |
| Category growth | 25% | > 5% = 100, 3–5% = 75, 1–3% = 50, < 1% or declining = 25 |
| Competitive intensity | 20% | Low (fragmented) = 100, Medium = 60, High (concentrated) = 30 |
| Consumer trend alignment | 20% | Strong tailwind = 100, Neutral = 50, Headwind = 20 |
| Margin potential | 15% | > Category avg = 100, At avg = 60, Below avg = 30 |

**Market gap validation**: Cross-reference with Assortment Gap Analysis—does the new product fill an identified gap?

**Timing assessment**: Is market timing favorable? Consider seasonality, competitive launch windows, regulatory changes.

### Step 2: Product Differentiation Evaluation

Assess whether the product offers meaningful differentiation:

**Differentiation Scorecard**:

| Dimension | Score (1-5) | Evidence |
|---|---|---|
| **Unique benefit** | — | Does it offer something competitors don't? |
| **Perceptible difference** | — | Can consumers see/taste/feel the difference without being told? |
| **Sustainable advantage** | — | How long before competitors can copy? (< 6 months = 1, > 2 years = 5) |
| **Brand fit** | — | Does it leverage existing brand equity and credibility? |
| **Price/value proposition** | — | Does the price-to-benefit ratio make sense vs. alternatives? |

**Minimum threshold**: Average score must be ≥ 3.0 to proceed. Any dimension scoring 1 is a red flag requiring resolution.

**Consumer validation**: Map concept test scores to launch success probability:
- Top-2-Box Purchase Intent > 40%: Strong (historical success rate ~45%)
- Top-2-Box 30–40%: Moderate (success rate ~25%)
- Top-2-Box < 30%: Weak (success rate ~10%)

Adjust for category-specific norms; purchase intent benchmarks vary by category.

### Step 3: Commercial Readiness Assessment

**Distribution Readiness**:
```
Distribution Score = Confirmed ACV% / Target ACV% × 100
```
- Target: > 80% of planned distribution confirmed before launch
- Minimum viable: 40% ACV in Year 1 for national brands; 15% for regional/niche

**Retail Execution Checklist**:
- [ ] Buyer authorization confirmed at target retailers
- [ ] Shelf placement/planogram position confirmed
- [ ] New item setup complete (UPC registered, item master, images, content)
- [ ] First PO placed or committed
- [ ] Promotional plan agreed (intro deals, slotting, display)
- [ ] In-store execution standards documented (shelf tag, position, facings)

**Pricing Architecture Validation**:
```
Price Index vs. Category = New Product Price / Category Average Price × 100
```
Validate that pricing is consistent with positioning:
- Premium positioning: PI 115–140
- Mainstream: PI 95–110
- Value: PI 70–90

### Step 4: Operational Readiness Assessment

**Supply Chain Readiness Score**:

| Factor | Status | Risk Level |
|---|---|---|
| Manufacturing line validated | Ready/In Progress/Not Started | — |
| First production run completed | — | — |
| Quality standards met | — | — |
| Packaging approved and sourced | — | — |
| Inventory available (weeks of supply) | — | Target: 6–8 weeks at launch |
| Logistics/warehousing set up | — | — |
| Retailer EDI/data integration | — | — |

**Launch Inventory Calculation**:
```
Launch Inventory = (Target Stores × Units/Store/Week × Pipeline Fill Weeks) + Safety Stock
```
Where Pipeline Fill = time to fill shelf + distribution center + in-transit. Typically 4–8 weeks for CPG.

### Step 5: Financial Viability Check

**Year 1 Revenue Forecast Validation**:
```
Revenue = Target ACV% × Stores in ACV × Units/Store/Week × 52 × ASP × (1 − Trade Rate)
```

**Velocity Benchmark**: Compare projected units/store/week to category norms:
- Top-quartile launch: > 2× category average velocity
- Median launch: 0.8–1.5× category average
- Struggling launch: < 0.5× category average

**Break-Even Analysis**:
```
Break-Even Volume = Fixed Launch Costs / (ASP − Variable Cost per Unit)
Break-Even Timeline = Break-Even Volume / (Projected Weekly Volume × 52)
```
Target: break-even within 18–24 months for most CPG launches.

**P&L Waterfall**: Revenue → COGS → Gross Margin → Trade Spend → Marketing → Contribution Margin

### Step 6: Launch Readiness Score

Compute an overall readiness score:

```
Launch Readiness Score = Σ (Dimension Score × Dimension Weight)
```

| Dimension | Weight | Score (0-100) | Weighted |
|---|---|---|---|
| Market Opportunity | 20% | — | — |
| Product Differentiation | 25% | — | — |
| Commercial Readiness | 25% | — | — |
| Operational Readiness | 20% | — | — |
| Financial Viability | 10% | — | — |
| **Total** | **100%** | — | **—** |

**Decision thresholds**:
- **≥ 75**: Green — Proceed with launch
- **60–74**: Yellow — Proceed with conditions (address specific gaps)
- **< 60**: Red — Delay launch; critical gaps must be resolved

## Output Specification

### 1. Launch Readiness Dashboard

One-page summary with overall score, dimension scores, traffic-light indicators, and top 3 risks.

### 2. Detailed Dimension Scorecards

Breakdowns for each of the 5 dimensions with evidence, scores, and gap identification.

### 3. Risk Register

| Risk | Probability | Impact | Severity | Mitigation |
|---|---|---|---|---|
| Distribution below target | — | — | — | — |

### 4. Action Plan (Countdown to Launch)

| Weeks to Launch | Action Item | Owner | Status |
|---|---|---|---|
| T−12 | Confirm retailer authorizations | — | — |
| T−8 | First production run complete | — | — |
| T−4 | Launch inventory in distribution | — | — |
| T−0 | In-store date / go-live | — | — |
| T+4 | First read of launch performance | — | — |
| T+13 | 90-day post-launch review | — | — |

### 5. Post-Launch KPI Tracker

Metrics to monitor weekly for the first 13 weeks, with targets and trigger points for intervention.

## Analysis Framework

### Key Launch Metrics

- **Trial Rate**: % of target consumers who purchase in first 13 weeks (benchmark: 5–15% for CPG)
- **Repeat Rate**: % of triers who repurchase (benchmark: 25–40% for successful launches)
- **Velocity (units/store/week)**: vs. category average and vs. plan
- **Distribution Build**: Actual ACV% vs. plan by week
- **Share of Shelf**: Facings and shelf position achieved
- **Awareness**: Aided/unaided awareness in target market (if measured)
- **Incrementality**: % of new product sales that are incremental to the category vs. cannibalization of own portfolio
- **Retailer Scorecard Compliance**: On-shelf availability, display execution, price compliance

### Success Rate Benchmarks

- CPG new product 1-year survival rate: 20–30%
- Products with distribution > 50% ACV in Week 13 survive at 2× the rate of those below
- Products achieving > 80% of velocity target in first 4 weeks have 60%+ chance of year-1 success
- Marketing spend of 25–40% of Year 1 revenue is typical for successful CPG launches

## Examples

**Input**: "We're launching a new plant-based protein bar in 8 weeks. It's a premium product ($3.49, category average is $2.29), sold through natural/specialty and mainstream grocery. We have confirmed authorization at Whole Foods and Sprouts (12% ACV), with Target and Kroger pending (additional 38% ACV). Manufacturing is ready. Marketing budget is $2M. Evaluate our launch readiness."

**Output**:
1. **Overall Readiness Score: 62 (Yellow — Proceed with Conditions)**
2. **Market Opportunity: 78** — Plant-based snacking is a $4.2B category growing 12%. Strong tailwind.
3. **Product Differentiation: 72** — Unique flavor profiles, clean ingredient list. However, protein bar space is crowded (200+ competitors). Differentiation is moderate.
4. **Commercial Readiness: 48 (RED)** — Only 12% ACV confirmed with 8 weeks to launch. Target and Kroger not confirmed. Pricing at PI 152 vs. category is very premium—may limit velocity in mainstream grocery.
5. **Operational Readiness: 82** — Manufacturing validated, 8 weeks of inventory available, packaging approved.
6. **Financial: 55** — Revenue forecast assumes 50% ACV; only 12% is confirmed. Break-even requires 22 months at current projections.
7. **Top Risks**: (a) Distribution gap — launch with 12% ACV instead of 50% will deliver $1.8M vs. $4.5M Year 1 revenue; (b) Premium pricing may limit trial in mainstream; (c) Competitor Brand Y launching similar product in 6 weeks.
8. **Recommendation**: Delay mainstream launch by 8 weeks to secure Target/Kroger authorization. Launch on-time in Whole Foods/Sprouts (natural channel) as Phase 1. Use Phase 1 velocity data to strengthen mainstream retail pitch.

## Guidelines

- Assess readiness across all five dimensions — a product can be brilliant but fail due to poor distribution or supply chain
- Be honest about distribution reality: confirmed POs are the only reliable measure, not buyer conversations or "expected" authorizations
- Apply the 13-week rule: launch performance should be evaluated at Week 13 (one quarter), not Week 1–2
- For premium-priced launches, validate the price/value proposition with consumer research; pricing > 130% of category index has significantly lower success rates
- Consider competitive timing: launching into a competitor's major promotional period or new product launch wave reduces share of attention
- Marketing front-loading matters: 60–70% of launch marketing spend should land in the first 8 weeks to drive trial
- Plan for contingencies: what if distribution is 50% of target? What if velocity is 30% below plan? Have trigger points and contingency actions defined
- For line extensions vs. entirely new brands, adjust success benchmarks: extensions have 2× the survival rate of new brands
- Include retailer perspective: what does the retailer need to see (velocity, margin, incrementality) to keep the item past reset?

## Validation Checklist

- [ ] All five readiness dimensions are scored with evidence
- [ ] Market opportunity is validated with category data, not just intuition
- [ ] Distribution plan has confirmed vs. pending clearly distinguished
- [ ] Pricing is benchmarked against category and competitive set
- [ ] Supply chain has been tested (first production run, quality approval)
- [ ] Financial projections use confirmed (not aspirational) distribution
- [ ] Risk register identifies at least 3 risks with mitigation plans
- [ ] Post-launch KPI targets are defined with intervention triggers
- [ ] Competitive response scenario is considered
- [ ] Countdown action plan covers T−12 weeks through T+13 weeks
