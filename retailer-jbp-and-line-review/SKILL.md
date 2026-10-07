---
name: retailer-jbp-and-line-review
description: For CPG and brand key-account teams selling into retailers, distributors and marketplaces. Builds the category story and line-review or new-item pitch, joint business plan (JBP) and trade-term negotiation prep, promotion post-event analysis with true incrementality, trade-spend ROI, price-increase and cost pass-through conversations, and retailer scorecard reviews (OTIF, fill rate, deductions). Use it whenever the user mentions a retailer buyer or category manager, line or category review, JBP, trade terms, slotting, promo calendar, TPR/BOGO results, a price increase to a retailer, facings or shelf space, or OTIF fines, even if they only paste POS or syndicated data. Not for selling software or services (use enterprise-deal-strategy).
---

# Retailer JBP & Line Review

A retail buyer is measured on **their category**, not your brand: category sales and share against the market, category margin dollars (including trade funds), traffic, turns, in-stock and private-label goals. Brands that win shelf space present a category story in which their plan grows the buyer's numbers. Brands that pitch their own brand growth get treated as a cost line.

**Shared rules for every output:**
- Label every data source. Syndicated data (Circana, NielsenIQ), retailer POS portals and panel data (Numerator) each come with use restrictions. Retailer-provided data is used only as its agreement allows, and never in another retailer's materials.
- No industry benchmarks unless they are in the proof library with a source. Ranges about "typical" promo lift or trade rates are folklore; the user's own history is the benchmark.
- Show your maths. Buyers and category analysts will check it. The formulas are in `references/commercial-math.md`.
- Anything going to the retailer passes through `customer-facing-quality-gate` (and its `customer-facing-quality-gate/references/industry-rules/cpg-product-claims.md` for product claims and commercial terms).

## 1. Category story and line review

**Build the fact base first:**
- Compare category and brand performance against year-ago, plan and the **total market**. If the category grows more slowly at this retailer than in the total market (both figures sourced), the retailer is losing share, and that is the opening.
- Build a **growth bridge**: Sales = traffic × conversion × units per basket × average unit price. Measure basket in units so price isn't counted twice. The drivers multiply, so attribute Δ sales with a log (LMDI) or sequential-substitution method that makes the parts sum exactly to the total. Split price/mix into pure price, tier trade-up or trade-down, size and channel.

**Diagnose the cause:**

| Pattern | Likely cause |
|---|---|
| Traffic down, conversion stable | Relevance or media problem |
| Conversion down | Assortment, price gap or friction |
| Conversion up, basket down | Cherry-picking or out-of-stocks |
| Average price down, units flat | Trade-down, deeper promos, channel mix |
| Average price up, units down | Elasticity threshold crossed |

Separate base volume from promoted volume, and adjust for calendar shifts such as holidays moving between weeks.

**Make the ask with these tools:**
- **Share-to-space:** compare brand share of category sales with share of shelf ("18% of sales on 5% of the section"). Add the growth contribution index: share of category growth ÷ share of category sales.
- **Consumer decision tree:** need state → form → tier → size → variant. Empty cells are white space; validate each with two independent signals. Keep *assortment* gaps (a segment missing) separate from *distribution* gaps (listed but not carried in every store).

**New-item sell-in checklist.** The buyer needs:
- source of volume (incremental vs. cannibalization)
- expected velocity against the category average, with its basis
- marketing and shopper support, with timing
- distribution plan, with confirmed POs kept separate from pending ones
- supply readiness
- item setup **and PDP content live at every channel before ship date** (see `pdp-content`)
- a 13-week read plan with checkpoints
- what the buyer needs to see to keep the item past the next reset

**Defending an at-risk SKU:** argue on transferable demand (how much volume would *not* move to other items), velocity rank within its segment, and its role: traffic driver, trial, or price-tier anchor.

## 2. Promotion post-event analysis

1. **Baseline.** Use one of:
   - (A) the average of non-promoted weeks before the event (e.g., 4–8 weeks), adjusted for trend and seasonality. Exclude post-event weeks, which contain the dip, and any weeks with other promotions
   - (B) matched control stores or SKUs (preferred)
   - (C) a time-series model

   Always net out the post-promo dip in the following weeks.
2. **Decompose the lift:** baseline (subsidized), category expansion, switching from competitors, cannibalization of your own items, and pull-forward. Measure pull-forward **once**, preferably as the post-period dip against baseline. Never subtract both a pantry-loading estimate and the dip.
   - **Manufacturer:** true incremental = expansion + brand switching.
   - **Retailer:** true incremental = category expansion + shoppers switching from other stores. Brand switching within the category isn't incremental to the retailer.
3. **Cost and profit impact.** Use one consistent method; both are given in `references/commercial-math.md`. Always run this check: incremental contribution − promo cost = profit with the promo − profit without it. Report separately the share of funding that subsidized volume which would have sold anyway.
4. **ROI at three levels:**
   - gross: incremental revenue ÷ spend
   - net: incremental contribution ÷ spend
   - true: net, after cannibalization, the dip and execution costs
5. **Compare actual lift with breakeven lift.** A promo that "lifted 80%" can still lose money.

**Rules:**
- Calculate ROI separately for the retailer and the manufacturer.
- Split variable trade (scan, bill-back, TPR) from fixed trade (slotting, lump sums). Fixed trade is excluded from per-event ROI.
- Track promo dependency: the share of volume sold on deal.
- Recommend **reallocation**, not just cuts.

## 3. JBP and trade-term negotiation prep (internal only)

- **Power and alternatives.** Assess:
  - brand pull
  - this retailer's share of our sales, and our share of their category
  - our alternative channels
  - the retailer's private-label readiness
  - switching costs

  Write down the **BATNA for both sides**; the retailer's usually includes its private label and the #2 brand. Estimate the zone of possible agreement.
- **Value levers, ranked by cost to us against value to them.** Lead with low-cost, high-value levers:
  - exclusive pack, flavor or size
  - early access to innovation
  - category insights (within data rights)
  - joint forecasting
  - display and merchandising support
  - payment terms (expensive, because they tie up working capital)
- **Concession discipline:**
  - Trade, never give. Every concession is tied to something in return.
  - Each concession is smaller than the last.
  - Keep one concession in reserve for the close.
  - Keep a hard-no list, with the reason for each item.
- **Rehearse three scenarios:**
  - best
  - base
  - worst: a delist threat, answered by proposing a test, a pilot or a timeline
- **Every talking point carries a quantified benefit to the retailer** and a line for "if they push back".
- **Commitments:**
  - Get approval at the right authority level before any verbal commitment.
  - Exclusives and special terms can trigger most-favored-customer clauses in other retailers' agreements.

## 4. Price increase and cost pass-through

- **Justify cost by component:** commodity, packaging, freight, labor. Give a source for each and a date for each source.
- **Breakeven volume loss** = p ÷ (m + p), where p is the price increase % and m is the contribution margin %.
- **Elasticity:** show a range, not a point estimate. Never extrapolate beyond price points actually observed.
- **Check the retailer's side:**
  - Model the retailer's margin. The manufacturer sets list price; **the retailer sets shelf price**.
  - Re-check the price gap to private label.
- **Offer alternatives:** partial pass-through; pack-size or price-pack-architecture change (keeping unit price logical across the size ladder); mix.
- **Follow the notice period** in the agreement.

## 5. Scorecard, OTIF and deductions review

- **Define OTIF exactly as this retailer's current supplier guide does.** Programs differ and change, so pull thresholds and fine rates from the current guide, never from memory.
- Track 4-week and 13-week rolling figures. Flag three consecutive periods of decline.
- **Deductions:**
  - Classify by type: delivery, quantity, documentation, labeling, packaging, compliance.
  - Report as a percentage of net sales.
  - Run a Pareto to find the few causes behind most of the value, then 5-whys to the root cause, with an owner per function (demand planning, procurement, 3PL, carrier, EDI, QA).
- **Disputes:** back them with evidence: POD/BOL, EDI timestamps, duplicate-deduction checks, program-guide citations.
- **Corrective action plan:** owner, date, milestones, leading indicators.

## Guardrails (legal; flag, don't decide)

- **Robinson-Patman (US).** Price and promotional-allowance differences between competing retailers need legal review. Allowances must be offered to competitors on proportionally equal terms.
- **Antitrust.** Never request, share or infer competitor pricing or plans. If the user receives such information unasked ("a friend at a competitor told me…"), don't use or forward it. Advise them to tell legal or compliance. Category captains keep firewalls. Suggested retail prices and unilateral pricing policies are fine. Never agree or negotiate a retailer's resale price: that is rule of reason federally, but per se illegal in some states. MAP limits *advertised* price only.
- **Internal stays internal.** Floors, other retailers' terms, and the hard-no list never appear in anything the buyer sees.

## Outputs
- **Line-review / category-story deck outline.** Each slide carries a headline that states the insight, the evidence behind it, and the ask in the buyer's metrics.
- **New-item pitch one-pager.**
- **Promo post-event readout:** verdict first, then breakeven vs. actual, the decomposition, and the reallocation recommendation.
- **Negotiation prep sheet** (internal).
- **Price-increase rationale and buyer talk track.**
- **Scorecard corrective action plan.**

Lead with the answer to the user's question. Put the supporting tables in an appendix.
