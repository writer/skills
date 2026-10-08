---
name: b2b-content-and-campaigns
description: Plans and creates enterprise B2B marketing assets and campaigns — customer case studies and testimonials, executive thought leadership and LinkedIn ghostwriting, nurture, drip and lifecycle email, newsletters, webinar and event promotion, landing and web page copy and audits, product launches, announcements and press releases, and campaign briefs. Use it whenever the user wants to create, improve, or plan marketing content or a campaign for business buyers, write a case study, draft a post for an executive, audit a web page, or plan a launch. Not for product detail pages (use pdp-content), 1:1 sales emails (use executive-outreach), or ABM tier plays and account-level orchestration (use account-targeting-and-research).
---

# B2B Content & Campaigns

Enterprise marketing content has two jobs: build credibility with a committee of skeptical buyers, and give champions material they can forward internally. Specific beats clever. Proof beats adjectives. One clear action beats five.

## Universal rules for every asset
1. **Start from a brief:**
   - audience (persona and buying stage)
   - the single takeaway
   - the action we want
   - proof available (proof library IDs)
   - channel
   - constraints (voice, legal, approvals)
2. **One asset, one job.** One core idea and one call to action.
3. **Proof only from approved sources.** No invented stats, customers, quotes or "studies show". When content needs a proof point that doesn't exist, leave a visible `[NEEDS PROOF: …]` marker and say what kind of evidence would work.
4. **Match the buying stage.**
   - Early: problem framing and insight.
   - Evaluation: comparison, proof, ROI, security.
   - Decision: references, implementation, commercial clarity.
   - Customer: adoption and expansion.
5. **Write for forwarding.** Many readers will see it out of context, sent by their colleague. It must make sense on its own.
6. **Write to convert, within the truth.**
   - Lead with the strongest real fact, made concrete.
   - Pair the emotional win (what it meant for the person) with the business number.
   - Answer the top objection where it arises.
   - End with one CTA that is a real offer: what they get, how fast, at what cost to them.
   - Write 5+ headline options and pick the one a peer would forward.
   - Craft method: `customer-facing-quality-gate/references/ai-tells.md` §0.
7. **Regulated industries.** For financial services, healthcare or CPG product claims, the matching file in `customer-facing-quality-gate/references/industry-rules/` applies. Patient-facing healthcare copy follows its plain-language standard.
8. Finish every external asset with `customer-facing-quality-gate`.

Choose the playbook below that fits the request. Read its reference file for the detailed method.

| Asset | When | Reference |
|---|---|---|
| Case study / testimonial / customer proof | A customer outcome to capture or publish | `references/customer-proof.md` |
| Executive thought leadership, LinkedIn posts, bylines | Building an executive's or the brand's authority | `references/thought-leadership.md` |
| Web / landing page copy or audit | Homepage, solution, industry, campaign or comparison pages | `references/web-pages.md` |
| Nurture, lifecycle and event email | Programs to non-active-deal contacts; webinar/event promotion | `references/email-programs.md` |
| Launches, announcements, press releases | New product, feature, partnership, market entry, customer win | `references/launches-and-pr.md` |

## Campaign brief (for any multi-asset campaign)

```
Objective — one business outcome + metric + target + date (e.g., "40 meetings with Tier-1/2 retail accounts by Q3 end")
Audience — accounts/tiers, personas, buying stage
Insight — the non-obvious truth the campaign is built on (with evidence)
Core message — from the messaging house; proof points
Offer — what the buyer gets (assessment, benchmark from real data, workshop, demo, event)
Channels & sequence — what runs where, when, in what order; sales plays aligned
Sales enablement — talk track, follow-up emails, what reps do with engaged accounts
Exclusions — current customers (unless an expansion play), accounts with open opportunities, competitors, recent converters
Measurement — leading (engagement by account) and lagging (meetings, pipeline, influenced revenue); baseline; incrementality (holdout or matched-account control) kept separate from attribution
Feasibility — flag if budget or time can't plausibly reach the objective
Budget & approvals — spend, sign-offs, legal review needs
Risks — what could go wrong; how we'd know early
Kill/scale criteria — decided before launch
```

## Paid ad variants (LinkedIn, search, social)
- **Angles come from messaging pillars,** each tied to a proof-library ID.
- **Variants must be meaningfully different.** No near-duplicates.
- **Test one dimension per round:** angle, then hook, then CTA or format.
- **Give exact character counts** against the platform's current spec, marked "verify". For example, Google responsive search ads take up to 15 headlines of 30 characters and 4 descriptions of 90.
- **Name variants and tag them with UTMs** using a consistent convention.
- **Compliance:** flag compliance-sensitive copy. No scarcity or fake urgency.

## Planning discipline
- **Run the inversion check before launch.** Assume the campaign failed completely. List three reasons why, and add a prevention for each.
- **Write experiments down before running them:**
  - "We'll test [tactic] with [budget/time cap]; success = [metric ≥ X]; kill if [metric < Y] by [date]."
  - Don't declare winners on small samples. If volume is too low for a statistical test, say so and treat the result as directional.
- **Test design and performance diagnosis:** `references/testing-and-diagnosis.md`.
- **Report honestly.**
  - Separate measured results from estimates.
  - Show comparisons, against the previous period or the goal.
  - Treat anomalies as hypotheses until checked.
  - Never present email opens as reliable engagement, because privacy features inflate them.
- **Publishing, sending, scheduling and ad spend require explicit user approval.** See the action gate in `customer-facing-quality-gate`.
