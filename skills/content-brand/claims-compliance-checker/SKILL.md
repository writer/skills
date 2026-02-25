---
name: Claims Compliance Checker
description: Validate product claims against FTC, FDA, EPA, and retailer-specific regulatory frameworks for CPG categories including food, supplements, OTC drugs, cosmetics, and household products.

metadata:
  display_name: "Claims Compliance Checker"
  short_description: "Validate CPG product marketing claims against FTC/FDA rules"
  default_prompt: "Check my claims compliance for gaps risks and required fixes"
  version: "1.0.0"
  tags:
    - cpg-retail
  icon_path: "assets/icon.png"
---

# Claims Compliance Checker

## Overview

This skill screens consumer-facing product claims for regulatory compliance across the major U.S. and EU frameworks governing CPG products. It identifies prohibited claims, flags unsubstantiated language, and suggests compliant alternatives — preventing costly warning letters, listing removals, and brand reputation damage.

The checker operates as a pre-publication gate in the content workflow, sitting between copywriting and go-live approval.

## When to Use

- Before publishing any PDP copy, packaging text, advertising creative, or social media content.
- When launching products in regulated categories (supplements, OTC, cosmetics, food, cleaning).
- After reformulating a product or changing ingredient sourcing.
- When expanding to new markets with different regulatory regimes (US → EU, US → Canada).
- During periodic compliance audits of existing content libraries.

## Required Inputs

| Input | Description | Example |
|---|---|---|
| `content` | The full text to be validated | PDP copy, ad script, packaging text |
| `product_category` | FDA/FTC product classification | "dietary supplement", "cosmetic", "conventional food", "OTC drug" |
| `approved_claims` | List of claims cleared by legal/regulatory | `["Clinically tested", "Dermatologist recommended"]` |
| `certifications` | Active third-party certifications | `["USDA Organic", "Non-GMO Project Verified", "NSF Certified"]` |
| `ingredient_list` | Full ingredient/supplement facts panel | Structured list |
| `target_markets` | Regulatory jurisdictions | `["US", "EU", "Canada"]` |
| `channel` | Distribution channel with its own policies | "Amazon", "Walmart", "Meta Ads", "Google Ads" |
| `substantiation_docs` | Available clinical studies, tests, or certifications | List of document references |

## Methodology

### Step 1 — Claim Extraction & Classification

Parse the content and identify every explicit or implicit claim. Classify each into:

| Claim Type | Definition | Example | Governing Authority |
|---|---|---|---|
| **Structure/Function** | Describes role of nutrient in body | "Supports immune health" | FDA (DSHEA) |
| **Health Claim** | Links substance to disease risk reduction | "May reduce risk of heart disease" | FDA (authorized/qualified) |
| **Drug Claim** | Claims to diagnose, treat, cure, or prevent disease | "Cures acne" | FDA (prohibited for non-drugs) |
| **Nutrient Content** | Quantifies nutrient level | "Excellent source of Vitamin C" | FDA (21 CFR 101.54) |
| **Cosmetic Claim** | Affects appearance, not structure | "Reduces appearance of wrinkles" | FTC / FDA |
| **Environmental** | Sustainability or eco-related | "Biodegradable", "Carbon neutral" | FTC Green Guides |
| **Comparative** | References competitors or alternatives | "50% more effective than leading brand" | FTC (substantiation required) |
| **Testimonial** | Consumer or expert endorsement | "9 out of 10 dentists recommend" | FTC Endorsement Guides |

### Step 2 — Regulatory Rule Application

For each claim, apply the relevant regulatory framework:

**FDA Framework (Food, Supplements, Cosmetics)**:
- Structure/function claims require the DSHEA disclaimer: *"This statement has not been evaluated by the FDA. This product is not intended to diagnose, treat, cure, or prevent any disease."*
- Health claims must be authorized (FDA-approved) or qualified (with required disclaimer language).
- Drug claims on non-drug products are **automatic violations** — flag as critical.
- Nutrient content claims must meet defined thresholds (e.g., "good source" = 10-19% DV per RACC).
- "Natural" on food: no FDA definition; flag for risk assessment. On cosmetics: must be substantiated.

**FTC Framework (Advertising)**:
- All claims must be truthful, not misleading, and substantiated before dissemination.
- Comparative claims require head-to-head testing or equivalent evidence.
- Testimonials must reflect typical results or include clear disclaimers.
- "Clinically proven" requires at least one well-designed, peer-reviewed clinical trial.
- Influencer/endorsement content must disclose material connections (#ad, #sponsored).

**EPA Framework (Household/Cleaning)**:
- Antimicrobial claims on surfaces require EPA registration.
- "Kills 99.9% of germs" requires specific EPA-registered test protocol reference.
- "Safer Choice" label requires active EPA partnership agreement.

**EU Framework (if applicable)**:
- Health claims must appear on the EU Register of authorized claims (EC 432/2012).
- "Free from" claims governed by allergen labeling regulation (EU 1169/2011).
- Cosmetic claims regulated by EC 655/2013 common criteria.

### Step 3 — Severity Scoring

Rate each flagged claim:

| Severity | Definition | Action |
|---|---|---|
| **Critical** | Illegal claim (drug claim on supplement, unauthorized health claim) | Block publication. Mandatory legal review. |
| **High** | Unsubstantiated claim that could trigger FTC/FDA action | Rewrite required before publication. |
| **Medium** | Technically compliant but misleading or missing required context | Add disclaimer or qualifying language. |
| **Low** | Style preference or best-practice recommendation | Suggest improvement; not a blocker. |

### Step 4 — Compliant Alternative Generation

For every flagged claim at medium severity or above, propose a compliant rewrite:

1. Downgrade drug claims to structure/function: "Cures joint pain" → "Supports joint comfort."
2. Add required qualifiers: "Clinically proven" → "Clinically tested in a 12-week study of 200 participants."
3. Replace absolute claims with hedged language: "Eliminates allergies" → "May help reduce common allergy symptoms."
4. Ensure environmental claims meet FTC Green Guides specificity: "Eco-friendly" → "Made with 80% post-consumer recycled plastic."

### Step 5 — Channel-Specific Policy Overlay

Apply retailer/platform-specific restrictions on top of regulatory rules:

| Channel | Key Restrictions |
|---|---|
| Amazon | No disease claims in any field; no references to FDA approval; restricted categories require pre-approval |
| Walmart | Prop 65 warnings required for CA; category-specific claim restrictions |
| Meta/Google Ads | No before/after for supplements; restricted health categories require certification |
| TikTok Shop | No medical claims; supplement ads require disclaimers in creative |

## Output Specification

```yaml
output:
  compliance_score: float           # 0-100 overall compliance rating
  total_claims_found: int
  claims_analysis: list[ClaimFinding]
  critical_violations: int
  high_violations: int
  medium_findings: int
  low_findings: int
  required_disclaimers: list[string]
  compliant_rewrites: dict          # Original → compliant alternative
  publication_recommendation: string # "approved" | "approved_with_changes" | "blocked"
  regulatory_references: list[string]
```

## Analysis Framework

The **Compliance Risk Matrix** cross-references two axes:

- **Likelihood of Enforcement** (low/medium/high): Based on category scrutiny, recent enforcement trends, and claim visibility.
- **Severity of Consequence** (low/medium/high): Warning letter, product seizure, class-action exposure, retailer delisting.

Claims in the high-likelihood × high-severity quadrant are critical blockers. Claims in low × low are informational only.

## Examples

**Input**: "Our probiotic gummy boosts immunity and prevents colds. Made with all-natural ingredients. #1 Doctor Recommended."

**Findings**:
1. "prevents colds" — **Critical**. Drug claim on a dietary supplement. FDA violation. → "Supports immune health†" + DSHEA disclaimer.
2. "boosts immunity" — **Medium**. Structure/function claim requires disclaimer notation (†). → Add DSHEA disclaimer.
3. "all-natural" — **Medium**. No FDA standard definition; FTC requires substantiation. → "Made with naturally sourced ingredients."
4. "#1 Doctor Recommended" — **High**. Requires substantiation (survey methodology, sample size). → "Recommended by doctors" with footnote to survey.

**Compliance Score**: 28/100. **Recommendation**: Blocked.

## Guidelines

- Always err on the side of caution — false negatives (missed violations) are far more costly than false positives.
- This skill does not replace legal counsel. Critical and high findings must be routed to legal/regulatory teams.
- Maintain a living library of approved claim language per product category.
- Re-validate all content when regulations change (e.g., FDA final rule on "healthy," FTC updated endorsement guides).
- Track FDA warning letters and FTC consent decrees in your category as precedent signals.

## Validation Checklist

- [ ] Every claim in the content is extracted and classified by type.
- [ ] Applicable regulatory frameworks (FDA, FTC, EPA, EU) are applied per product category.
- [ ] All critical and high violations have compliant alternative rewrites.
- [ ] Required disclaimers are identified and placed correctly.
- [ ] Channel-specific policy overlays are applied.
- [ ] Publication recommendation is clearly stated (approved / approved with changes / blocked).
- [ ] Regulatory references and citation links are provided for each finding.
- [ ] Substantiation documentation is cross-referenced against claim requirements.
- [ ] No drug claims exist on non-drug products.
- [ ] Environmental claims comply with FTC Green Guides specificity requirements.
