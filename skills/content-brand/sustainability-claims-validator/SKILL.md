---
name: Sustainability Claims Validator
description: Validate environmental, social, and governance (ESG) claims for accuracy, substantiation, and compliance with FTC Green Guides, EU Green Claims Directive, and retailer sustainability programs.

metadata:
  display_name: "Sustainability Claims Validator"
  short_description: "Validate ESG and sustainability claims for FTC compliance"
  default_prompt: "Check my sustainability claims for gaps risks and required fixes"
  version: "1.0.0"
  tags:
    - cpg-retail
  icon_path: "assets/icon.png"
---

# Sustainability Claims Validator

## Overview

This skill validates sustainability and ESG-related claims on product packaging, marketing materials, and e-commerce listings against regulatory frameworks and emerging legislation. Greenwashing risk is at an all-time high — the FTC, EU, and class-action plaintiffs are aggressively pursuing vague or unsubstantiated environmental claims.

The validator ensures that every sustainability claim is specific, substantiated, and compliant with current and pending regulations, protecting brands from enforcement actions, retailer penalties, and consumer trust erosion.

## When to Use

- Reviewing product claims that reference environmental benefits (recyclable, biodegradable, carbon neutral, sustainable).
- Preparing for retailer sustainability scorecard submissions (Walmart Project Gigaton, Target Forward, Amazon Climate Pledge Friendly).
- Validating ESG report language that appears in consumer-facing materials.
- Assessing new sustainability certifications for marketing use.
- Auditing existing content after regulatory changes (FTC Green Guides update, EU Green Claims Directive).
- Evaluating supplier sustainability claims in co-branded or private label products.

## Required Inputs

| Input | Description | Example |
|---|---|---|
| `claims` | All sustainability-related claims to validate | List of claim strings with source location |
| `substantiation` | Supporting evidence for each claim | LCA data, certifications, test reports |
| `product_info` | Product composition, packaging materials, supply chain | Bill of materials, packaging spec |
| `certifications` | Active sustainability certifications | `["FSC Certified", "Cradle to Cradle", "B Corp"]` |
| `target_markets` | Regulatory jurisdictions | `["US", "EU", "UK", "Canada"]` |
| `channel` | Where claims will appear | "Packaging", "PDP", "social media ad" |
| `retailer_programs` | Applicable retailer sustainability programs | "Climate Pledge Friendly", "Walmart ESG" |
| `competitive_context` | Competitor sustainability claims for benchmarking | URLs or claim summaries |

## Methodology

### Step 1 — Claim Extraction & Categorization

Identify and classify every sustainability-related claim:

| Category | Examples | Key Risk |
|---|---|---|
| **Recyclability** | "Recyclable", "Made from recycled materials", "100% recyclable packaging" | Must reflect actual recycling infrastructure access |
| **Biodegradability** | "Biodegradable", "Compostable", "Breaks down naturally" | Requires specific timeframe and conditions |
| **Carbon/Climate** | "Carbon neutral", "Net zero", "Climate positive", "Low carbon footprint" | Must be substantiated by verified offsets or LCA |
| **Material Sourcing** | "Sustainably sourced", "Responsibly harvested", "Conflict-free" | Vague unless tied to certification or audit |
| **Water/Energy** | "Water-saving", "Energy efficient", "Reduced water footprint" | Requires quantified comparison and baseline |
| **Social Impact** | "Fair trade", "Living wage", "Community supported" | Must meet specific certification criteria |
| **Circularity** | "Zero waste", "Circular economy", "Refillable" | Must demonstrate closed-loop system |
| **General Environmental** | "Eco-friendly", "Green", "Sustainable", "Earth-friendly" | Highest greenwashing risk — nearly always flagged |

### Step 2 — FTC Green Guides Analysis (US)

Apply the FTC's Guides for the Use of Environmental Marketing Claims (16 CFR 260):

1. **General Principles**:
   - Claims must be clear, prominent, and specific — not vague or overly broad.
   - Qualifications must be clear, prominent, and in close proximity to the claim.
   - Claims should be substantiated by competent and reliable evidence.

2. **Specific Claim Rules**:

| Claim | FTC Green Guides Requirement |
|---|---|
| "Recyclable" | Substantial majority (≥ 60%) of consumers/communities have access to recycling for that material. Otherwise qualify: "Check locally — not recycled in all communities." |
| "Recycled Content" | Must specify pre-consumer vs. post-consumer recycled content. "Made with 30% post-consumer recycled plastic." |
| "Biodegradable" | Must completely break down and return to nature within one year. Cannot claim for landfill-disposed products. |
| "Compostable" | Must break down in a composting facility at the same rate as known compostable materials. Specify if industrial composting required. |
| "Carbon Neutral" / "Carbon Offset" | Must account for full lifecycle emissions. Offsets must be verified by recognized standards (Gold Standard, VCS). Cannot imply zero emissions. |
| "Non-Toxic" | Must substantiate for human and environmental exposure pathways. Extremely difficult to defend as an absolute claim. |
| "Free of [substance]" | Only meaningful if the substance is normally present in competitors' products and the absence provides environmental benefit. |
| "Sustainable" | Too vague as standalone. Must be qualified with specific, verifiable meaning. |

### Step 3 — EU Green Claims Directive Compliance

For EU-market claims, apply the proposed Green Claims Directive (2023/0085(COD)):

1. Claims must be substantiated by a life cycle assessment (LCA) or recognized scientific methodology.
2. Primary data must be used where available; secondary data only with justification.
3. Claims must distinguish between the product and the company's overall operations.
4. Carbon offsetting cannot be the sole basis for "carbon neutral" or "climate neutral" claims.
5. Generic environmental claims ("eco-friendly," "green") are prohibited without approved EU Ecolabel or equivalent.
6. Sustainability labels must be based on third-party verified certification schemes.

### Step 4 — Substantiation Depth Assessment

For each claim, evaluate the depth and quality of supporting evidence:

| Evidence Level | Description | Confidence |
|---|---|---|
| **Level 1 — Certified** | Third-party certification from recognized body (FSC, Cradle to Cradle, B Corp, SCS Global) | High |
| **Level 2 — Verified** | Independent audit or verified LCA data | High |
| **Level 3 — Tested** | Internal testing with documented methodology | Medium |
| **Level 4 — Calculated** | Internal calculations based on industry data | Medium-Low |
| **Level 5 — Asserted** | Claim made without independent verification | Low — Flag for substantiation |

Claims at Level 4-5 receive automatic warnings. Claims at Level 5 with high consumer visibility are flagged as critical.

### Step 5 — Retailer Program Alignment

Validate claims against specific retailer sustainability program requirements:

| Program | Key Requirements |
|---|---|
| **Amazon Climate Pledge Friendly** | Must hold qualifying third-party certification (Compact by Design, SCS, Cradle to Cradle, etc.) |
| **Walmart Project Gigaton** | Quantified emissions, waste, or resource reduction commitments with annual reporting |
| **Target Forward** | Sustainable materials commitments with defined timelines |
| **Kroger Zero Hunger / Zero Waste** | Packaging recyclability and food waste reduction |

### Step 6 — Greenwashing Risk Scoring

Apply the **Greenwashing Risk Index** to each claim:

| Factor | Weight | High Risk Indicators |
|---|---|---|
| Specificity | 25% | Vague language, no quantification, no timeframe |
| Substantiation | 25% | No third-party verification, no supporting data |
| Materiality | 20% | Claim about trivial aspect while ignoring larger impacts |
| Transparency | 15% | Hidden trade-offs, lifecycle cherry-picking |
| Comparability | 15% | Misleading comparisons, undefined baselines |

**Risk Score**: 0-100 (lower = less risk). Claims scoring > 60 require revision. Claims > 80 are blocked.

## Output Specification

```yaml
output:
  overall_risk_level: string          # "low" | "moderate" | "high" | "critical"
  greenwashing_risk_score: float      # 0-100
  claims_analysis: list[ClaimAnalysis]
  compliant_claims: int
  non_compliant_claims: int
  flagged_claims: int
  required_substantiation: list[string]  # Evidence gaps to fill
  compliant_rewrites: dict             # Original → substantiated alternative
  retailer_program_status: dict        # Program → pass/fail/gap
  regulatory_references: list[string]  # Applicable regulatory citations
  publication_recommendation: string   # "approved" | "revise" | "blocked"
```

## Analysis Framework

**Sustainability Claims Maturity Model**:

| Level | Description | Typical Claims |
|---|---|---|
| **Level 1 — Aspirational** | Claims based on goals, not current state | "Committed to sustainability" |
| **Level 2 — Directional** | Claims show progress without quantification | "Reducing our carbon footprint" |
| **Level 3 — Quantified** | Claims include specific, measurable data | "Reduced packaging weight by 20% since 2020" |
| **Level 4 — Verified** | Claims independently audited or certified | "FSC Certified packaging; verified by SCS Global" |
| **Level 5 — Systemic** | Full lifecycle transparency, science-based targets | "SBTi-validated 50% scope 1+2 reduction by 2030" |

Target Level 3+ for all consumer-facing claims. Level 1-2 claims in advertising are high greenwashing risk.

## Examples

**Input Claim**: "Eco-Friendly Packaging — Our bottles are good for the planet!"

**Analysis**:
- **Greenwashing Risk**: 85/100 (Critical)
- **Issues**: (1) "Eco-friendly" is vague, undefined — FTC Green Guides violation. (2) "Good for the planet" is an unqualified general environmental benefit claim. (3) No specificity on what makes packaging eco-friendly.
- **Compliant Rewrite**: "Our bottles are made from 100% post-consumer recycled PET plastic, reducing virgin plastic use. Please recycle where facilities exist."
- **Substantiation Needed**: Recycled content certification (e.g., SCS Recycled Content), recycling access data.

## Guidelines

- "Sustainable," "eco-friendly," "green," and "earth-friendly" are effectively banned as standalone claims — always qualify with specifics.
- Carbon neutral / net zero claims are under increasing regulatory scrutiny — ensure offset quality and full lifecycle accounting.
- Do not claim recyclability unless the material is actually recycled (not just technically recyclable) in the majority of markets where sold.
- Anticipate regulation — the EU Green Claims Directive will make substantiation mandatory; prepare now.
- Track competitor claims for both benchmarking and potential FTC challenge opportunities.
- Maintain a substantiation file for every sustainability claim, accessible within 48 hours of a regulatory inquiry.

## Validation Checklist

- [ ] Every sustainability claim is extracted, categorized, and individually assessed.
- [ ] FTC Green Guides requirements are applied to each applicable claim type.
- [ ] EU Green Claims Directive requirements are applied for EU-market content.
- [ ] Substantiation evidence is evaluated and graded (Level 1-5).
- [ ] Greenwashing Risk Index score is calculated per claim.
- [ ] Vague or unqualified environmental claims are flagged or blocked.
- [ ] Carbon/climate claims include full lifecycle scope and verified offsets.
- [ ] Recyclability claims reflect actual recycling infrastructure access.
- [ ] Retailer sustainability program requirements are cross-referenced.
- [ ] Compliant alternative language is provided for every flagged claim.
