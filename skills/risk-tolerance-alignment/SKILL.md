---
name: risk-tolerance-alignment
description: Check portfolio suitability alignment against client risk tolerance, capacity, and investment objectives per Reg BI and fiduciary standards. Use when onboarding clients, conducting suitability reviews, documenting Reg BI best interest determinations, resolving conflicts between stated risk tolerance and actual portfolio positioning, or responding to client complaints about investment outcomes.

metadata:
  display_name: "Risk Tolerance Alignment"
  short_description: "Align portfolios with client risk tolerance per Reg BI"
  default_prompt: "Analyze my risk tolerance alignment and recommend clear next actions"
  version: "1.0.0"
  tags:
    - financial-services
  icon_path: "assets/icon.png"
---

# Risk Tolerance Alignment

## Overview

Evaluate the alignment between a client's risk profile (tolerance, capacity, and need) and their actual portfolio positioning. This skill detects mismatches that could indicate suitability violations, documents the best interest determination process under Reg BI, and generates remediation recommendations when portfolios are misaligned with client objectives. Outputs serve as the primary suitability documentation for compliance and regulatory examination.

## When to Use

- New account suitability verification before initial investment
- Periodic suitability reviews (at least annually or after material life changes)
- Responding to client concerns about portfolio losses or volatility
- Documenting Reg BI best interest determinations for recommendations
- Resolving conflicts between risk questionnaire scores and client-expressed preferences
- Compliance audits of advisor recommendation patterns
- Post-market-event suitability reassessment

## Required Inputs

| Input | Description | Format |
|-------|-------------|--------|
| Risk questionnaire | Completed validated risk assessment instrument | Scored questionnaire |
| Client profile | Age, income, net worth, time horizon, goals, liquidity needs | Client data |
| Portfolio holdings | Current investment positions across all accounts | Custodian data |
| Account types | Registration types (IRA, Roth, trust, joint, UTMA) | Account records |
| Investment history | Past investment experience, years investing | Client disclosure |
| Prior interactions | Notes on client-expressed risk preferences and concerns | CRM notes |
| Product information | Cost, risk, complexity of recommended products | Product data |

## Methodology

### Step 1 — Multi-Dimensional Risk Profile Construction

Assess risk across three independent dimensions:

**Risk Tolerance (Willingness):**
- Quantitative score from validated questionnaire (e.g., Riskalyze, FinaMetrica)
- Qualitative assessment from client interview and behavioral observations
- Historical behavior: How did the client react to past drawdowns? (Called to sell? Stayed the course? Bought more?)
- Score mapping to risk categories:
  - 1–20: Conservative (capital preservation priority)
  - 21–40: Moderately conservative (income with limited growth)
  - 41–60: Moderate (balanced growth and income)
  - 61–80: Moderately aggressive (growth priority with income secondary)
  - 81–100: Aggressive (maximum growth, high volatility acceptance)

**Risk Capacity (Ability):**
- **Time horizon**: Years until funds needed (longer = higher capacity)
- **Income stability**: Predictable salary vs. variable/business income
- **Liquid net worth**: Investable assets relative to annual expenses
- **Income replacement ratio**: Investment income as % of total income needs
- **Human capital**: Present value of future earnings (younger = more human capital = more capacity)
- **Insurance adequacy**: Life, disability, LTC coverage sufficiency
- Capacity scoring: Combine factors into a composite capacity score

**Risk Need (Required return):**
- Calculate the return required to meet stated financial goals
- Monte Carlo simulation: What return at what risk level achieves goals with ≥80% probability?
- If required return is achievable at lower risk than tolerance allows, the need constrains upward
- If required return demands more risk than tolerance allows, document the gap and advise

### Step 2 — Risk Profile Reconciliation

Resolve conflicts between tolerance, capacity, and need:

| Scenario | Tolerance | Capacity | Need | Resolution |
|----------|-----------|----------|------|------------|
| Aligned | Moderate | Moderate | Moderate | Invest at moderate risk |
| Conservative gap | Conservative | High | High | Educate; invest conservatively but document goal shortfall risk |
| Aggressive gap | Aggressive | Low | Low | Invest conservatively; document that capacity governs |
| Need exceeds tolerance | Moderate | Moderate | High | Present trade-off; document client's informed decision |
| Need below capacity | Any | High | Low | Invest at lower end; excess capacity provides safety margin |

**Key principle**: Invest at the LOWEST of the three dimensions. Document any client request to override with informed consent.

### Step 3 — Portfolio Risk Assessment

Measure the actual risk level of the current portfolio:

- **Portfolio volatility**: Annualized standard deviation (historical and forward-looking)
- **Maximum drawdown**: Worst peak-to-trough decline in the portfolio's history or backtest
- **Value-at-Risk (95%)**: Maximum expected loss in 1 month at 95% confidence
- **Beta**: Portfolio sensitivity to broad market movements
- **Downside capture ratio**: Performance in down markets relative to benchmark
- **Stress test results**: Portfolio performance under 2008 GFC, 2020 COVID, rising rate scenarios
- **Risk score**: Map portfolio to the same 1–100 scale used for risk tolerance

### Step 4 — Alignment Assessment

Compare portfolio risk to client risk profile:

**Alignment matrix:**

| Client Risk Category | Acceptable Portfolio Risk Score Range | Acceptable Equity Range |
|---------------------|--------------------------------------|------------------------|
| Conservative (1–20) | 1–25 | 0%–25% |
| Mod Conservative (21–40) | 20–45 | 20%–40% |
| Moderate (41–60) | 40–65 | 35%–65% |
| Mod Aggressive (61–80) | 60–82 | 55%–80% |
| Aggressive (81–100) | 78–100 | 70%–100% |

**Misalignment detection:**
- **Over-risked**: Portfolio risk score exceeds the client's acceptable range
- **Under-risked**: Portfolio risk score is below the client's acceptable range
- **Product mismatch**: Specific products are unsuitable regardless of aggregate allocation (e.g., complex derivatives for unsophisticated client, illiquid alternatives for client with near-term liquidity needs)
- **Concentration risk**: Single positions or correlated exposures creating undisclosed tail risk
- **Cost misalignment**: High-cost products where lower-cost suitable alternatives exist (Reg BI cost consideration)

### Step 5 — Product-Level Suitability Screening

Evaluate each holding for individual suitability:

- **Complexity assessment**: Is the product complexity appropriate for the client's sophistication level?
  - Level 1 (Basic): Mutual funds, ETFs, individual stocks/bonds
  - Level 2 (Intermediate): Options (covered calls, protective puts), REITs, interval funds
  - Level 3 (Complex): Structured products, alternatives, private placements, leveraged/inverse ETFs
- **Liquidity assessment**: Can the client afford the lock-up period? (Private equity, interval funds, annuity surrender periods)
- **Cost reasonableness**: Are product costs justified by the specific benefit to this client?
- **Concentration appropriateness**: Is the position sized appropriately for the client's total portfolio?
- **Tax efficiency**: Is the product in the appropriate account type for tax efficiency?

### Step 6 — Reg BI Best Interest Documentation

Document the four Reg BI obligations:

1. **Disclosure**: Have all material facts about the recommendation been disclosed? (Form CRS, fee schedules, conflicts)
2. **Care**: Does the recommendation reflect reasonable diligence, care, and skill?
   - Reasonable basis suitability (product is suitable for at least some investors)
   - Customer-specific suitability (product is suitable for THIS client)
   - Quantitative suitability (no excessive trading or churning)
3. **Conflicts of interest**: Have all material conflicts been identified, disclosed, and mitigated?
   - Compensation differentials between recommended and alternative products
   - Revenue sharing, 12b-1 fees, proprietary product incentives
   - Account type conflicts (brokerage vs. advisory)
4. **Compliance**: Are firm-level policies and procedures followed?

### Step 7 — Remediation and Documentation

Address any identified misalignments:

## Output Specification

```
## Risk Tolerance Alignment Report — [Client Name]

### Risk Profile Summary
| Dimension | Score | Category | Driver |
|-----------|-------|----------|--------|
| Risk tolerance | XX/100 | [Category] | Questionnaire + interview |
| Risk capacity | XX/100 | [Category] | Time horizon, net worth, income |
| Risk need | XX/100 | [Category] | Goal-based return requirement |
| **Governing risk level** | **XX/100** | **[Category]** | **[Lowest dimension]** |

### Portfolio Risk Assessment
| Metric | Portfolio | Target Range | Status |
|--------|-----------|-------------|--------|
| Risk score | XX/100 | XX–XX | [Aligned/Misaligned] |
| Volatility | XX.X% | XX–XX% | [Aligned/Misaligned] |
| Max drawdown (est.) | -XX% | -XX to -XX% | [Aligned/Misaligned] |
| Equity allocation | XX% | XX–XX% | [Aligned/Misaligned] |

### Alignment Determination
- **Overall alignment**: [Aligned / Marginally misaligned / Materially misaligned]
- **Direction**: [Over-risked / Under-risked / Appropriate]
- **Magnitude**: [X points/X% outside acceptable range]

### Product Suitability Flags
| Product | Issue | Severity | Action Required |
|---------|-------|----------|----------------|
| [Product] | [Issue] | [Low/Med/High] | [Action] |

### Reg BI Documentation
- Disclosure obligation: [Met / Gap identified]
- Care obligation: [Met / Gap identified]
- Conflict obligation: [Met / Gap identified]

### Remediation Recommendations
1. [Action — timeline — responsible party]
2. [Action — timeline — responsible party]

### Advisor Attestation
I confirm this suitability assessment accurately reflects the client's risk profile
and the portfolio's alignment with their investment objectives.

Advisor: _________________ Date: _________
```

## Analysis Framework

Apply the **MATCH** framework:

- **M**easure — Quantify risk tolerance, capacity, and need independently
- **A**ssess — Evaluate the portfolio's actual risk characteristics
- **T**est — Compare portfolio risk to the client's governing risk level
- **C**orrect — Address misalignments with specific remediation actions
- **H**istory — Document the analysis and decision for compliance records

## Examples

**Example 1 — Over-Risked Retiree**

Client: 72-year-old retiree, risk tolerance score 35 (moderately conservative), depends on portfolio for 60% of income. Portfolio: 72% equities, risk score 74 (moderately aggressive). Misalignment: Material — portfolio risk score 39 points above governing level. Root cause: Advisor transitioned from accumulation to distribution phase 7 years ago but never adjusted allocation. Remediation: Reduce equities to 35%, establish bond ladder for 5 years of income, implement systematic withdrawal plan. Timeline: Complete within 60 days with tax-efficient execution plan.

**Example 2 — Under-Risked Young Professional**

Client: 28-year-old software engineer, $175K income, $95K in 401(k). Risk tolerance: 78 (moderately aggressive). Risk capacity: 90 (high — 35+ year horizon, stable income, no dependents). Portfolio: 100% target-date 2065 fund (appropriate) but also has $50K in a savings account earning 0.5%. Under-risked on the non-retirement portion. Recommendation: Establish taxable brokerage account, invest $35K in diversified growth allocation (80/15/5), maintain $15K emergency fund (6 months expenses). No suitability concern with current 401(k) — target-date fund is well-aligned.

## Guidelines

- Use a validated, third-party risk questionnaire instrument — not a home-grown survey
- Never invest above a client's risk tolerance without documented, informed client consent
- Risk capacity should govern when it is lower than stated tolerance
- Reassess risk tolerance after material life events (retirement, inheritance, health diagnosis, divorce)
- Document all conversations where clients express risk preferences inconsistent with their questionnaire
- Review product suitability at the recommendation level, not just the account level
- Maintain Reg BI best interest documentation for every recommendation, not just initial account opening
- Flag accounts where risk profile has not been updated in >24 months for priority review

## Validation Checklist

- [ ] Risk tolerance assessed using a validated questionnaire instrument
- [ ] Risk capacity evaluated independently across all relevant factors
- [ ] Risk need calculated from goal-based return requirements
- [ ] Governing risk level determined as the lowest of tolerance, capacity, and need
- [ ] Portfolio risk measured using multiple metrics (volatility, drawdown, VaR, risk score)
- [ ] Alignment tested against defined acceptable ranges, not subjective judgment
- [ ] Product-level suitability screened for complexity, liquidity, cost, and concentration
- [ ] Reg BI four-obligation framework documented for all recommendations
- [ ] Misalignments have documented remediation plans with timelines
- [ ] Advisor attestation recorded with date for compliance records
