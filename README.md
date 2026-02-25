# Writer Enterprise Agent Skills Catalog

> **200 production-grade agent skills** across three enterprise verticals: CPG & Retail E-Commerce, Healthcare, and Financial Services & Banking.

---

## Catalog Summary

| Domain | Skills | Categories |
|--------|--------|------------|
| [CPG & Retail E-Commerce](#1-cpg--retail-e-commerce) | 67 | 7 |
| [Healthcare](#2-healthcare) | 67 | 7 |
| [Financial Services & Banking](#3-financial-services--banking) | 66 | 7 |
| **Total** | **200** | **21** |

---

## Skill Architecture

Each skill follows the Anthropic Agent Skills specification:

```
skill-name/
└── SKILL.md
    ├── YAML Frontmatter (name + description)
    └── Markdown Body
        ├── Overview
        ├── When to Use
        ├── Required Inputs
        ├── Methodology (5-7 step analytical framework)
        ├── Output Specification
        ├── Analysis Framework
        ├── Examples
        ├── Guidelines
        └── Validation Checklist
```

---

## 1. CPG & Retail E-Commerce

**67 skills** across 7 categories covering the full retail value chain.

### A. Commerce Intelligence & Merchandising (10 skills)

| Skill | Description |
|-------|-------------|
| [assortment-gap-analysis](cpg-retail/commerce-intelligence/assortment-gap-analysis/) | Identify missing SKUs vs market demand and competitors |
| [category-performance-diagnosis](cpg-retail/commerce-intelligence/category-performance-diagnosis/) | Explain category growth/decline drivers |
| [sku-rationalization-advisor](cpg-retail/commerce-intelligence/sku-rationalization-advisor/) | Recommend SKU add/remove decisions |
| [price-elasticity-estimator](cpg-retail/commerce-intelligence/price-elasticity-estimator/) | Predict demand sensitivity to price changes |
| [competitive-price-monitoring](cpg-retail/commerce-intelligence/competitive-price-monitoring/) | Track and summarize competitor pricing moves |
| [promotion-effectiveness-analysis](cpg-retail/commerce-intelligence/promotion-effectiveness-analysis/) | Measure uplift from discounts and promos |
| [seasonality-forecasting](cpg-retail/commerce-intelligence/seasonality-forecasting/) | Predict demand swings by seasonality patterns |
| [new-product-launch-readiness](cpg-retail/commerce-intelligence/new-product-launch-readiness/) | Assess launch risks and go-to-market gaps |
| [private-label-opportunity-finder](cpg-retail/commerce-intelligence/private-label-opportunity-finder/) | Identify profitable private-label gaps |
| [store-vs-online-mix-optimizer](cpg-retail/commerce-intelligence/store-vs-online-mix-optimizer/) | Recommend channel allocation strategies |

### B. Marketing & Growth (10 skills)

| Skill | Description |
|-------|-------------|
| [campaign-brief-generator](cpg-retail/marketing-growth/campaign-brief-generator/) | Create performance-driven campaign briefs |
| [ad-creative-variant-generator](cpg-retail/marketing-growth/ad-creative-variant-generator/) | Generate on-brand creative variations |
| [creative-fatigue-detector](cpg-retail/marketing-growth/creative-fatigue-detector/) | Identify declining ad performance patterns |
| [influencer-fit-scoring](cpg-retail/marketing-growth/influencer-fit-scoring/) | Score creators vs brand alignment |
| [customer-segmentation-builder](cpg-retail/marketing-growth/customer-segmentation-builder/) | Build actionable customer segments |
| [ltv-prediction](cpg-retail/marketing-growth/ltv-prediction/) | Predict customer lifetime value |
| [churn-risk-detection](cpg-retail/marketing-growth/churn-risk-detection/) | Flag customers likely to churn |
| [retention-playbook-generator](cpg-retail/marketing-growth/retention-playbook-generator/) | Generate retention strategies per segment |
| [cross-sell-opportunity-engine](cpg-retail/marketing-growth/cross-sell-opportunity-engine/) | Identify cross-sell pairings |
| [upsell-timing-optimizer](cpg-retail/marketing-growth/upsell-timing-optimizer/) | Recommend best upsell moments |

### C. Content & Brand (10 skills)

| Skill | Description |
|-------|-------------|
| [product-description-optimizer](cpg-retail/content-brand/product-description-optimizer/) | SEO + conversion optimized PDP copy |
| [brand-voice-enforcer](cpg-retail/content-brand/brand-voice-enforcer/) | Rewrite content to strict brand guidelines |
| [claims-compliance-checker](cpg-retail/content-brand/claims-compliance-checker/) | Validate regulated claims (CPG safe) |
| [ugc-moderation-assistant](cpg-retail/content-brand/ugc-moderation-assistant/) | Screen reviews and user content |
| [localization-cultural-adaptation](cpg-retail/content-brand/localization-cultural-adaptation/) | Market-specific content adaptation |
| [packaging-copy-validator](cpg-retail/content-brand/packaging-copy-validator/) | Validate legal + marketing copy on packaging |
| [sustainability-claims-validator](cpg-retail/content-brand/sustainability-claims-validator/) | Validate ESG claims accuracy |
| [retailer-content-customizer](cpg-retail/content-brand/retailer-content-customizer/) | Tailor content per retailer rules |
| [ab-test-hypothesis-generator](cpg-retail/content-brand/ab-test-hypothesis-generator/) | Generate testable A/B test hypotheses |
| [content-performance-explainer](cpg-retail/content-brand/content-performance-explainer/) | Explain why content is or isn't working |

### D. Operations & Supply Chain (10 skills)

| Skill | Description |
|-------|-------------|
| [demand-forecast-explanation](cpg-retail/operations-supply-chain/demand-forecast-explanation/) | Explain forecast drivers to planners |
| [inventory-risk-alerting](cpg-retail/operations-supply-chain/inventory-risk-alerting/) | Flag overstock / stockout risks |
| [replenishment-recommendation](cpg-retail/operations-supply-chain/replenishment-recommendation/) | Suggest reorder quantities |
| [supplier-risk-monitor](cpg-retail/operations-supply-chain/supplier-risk-monitor/) | Identify supplier reliability risks |
| [lead-time-variance-analyzer](cpg-retail/operations-supply-chain/lead-time-variance-analyzer/) | Diagnose supply delays |
| [logistics-cost-optimization](cpg-retail/operations-supply-chain/logistics-cost-optimization/) | Identify cost-saving opportunities |
| [returns-root-cause-analysis](cpg-retail/operations-supply-chain/returns-root-cause-analysis/) | Explain why returns are happening |
| [warehouse-slotting-optimizer](cpg-retail/operations-supply-chain/warehouse-slotting-optimizer/) | Recommend product placement in warehouse |
| [sell-through-velocity-tracker](cpg-retail/operations-supply-chain/sell-through-velocity-tracker/) | Track velocity vs benchmarks |
| [shrinkage-risk-detector](cpg-retail/operations-supply-chain/shrinkage-risk-detector/) | Flag theft/fraud risk patterns |

### E. Retail Ops & CX (10 skills)

| Skill | Description |
|-------|-------------|
| [store-performance-narratives](cpg-retail/retail-ops-cx/store-performance-narratives/) | Auto-generate store performance insights |
| [associate-enablement-coach](cpg-retail/retail-ops-cx/associate-enablement-coach/) | Generate store-level playbooks |
| [omnichannel-journey-mapper](cpg-retail/retail-ops-cx/omnichannel-journey-mapper/) | Map customer journeys across channels |
| [customer-complaint-root-cause](cpg-retail/retail-ops-cx/customer-complaint-root-cause/) | Identify systemic CX issues |
| [csat-driver-analysis](cpg-retail/retail-ops-cx/csat-driver-analysis/) | Explain CSAT changes |
| [nps-action-planner](cpg-retail/retail-ops-cx/nps-action-planner/) | Recommend actions from NPS data |
| [voice-of-customer-summarizer](cpg-retail/retail-ops-cx/voice-of-customer-summarizer/) | Summarize feedback at scale |
| [return-policy-optimization](cpg-retail/retail-ops-cx/return-policy-optimization/) | Recommend policy changes |
| [fraud-pattern-explanation](cpg-retail/retail-ops-cx/fraud-pattern-explanation/) | Explain transaction fraud signals |
| [checkout-drop-off-analyzer](cpg-retail/retail-ops-cx/checkout-drop-off-analyzer/) | Diagnose cart abandonment |

### F. Strategy & Exec (10 skills)

| Skill | Description |
|-------|-------------|
| [weekly-exec-commerce-brief](cpg-retail/strategy-exec/weekly-exec-commerce-brief/) | Auto-generated weekly executive brief |
| [board-ready-kpi-narratives](cpg-retail/strategy-exec/board-ready-kpi-narratives/) | Investor-safe KPI narratives |
| [market-expansion-readiness](cpg-retail/strategy-exec/market-expansion-readiness/) | New region viability analysis |
| [retailer-negotiation-prep](cpg-retail/strategy-exec/retailer-negotiation-prep/) | Prepare negotiation talking points |
| [trade-spend-roi-analyzer](cpg-retail/strategy-exec/trade-spend-roi-analyzer/) | Explain trade spend impact |
| [scenario-planning-engine](cpg-retail/strategy-exec/scenario-planning-engine/) | "What if" scenario modeling |
| [margin-decomposition](cpg-retail/strategy-exec/margin-decomposition/) | Explain margin erosion drivers |
| [pricing-strategy-simulator](cpg-retail/strategy-exec/pricing-strategy-simulator/) | Simulate pricing strategies |
| [channel-conflict-analyzer](cpg-retail/strategy-exec/channel-conflict-analyzer/) | Identify channel cannibalization |
| [growth-constraint-identifier](cpg-retail/strategy-exec/growth-constraint-identifier/) | Identify bottlenecks to scale |

### G. Compliance & Governance (7 skills)

| Skill | Description |
|-------|-------------|
| [advertising-compliance-checker](cpg-retail/compliance-governance/advertising-compliance-checker/) | Validate ad compliance (FTC, NAD) |
| [data-sharing-risk-review](cpg-retail/compliance-governance/data-sharing-risk-review/) | Review retailer data sharing risks |
| [contract-clause-analyzer](cpg-retail/compliance-governance/contract-clause-analyzer/) | Highlight risky contract clauses |
| [retailer-sla-compliance-monitor](cpg-retail/compliance-governance/retailer-sla-compliance-monitor/) | Track SLA adherence |
| [regulatory-change-impact](cpg-retail/compliance-governance/regulatory-change-impact/) | Explain regulation impact |
| [internal-policy-alignment-checker](cpg-retail/compliance-governance/internal-policy-alignment-checker/) | Ensure policy adherence |
| [audit-prep-assistant](cpg-retail/compliance-governance/audit-prep-assistant/) | Prepare audit-ready documentation |

---

## 2. Healthcare

**67 skills** across 7 categories covering the full care delivery and operations continuum.

### A. Clinical & Medical Ops (10 skills)

| Skill | Description |
|-------|-------------|
| [clinical-note-structuring](healthcare/clinical-medical-ops/clinical-note-structuring/) | Structure unstructured clinical notes |
| [care-pathway-summarization](healthcare/clinical-medical-ops/care-pathway-summarization/) | Summarize patient care journeys |
| [clinical-guideline-matching](healthcare/clinical-medical-ops/clinical-guideline-matching/) | Match cases to clinical guidelines |
| [utilization-review-assistant](healthcare/clinical-medical-ops/utilization-review-assistant/) | Support utilization review decisions |
| [readmission-risk-explanation](healthcare/clinical-medical-ops/readmission-risk-explanation/) | Explain readmission risk drivers |
| [care-gap-identification](healthcare/clinical-medical-ops/care-gap-identification/) | Identify missing care steps |
| [patient-stratification-engine](healthcare/clinical-medical-ops/patient-stratification-engine/) | Risk-stratify patient populations |
| [diagnostic-support-summaries](healthcare/clinical-medical-ops/diagnostic-support-summaries/) | Generate evidence-based diagnostic summaries |
| [lab-result-explanation](healthcare/clinical-medical-ops/lab-result-explanation/) | Explain lab results for clinicians |
| [clinical-workflow-optimization](healthcare/clinical-medical-ops/clinical-workflow-optimization/) | Identify clinical workflow inefficiencies |

### B. Revenue Cycle & Claims (10 skills)

| Skill | Description |
|-------|-------------|
| [claim-denial-root-cause](healthcare/revenue-cycle-claims/claim-denial-root-cause/) | Explain claim denial reasons |
| [prior-auth-readiness-checker](healthcare/revenue-cycle-claims/prior-auth-readiness-checker/) | Validate prior authorization completeness |
| [coding-accuracy-validator](healthcare/revenue-cycle-claims/coding-accuracy-validator/) | ICD/CPT code validation |
| [underpayment-detection](healthcare/revenue-cycle-claims/underpayment-detection/) | Identify payer underpayments |
| [appeal-letter-generator](healthcare/revenue-cycle-claims/appeal-letter-generator/) | Generate appeal letter drafts |
| [revenue-leakage-detection](healthcare/revenue-cycle-claims/revenue-leakage-detection/) | Identify lost revenue opportunities |
| [billing-compliance-checker](healthcare/revenue-cycle-claims/billing-compliance-checker/) | Ensure billing compliance |
| [payer-rule-interpretation](healthcare/revenue-cycle-claims/payer-rule-interpretation/) | Explain payer policies and coverage |
| [authorization-timeline-predictor](healthcare/revenue-cycle-claims/authorization-timeline-predictor/) | Predict authorization processing delays |
| [claim-complexity-scoring](healthcare/revenue-cycle-claims/claim-complexity-scoring/) | Score claim difficulty for prioritization |

### C. Patient Experience (10 skills)

| Skill | Description |
|-------|-------------|
| [patient-journey-mapping](healthcare/patient-experience/patient-journey-mapping/) | End-to-end patient journey mapping |
| [access-friction-detector](healthcare/patient-experience/access-friction-detector/) | Identify access barriers |
| [no-show-risk-predictor](healthcare/patient-experience/no-show-risk-predictor/) | Predict missed appointments |
| [patient-communication-simplifier](healthcare/patient-experience/patient-communication-simplifier/) | Plain-language medical explanations |
| [discharge-instruction-generator](healthcare/patient-experience/discharge-instruction-generator/) | Generate safe discharge summaries |
| [multilingual-patient-content](healthcare/patient-experience/multilingual-patient-content/) | Language-safe patient communications |
| [patient-feedback-analysis](healthcare/patient-experience/patient-feedback-analysis/) | Analyze patient complaints at scale |
| [sdoh-risk-identifier](healthcare/patient-experience/sdoh-risk-identifier/) | Identify social determinants of health risks |
| [care-navigation-assistant](healthcare/patient-experience/care-navigation-assistant/) | Guide patients through care processes |
| [health-literacy-adapter](healthcare/patient-experience/health-literacy-adapter/) | Adjust content to appropriate reading level |

### D. Provider Ops (10 skills)

| Skill | Description |
|-------|-------------|
| [clinician-burnout-signal-detection](healthcare/provider-ops/clinician-burnout-signal-detection/) | Identify clinician burnout risk signals |
| [provider-capacity-forecasting](healthcare/provider-ops/provider-capacity-forecasting/) | Predict provider capacity shortages |
| [schedule-optimization-advisor](healthcare/provider-ops/schedule-optimization-advisor/) | Optimize provider schedules |
| [referral-leakage-detection](healthcare/provider-ops/referral-leakage-detection/) | Identify referral network losses |
| [network-adequacy-analysis](healthcare/provider-ops/network-adequacy-analysis/) | Assess provider network coverage |
| [credentialing-status-monitor](healthcare/provider-ops/credentialing-status-monitor/) | Track credentialing status and risks |
| [clinical-documentation-quality](healthcare/provider-ops/clinical-documentation-quality/) | Assess documentation completeness |
| [peer-comparison-analytics](healthcare/provider-ops/peer-comparison-analytics/) | Compare provider performance metrics |
| [variation-of-care-analysis](healthcare/provider-ops/variation-of-care-analysis/) | Identify unwarranted care variation |
| [on-call-load-optimization](healthcare/provider-ops/on-call-load-optimization/) | Balance on-call schedules fairly |

### E. Compliance & Risk (10 skills)

| Skill | Description |
|-------|-------------|
| [hipaa-risk-review](healthcare/compliance-risk/hipaa-risk-review/) | Identify HIPAA privacy and security risks |
| [clinical-audit-prep](healthcare/compliance-risk/clinical-audit-prep/) | Prepare clinical audit summaries |
| [policy-adherence-monitoring](healthcare/compliance-risk/policy-adherence-monitoring/) | Track clinical guideline compliance |
| [incident-report-summarization](healthcare/compliance-risk/incident-report-summarization/) | Summarize patient safety events |
| [root-cause-analysis-generator](healthcare/compliance-risk/root-cause-analysis-generator/) | Generate RCA drafts for adverse events |
| [consent-documentation-validator](healthcare/compliance-risk/consent-documentation-validator/) | Validate informed consent records |
| [regulatory-change-interpreter](healthcare/compliance-risk/regulatory-change-interpreter/) | Explain healthcare regulation updates |
| [data-access-governance](healthcare/compliance-risk/data-access-governance/) | Enforce data access policies |
| [third-party-risk-review](healthcare/compliance-risk/third-party-risk-review/) | Vendor and BAA risk assessment |
| [quality-measure-alignment](healthcare/compliance-risk/quality-measure-alignment/) | Align to HEDIS/STAR/MIPS quality programs |

### F. Population Health (10 skills)

| Skill | Description |
|-------|-------------|
| [chronic-condition-cohorting](healthcare/population-health/chronic-condition-cohorting/) | Cohort and segment chronic disease patients |
| [preventive-care-gap-finder](healthcare/population-health/preventive-care-gap-finder/) | Identify missed preventive care |
| [risk-adjustment-support](healthcare/population-health/risk-adjustment-support/) | Support HCC/RAF accuracy |
| [population-trend-narratives](healthcare/population-health/population-trend-narratives/) | Explain population health trends |
| [care-program-effectiveness](healthcare/population-health/care-program-effectiveness/) | Measure intervention impact |
| [health-equity-monitoring](healthcare/population-health/health-equity-monitoring/) | Identify and track health disparities |
| [outcomes-attribution](healthcare/population-health/outcomes-attribution/) | Attribute outcomes to interventions |
| [cost-driver-decomposition](healthcare/population-health/cost-driver-decomposition/) | Explain healthcare cost growth drivers |
| [longitudinal-patient-summaries](healthcare/population-health/longitudinal-patient-summaries/) | Generate timeline-based patient summaries |
| [clinical-program-roi-analysis](healthcare/population-health/clinical-program-roi-analysis/) | Calculate ROI of clinical programs |

### G. Executive & Strategy (7 skills)

| Skill | Description |
|-------|-------------|
| [board-ready-clinical-insights](healthcare/executive-strategy/board-ready-clinical-insights/) | Executive-safe clinical summaries |
| [value-based-care-readiness](healthcare/executive-strategy/value-based-care-readiness/) | Assess VBC contract readiness |
| [service-line-profitability](healthcare/executive-strategy/service-line-profitability/) | Profitability analysis by service line |
| [market-expansion-analysis](healthcare/executive-strategy/market-expansion-analysis/) | New facility viability analysis |
| [ma-clinical-diligence](healthcare/executive-strategy/ma-clinical-diligence/) | Clinical due diligence for M&A |
| [strategic-initiative-tracking](healthcare/executive-strategy/strategic-initiative-tracking/) | Track strategic initiative progress |
| [operational-kpi-narratives](healthcare/executive-strategy/operational-kpi-narratives/) | Generate KPI explanations for leadership |

---

## 3. Financial Services & Banking

**66 skills** across 7 categories covering risk, operations, and growth.

### A. Risk & Compliance (10 skills)

| Skill | Description |
|-------|-------------|
| [credit-risk-explanation](financial-services/risk-compliance/credit-risk-explanation/) | Explain credit risk drivers and scoring |
| [transaction-monitoring-summaries](financial-services/risk-compliance/transaction-monitoring-summaries/) | AML transaction monitoring explanations |
| [fraud-pattern-interpretation](financial-services/risk-compliance/fraud-pattern-interpretation/) | Explain fraud detection signals |
| [kyc-completeness-validator](financial-services/risk-compliance/kyc-completeness-validator/) | Validate KYC/CDD documentation |
| [regulatory-change-impact](financial-services/risk-compliance/regulatory-change-impact/) | Explain regulatory rule change impact |
| [model-risk-documentation](financial-services/risk-compliance/model-risk-documentation/) | Document model decisions (SR 11-7) |
| [sanctions-screening-review](financial-services/risk-compliance/sanctions-screening-review/) | Sanctions screening explanations |
| [operational-risk-narratives](financial-services/risk-compliance/operational-risk-narratives/) | Loss event and OpRisk analysis |
| [stress-test-scenario-narratives](financial-services/risk-compliance/stress-test-scenario-narratives/) | Explain stress test scenarios |
| [audit-response-drafting](financial-services/risk-compliance/audit-response-drafting/) | Draft regulator-ready audit responses |

### B. Banking Ops (10 skills)

| Skill | Description |
|-------|-------------|
| [account-lifecycle-summaries](financial-services/banking-ops/account-lifecycle-summaries/) | Full account history narratives |
| [customer-issue-root-cause](financial-services/banking-ops/customer-issue-root-cause/) | Banking complaint root cause analysis |
| [operational-sla-monitoring](financial-services/banking-ops/operational-sla-monitoring/) | SLA tracking and explanation |
| [payment-failure-diagnosis](financial-services/banking-ops/payment-failure-diagnosis/) | Diagnose payment processing failures |
| [exception-queue-prioritization](financial-services/banking-ops/exception-queue-prioritization/) | Prioritize operations exception queues |
| [process-bottleneck-detection](financial-services/banking-ops/process-bottleneck-detection/) | Identify operational bottlenecks |
| [branch-performance-analysis](financial-services/banking-ops/branch-performance-analysis/) | Branch-level performance insights |
| [digital-channel-migration-analysis](financial-services/banking-ops/digital-channel-migration-analysis/) | Analyze channel shift patterns |
| [cost-to-serve-decomposition](financial-services/banking-ops/cost-to-serve-decomposition/) | Decompose customer service costs |
| [ops-automation-opportunity-finder](financial-services/banking-ops/ops-automation-opportunity-finder/) | Identify automation opportunities |

### C. Lending & Credit (10 skills)

| Skill | Description |
|-------|-------------|
| [loan-application-explanation](financial-services/lending-credit/loan-application-explanation/) | Explain loan approval/denial decisions |
| [underwriting-consistency-checker](financial-services/lending-credit/underwriting-consistency-checker/) | Detect underwriting bias |
| [portfolio-risk-drift-detection](financial-services/lending-credit/portfolio-risk-drift-detection/) | Detect portfolio risk drift |
| [early-delinquency-predictor](financial-services/lending-credit/early-delinquency-predictor/) | Predict early-stage default risk |
| [collections-strategy-optimizer](financial-services/lending-credit/collections-strategy-optimizer/) | Optimize collections strategies |
| [credit-policy-interpretation](financial-services/lending-credit/credit-policy-interpretation/) | Explain credit policy rules |
| [loan-pricing-optimization](financial-services/lending-credit/loan-pricing-optimization/) | Risk-adjusted loan pricing guidance |
| [collateral-risk-summaries](financial-services/lending-credit/collateral-risk-summaries/) | Assess and summarize collateral risk |
| [credit-memo-generator](financial-services/lending-credit/credit-memo-generator/) | Generate investment-grade credit memos |
| [exposure-concentration-analysis](financial-services/lending-credit/exposure-concentration-analysis/) | Analyze portfolio concentration risks |

### D. Wealth & Advisory (10 skills)

| Skill | Description |
|-------|-------------|
| [client-profile-summarization](financial-services/wealth-advisory/client-profile-summarization/) | Generate holistic client summaries |
| [investment-policy-mapping](financial-services/wealth-advisory/investment-policy-mapping/) | Map portfolios to IPS targets |
| [portfolio-drift-explanation](financial-services/wealth-advisory/portfolio-drift-explanation/) | Explain portfolio drift from targets |
| [risk-tolerance-alignment](financial-services/wealth-advisory/risk-tolerance-alignment/) | Check suitability alignment |
| [advisor-prep-briefs](financial-services/wealth-advisory/advisor-prep-briefs/) | Generate meeting prep briefs |
| [market-event-impact-explainer](financial-services/wealth-advisory/market-event-impact-explainer/) | Explain market event portfolio impact |
| [client-communication-drafting](financial-services/wealth-advisory/client-communication-drafting/) | Draft regulation-safe client comms |
| [product-suitability-screening](financial-services/wealth-advisory/product-suitability-screening/) | Screen product suitability |
| [aum-growth-attribution](financial-services/wealth-advisory/aum-growth-attribution/) | Attribute AUM growth drivers |
| [client-attrition-risk](financial-services/wealth-advisory/client-attrition-risk/) | Predict client attrition risk |

### E. Treasury & Finance (8 skills)

| Skill | Description |
|-------|-------------|
| [liquidity-forecast-narratives](financial-services/treasury-finance/liquidity-forecast-narratives/) | Explain liquidity forecasts and positions |
| [interest-rate-sensitivity-analysis](financial-services/treasury-finance/interest-rate-sensitivity-analysis/) | Analyze interest rate risk impact |
| [alm-scenario-explanation](financial-services/treasury-finance/alm-scenario-explanation/) | Explain ALM scenarios and decisions |
| [funding-cost-decomposition](financial-services/treasury-finance/funding-cost-decomposition/) | Decompose funding cost drivers |
| [capital-adequacy-summaries](financial-services/treasury-finance/capital-adequacy-summaries/) | Summarize capital adequacy position |
| [stress-liquidity-narratives](financial-services/treasury-finance/stress-liquidity-narratives/) | Explain stress liquidity scenarios |
| [cash-flow-variance-analysis](financial-services/treasury-finance/cash-flow-variance-analysis/) | Explain cash flow variance drivers |
| [balance-sheet-optimization](financial-services/treasury-finance/balance-sheet-optimization/) | Generate balance sheet optimization insights |

### F. Strategy & Exec (8 skills)

| Skill | Description |
|-------|-------------|
| [weekly-bank-exec-brief](financial-services/strategy-exec/weekly-bank-exec-brief/) | Auto-generate weekly executive summaries |
| [board-risk-dashboards-narratives](financial-services/strategy-exec/board-risk-dashboards-narratives/) | Board-safe risk dashboard narratives |
| [ma-financial-diligence](financial-services/strategy-exec/ma-financial-diligence/) | M&A financial due diligence |
| [product-profitability-analysis](financial-services/strategy-exec/product-profitability-analysis/) | Product-level profitability analysis |
| [market-entry-feasibility](financial-services/strategy-exec/market-entry-feasibility/) | New market entry feasibility |
| [pricing-strategy-evaluation](financial-services/strategy-exec/pricing-strategy-evaluation/) | Evaluate pricing strategies |
| [customer-lifetime-value-banking](financial-services/strategy-exec/customer-lifetime-value-banking/) | Banking CLV models and analysis |
| [digital-transformation-readiness](financial-services/strategy-exec/digital-transformation-readiness/) | Assess digital transformation readiness |

### G. Governance & Controls (10 skills)

| Skill | Description |
|-------|-------------|
| [policy-exception-review](financial-services/governance-controls/policy-exception-review/) | Analyze policy exceptions for risk |
| [internal-control-effectiveness](financial-services/governance-controls/internal-control-effectiveness/) | Assess internal control effectiveness |
| [third-party-risk-summaries](financial-services/governance-controls/third-party-risk-summaries/) | Vendor/third-party risk assessment |
| [data-lineage-explanation](financial-services/governance-controls/data-lineage-explanation/) | Explain data traceability and lineage |
| [access-control-review](financial-services/governance-controls/access-control-review/) | Review access control and SoD risks |
| [operational-resilience-planning](financial-services/governance-controls/operational-resilience-planning/) | Operational resilience planning |
| [bcp-readiness-analysis](financial-services/governance-controls/bcp-readiness-analysis/) | Business continuity readiness |
| [incident-postmortem-generator](financial-services/governance-controls/incident-postmortem-generator/) | Generate incident postmortem reviews |
| [regulator-communication-drafting](financial-services/governance-controls/regulator-communication-drafting/) | Draft regulator-ready communications |
| [enterprise-risk-heatmap-narratives](financial-services/governance-controls/enterprise-risk-heatmap-narratives/) | Generate risk heatmap narratives |

---

## Key Frameworks Referenced

### CPG & Retail
- Nielsen/Circana syndicated data, GS1 standards, GTIN/UPC
- FTC Act, FDA 21 CFR 101, NAD Guidelines, FTC Green Guides (16 CFR 260)
- Price elasticity (log-log models), EOQ, safety stock, ABC-XYZ analysis
- RFM segmentation, cohort LTV, BG/NBD + Gamma-Gamma models

### Healthcare
- ICD-10-CM/PCS, CPT, HCPCS coding systems
- CMS-HCC v28, RAF scoring, HEDIS/STAR/MIPS quality measures
- HIPAA Privacy & Security Rules (45 CFR 164), Joint Commission standards
- LACE readmission scoring, Maslach Burnout Inventory, PRAPARE/AHC-HRSN SDoH screening
- VA NCPS Root Cause Analysis, AHRQ patient safety indicators

### Financial Services
- Basel III/IV (CET1, LCR, NSFR, SMA), CECL/IFRS 9
- BSA/AML (FinCEN), OFAC sanctions, Reg BI/Reg E/Reg B
- SR 11-7 model risk, CCAR/DFAST stress testing
- COSO 2013/ERM 2017, SOX 302/404, FFIEC examination handbooks
- Modern Portfolio Theory, Brinson attribution, FTP methodology

---

## License

These skills are provided for enterprise use. Each skill is self-contained and can be used independently or as part of a larger agent system.
