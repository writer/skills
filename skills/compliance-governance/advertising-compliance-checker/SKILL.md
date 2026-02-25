---
name: advertising-compliance-checker
description: Validate CPG advertising content for compliance with FTC Act, NAD guidelines, FDA regulations, and retailer-specific advertising policies. Use when reviewing ad claims, packaging copy, influencer content, digital advertising, or any consumer-facing marketing material for legal and regulatory compliance.

metadata:
  display_name: "Advertising Compliance Checker"
  short_description: "Check CPG advertising content against FTC/FDA compliance"
  default_prompt: "Check my advertising compliance for gaps risks and required fixes"
  version: "1.0.0"
  tags:
    - cpg-retail
  icon_path: "assets/icon.png"
---

# Advertising Compliance Checker

## Overview

Review and validate CPG advertising and marketing content against federal regulations (FTC Act Section 5, FDA labeling rules), industry self-regulatory standards (NAD/NARB), platform-specific policies (Meta, Google, Amazon), and retailer media network requirements. Produce a structured compliance assessment with risk-rated findings and remediation guidance.

## When to Use

- Pre-launch review of advertising creative (TV, digital, print, social)
- Product packaging claim validation
- Influencer and creator content compliance review
- Retailer media network ad submission preparation
- Competitive advertising challenge assessment (NAD)
- Comparative advertising claim substantiation review
- Health, wellness, and sustainability claim validation
- Post-market advertising audit

## Required Inputs

| Input | Description | Format |
|-------|-------------|--------|
| Ad content | Copy, creative, claims, imagery to be reviewed | Text, image, or video description |
| Product details | Product type, ingredients, target audience | Product brief |
| Claim substantiation | Supporting evidence for claims made | Studies, data, certifications |
| Target channels | Where the ad will run (TV, social, retail media, etc.) | Channel list |
| Target audience | Consumer demographic and any vulnerable populations | Audience description |
| Product category | Food, beverage, supplement, personal care, household | Category selection |
| Geographic scope | US, EU, or specific markets | Market list |

## Methodology

### Step 1: Claim Inventory and Classification

Extract and classify every claim in the advertising content:

| Claim Type | Definition | Regulatory Standard | Substantiation Required |
|-----------|-----------|--------------------|-----------------------|
| Express claims | Directly stated ("Clinically Proven") | FTC Act §5 | Competent and reliable scientific evidence |
| Implied claims | Reasonably inferred by consumers | FTC Act §5 | Same as express |
| Comparative claims | vs. competitor or previous version | Lanham Act §43(a) | Head-to-head testing data |
| Health claims | FDA-authorized health relationships | FDCA §403(r) | FDA pre-authorization or qualified claim |
| Nutrient content | "Low fat," "High fiber," etc. | 21 CFR 101.13 | Meet defined nutrient thresholds |
| Structure/function | "Supports immune health" | DSHEA §6 | Manufacturer substantiation + disclaimer |
| Environmental | "Sustainable," "Eco-friendly" | FTC Green Guides | Specific, qualified, substantiated |
| "Free from" | "No artificial flavors," "BPA-free" | FTC Act §5 | Truthful + not misleading by omission |
| Testimonials | Consumer or expert endorsements | FTC Endorsement Guides | Typical results, material connection disclosure |
| Puffery | "Best taste ever" | Generally exempt | Must not be measurable/verifiable |

### Step 2: FTC Act Section 5 Analysis

Apply the FTC's three-part deception test to each claim:

```
FTC Deception Standard:
1. Is there a representation, omission, or practice likely to mislead?
2. Is it examined from the perspective of a reasonable consumer?
3. Is the representation material (would it affect purchase decision)?

All three must be YES for a finding of deception.

FTC Unfairness Standard:
1. Does the practice cause substantial consumer injury?
2. Is the injury not reasonably avoidable by consumers?
3. Is the injury not outweighed by countervailing benefits?
```

**Advertising Substantiation Doctrine:**
- Advertisers must have a "reasonable basis" for claims BEFORE making them
- For health/safety claims: "competent and reliable scientific evidence" = well-controlled studies
- For performance claims: testing consistent with claim (e.g., "lasts 24 hours" requires 24-hour testing)
- For comparative claims: head-to-head comparison using same methodology

### Step 3: NAD (National Advertising Division) Standards

Apply NAD's self-regulatory framework:

**NAD Review Criteria:**
- Truthfulness: Is the claim literally true?
- Substantiation adequacy: Does evidence support the claim as communicated?
- Consumer takeaway: What does a reasonable consumer understand from the ad?
- Implied claims: Are there implied messages beyond the literal text?
- Disclaimers: Are qualifications clear, conspicuous, and proximate?

**NAD Common Challenge Areas for CPG:**
| Area | Common Issue | NAD Standard |
|------|-------------|-------------|
| "#1 Brand" claims | Outdated data, narrow scope | Must be current and clearly defined |
| "Clinically proven" | Insufficient study quality | Requires well-designed clinical study |
| Taste claims | Subjective but testable | Consumer preference testing required |
| "Natural" | No federal definition for most products | Must not mislead; specify meaning |
| Superiority claims | Overly broad | Must be supported across all reasonable interpretations |

### Step 4: Category-Specific Regulatory Review

**Food and Beverage (FDA):**
- Nutrient content claims must meet 21 CFR 101.13 thresholds
- Health claims require FDA authorization (or qualified health claim letter)
- "Healthy" labeling: Must meet FDA's updated "healthy" criteria
- Allergen declarations: FALCPA requirements for Big 9 allergens
- Front-of-pack labeling: Check for consistency with Nutrition Facts panel

**Dietary Supplements (FDA/FTC):**
- Structure/function claims require 30-day FDA notification
- Must include "not evaluated by FDA" disclaimer
- Cannot claim to diagnose, treat, cure, or prevent disease
- Substantiation standard is higher per FTC for health-adjacent claims

**Personal Care/Household:**
- Cosmetic vs. drug claims (FDA distinction based on intended use)
- EPA registration requirements for antimicrobial claims
- CPSC compliance for safety-related claims

### Step 5: Digital and Social Media Compliance

**Influencer/Creator Content (FTC Endorsement Guides 2023):**
- Material connection must be disclosed clearly and conspicuously
- Disclosure must be in the same medium as the endorsement
- "#ad" or "#sponsored" must be immediately visible (not buried in hashtags)
- Influencer must have actually used the product
- Brand is liable for influencer claims — must monitor and control

**Platform-Specific Requirements:**
| Platform | Key Restrictions |
|----------|-----------------|
| Meta (Facebook/Instagram) | No before/after for supplements; restricted categories |
| Google Ads | Healthcare/medicine restrictions; substantiation requirements |
| Amazon | Claims must match product listing; no disease claims |
| TikTok | No misleading health claims; disclosure requirements |

### Step 6: Retailer Media Network Compliance

Review against retailer-specific advertising standards:
- Walmart Connect: Requires claim substantiation pre-submission
- Kroger Precision Marketing: Category-specific restrictions apply
- Amazon Advertising: Must align with product detail page claims
- Target Roundel: Restrictions on competitive references

### Step 7: Risk Rating and Remediation

Rate each identified issue:

| Risk Level | Definition | Action Required |
|-----------|-----------|----------------|
| Critical | Likely FTC/FDA enforcement action or NAD challenge | Stop use immediately; revise before any publication |
| High | Substantiation gap or misleading potential | Revise claim; strengthen substantiation |
| Medium | Disclosure deficiency or qualification needed | Add disclaimers; modify presentation |
| Low | Best practice improvement; not a violation | Recommend enhancement; optional |
| Compliant | Meets all applicable standards | No action required |

## Output Specification

```markdown
# Advertising Compliance Review — [Campaign/Asset Name]

## Review Summary
**Overall Risk Rating**: Critical / High / Medium / Low / Compliant
**Claims Reviewed**: [X]
**Issues Found**: [X Critical, X High, X Medium, X Low]
**Recommendation**: Approve / Approve with Modifications / Revise and Resubmit / Do Not Publish

## Claim-by-Claim Analysis

### Claim 1: "[Exact claim text]"
- **Type**: [Express/Implied/Comparative/Health/etc.]
- **Risk Rating**: [Critical/High/Medium/Low/Compliant]
- **Applicable Standards**: [FTC Act §5, NAD, FDA 21 CFR XXX, etc.]
- **Substantiation Status**: [Adequate / Inadequate / Partial / Not Provided]
- **Issue**: [Specific compliance concern]
- **Remediation**: [Specific recommended revision with example language]

### Claim 2: "[Exact claim text]"
[Same structure]

## Channel-Specific Flags
[Platform or retailer media issues with specific requirements cited]

## Disclosure Requirements
[Required disclosures with placement and formatting guidance]

## Substantiation Gaps
[Claims requiring additional evidence before publication]

## Recommended Revised Copy
[Suggested compliant alternative language for flagged claims]

## Regulatory References
[Specific regulations, guidance documents, and NAD precedents cited]
```

## Analysis Framework

**Claim Substantiation Hierarchy:**
```
Strongest → Weakest:
1. Randomized controlled trials (RCTs) — gold standard for health claims
2. Peer-reviewed published studies — strong for performance claims
3. Consumer perception studies — required for taste/preference claims
4. Internal testing data — acceptable for performance, not health
5. Expert endorsement alone — insufficient for objective claims
6. Anecdotal/testimonial — insufficient as sole substantiation
```

## Example

**Input**: "Ad copy for a snack bar: 'Clinically proven to boost energy. #1 selling protein bar in America. All-natural ingredients. Influencer post on Instagram.'"

**Analysis excerpt**:
> "**Overall Risk: HIGH — 3 issues identified.**
> (1) 'Clinically proven to boost energy': **CRITICAL**. 'Clinically proven' is an express efficacy claim requiring competent and reliable scientific evidence, specifically well-controlled human clinical trials. Per NAD precedent (Case #6842), this phrase creates a strong consumer expectation of clinical testing. If substantiation consists of general ingredient research rather than product-specific trials, the claim is unsupported. **Remediation**: Revise to 'Made with ingredients studied for energy support' with citation, or provide product-specific RCT data.
> (2) '#1 selling protein bar in America': **MEDIUM**. Requires current, clearly defined data source. Per NAD guidelines, '#1' claims must specify the measurement period, data source, and category definition. **Remediation**: Add qualifier: '#1 selling protein bar in America based on [Source] unit sales data for the [12-month period ending MM/YYYY] in [measured channels].'
> (3) Influencer post without disclosure: **HIGH**. FTC Endorsement Guides (2023 update) require clear and conspicuous disclosure of material connection. '#ad' must appear at the beginning of the post, not buried in hashtags. **Remediation**: Require '#ad' or 'Paid partnership with [Brand]' in first line of caption; use platform's built-in partnership label."

## Guidelines

- Review claims from the perspective of a "reasonable consumer" — not a legal expert
- When in doubt about a claim, flag it — false negatives are more costly than false positives
- Always check implied claims, not just express ones — what would a consumer reasonably infer?
- Substantiation must exist BEFORE the claim is made, not after
- Environmental claims are under intense FTC scrutiny — apply Green Guides rigorously
- "Natural" has no federal standard for most CPG categories — treat with heightened scrutiny
- This review is a risk assessment tool, not legal advice — recommend legal counsel review for Critical findings

## Validation Checklist

- [ ] All claims extracted and classified by type
- [ ] FTC deception three-part test applied to each material claim
- [ ] Substantiation status assessed against appropriate standard for claim type
- [ ] NAD self-regulatory standards applied (especially for comparative and #1 claims)
- [ ] Category-specific regulations checked (FDA, EPA, CPSC as applicable)
- [ ] Digital/social media compliance verified (endorsement disclosures, platform policies)
- [ ] Retailer media network requirements checked if applicable
- [ ] Each issue risk-rated with specific remediation language provided
- [ ] Recommended revised copy provided for all flagged claims
- [ ] Regulatory references cited for every finding
