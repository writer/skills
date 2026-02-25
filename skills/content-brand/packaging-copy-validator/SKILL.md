---
name: Packaging Copy Validator
description: Validate on-pack and digital packaging copy against legal mandates, marketing claims policy, regulatory labeling requirements, and retailer submission standards for CPG products.

metadata:
  display_name: "Packaging Copy Validator"
  short_description: "Validate CPG packaging copy for legal and label compliance"
  default_prompt: "Check my packaging copy for gaps risks and required fixes"
  version: "1.0.0"
  tags:
    - cpg-retail
  icon_path: "assets/icon.png"
---

# Packaging Copy Validator

## Overview

This skill validates all text appearing on physical packaging and its digital representation (e-commerce product images, digital shelf renderings) against a comprehensive matrix of legal, regulatory, marketing, and retailer requirements. Packaging errors are among the most costly content mistakes in CPG — a single labeling non-compliance can trigger product recalls, import holds, and retailer fines.

The validator treats packaging copy as a legal document that also serves as a marketing asset, applying both compliance rigor and brand effectiveness criteria.

## When to Use

- Reviewing packaging artwork proofs before print production.
- Validating digital shelf images and enhanced content for marketplace compliance.
- Auditing existing packaging for regulatory changes (e.g., updated FDA nutrition label rules).
- Preparing packaging for new market entry with different labeling requirements.
- Checking private label / co-manufacturing packaging specifications.
- Updating packaging after formulation changes, claim additions, or rebrand.

## Required Inputs

| Input | Description | Example |
|---|---|---|
| `packaging_copy` | All text from the packaging (structured by panel) | `{ "PDP_front": "...", "info_panel": "...", "back_panel": "..." }` |
| `product_category` | FDA product classification | "conventional food", "dietary supplement", "OTC drug", "cosmetic" |
| `ingredient_list` | Complete ingredient statement | Ordered list by predominance |
| `nutrition_facts` | Nutrition / supplement facts panel data | Structured nutritional data |
| `net_contents` | Product quantity and unit of measure | "12 oz (340g)" |
| `allergen_info` | Allergen declarations | "Contains: milk, soy, wheat" |
| `target_markets` | Countries/states of sale | `["US", "CA", "EU"]` |
| `certifications` | Active certifications and their logo usage guidelines | `["USDA Organic", "Fair Trade Certified"]` |
| `claims` | All on-pack claims (front and back panel) | List of claim strings |
| `upc_gtin` | Product barcode information | "0-12345-67890-5" |

## Methodology

### Step 1 — Panel-by-Panel Inventory

Map every text element on the packaging to its regulatory classification:

| Panel | Required Elements | Common Errors |
|---|---|---|
| **Principal Display Panel (PDP)** | Product identity statement, net quantity, brand name | Missing net quantity, identity statement not in required type size |
| **Information Panel** | Ingredient statement, nutrition facts, allergen declaration, manufacturer info | Ingredient order errors, missing sub-ingredients, allergen formatting |
| **Back/Side Panel** | Directions for use, warnings, storage instructions, UPC | Missing required warnings, incorrect UPC check digit |
| **Top/Bottom** | Lot code, expiration/best-by date, country of origin | Missing date format, ambiguous lot coding |

### Step 2 — Regulatory Compliance Validation

**FDA Labeling Requirements (21 CFR 101)**:

1. **Statement of Identity**: Common/usual name of food in bold type on PDP, parallel to base. Type size per 21 CFR 101.3.
2. **Net Quantity of Contents**: Lower 30% of PDP, in both metric and US customary units. Minimum type size per container size (21 CFR 101.7).
3. **Ingredient Statement**: Listed in descending order of predominance by weight. Sub-ingredients in parentheses. Color additives by specific name.
4. **Nutrition Facts Panel**: Current format per 21 CFR 101.9. Serving size per RACC. Updated dual-column format for packages 1-2 servings.
5. **Allergen Declaration**: Big 9 allergens (milk, eggs, fish, shellfish, tree nuts, peanuts, wheat, soybeans, sesame) declared per FALCPA + FASTER Act.
6. **Manufacturer/Distributor**: Name and address of manufacturer, packer, or distributor. "Manufactured for" or "Distributed by" language.

**Supplement-Specific (DSHEA)**:
- Supplement Facts panel format (not Nutrition Facts).
- DSHEA disclaimer required for structure/function claims.
- "Dietary Supplement" must appear on PDP.

**State-Level Requirements**:
- California Prop 65 warnings for applicable products.
- State-specific deposit/recycling marks (CA CRV, MI, OR, etc.).

### Step 3 — Claims Validation on Packaging

Cross-reference all on-pack claims against the approved claims library:

| Claim Category | Validation Rule |
|---|---|
| Nutrient Content Claims | Must meet defined thresholds (21 CFR 101.13, 101.54-101.67) |
| Health Claims | Must be FDA-authorized or qualified with prescribed disclaimer |
| Structure/Function | Requires DSHEA disclaimer and 30-day FDA notification |
| Organic | USDA Organic seal use per NOP; ingredient percentage thresholds |
| Non-GMO | Non-GMO Project Verified requires active enrollment |
| Kosher/Halal | Active certification from recognized authority; correct symbol |
| Free-From Claims | "Gluten-free" per FDA (< 20 ppm); "Sugar-free" per 21 CFR 101.60 |

### Step 4 — Typography & Formatting Compliance

| Element | Requirement |
|---|---|
| Product Identity type size | Based on PDP area: < 5 sq in = 1/16"; 5-25 sq in = 1/8"; 25-100 sq in = 3/16"; > 100 sq in = 1/4" |
| Net quantity type size | Based on PDP area per 21 CFR 101.7(j) |
| Ingredient statement | Minimum 1/16" (0.0625") type height; specific font legibility rules |
| Allergen declaration | "Contains:" statement or parenthetical within ingredient list; no smaller than ingredient list type |
| Nutrition Facts | Prescribed format, fonts (Franklin Gothic Heavy/Helvetica Black), hairlines |

### Step 5 — Barcode & Identification Validation

- UPC-A or EAN-13 check digit validation.
- Adequate quiet zone around barcode (minimum 9 modules left, 9 modules right for UPC-A).
- Barcode dimensions within GS1 specification (80-200% magnification).
- Lot code and date marking format consistency.

### Step 6 — Digital Shelf Readability Check

When packaging appears as a product image on e-commerce:

- **Hero Image**: Is the brand name legible at thumbnail size (150×150 px)?
- **Claims Visibility**: Are key claims readable on mobile (< 400px width)?
- **Nutrition Panel**: Is the nutrition facts legible in zoom view?
- **Color Contrast**: WCAG AA compliance for text on packaging backgrounds.

## Output Specification

```yaml
output:
  overall_compliance: string         # "compliant" | "non_compliant" | "needs_review"
  compliance_score: float            # 0-100
  findings: list[Finding]
  panel_status:
    pdp: string                      # "pass" | "fail" | "warning"
    info_panel: string
    back_panel: string
  critical_issues: int               # Print-blocking issues
  warnings: int                      # Should-fix before print
  recommendations: int               # Best practice suggestions
  missing_elements: list[string]     # Required elements not found
  claims_validation: list[ClaimResult]
  print_ready: boolean               # Final go/no-go recommendation
```

## Analysis Framework

**Packaging Compliance Severity Model**:

| Severity | Impact | Examples | Action |
|---|---|---|---|
| **Critical (P0)** | Product recall risk, import detention, regulatory action | Missing allergen declaration, wrong net quantity, unauthorized health claim | Stop print. Fix immediately. |
| **Major (P1)** | Retailer rejection, consumer complaint risk | Ingredient order error, wrong nutrition facts format, missing Prop 65 | Fix before print. |
| **Minor (P2)** | Audit finding, best practice gap | Type size slightly under threshold, missing recycling symbol | Fix in next print run. |
| **Advisory** | Opportunity to improve effectiveness | Better claim hierarchy on PDP, enhanced readability | Consider for next revision. |

## Examples

**Input**: Front panel of a granola bar packaging.
- Copy: "SuperGrain Protein Bar — ALL NATURAL — 20g Protein — Gluten Free — Net Wt. 2.4 oz"

**Findings**:
1. **Critical**: "ALL NATURAL" — FDA has proposed (not finalized) definition; currently high enforcement risk. Recommend removal or replacement with specific claims.
2. **Major**: "20g Protein" — Qualifies as "Excellent Source of Protein" (≥ 10g per RACC), but the nutrient content claim format should reference the DV% basis under 21 CFR 101.54.
3. **Pass**: "Gluten Free" — Acceptable if product tests < 20 ppm gluten per FDA rule.
4. **Pass**: Net weight statement present. Verify type size ≥ 1/8" for this PDP area.
5. **Advisory**: Consider adding "Non-GMO" if verified — high consumer demand in this category.

## Guidelines

- Packaging validation must occur at proof stage, not after print. Changes post-print cost 10-50x more.
- Always validate against the most restrictive market if selling across multiple jurisdictions.
- Certification logo usage must comply with each certifier's brand guide (size minimums, color specs, placement rules).
- Keep a version-controlled record of every packaging proof reviewed and findings resolved.
- Coordinate with procurement on lead times — some critical fixes may require plate changes.
- When in doubt about a claim, escalate to regulatory counsel — do not self-approve.

## Validation Checklist

- [ ] All required labeling elements are present on the correct panels.
- [ ] Ingredient statement is in descending order of predominance with correct sub-ingredient formatting.
- [ ] Allergen declarations cover all Big 9 allergens present in the product.
- [ ] Nutrition Facts panel follows current FDA format requirements.
- [ ] Net quantity statement meets type size and placement requirements.
- [ ] All on-pack claims are cross-referenced against the approved claims library.
- [ ] Certification logos meet each certifier's usage guidelines.
- [ ] Barcode check digit validates correctly and meets GS1 size/quiet zone specs.
- [ ] State-specific requirements (Prop 65, deposit markings) are included for applicable markets.
- [ ] Digital shelf readability is confirmed at thumbnail and mobile sizes.
