---
name: advisor-prep-briefs
description: Generate comprehensive meeting preparation briefs for financial advisors before client reviews. Use when preparing for quarterly reviews, annual planning meetings, prospect discovery meetings, client onboarding sessions, or any client-facing interaction requiring advisor preparation with portfolio, market, and personal context.

metadata:
  display_name: "Advisor Prep Briefs"
  short_description: "Build meeting preparation briefs for financial advisors"
  default_prompt: "Optimize my meeting preparation for financial advisors and suggest the best next steps"
  version: "1.0.0"
  tags:
    - financial-services
  icon_path: "assets/icon.png"
---

# Advisor Meeting Prep Briefs

## Overview

Generate concise, actionable meeting preparation briefs that equip financial advisors with everything needed for productive client interactions. Briefs synthesize portfolio performance, recent life events, outstanding action items, market context, and discussion agenda into a single document that can be reviewed in 5–10 minutes before a meeting. The goal is to enable advisors to demonstrate knowledge, preparedness, and proactive care.

## When to Use

- Quarterly and annual client review meeting preparation
- First meeting with a prospect or referral
- Client calling with concerns (rapid context assembly)
- Advisor transition — preparing for first meeting with inherited clients
- Post-market-event check-in calls with top clients
- Estate planning, tax planning, or insurance review sessions

## Required Inputs

| Input | Description | Format |
|-------|-------------|--------|
| Client profile | Household composition, goals, risk profile | CRM data |
| Portfolio data | Current holdings, performance, allocation | Custodian feed |
| CRM notes | Recent interactions, action items, client sentiment | CRM records |
| Market context | Recent market performance, economic outlook | Market commentary |
| Planning data | Financial plan status, Monte Carlo results, goal progress | Planning software |
| Compliance flags | Outstanding compliance items, suitability reviews due | Compliance system |
| Calendar | Meeting date, time, type (in-person/virtual), attendees | Calendar data |

## Methodology

### Step 1 — Client Context Assembly

Pull together the essential client knowledge for the advisor:

**Relationship snapshot:**
- Client name(s), preferred name/greeting, pronunciation notes
- Relationship tenure and total AUM
- Service tier and fee schedule
- Last meeting date and type
- Client sentiment indicator (based on recent interactions)

**Personal context:**
- Recent life events flagged in CRM (job change, retirement, health, family, real estate)
- Upcoming milestones (birthdays, anniversaries, retirement date, child starting college)
- Client's interests, hobbies, or conversation topics from prior notes
- Any sensitivities or communication preferences noted

**Professional team:**
- CPA, estate attorney, insurance agent — any recent interactions or referrals
- Coordination items pending across professional team

### Step 2 — Portfolio Performance Summary

Prepare concise portfolio performance talking points:

- **Returns**: QTD, YTD, 1-year, 3-year, since-inception — net of fees
- **Benchmark comparison**: Performance vs. IPS benchmark with attribution summary
  - Allocation effect: Contribution from asset class weighting decisions
  - Selection effect: Contribution from security/manager selection within asset classes
- **Absolute dollar context**: "Your portfolio grew by $[X] this quarter to $[X] total"
- **Key contributors**: Top 3 positive and negative performance contributors
- **Fees**: Total fees paid YTD and trailing 12 months
- **Allocation drift**: Current vs. target allocation, any bands exceeded
- **Risk metrics**: Volatility, Sharpe ratio, max drawdown vs. benchmark

**Key talking point**: Frame performance in context of the client's goals, not just market benchmarks. "Your plan needs 6.5% annual returns, and you're tracking at 7.2% over three years."

### Step 3 — Goal Progress and Planning Update

Summarize the client's progress toward each stated goal:

| Goal | Target | Progress | Monte Carlo | Status |
|------|--------|----------|-------------|--------|
| Retirement at [age] | $[X]M needed | $[X]M current | XX% probability | [On track/Watch/Behind] |
| Education (child) | $[X]K needed | $[X]K funded | N/A | [X]% funded |
| Home purchase | $[X]K down payment | $[X]K saved | N/A | [X]% funded |
| Legacy | $[X]M bequest | $[X]M projected | XX% probability | [On track/Behind] |

- **Monte Carlo update**: Has the probability of success changed materially since last review?
- **Savings rate assessment**: Is the client on track with planned contributions?
- **Social Security timing**: Any new analysis needed as client approaches claiming window?
- **Insurance gaps**: Any identified coverage gaps requiring attention?

### Step 4 — Outstanding Action Items Review

Compile all open action items from prior meetings and communications:

| Action Item | Owner | Original Date | Status | Priority |
|-------------|-------|---------------|--------|----------|
| Update beneficiary designations on IRA | Client | [Date] | Open | High |
| Obtain LTC insurance quotes | Advisor | [Date] | Complete — present | Medium |
| Review 529 contribution strategy | Advisor | [Date] | In progress | Medium |
| Estate document review with attorney | Client | [Date] | Pending | Low |

- Flag any items overdue by >90 days for escalation
- Prepare updates on advisor-owned items
- Draft follow-up language for client-owned items that are overdue

### Step 5 — Market Context and Talking Points

Prepare market discussion points relevant to the client:

- **Market summary**: Key developments since last meeting (2–3 sentences max)
- **Client-relevant context**: How market events specifically affect THIS client's portfolio
  - Example: "Interest rate cuts benefit your bond allocation — your bond fund gained 4.2%"
  - Example: "Tech sector volatility affected your concentrated Apple position"
- **Anticipated client questions**: Based on headlines, predict likely client questions and prepare responses
  - "What does [headline event] mean for my portfolio?"
  - "Should I be doing anything differently?"
  - "Is my money safe?"
- **Forward outlook**: Brief, balanced perspective (avoid predictions; focus on plan adherence)

### Step 6 — Agenda and Discussion Topics

Structure the meeting agenda with time allocations:

```
Meeting Agenda — [Client Name] — [Date]

1. Personal catch-up and life updates (5 min)
   - Ask about: [specific personal items from CRM]

2. Portfolio review (10 min)
   - Performance summary and key drivers
   - Allocation review and rebalancing (if needed)

3. Goal progress check (10 min)
   - [Top priority goal] — progress and adjustments
   - Monte Carlo probability update

4. Action items review (5 min)
   - Outstanding items from last meeting
   - New items to assign

5. Proactive recommendations (10 min)
   - [Topic 1]: [Specific recommendation]
   - [Topic 2]: [Specific recommendation]

6. Questions and next steps (5 min)
   - Schedule next meeting
   - Confirm action item owners and deadlines
```

### Step 7 — Compliance and Risk Flags

Identify any compliance or risk items requiring attention:

- **Suitability review**: Is a periodic suitability review due? When was risk tolerance last assessed?
- **Form CRS**: Has the client received the current Form CRS? Document delivery
- **Large cash positions**: Any uninvested cash that may indicate a suitability concern
- **Concentration alerts**: Single positions exceeding threshold (typically 10% of portfolio)
- **Account documentation**: Any missing or expired documents (W-9, trust certification, POA)
- **RMD status**: For clients 73+, has the Required Minimum Distribution been satisfied?
- **Reg BI documentation**: Is the best interest determination current for recent recommendations?

## Output Specification

```
## Advisor Meeting Prep Brief

### Meeting Details
- Client: [Name(s)]
- Date/Time: [DateTime]
- Type: [In-person / Virtual / Phone]
- AUM: $[X] | Tenure: [X] years | Tier: [Service tier]

### Personal Notes
- [Greeting note, pronunciation, conversation starters]
- Recent events: [Life events from CRM]
- Upcoming milestones: [Birthdays, retirement date, etc.]

### Performance Snapshot
| Period | Portfolio | Benchmark | +/- | Dollar Change |
|--------|-----------|-----------|-----|---------------|
| QTD | X.X% | X.X% | +/-X.X% | +$XX,XXX |
| YTD | X.X% | X.X% | +/-X.X% | +$XXX,XXX |
| 1Y | X.X% | X.X% | +/-X.X% | +$XXX,XXX |
- Key drivers: [Top contributors and detractors]
- Allocation: [Current vs. target — any rebalancing needed]

### Goal Progress
[Goal summary table with on-track indicators]

### Open Action Items
[Action items table with status and priority]

### Market Talking Points
- [2–3 relevant market points with client-specific context]
- Anticipated questions: [Predicted questions with prepared responses]

### Proactive Recommendations
1. [Recommendation with rationale]
2. [Recommendation with rationale]

### Compliance Flags
- [Any items requiring attention]

### Suggested Agenda
[Structured agenda with time allocations]
```

## Analysis Framework

Apply the **READY** framework:

- **R**elationship context — Assemble personal and relationship history
- **E**arnings and performance — Summarize portfolio results with attribution
- **A**ction items — Track outstanding and new action items
- **D**iscussion topics — Prepare proactive recommendations and market context
- **Y**ield — Ensure every meeting produces value and advances the relationship

## Examples

**Example 1 — Quarterly Review for Pre-Retiree**

Brief: Tom and Linda Garcia, next meeting Thursday 2pm (in-person). AUM: $1.8M. Tenure: 8 years. Tom retiring in 14 months — this is a critical transition meeting. Portfolio: +3.2% QTD vs. +2.8% benchmark. Monte Carlo: 87% success at planned retirement date (up from 82% last quarter due to market gains). Action items: Tom needs to schedule HR meeting about pension election (overdue 2 months), Linda's IRA beneficiary update complete. Proactive: Present Social Security optimization analysis (delay Tom to 67, Linda claims at 64), discuss Medicare supplement options, introduce retirement income waterfall strategy. Compliance: Annual suitability review due — update risk tolerance questionnaire for post-retirement profile.

**Example 2 — Rapid Prep for Inbound Client Call**

Brief: Margaret Chen calling (unscheduled). AUM: $420K. Tenure: 3 years. Last contact: 6 weeks ago (routine). Recent market: S&P down 8% in 2 weeks. Margaret's portfolio: -5.2% (moderate allocation absorbing less of the decline). History: Margaret called during COVID selloff wanting to sell everything — was talked through it and stayed invested (portfolio fully recovered within 6 months). Key message: "Margaret, your portfolio is doing exactly what we designed it to do — absorbing less of the market's decline because of your diversified mix. You're down about 5% compared to the market's 8% drop. Remember in 2020 when we had a similar conversation? Your portfolio recovered fully within six months."

## Guidelines

- Limit the brief to 2 pages — advisors need to review in 5–10 minutes before the meeting
- Lead with personal context, not performance numbers — relationships first
- Frame performance relative to the client's goals, not just market benchmarks
- Prepare for the questions the client is likely to ask based on market conditions
- Always include at least one proactive recommendation — demonstrate value beyond reporting
- Flag compliance items prominently — these cannot be deferred
- Update the CRM with meeting notes and new action items immediately after the meeting
- For prospect meetings, substitute referral source context and discovery question framework

## Validation Checklist

- [ ] Client name, pronouns, and communication preferences are correct
- [ ] Performance data is current (within 1 business day of the meeting)
- [ ] Performance is presented net of fees with appropriate benchmark comparison
- [ ] Goal progress reflects current planning software outputs
- [ ] All outstanding action items are listed with current status
- [ ] Market talking points are relevant to THIS client's portfolio and concerns
- [ ] Proactive recommendations are suitable and documented per Reg BI
- [ ] Compliance flags are checked (suitability review, RMD, documentation)
- [ ] Agenda is structured with realistic time allocations
- [ ] Brief is concise enough to review in 5–10 minutes
