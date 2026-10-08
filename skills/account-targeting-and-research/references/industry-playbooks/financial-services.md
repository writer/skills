# Industry Playbook: Financial Services (Banks, Wealth, Insurance)

These are lenses for research and messaging, not facts about any account. Every account-specific value must come from that institution's own filings or conversations. Regulations change, so items marked **[VERIFY]** need a primary source before they reach a customer.

## Who buys, and what they're measured on

### Banks
| Role | Usually measured on |
|---|---|
| CEO / CFO | Net interest margin (NIM), efficiency ratio, pre-tax pre-provision income (PTPP), ROAA / ROTCE, fee-income mix, cost of deposits / deposit beta |
| COO / Head of Operations | Efficiency ratio (shared with CFO), cost-to-serve, straight-through processing, backlogs (KYC refresh, AML alert queues, loan documents) |
| CIO / CTO | Core modernization, cloud, vendor consolidation |
| Chief Data / AI Officer | Data quality, AI governance, use-case pipeline |
| CISO | Third-party cyber risk; NYDFS Part 500 (NY-licensed firms) |
| CRO / CCO | Exam findings, UDAAP and fair-lending exposure, model risk |
| Heads of Retail, Commercial, Digital | Acquisition, primacy, digital enrollment and active rate, digital account opening, abandonment |
| CMO | Content velocity through compliance review; personalization within fair-lending limits |

### Wealth management and broker-dealers
| Role | Usually measured on |
|---|---|
| Head of Wealth | Net new assets (NNA), organic growth, advisor recruiting and retention |
| Advisor experience / field enablement | Households per advisor, meeting prep time, CRM / custodian data fragmentation |
| CCO / supervision principals | Communications approval, archiving, off-channel communications |
| COO | Not-in-good-order (NIGO) rates, onboarding time |
| CMO | Advisor marketing and social media under FINRA 2210 and the SEC Marketing Rule |

### Insurers
| Role | Usually measured on |
|---|---|
| CFO | Combined, loss and expense ratios |
| Chief Underwriting Officer / Chief Actuary | Pricing; use of AI in underwriting under state AI bulletins |
| Head of Claims | Cycle time, leakage |
| Head of Distribution | Agent and broker productivity, quote-to-bind |
| CCO | State advertising rules, market-conduct exams |

## How they buy: the vendor due-diligence path
This is the main reason FS deals take long. Map it early, and start the work in parallel (see `enterprise-deal-strategy`, mutual action plan).

**Typical gates:**
1. **Business sponsor.**
2. **Architecture review.**
3. **InfoSec:**
   - a questionnaire such as SIG, SIG Lite or CAIQ
   - SOC 2 Type II
   - SOC 1 if the vendor touches financial reporting
   - a pen-test summary
   - ISO 27001 scope
4. **Third-party risk management (TPRM):** an inherent-risk questionnaire, then criticality tiering.
5. **Privacy:** GLBA, plus a GDPR DPA where it applies.
6. **Compliance review of the use case.**
7. **Model Risk Management**, for AI.
8. **AI governance committee.**
9. **BCP / DR.**
10. **Legal and procurement.**
11. **Senior management or board reporting**, for critical relationships.

**US third-party risk guidance (OCC Bulletin 2023-17 / Fed SR 23-4 / FDIC FIL-29-2023, June 2023),** still in effect. A September 2026 interagency proposal would replace it with more principles-based guidance [VERIFY whether finalized]:
- **Lifecycle:** planning → due diligence → contract → ongoing monitoring → termination.
- **Critical activities** get more rigorous oversight.
- **Contracts are expected to cover:**
  - performance measures
  - audit and regulator access rights
  - data ownership and return
  - subcontractors and fourth parties
  - business continuity
  - exit assistance
  - incident notification
- **Bank service provider incident notification:** under the 2021 rule, a bank service provider must notify the bank as soon as possible when an incident materially disrupts service for 4 or more hours. Expect this as a contract clause.

**Model risk.** Interagency guidance issued 17 April 2026 (Fed SR 26-2 and OCC/FDIC equivalents) replaced SR 11-7 / OCC 2011-12. The UK equivalent is PRA SS1/23. The new guidance is risk-based and proportionate, and it explicitly leaves generative and agentic AI out of scope, so banks apply their own AI-governance frameworks to GenAI tools [VERIFY any AI-specific guidance issued since]:
- **The bank must validate vendor models,** covering conceptual soundness, ongoing monitoring and outcomes analysis.
- **Vendors are expected to supply:** development and testing documentation, known limitations, monitoring, and change notification.
- **GenAI tools are increasingly put in the model or AI inventory.** Expect requests for:
  - accuracy and hallucination testing
  - bias testing
  - drift monitoring
  - human-in-the-loop design
  - evaluation evidence

**EU DORA (Regulation (EU) 2022/2554, applies from 17 January 2025):**
- **Mandatory ICT contract terms (Article 30),** stricter for critical or important functions:
  - audit and access rights
  - exit strategies
  - participation in threat-led penetration testing
  - subcontracting controls
- **Banks keep a register of information** on all ICT third-party arrangements.
- **The ESAs designated the first critical ICT third-party providers in November 2025**, including major cloud and enterprise-software firms. They come under direct EU oversight.

**UK:**
- PRA SS2/21 covers outsourcing and third-party risk.
- PRA SS1/21 and FCA PS21/3 cover operational resilience: important business services and impact tolerances.
- The critical third parties regime under FSMA 2023 is also in force. HM Treasury made the first designations in July 2026.

**Insurers and AI:**
- The NAIC Model Bulletin on insurers' use of AI (December 2023, adopted in many states) expects oversight of third-party AI vendors.
- NYDFS Insurance Circular Letter No. 7 (2024) covers AI in underwriting and pricing.

**Procurement timelines:**
- No reliable public benchmark exists, so treat them as Unknown. Ask how long their last comparable vendor onboarding took.
- **Plan around:**
  - fiscal-year budgeting
  - year-end change freezes (confirm per account)
  - earnings quiet periods
  - exam cycles

## Research sources (FS-specific)
- **US banks:**
  - Call Reports (FFIEC CDR), UBPR, FR Y-9C, FDIC BankFind
  - public OCC, Fed, FDIC and CFPB enforcement actions (for research only; don't quote them in outreach)
- **Wealth:**
  - Form ADV and Form CRS (IAPD) for advisers
  - BrokerCheck for broker-dealers
- **Insurers:** NAIC and state DOI filings, market-conduct exams.
- **UK:** FCA Register. **EU:** Pillar 3 disclosures.
- **Public companies:** 10-K risk factors and proxy compensation metrics show what leaders are paid to move.

## Vocabulary
- **Risk governance:** three lines of defense · effective challenge · inherent vs. residual risk · MRA / MRIA · consent order · BCBS 239.
- **Vendor and third-party risk:** critical activity · fourth party · concentration risk · exit plan · complementary user entity controls (CUECs).
- **Operational resilience:** important business service · impact tolerance.
- **Wealth and broker-dealer compliance:** Reg BI · Form CRS · principal pre-approval · lexicon review · books and records · off-channel communications · NIGO.

## Sensitivities
- **Confidential supervisory information is off-limits.** Never ask for or refer to it: exam findings, CAMELS ratings, unpublished MRAs. The bank is legally barred from sharing it.
- **Regulators don't approve vendors.** Never claim to be "SR 26-2 / model-risk-guidance compliant", "OCC/FINRA/SEC approved" or "DORA certified". Instead say: "we provide documentation to support your model validation / DORA Article 30 contract terms."
- **AI capability claims are an enforcement priority** (SEC "AI-washing" actions in 2024; FTC Operation AI Comply). Substantiate every AI claim.
- **Banks rarely allow publicity.** Check the proof library permission for every name.
- **Make content capturable for archiving.** Anything the agent drafts that an FS customer will send must be capturable under their recordkeeping rules: SEA Rule 17a-4 for broker-dealers, Advisers Act Rule 204-2 for advisers. FINRA treats GenAI-produced communications under its existing, technology-neutral rules.
- **Marketing rules for FS content:** see `customer-facing-quality-gate/references/industry-rules/financial-services-marketing.md`.
