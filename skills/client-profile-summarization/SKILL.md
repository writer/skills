---
name: client-profile-summarization
description: Generate holistic client profile summaries for wealth management relationships. Use when onboarding new clients, preparing for annual reviews, conducting relationship transitions between advisors, aggregating data across custodians, or creating a unified view of client financial position, goals, risk profile, and household dynamics.

metadata:
  display_name: "Client Profile Summarization"
  short_description: "Summarize wealth management client profiles holistically"
  default_prompt: "Summarize my client profile with key findings and next steps"
  version: "1.0.0"
  tags:
    - financial-services
  icon_path: "assets/icon.png"
---

# Client Profile Summarization

## Overview

Produce comprehensive client profile summaries that aggregate financial position, investment holdings, insurance coverage, estate planning status, tax situation, and personal/family context into a unified document. These summaries serve as the foundation for advisory relationships — enabling advisors to deliver personalized advice, demonstrate fiduciary care, and maintain continuity across team transitions. Outputs conform to Reg BI suitability documentation and Form CRS relationship standards.

## When to Use

- New client onboarding — creating the initial comprehensive profile
- Annual review preparation — updating and refreshing the client profile
- Advisor transition — ensuring relationship continuity with complete context transfer
- Multi-generational planning — capturing household and family dynamics
- Compliance review — documenting know-your-client (KYC) and suitability basis
- Relationship deepening — identifying unmet needs and cross-service opportunities

## Required Inputs

| Input | Description | Format |
|-------|-------------|--------|
| Client questionnaire | Risk tolerance, goals, time horizon, income, expenses | Completed intake form |
| Account statements | All investment, banking, and retirement accounts | Custodian statements |
| Insurance policies | Life, disability, LTC, P&C coverage summaries | Policy declarations |
| Estate documents | Will, trust, POA, beneficiary designations summary | Legal document review |
| Tax returns | 2–3 years of federal and state returns | Tax documents |
| Personal information | Family composition, employment, health considerations | Client-provided |
| Existing plans | Prior financial plans, IPS documents, advisor notes | Historical records |

## Methodology

### Step 1 — Household Composition and Personal Context

Document the complete household picture:

- **Primary client**: Name, DOB, SSN (last 4), employment status, employer, title, compensation structure
- **Spouse/partner**: Same details, including separate employment and benefits
- **Dependents**: Children (ages, education status, special needs), aging parents, other dependents
- **Key life events**: Recent or upcoming marriage, divorce, retirement, inheritance, business sale, relocation
- **Health considerations**: Any health factors relevant to insurance needs, life expectancy assumptions, or LTC planning
- **Professional network**: CPA, estate attorney, insurance agent — contact information and coordination notes
- **Communication preferences**: Meeting frequency, communication channels, level of detail desired, decision-making style (delegator vs. involved)

### Step 2 — Financial Position Aggregation

Consolidate all financial data into a unified balance sheet:

**Assets:**
- Liquid investments (taxable brokerage, money market, CDs)
- Retirement accounts (401(k), IRA, Roth IRA, 403(b), SEP, defined benefit pension value)
- Real estate (primary residence, vacation property, rental/investment properties)
- Business interests (ownership stakes, estimated valuations, liquidity constraints)
- Insurance cash values (whole life CSV, annuity values)
- Other assets (collectibles, deferred compensation, stock options/RSUs, trust interests)

**Liabilities:**
- Mortgage(s) with balance, rate, term, and payment
- Student loans, auto loans, personal loans
- Credit card balances
- Business debt personally guaranteed
- Future commitments (education funding, eldercare)

**Net worth calculation**: Total assets minus total liabilities with year-over-year trend

### Step 3 — Income and Cash Flow Analysis

Map all income sources and spending patterns:

- **Earned income**: Salary, bonus, commissions, business income (note variability)
- **Investment income**: Dividends, interest, rental income, capital gains distributions
- **Retirement income**: Pension, Social Security (current or projected), annuity payments
- **Other income**: Trust distributions, alimony, consulting, board fees
- **Expense analysis**: Fixed expenses, discretionary spending, savings rate
- **Cash flow surplus/deficit**: Monthly and annual net cash flow with savings capacity
- **Tax efficiency**: Current marginal tax rate (federal + state), AMT exposure, NIIT applicability

### Step 4 — Investment Holdings Analysis

Summarize investment holdings across all accounts:

- **Asset allocation**: Current allocation vs. target (equity, fixed income, alternatives, cash)
- **Account-level detail**: Holdings by account with purpose designation
- **Tax location optimization**: Tax-efficient placement (bonds in tax-deferred, growth in Roth)
- **Concentration risk**: Single-stock positions, employer stock, sector concentration
- **Cost basis**: Unrealized gains/losses and tax lot management status
- **Income yield**: Current portfolio income yield and projected income generation
- **Fee analysis**: Weighted average expense ratio, advisory fees, platform fees

### Step 5 — Risk Profile Assessment

Document the client's comprehensive risk profile:

- **Risk tolerance questionnaire score**: Quantitative score from validated instrument
- **Risk capacity**: Objective financial ability to absorb losses (time horizon, income stability, net worth, liquidity needs)
- **Risk need**: Required return to meet goals (if return need < capacity, can reduce risk)
- **Behavioral considerations**: Past behavior during market stress, loss aversion indicators
- **Risk profile reconciliation**: If tolerance, capacity, and need conflict, document how the advisory team resolved the conflict
- **Suitability determination**: Client classification (conservative, moderate, moderate growth, growth, aggressive) with rationale per Reg BI

### Step 6 — Goals and Planning Gap Analysis

Document stated goals and assess progress:

| Goal | Priority | Target Amount | Timeline | Current Funding | Gap | On Track |
|------|----------|--------------|----------|----------------|-----|----------|
| Retirement | High | $X.XM | XX years | $XXX K | $XXX K | [Y/N] |
| Education | High | $XXX K | XX years | $XX K | $XX K | [Y/N] |
| Home purchase | Medium | $XXX K | X years | $XX K | $XX K | [Y/N] |
| Legacy/charity | Medium | $X.XM | Lifetime | $XXX K | $XXX K | [Y/N] |

- **Retirement readiness**: Monte Carlo simulation results (probability of success at X% confidence)
- **Education funding**: 529 plan status, projected costs, funding gap
- **Insurance needs**: Life insurance gap analysis, disability coverage adequacy, LTC coverage assessment
- **Estate planning status**: Will/trust currency, beneficiary designation review, estate tax exposure

### Step 7 — Profile Summary and Action Items

Generate the final profile document:

## Output Specification

```
## Client Profile Summary — [Client Name(s)]

### Personal Information
- Household: [Primary client and spouse/partner]
- Dependents: [Children, ages]
- Employment: [Status, employer, anticipated changes]
- Communication preference: [Frequency, channel, style]

### Financial Position Summary
| Category | Amount | % of Total |
|----------|--------|-----------|
| Liquid investments | $X,XXX,XXX | XX% |
| Retirement accounts | $X,XXX,XXX | XX% |
| Real estate (net) | $X,XXX,XXX | XX% |
| Other assets | $XXX,XXX | XX% |
| **Total assets** | **$X,XXX,XXX** | **100%** |
| Total liabilities | ($XXX,XXX) | |
| **Net worth** | **$X,XXX,XXX** | |

### Income Summary
- Total household income: $XXX,XXX
- Investment income: $XX,XXX
- Savings rate: XX%
- Marginal tax rate: XX% (federal + state)

### Investment Summary
- Total investable assets: $X,XXX,XXX
- Current allocation: XX% equity / XX% FI / XX% alt / XX% cash
- Target allocation: XX% equity / XX% FI / XX% alt / XX% cash
- Weighted expense ratio: X.XX%
- Concentration flags: [Any single positions > 10%]

### Risk Profile
- Risk tolerance: [Score and category]
- Risk capacity: [Assessment]
- Suitability classification: [Category]

### Goals Status
[Goals table with funding status and on-track indicators]

### Planning Gaps Identified
1. [Gap with recommended action]
2. [Gap with recommended action]
3. [Gap with recommended action]

### Next Steps
1. [Action — owner — deadline]
2. [Action — owner — deadline]
3. [Action — owner — deadline]

### Professional Team
- CPA: [Name, firm, contact]
- Attorney: [Name, firm, contact]
- Insurance: [Name, firm, contact]
```

## Analysis Framework

Apply the **WEALTH** framework:

- **W**hole picture — Aggregate all financial, personal, and family data
- **E**arnings — Map income sources, tax situation, and cash flow
- **A**ssets — Catalog and analyze all investment and non-investment assets
- **L**iabilities — Document debts and future financial commitments
- **T**argets — Define and prioritize financial goals with timelines
- **H**ealth — Assess risk profile, insurance adequacy, and estate readiness

## Examples

**Example 1 — Pre-Retirement Couple**

Client: John (58) and Maria (55) Chen. Combined income: $425K. Investable assets: $2.8M across 4 accounts (2 IRAs, joint brokerage, Maria's 401k). Primary residence: $650K (mortgage: $180K at 3.2%). Risk tolerance: Moderate. Goals: Retire at 62 (John) and 60 (Maria), fund remaining 2 years of daughter's college ($80K), maintain current lifestyle. Gaps identified: Portfolio overweight equities at 78% vs. 60% target for 4–7 year retirement horizon; no LTC coverage; estate documents 12 years old and pre-date current trust law. Actions: Rebalance to 60/35/5, obtain LTC quotes, schedule estate document review with attorney.

**Example 2 — Next-Gen Wealth Transfer**

Client: Sarah Williams (32), recently inherited $1.4M from grandmother's trust. First-time investor. Employment: Software engineer, $185K salary. Student loans: $42K at 5.5%. No existing investment accounts beyond employer 401(k) with $35K balance. Risk tolerance: Growth (long time horizon, high capacity). Goals: Buy home in 2 years ($200K down payment), maximize long-term growth, establish charitable giving. Actions: Segregate $200K for home purchase in short-term instruments, establish taxable brokerage with 80/15/5 allocation for long-term assets, accelerate student loan payoff from inheritance, establish donor-advised fund with $25K initial contribution.

## Guidelines

- Obtain explicit client consent before aggregating data from external custodians or advisors
- Mark all profile documents as confidential with appropriate handling procedures
- Update profiles at least annually and after any material life event
- Cross-reference beneficiary designations across all accounts for consistency
- Flag any discrepancies between stated risk tolerance and current portfolio positioning
- Document the source of all data elements (client-provided vs. verified vs. estimated)
- Comply with Reg BI documentation requirements for suitability basis
- Maintain version history of profile updates with timestamps

## Validation Checklist

- [ ] All household members and dependents are documented with current information
- [ ] Financial position includes all known accounts, assets, and liabilities
- [ ] Income analysis covers all sources including variable and non-recurring
- [ ] Investment holdings are current (within 30 days) and cover all accounts
- [ ] Risk profile assessment uses a validated questionnaire instrument
- [ ] Goals are specific, measurable, and prioritized with timelines
- [ ] Planning gaps are identified with recommended actions
- [ ] Professional team contacts are current and coordination notes documented
- [ ] Beneficiary designations reviewed for consistency across accounts
- [ ] Profile meets Reg BI suitability documentation requirements
