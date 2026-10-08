# Industry Playbook: Healthcare (Providers, Payers, Life Sciences)

These are lenses for research and messaging, not facts about any account. Validate each point per account. Items marked **[VERIFY]** need a primary source before they reach a customer.

**Watch the ambiguous terms:**
- **"CMO"** in a health system usually means Chief *Medical* Officer. The marketing leader is typically the Chief Marketing & Communications, Experience, or Growth/Strategy Officer.
- **"MLR"** means medical loss ratio at a payer, but medical-legal-regulatory review in pharma.
- **Use each segment's own word:** "patients" for providers, "members" for payers, "clinicians" (not "users").
- **Never call patients "leads" or "conversions"** in anything a buyer sees.

## Health systems and hospitals
| Role | Usually measured on |
|---|---|
| CEO and board | Operating margin, days cash on hand, bond covenants, market share, quality and safety reputation (CMS star rating, Leapfrog grade), community benefit (nonprofits) |
| CFO / VP Revenue Cycle | Operating margin, cost per adjusted discharge, labor and contract-labor cost, denial rate, A/R days, DNFB, cost to collect, payer mix, CMS penalty programs |
| COO / Chief Nursing Officer | Throughput (length of stay, ED boarding), capacity, nurse turnover and agency spend, HCAHPS |
| Chief Medical / Quality Officer | Quality measures, safety events, clinical variation, physician engagement |
| CIO, CMIO, CNIO | Clinician documentation and inbox burden ("pajama time"), EHR optimization, interoperability, AI governance, application sprawl (favoring tools that work inside the EHR) |
| Marketing, growth, patient access | New-patient acquisition, appointment conversion, access, referral leakage / "network integrity", digital front door, service-line growth, reputation |
| CISO, Privacy Officer, Compliance, Legal | Vendor risk, BAA terms, PHI flows, offshore data, AI risk. **These roles can veto a deal; they don't merely review it.** |

**Pains to validate:**
- Thin margins.
- Labor costs and shortages.
- Prior authorization and denials.
- Cyber resilience (heightened since the Change Healthcare attack in February 2024).
- Medicaid funding pressure from the July 2025 federal budget law, with work requirements from end-2026 and provider-tax limits phasing in from FY2028.
- The shift of care to ambulatory settings.
- Mergers and integration.
- AI governance.

**How they buy:**
- **Approvals:** IT governance or intake → AI governance committee (now common) → security / vendor-risk assessment → value analysis committee for clinical-facing products → legal → board approval for large contracts.
- **Security review:**
  - expect long questionnaires
  - HITRUST is often valued above SOC 2 Type II
  - many systems won't let PHI leave the country
  - subcontractors must be disclosed
  - BAA redlines commonly shorten breach-notice windows and add cyber insurance and indemnity
- **EHR fit:**
  - Integration with the EHR (Epic, Oracle Health) is usually expected.
  - EHR go-lives and upgrades freeze other work.
- **Budget:**
  - Fiscal years vary; check the account's Form 990 or bond disclosures.
  - Capital and operating budgets are approved separately.
- **Purchasing:**
  - Group purchasing organizations may hold contract vehicles.
  - Public and academic systems follow procurement law, and proposals may become public records.
  - Catholic systems apply the Ethical and Religious Directives.
- **Proof they trust:** peers of the same size, on the same EHR, in the same region. KLAS ratings and named references weigh heavily.

## Payers and health plans
| Role | Usually measured on |
|---|---|
| CEO / CFO / Chief Actuary | Medical loss ratio (ACA minimums: 80% individual and small group, 85% large group), medical cost trend, PMPM cost, admin ratio, membership growth and retention |
| Chief Medical Officer, utilization management, Stars and quality | Medicare Advantage Star Ratings (4+ stars earns the quality bonus), HEDIS, CAHPS, risk-adjustment accuracy and audit exposure |
| Chief Marketing / Growth Officer, member experience | Annual Enrollment Period sales, acquisition cost, disenrollment, service experience, broker channel |
| Operations | Auto-adjudication, prior-authorization turnaround (CMS-0057-F: 72-hour expedited and 7-day standard decisions from January 2026; prior-auth APIs due January 2027) |
| Compliance | CMS audits, MA marketing rules, oversight of downstream vendors |

**How they buy and when:**
- **CMS oversight passes down to vendors.** A vendor performing Medicare Advantage functions falls under it as a downstream entity:
  - compliance-training attestations
  - exclusion-list screening
  - offshore disclosure
  - a BAA
- **Calendar:**
  - MA bids are due in early June.
  - Star Ratings are released in October.
  - The Annual Enrollment Period runs 15 October–7 December. Marketing teams are saturated then, so don't pitch them.

## Life sciences (pharma, biotech, medtech)
| Role | Usually measured on |
|---|---|
| Commercial, brand, omnichannel | Launch uptake, HCP reach and frequency, share of voice, field productivity, speed to market |
| Medical affairs (kept separate from commercial) | Scientific exchange |
| Medical-legal-regulatory (MLR) review | Review cycle time, first-pass approval, content reuse |
| Market access / HEOR | Coverage, value dossiers |
| Regulatory and compliance | FDA promotion rules, PhRMA Code, Sunshine Act reporting |

**Pains to validate:**
- MLR review bottlenecks.
- Medicare drug-price negotiation under the IRA.
- Patent expiries.
- Field-force restructuring.
- Heightened FDA scrutiny of DTC advertising since September 2025.

**How they buy:**
- Preferred-vendor master agreements.
- Integration with the MLR system (often Veeva).
- Validation when the tool falls under GxP or 21 CFR Part 11.
- **Adverse-event routing.** Any tool that sees patient or clinician comments must route possible adverse events to pharmacovigilance.

## Research sources (high-value, non-obvious)
- **Nonprofit systems:** IRS Form 990, including Schedule H (community benefit) and executive compensation.
- **Municipal bond disclosures (MSRB EMMA):** financials, utilization, payer mix, strategy.
- **CMS data:** cost reports and Care Compare.
- **Leapfrog Hospital Safety Grades.**
- **Community Health Needs Assessments:** nonprofits publish one every 3 years, and they state priorities.
- **State Certificate of Need filings.**
- **Benchmark sources the buyer trusts:** Vizient, MGMA, HFMA, Kaufman Hall.
- **The HHS breach portal:** a sensitivity check only. Never reference it in outreach.

**Triggers:**
- A new CEO, CFO, CIO or CMIO.
- An affiliation or M&A.
- An EHR migration (also a timing blocker).
- A bond issuance.
- A new CHNA.
- CMS final rules: the inpatient rule typically comes around August; the physician fee schedule and outpatient rules around November.
- New facilities.
- A cyber incident. **Wait, and never exploit it.**

## Sensitivities
- **Never imply the product replaces clinicians or makes clinical decisions** ("diagnoses", "decides"). This is a trust issue and a regulatory one: claims can turn software into a medical device. See the healthcare rules reference.
- **Don't sell on fear** of named breaches, layoffs or penalties.
- **Many systems own health plans,** so avoid "beat the payer" messaging.
- **Mirror the account's own language on equity and community health.** Federal policy shifted in 2025 [VERIFY].
- **Outcome claims get scrutinized:**
  - Expect questions on regression to the mean, comparison groups, and cost avoidance vs. cash savings.
  - Use matched comparisons and "contributed to" language (see `business-case-and-proposal`).
- **Marketing and communication rules** (HIPAA marketing, testimonials, pixels, FDA claims, accessibility, Section 1557): `customer-facing-quality-gate/references/industry-rules/healthcare-marketing.md`.
