---
name: pdp-content
description: Creates, rewrites, audits and scales product detail page (PDP) content for brands and retailers. Covers product titles, bullets, descriptions, spec tables, FAQs, alt text, meta tags and structured data for brand.com, Amazon, Walmart, Target and other retailers, plus Google Shopping and other product feeds. Every claim is grounded in product attribute data, and the skill applies product-claims compliance, channel-specific rules, localization, and batch quality control across thousands of SKUs. Use it whenever the user mentions PDPs, product pages, product descriptions or titles, listings, catalog or PIM content, product feeds, digital shelf, A+ or enhanced content, or "write copy for these SKUs", even if they just paste a product spreadsheet.
---

# PDP Content

Product content works at the scale of the catalog. One error pattern in a template becomes thousands of wrong pages. Those errors drive returns ("not as described"), retailer suppressions, regulatory exposure, and lost search visibility. The job is to be **accurate first, then findable and persuasive**, consistently across every SKU and channel.

## Rule zero: every fact comes from the data

- **Every factual statement must trace to a source attribute.** Facts include dimensions, materials, compatibility, quantities, certifications, ingredients, performance, origin and warranty. Sources are the PIM or catalog data, the spec sheet, the label or packaging copy, or the approved claims list.
- **Not in the data means not in the copy.** Put it in the **gap report**, where merchandising or the brand can fill it. Never infer a spec from the product name, a sibling SKU or "typical" products in the category. A guessed "100% cotton" or "waterproof" is a real liability.
- **Conflicting sources get flagged, never resolved silently.** Example: the PIM says 500 ml and the image shows 16 oz.
- **Variant accuracy.** Size, color, count and pack facts belong to the specific SKU. Shared copy at the parent level must hold true for every child.
- **Image descriptions.**
  - Image notes and descriptions can source alt text and purely visual facts that can be seen (color, print, visible components).
  - They cannot source specs, performance or **materials**, even when a material looks visible (e.g., "leather trim" in an image note). Put materials in the gap report.
  - If an image contradicts the data (for example, the image shows a black strap on a SKU listed as navy), flag it and block that SKU until it's resolved.
- **Restricted-claim attributes.** A PIM "yes" on a restricted-claim attribute (BPA-free, organic, recyclable) is evidence, but the copy uses only the approved wording from the claims list. If no approved wording exists, list the claim as "available once wording is approved" rather than writing your own version.
- **Siblings that disagree.** For example, size M lists machine wash and size L lists dry clean only. Write each SKU from its own data. Flag the discrepancy to merchandising as a possible data error, and never harmonize it. To unlock a claim, advise **verifying** the attribute, with evidence (test, spec sheet, label). Never advise simply changing the field.
- **Customer language is for framing, not facts.** Reviews, Q&A, search terms and return reasons show what shoppers care about and worry about. Use them to choose emphasis and answer real questions. Never turn a reviewer's claim into a brand claim ("it cured my back pain").

## Inputs to collect

1. **Product data.** A PIM export or spreadsheet with attributes per SKU, variant relationships, and images or their descriptions.
2. **Brand voice and restrictions**, plus the approved claims list for the category.
3. **Target channels**, and the current style guides or templates for each retailer. Retailer rules change often, so prefer the user's current guide over anything remembered (see `references/channel-rules.md`).
4. **Markets and languages.** For any locale other than the source, apply `customer-facing-quality-gate/references/localization-qa.md`.
5. **Shopper voice. Ask for it every time; it's the biggest conversion lever.**
   - Sources: reviews (your own and top competitors', especially 2–4 star), Q&A, search terms, return reasons, support tickets.
   - Extract the top 3 purchase questions, the top 3 worries, and the phrases shoppers repeat. Use them to order bullets, write the FAQ and choose words.
   - If none is supplied, say so in one line and label the emphasis "category knowledge; validate with reviews".
   - **Safety mentions:** if reviews or Q&A mention safety or adverse events (rash, burn, choking, allergic reaction, hospitalized), list them for the user's safety or regulatory team. Never use them in copy, and never suggest suppressing them.
6. **Scope:** a new launch, a rewrite or optimization, an audit, or a catalog-scale program.

If product data is missing, don't write from the product name alone. Ask for the data, or produce a clearly labeled **structure-only draft** with `[ATTR NEEDED: …]` markers.

## PDP anatomy (brand.com baseline; adapt per channel)

| Element | Job | Rules |
|---|---|---|
| **Title** | Be found and be recognized | Front-load what shoppers search and need to identify the item: brand + product line + product type + key differentiating attributes (size, count, color, material, compatibility). Respect channel limits. No promotional language. |
| **Key benefits (3–5 bullets)** | Answer "why this one?" fast | Order by what decides the purchase, strongest first. Each bullet opens with the shopper outcome in bold (2–5 words), then the spec that proves it. A bare spec ("18/8 stainless steel.") isn't a bullet: pair it with a benefit the data supports, or move it to specs. Care limits and fine print go in specs, the FAQ and a "Good to know" line next to add-to-cart. They stay visible and are never spun, but they don't sit in the benefit stack. |
| **Description** | Help the undecided shopper picture using it | Who it's for and when to use it; what makes it different; details. Scannable: short paragraphs, no keyword lists. |
| **Specifications** | Exact facts for comparison | Taken from the data, unchanged. Consistent units and formatting. Group logically (dimensions, materials, power, compatibility). |
| **In the box / compatibility / care / warranty** | Prevent returns and support contacts | Exact. Link to the full warranty terms rather than paraphrasing them. |
| **FAQ** | Answer real questions | Source the questions from Q&A, reviews and support. If none are supplied, use standard purchase questions for the category (label them as such). Every answer comes only from the data. Omit any question the data can't answer. |
| **Image alt text** | Accessibility and image search | Describe what the image shows: product, variant, angle, feature. No keyword stuffing. |
| **Meta title / description** (brand.com) | Earn the click from search | Roughly 50–60 / 150–160 characters. This is a display heuristic only: Google truncates by pixel width and may rewrite them. Unique per page. |
| **Structured data** (brand.com) | Machine-readable facts for search and AI shopping | Product with Offer data, kept consistent with the visible page. See `references/seo-and-feeds.md`. |

**Writing principles:**
- Benefit first, then proof. "Keeps drinks cold for 24 hours" must come from the attribute that says so.
- **Specific beats superlative.** "Holds a 16-inch laptop" beats "spacious".
- **Write for the shopper's decision, not for the brand's adjectives.** Cut "premium", "high-quality" and "innovative" unless something concrete stands behind them.
- **Answer the objection that causes returns.** If sizing runs small per the brand's fit data, say how to choose a size.
- **Uniqueness.** Don't publish manufacturer boilerplate unchanged across retailers. Don't publish near-identical copy across sibling SKUs; consolidate variants under one parent page where the platform supports it.
- **Brand voice applies, but clarity wins on PDPs.** Shoppers are scanning.
- **Make the numbers felt.** Energy comes from translating real attribute values, never from adjectives. Translate into:
  - **a moment:** "10-hour battery" → "lasts a full workday on one charge"
  - **a felt unit:** "980 g" → "under a kilo"; "34 × 23 × 15 cm" answers "will it fit under the seat?" (state the dimensions; never claim it fits)
  - **a sibling contrast:** "8 L more than the 22 L"

  Use each device once per page; repeating one device across bullets reads as a template. A moment may add a setting (workday, commute) but never a capability the data lacks (waterproof, carry-on approved). Fragments that carry a fact are fine ("10 hours of battery. 980 g.").

## Compliance hotspots for products

Check these on every batch. Details are in the claims reference of `customer-facing-quality-gate`, section 5.

- **CPG claim classification and the detailed rules** (FDA, EPA, Green Guides, EU): `customer-facing-quality-gate/references/industry-rules/cpg-product-claims.md`.
- **Restricted claim types:**
  - health and medical (supplements, cosmetics, devices)
  - environmental: "eco-friendly", "sustainable", "recyclable", "carbon neutral"
  - origin: "Made in USA"
  - safety and children's products
  - free-from and chemical claims: BPA-free, PFAS-free, lead-free, "non-toxic", "hypoallergenic"
  - "clinically proven", "organic"
  - certifications and certification marks
- **Each needs approved substantiation and exact approved wording.** Use only phrasing from the approved claims list.
- **EU consumer markets:** since 27 September 2026, Directive (EU) 2024/825 (through national law) bans:
  - generic environmental claims unless recognized excellent environmental performance can be shown
  - claims of neutral, reduced or positive environmental impact based on offsetting
  - uncertified sustainability labels
- **Retailer content policies:** typically no pricing, promotions, shipping claims, time-sensitive language, competitor comparisons, or contact details in the listing content.
- **Prices and "was" prices** belong in the commerce system, not in copy. Reference-price rules apply.
- **Consistency across channels.** The claim on brand.com, each retailer listing, ads and the packaging must match. Claims drift between channels is a common source of exposure.

## Workflows

### A. Create or rewrite (one SKU or a handful)
1. Parse the attributes and build a fact sheet: each fact with its source field.
   - Check the **minimum attribute set** for the category before writing.
   - Example for drinkware: capacity, material, care, dimensions.
   - Children's and regulated items also need materials, certifications and age grading.
   - SKUs below the minimum get a structure-only draft with `[ATTR NEEDED]` markers and go to the gap report.
2. Identify the 3–5 things shoppers most need to know, from shopper insight or category knowledge, and label which was used.
3. Draft per channel using the anatomy above and the channel rules. **Channel limits:** if a limit isn't known and the user can't be asked right away, use a conservative default, mark it "default; verify", and list it under rule sources.
4. Self-check:
   - attribute fidelity: every number, unit and claim maps to the fact sheet
   - restricted claims
   - length limits
   - variant accuracy
5. Output in the format below, then run `customer-facing-quality-gate` (short or full form; batch form for 10+ SKUs).
   - **If the user asked for a claim the data doesn't support** (e.g. "say it's waterproof" when the data only says water-resistant), put that at the very top of the response.
   - Say what wasn't included and why, what data or approved wording would unlock it, and what was written instead.

### B. Audit or optimize existing PDPs
Score each page or listing against the rubric below. Compare the same SKU across channels for inconsistencies (titles, specs, images, claims). Mine reviews and Q&A for unanswered questions and the causes of "not as described" returns.

Returns coded "not as described", "image mismatch" or "wrong spec" are evidence of content defects, and they make the business case for fixing them. Mine reviews by aspect: one review can be positive on quality and negative on fit. Recurring questions point to missing attributes.

To explain why a PDP's performance changed, or to design a content test, use `b2b-content-and-campaigns/references/testing-and-diagnosis.md`.

Prioritize SKUs by:
- revenue or traffic
- retail-media spend (don't advertise SKUs with weak content or stock problems)
- "not as described" return rate
- new launches

Deliver prioritized fixes. Predict impact only qualitatively unless the user has real test data; never invent conversion lifts.

### C. Catalog-scale program
Follow `references/scale-and-qa.md`: pilot set, calibrated templates and prompts, golden examples, automated checks, sampled human review, staged rollout, and monitoring.

At catalog scale, the automated checks act as the gate for every SKU. Run the full `customer-facing-quality-gate` on:
- the golden set
- the human-review sample
- regulated SKUs
- anything flagged

## Quality rubric

**Hard gates.** Every SKU must pass all of these before publishing:
- **Attribute fidelity: 100%.** No fact without a source; no contradictions with the data.
- **Compliance: 100%.** No unapproved restricted claims; required disclosures present.
- **Channel compliance: 100%.** Limits, required fields, prohibited content.
- **Amazon's five bullets with thin data.** Order them by purchase decision. A required care or usage limit may take the last bullet, stated plainly. Mention a warranty only with the exact term from the data, and only where the category style guide allows it. Otherwise mark it "default; verify".
- **Warranty and policy links.** Use the URL from the data. If there isn't one, insert `[WARRANTY URL]`, which makes the SKU a `DRAFT — open item` rather than a blocked SKU.
- **Channel-required fields** (e.g., GTIN for Amazon or Merchant Center): if one is missing, block that channel listing only. The approved copy can still be used elsewhere.
- **No placeholders or `[ATTR NEEDED]` markers** in published content. Fields that systems fill at runtime, such as commerce price and availability in templates and structured data, are not copy placeholders.

**Scored dimensions** (1–5 each; target an average of 4 or more, with nothing below 3):
- **Completeness:** top purchase questions answered; required attributes present.
- **Shopper clarity:** benefits are clear, specific and scannable.
- **Findability:** title and copy use real shopper terms naturally; structured data is complete.
- **Differentiation and choice:** a clear why-this-one, and an easy pick between siblings (a "Which size?" line or chart built from real attribute values).
- **Persuasion:**
  - The strongest true benefit is the first line a shopper reads.
  - The top objection is answered before add-to-cart.
  - Risk reducers in the data (warranty, returns) sit near the buy button.
  - Read it aloud. If it sounds like a spec sheet with verbs, rewrite it.
- **Voice:** on-brand within channel constraints.

## Output format

For each SKU and channel, return content plus the evidence behind it:

```yaml
sku: "ABC-123-BLU-M"            # or parent_sku + children: [..] when variants share one page
channel: "brand.com"            # or amazon / walmart / google_feed / ...
locale: "en-US"
title: "..."                     # (n chars / limit)
bullets:
  - "..."
description: "..."
specs: { material: "...", dimensions: "..." }
faq: [{ q: "...", a: "..." }]
alt_text: ["..."]
meta: { title: "...", description: "..." }
source_map:                      # every factual phrase → attribute field
  "lasts a full workday": "attr.battery_hours (10)"
flags:                           # gaps, conflicts, compliance notes, assumptions
  - "GAP: no care instructions in PIM — care bullet omitted"
  - "CONFLICT: capacity 500 ml (PIM) vs 16 oz (image) — verify"
gate: "PASS | PASS WITH WARNINGS | BLOCKED (reason)"
```

In chat, lead with:
- the declined requests
- counts by verdict
- the top gaps

For more than a few SKUs, put the full per-SKU content in a file.

For batches, also return a summary:
- counts by verdict (PASS / PASS WITH WARNINGS / BLOCKED)
- the gap report, aggregated by attribute (e.g., "312 SKUs missing `material`") and **ranked by conversion impact first, then SKU count**. Restricted claims with a PIM "yes" but no approved wording (e.g., BPA-free) go to the top, because they are usually a quick approval with a large payoff.
- recurring issues that point to a template or data fix rather than an individual SKU fix

**Publishing, feed uploads and retailer submissions require explicit user approval.** Preview a sample first, and state the SKU count.
