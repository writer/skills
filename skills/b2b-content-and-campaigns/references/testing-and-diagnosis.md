# Testing & Performance Diagnosis

Use this to design a content, PDP, ad or email test, and to explain why a metric moved. Both jobs fail in the same way: confident conclusions drawn from noise. The discipline below prevents that.

## 1. Designing a test
- **Hypothesis:** "IF we change [one variable] THEN [primary metric] will [direction] BECAUSE [evidence: review theme, data, customer quote]." State a direction only. Don't predict the size of the effect.
- **Pre-register before launch:**
  - one primary metric
  - secondary metrics
  - guardrail metrics (returns, unsubscribes, lead quality, complaints)
  - the rules for calling it a win, a loss or inconclusive
- **Change one variable per round.** For ads, test the angle first, then the hook or framework, then the CTA or format.
- **No dark-pattern variants.** No fake scarcity, countdowns, decoys or confirmshaming, even as a test.

## 2. Feasibility gate (most B2B and low-traffic tests fail it)
- **Sample size per arm** (two proportions, α = 0.05, power = 0.8):
  - n = (1.96 + 0.84)² × [p₁(1−p₁) + p₂(1−p₂)] ÷ (p₁ − p₂)²
  - p₁ is the baseline rate. p₂ = p₁ × (1 + MDE) for a relative minimum detectable effect, or p₁ + MDE for an absolute one. Example: p₁ = 3% with a 10% relative MDE (p₂ = 3.3%) needs about 53,000 per arm; a 1-point absolute MDE (p₂ = 4%) needs about 5,300.
  - State whether the minimum detectable effect is relative or absolute; the two give very different answers.
- **Duration:** n ÷ daily traffic per arm, rounded up to whole weeks. Run for at least 2 full weeks to cover weekly cycles and novelty effects.
- **If it's infeasible,** don't run a fake test. Do one of these instead:
  - ship obvious fixes, such as missing information or errors, without testing
  - run a before/after comparison labeled **directional**, noting seasonality and promotions
  - use qualitative evidence: customer interviews, sales feedback
- **Reading results:**
  - Don't peek, unless you use a sequential method designed for it.
  - p = 0.08 is not a win.
  - Report the confidence interval, not just the winner.
  - Keep a learning log.
- **Prioritizing the backlog:** rank by Impact × Confidence × Ease. Confidence comes from evidence, not enthusiasm.
- **Platform tools exist for some channels.** For example, Amazon's Manage Your Experiments tests titles, main images, bullets, descriptions and A+ content. It needs Brand Registry and enough recent traffic per ASIN.

## 3. Diagnosing why a metric moved
1. **Locate the change in the funnel:** impressions → click-through → detail views or visits → add-to-cart or form start → conversion → revenue or pipeline.
2. **Rule out non-content causes first:**
   - stock or availability, Buy Box loss
   - price changes, promotions ending
   - rating or review-count change
   - ad spend or bid changes
   - seasonality
   - competitor launches or price moves
   - ranking or algorithm shifts
   - **tracking or reporting changes** (check this first: broken tags often look like performance problems)
3. **Then check content.** Diff the dated content versions against the date the metric moved. Map each content lever to its stage:
   - title and main image → click-through
   - backend terms and categorization → impressions
   - bullets, A+ and images → conversion
4. **Run a counterfactual check** on each candidate cause: "If this hadn't changed, would the metric have held?" Give each cause a confidence label. Correlation is not causation.
5. **Report in this order:** situation → analysis (with evidence) → recommendation (by impact × speed) → what's working and should be kept. Show the inputs for any projection, and label it an estimate.

**Ad creative fatigue checks:**
- **All creatives declining together:** the cause is systemic (audience, budget, tracking, seasonality), not fatigue.
- **Stable CTR with rising cost per conversion:** the problem is post-click (landing page, offer, lead quality).
- **High frequency, stable CTR, rising CPM:** the audience is saturated. Small ABM audiences reach this fast.
- **A recent budget increase:** efficiency often drops after one. That is not fatigue.
- **Method:** read 7-day rolling rate metrics, with at least 14 days of data.
