# ABM Program Design

ABM works when sales and marketing aim at the same accounts with the same story at the same time. Most ABM failures are coordination failures, not creative ones.

## 1. Plays by tier

### Tier 1 — 1:1
- **Account plan** (see `enterprise-deal-strategy`): committee map, value hypothesis, entry points, mutual milestones.
- **Bespoke assets:**
  - an account-specific point of view or assessment, e.g. "Your PDP content across 3 retailers — gaps and opportunity"
  - a tailored business case
  - an executive briefing
- **Executive alignment:** pair our executives with theirs, and plan executive sponsorship of each interaction.
- **Orchestration:** sales, marketing, partners and executives each own named touches on a shared calendar.
- **Outside-in assessment as the entry asset.** For example, a review of the account's public PDPs across retailers, or of its public web content.
  - Use public pages only.
  - State the sample size and the date checked.
  - Show 2–3 concrete examples, framed as opportunities, never as shaming.
  - Never imply access to their internal data.
  - Run it through `customer-facing-quality-gate` as External – high sensitivity.
- **Advertising:** account-targeted ads that support the active narrative and stay consistent with what reps are saying. They warm the account but don't replace outreach.

### Tier 2 — 1:few
- **Clusters** share a meaningful attribute: industry, use case, trigger (e.g. "new CDO in last 6 months") or tech stack.
- **Cluster content:** industry point of view, use-case demo, peer roundtable, benchmark built only from real data.
- **Personalization:** at the cluster level, plus a personalized opening line and proof matched to each account.

### Tier 3 — 1:many
- Programmatic and intent-driven content, webinars, events, nurture.
- Sales engages only when account-level engagement or a strong trigger crosses an agreed threshold.

## 2. Sales–marketing operating agreement
Write this down. Ambiguity here is where ABM breaks.
- **Shared target account list**, owned jointly and refreshed on a set cadence (quarterly for tiers, immediately when signals change).
- **Engagement definition:** what counts as an "engaged account".
  - Example: 3+ known contacts from the account engaged in 30 days, at least one at Director+ level in the buying function.
  - Count meaningful actions only (meeting, reply, event attendance, high-intent page visits). Email opens are unreliable because privacy features inflate them.
- **Handoff:** when an account crosses the threshold, the owner gets a short summary of who engaged with what, plus a suggested angle. They accept or decline with a reason within an agreed SLA.
- **Named accounts route to the owner regardless of score.**
- **Cadence:** a weekly Tier-1 working session, a monthly program review, and a quarterly list and model refresh.
- **Feedback loop:** sales disposition reasons flow back into scoring and messaging.

## 3. Measurement (account-level, not lead-level)
| Stage | Metrics |
|---|---|
| Coverage | % of target accounts with the full committee identified; contacts per account in the buying function |
| Engagement | Engaged accounts; executive-level engagement; meetings held |
| Pipeline | Opportunities created from target accounts; pipeline value; stage progression |
| Velocity & conversion | Time between stages; win rate; deal size — compared against non-target accounts |
| Expansion | New business units, brands or regions added within existing customers |

- Don't judge ABM on cost per lead or volume of MQLs. It deliberately trades volume for value.
- Long cycles (9–24 months) need influence-based, account-level attribution and leading indicators.
- Report directional trends honestly rather than false precision.
- When comparing ABM with non-ABM accounts, note selection bias: target accounts were chosen because they looked better.

## 4. Lead and account scoring hygiene
- Score fit (who they are) and engagement (what they do) separately.
- Decay engagement over time; never decay fit.
- Scoring is a routing aid, not truth. If more than half of the routed accounts or leads get rejected by sales, the threshold or model is wrong.
- At low volume, review every inbound from target accounts manually instead of trusting a score.
- Calibrate against outcomes. After enough opportunities, check whether score actually predicts conversion, and retune.

## 5. Nurture governance
See `b2b-content-and-campaigns/references/email-programs.md`. The key ABM rule: when an account enters an active sales cycle, pause generic nurture for its committee and switch to deal-stage content that sales controls.
