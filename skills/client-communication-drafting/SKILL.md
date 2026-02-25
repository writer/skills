---
name: client-communication-drafting
description: Draft regulation-safe client communications for wealth management and advisory relationships. Use when composing client emails, letters, market commentaries, performance reports, recommendation letters, or any written communication that must comply with SEC advertising rules, FINRA communications standards, Reg BI disclosure requirements, and firm compliance policies.

metadata:
  display_name: "Client Communication Drafting"
  short_description: "Draft compliant wealth management client communications"
  default_prompt: "Generate client communication for my case with clear next steps"
  version: "1.0.0"
  tags:
    - financial-services
  icon_path: "assets/icon.png"
---

# Client Communication Drafting

## Overview

Generate compliant, professional client communications that meet SEC, FINRA, and state regulatory standards. This skill produces communications that are fair, balanced, and not misleading — covering performance reporting, investment recommendations, market commentary, account updates, and relationship correspondence. All outputs are pre-screened against common regulatory pitfalls and include compliance annotations for reviewer efficiency.

## When to Use

- Drafting client emails about portfolio performance or market conditions
- Composing investment recommendation letters for documentation
- Writing market commentary or investment outlook pieces
- Creating client newsletters or educational content
- Preparing account review summaries for client distribution
- Responding to client complaints or inquiries in writing
- Drafting social media content for advisor profiles

## Required Inputs

| Input | Description | Format |
|-------|-------------|--------|
| Communication purpose | What message needs to be conveyed | Text description |
| Client context | Client name, relationship, sophistication level | CRM data |
| Portfolio data | Relevant performance, holdings, or account information | Custodian data |
| Compliance rules | Firm-specific communication policies and pre-approved language | Policy manual |
| Regulatory framework | Applicable rules (SEC Marketing Rule, FINRA 2210/2211) | Regulatory reference |
| Approval workflow | Required reviews and approvals before distribution | Compliance process |

## Methodology

### Step 1 — Communication Classification

Classify the communication under FINRA and SEC frameworks:

**FINRA Rule 2210 categories:**
- **Institutional communication**: To institutional investors only (QIBs, banks, registered entities) — principal pre-approval may not be required
- **Retail communication**: To 25+ retail investors within 30 days — principal pre-approval required
- **Correspondence**: To ≤25 retail investors within 30 days — subject to supervision but may not require pre-approval

**SEC Marketing Rule (Rule 206(4)-1) applicability:**
- Does the communication constitute an "advertisement"? (Any direct or indirect communication offering advisory services to more than one person, or endorsement/testimonial)
- If yes, apply the seven general prohibitions and specific requirements

**Content type determination:**
| Type | Description | Key Requirements |
|------|-------------|-----------------|
| Performance report | Account-specific returns | Net-of-fee returns, appropriate benchmark, time periods |
| Recommendation | Specific investment suggestion | Reg BI documentation, suitability basis |
| Market commentary | General market discussion | Fair and balanced, no predictions |
| Account update | Administrative or status information | Accuracy, completeness |
| Educational | General financial education | No specific recommendations implied |

### Step 2 — Content Drafting with Compliance Guardrails

Draft the communication applying regulatory requirements:

**SEC Marketing Rule — Seven General Prohibitions:**
1. No untrue statements of material fact or omission
2. No unsubstantiated material claims
3. No untrue or misleading implications
4. No discussion of potential benefits without fair and balanced treatment of risks
5. No cherry-picking favorable results without fair context
6. No information that is otherwise materially misleading
7. No references to specific past recommendations unless all conditions met

**Performance presentation standards:**
- Always present NET-of-fee performance (gross performance may be shown alongside net)
- Include 1-year, 5-year, and 10-year (or since-inception) periods
- Show performance through the most recent quarter-end
- Include appropriate benchmark with description of why it was selected
- Disclose material market conditions that contributed to performance
- Never imply that past performance indicates future results
- Include the required legend: "Past performance is not indicative of future results"

**Balanced presentation requirements:**
- For every potential benefit mentioned, address the associated risk
- Example: "While emerging market equities offer higher growth potential, they also carry higher volatility, currency risk, and political risk"
- Avoid superlatives: "best," "top-performing," "guaranteed," "safe"
- Avoid promissory language: "will," "ensure," "guarantee" — use "may," "seeks to," "is designed to"

### Step 3 — Tone and Readability Calibration

Adjust the communication for the intended audience:

**Client sophistication levels:**

| Level | Characteristics | Communication Style |
|-------|----------------|-------------------|
| Basic | Limited financial knowledge | Simple language, define terms, avoid acronyms |
| Intermediate | General market awareness | Moderate technical language with context |
| Sophisticated | Experienced investor, professional | Technical language acceptable, deeper analysis |
| Institutional | Professional fiduciaries | Technical, data-dense, industry terminology |

**Tone guidelines:**
- Professional but warm — avoid both sterile legalese and excessive informality
- Confident but not arrogant — acknowledge uncertainty where it exists
- Empathetic during volatile periods — recognize that portfolio declines cause stress
- Action-oriented — every communication should have a clear next step or takeaway
- Personalized — use the client's name, reference their specific situation when appropriate

### Step 4 — Required Disclosures and Disclaimers

Include all mandatory disclosures based on communication type:

**Standard disclosures (include in most communications):**
- Firm name, registration status, and contact information
- "Past performance is not indicative of future results"
- "Investing involves risk, including possible loss of principal"
- Material conflicts of interest relevant to the content
- Fee disclosure where performance is discussed

**Recommendation-specific disclosures:**
- Reg BI best interest determination basis
- Material conflicts of interest related to the recommendation
- Cost information for recommended products
- Alternative products considered and rationale for selection

**Performance-specific disclosures:**
- Benchmark description and selection rationale
- Performance calculation methodology (time-weighted vs. money-weighted)
- Fee impact disclosure
- Material market conditions disclaimer
- Composite construction methodology (if applicable)

**Testimonial/endorsement disclosures (SEC Marketing Rule):**
- Clear identification as a testimonial or endorsement
- Compensation disclosure
- Conflicts of interest
- Statement that experience may not be representative

### Step 5 — Prohibited Language Screening

Screen the draft for common regulatory violations:

**Red flag terms to avoid:**
- "Guaranteed" or "risk-free" (unless referring to government-backed instruments with full context)
- "Safe" as applied to any investment
- "Best" or "top" without substantiation and context
- "Will" (implies certainty) — replace with "may" or "seeks to"
- "Outperform" as a forward-looking statement
- "No-brainer" or "can't lose"
- "Aggressive" without risk context
- Specific return projections ("you'll earn 8%")
- Cherry-picked time periods that show only favorable results

**Compliant alternatives:**

| Avoid | Use Instead |
|-------|------------|
| "This investment is safe" | "This investment is designed to provide stability, though all investments carry risk" |
| "You'll earn 8% annually" | "The strategy targets a long-term return of approximately 8% annually, though actual returns will vary" |
| "Our fund is the best performer" | "Our fund ranked in the top quartile of its category over the trailing 3-year period ending [date]" |
| "I guarantee you'll be happy" | "We are committed to providing excellent service and working toward your financial goals" |

### Step 6 — Personalization and Contextualization

Tailor the communication to the specific client:

- Reference the client's stated goals and how the topic relates to their plan
- Use portfolio-specific data rather than generic market statistics
- Address anticipated client concerns based on their risk profile and communication history
- Adapt the length and detail level to the client's known preferences
- Include a specific call-to-action appropriate for the client's situation

### Step 7 — Compliance Review Preparation

Prepare the communication for compliance review:

- Annotate the draft with regulatory citations for key claims
- Flag any areas requiring compliance judgment call
- Provide source documentation for all data, statistics, and performance figures
- Note the distribution method and audience size for classification purposes
- Include the approval routing based on communication type and firm policy

## Output Specification

```
## Client Communication Draft

### Classification
- Type: [Retail / Institutional / Correspondence]
- Category: [Performance / Recommendation / Commentary / Update]
- SEC Marketing Rule applicable: [Yes/No]
- Approval required: [Yes — principal review / No]

### Draft Communication

Subject: [Email subject line]

Dear [Client Name],

[Body text — compliant, balanced, personalized]

[Required disclosures]

[Call to action]

Sincerely,
[Advisor Name, Title]
[Firm Name, Registration]

### Compliance Annotations
- [Line X]: Performance claim — source: [Custodian report, date]
- [Line Y]: Risk/benefit balanced — [risk statement] offsets [benefit statement]
- [Line Z]: Disclaimer included per [regulation]

### Disclosures Included
- [ ] Past performance disclaimer
- [ ] Risk of loss disclaimer
- [ ] Fee disclosure (if performance discussed)
- [ ] Benchmark description
- [ ] Conflict of interest disclosure
- [ ] Reg BI basis (if recommendation)

### Review Notes
- Flagged items for compliance judgment: [List]
- Source documentation attached: [List]
- Distribution: [Method, audience size, timing]
```

## Analysis Framework

Apply the **CLEAR** framework:

- **C**lassify — Determine the regulatory classification and requirements
- **L**anguage — Draft using compliant, balanced, client-appropriate language
- **E**vidence — Support all claims with documented sources
- **A**djust — Personalize for the specific client and context
- **R**eview — Prepare for compliance review with annotations and sources

## Examples

**Example 1 — Quarterly Performance Email**

Subject: Q3 Portfolio Review — Your Year-to-Date Progress

"Dear Tom and Linda, I'm pleased to share your portfolio's third-quarter results. Your portfolio returned 4.2% for the quarter and 9.8% year-to-date (net of fees), compared to your blended benchmark's 3.8% and 8.5% respectively. The outperformance was primarily driven by our allocation to international equities, which benefited from dollar weakness, and selection within US small-cap stocks. It's worth noting that while international markets provided a tailwind this quarter, they also carry currency risk and higher volatility that may work against us in other periods. Your portfolio remains well-aligned with your target allocation and retirement timeline. I'd welcome the opportunity to discuss these results in more detail at your upcoming quarterly review. Past performance is not indicative of future results. Investing involves risk, including possible loss of principal."

**Example 2 — Market Volatility Outreach**

Subject: Navigating Recent Market Volatility — Your Portfolio Update

"Dear Margaret, I wanted to reach out proactively given the recent market turbulence. Over the past two weeks, the S&P 500 has declined approximately 7%. Your portfolio, designed with diversification across asset classes, has declined approximately 4.2% — your bond and alternative allocations have provided meaningful stability during this period. Market corrections of this magnitude have occurred roughly once every 18 months historically, and markets have recovered within an average of 4–6 months following similar declines. While past recoveries do not guarantee future outcomes, this pattern underscores the importance of maintaining your long-term investment strategy. No changes to your portfolio are recommended at this time. If your financial situation or goals have changed, or if you'd like to discuss your portfolio in more detail, please don't hesitate to reach out."

## Guidelines

- Every communication must be fair, balanced, and not misleading
- Pair every potential benefit with its corresponding risk
- Never use forward-looking performance statements without clear disclaimers
- Include required disclosures even if they seem redundant — omission is the higher risk
- Use net-of-fee performance unless gross is accompanied by net and fee disclosure
- Maintain a compliance-approved language library for commonly used phrases
- Route all retail communications through principal review before distribution
- Archive all client communications per SEC Books and Records Rule (17a-4) — minimum 3 years
- Social media posts are treated as retail communications under FINRA 2210

## Validation Checklist

- [ ] Communication correctly classified under FINRA 2210 categories
- [ ] SEC Marketing Rule seven prohibitions checked against content
- [ ] Performance presented net of fees with required time periods
- [ ] Benefits balanced with corresponding risks throughout
- [ ] No prohibited language or forward-looking guarantees
- [ ] All data and statistics sourced and documented
- [ ] Required disclosures included (past performance, risk of loss, fees, conflicts)
- [ ] Tone appropriate for client sophistication level
- [ ] Personalized to client's specific situation and goals
- [ ] Compliance annotations prepared for reviewer efficiency
