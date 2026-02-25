---
name: claim-denial-root-cause
description: Analyze claim denial reasons using CARC/RARC codes, payer-specific rules, and billing data to identify root causes and recommend corrective actions. Use when investigating claim denials, building denial trend reports, preparing appeal strategies, or implementing denial prevention programs.

metadata:
  display_name: "Claim Denial Root Cause"
  short_description: "Analyze root causes of healthcare claim denials by payer"
  default_prompt: "Analyze my claim denial root cause and recommend clear next actions"
  version: "1.0.0"
  tags:
    - healthcare
  icon_path: "assets/icon.png"
---

# Claim Denial Root Cause Analysis

## Overview

Systematically analyze healthcare claim denials by decoding CARC (Claim Adjustment Reason Codes) and RARC (Remittance Advice Remark Codes), mapping to root causes across clinical documentation, coding, eligibility, authorization, and billing processes. This skill supports denial management teams in understanding why claims are denied, identifying systemic patterns, and implementing targeted corrective actions to improve clean claim rates and reduce revenue leakage.

## When to Use

- Investigating individual claim denials for appeal preparation
- Analyzing denial trends across payers, departments, or service lines
- Identifying systemic root causes driving denial volumes
- Building denial prevention workflows and front-end edits
- Benchmarking denial rates against industry standards
- Preparing denial management performance reports

## Required Inputs

| Input | Description | Format |
|-------|-------------|--------|
| Denial remittance data | CARC/RARC codes, denied amount, claim details | 835/ERA data or structured object |
| Original claim | CPT/HCPCS, ICD-10, modifiers, place of service | 837/claim object |
| Payer information | Payer name, plan type, contract terms | Structured object |
| Clinical documentation | Supporting notes, orders, authorizations | Document references |
| Historical denials | Prior denial data for trend analysis | Array with dates |

## Methodology

### Step 1: Denial Code Interpretation

Decode the CARC and RARC codes from the remittance:

**Common CARC Code Categories:**

| CARC Range | Category | Examples |
|-----------|----------|---------|
| 1-3 | Deductible/Coinsurance/Copay | Patient responsibility, not a true denial |
| 4-5 | Procedure inconsistency | Modifier missing, procedure conflicts with diagnosis |
| 16-18 | Information/Authorization | Missing information, lack of prior auth |
| 22 | Coordination of benefits | Duplicate or secondary payer issue |
| 26-27 | Expenses/Bundling | Not covered, included in another procedure |
| 29 | Time limit | Filing deadline exceeded |
| 31-32 | Patient eligibility | Not covered by plan at time of service |
| 50 | Medical necessity | Service not medically necessary per payer criteria |
| 96-97 | Non-covered service | Service excluded from plan benefits |
| 197 | Precertification/Authorization | Required auth not obtained |
| 204 | Service not payable | Per plan provisions |
| 252 | Bundling/CCI edits | Service bundled per NCCI edits |

**RARC Codes** provide additional context:
- N-series: General information (N30 = missing documentation)
- M-series: Medical policy (M79 = not medically necessary)
- MA-series: Medicare alerts
- N-series: Informational notifications

### Step 2: Root Cause Classification

Map each denial to one of six root cause categories:

**1. Registration/Eligibility (Front-End)**
- Patient not eligible at date of service
- Wrong payer on file, coordination of benefits errors
- Missing or invalid demographics/subscriber information
- Root: Verification process failure

**2. Authorization/Precertification**
- Prior auth not obtained or expired
- Auth obtained for different service or provider
- Retro-auth not requested within deadline
- Root: Authorization workflow gaps

**3. Coding/Billing**
- Incorrect CPT/ICD-10 codes, missing modifiers
- Unbundling violations (NCCI edits)
- Incorrect place of service or type of bill
- Root: Coder education or system edit gaps

**4. Clinical Documentation**
- Insufficient documentation of medical necessity
- Missing signature, date, or required elements
- Documentation does not support the billed code
- Root: CDI program gaps

**5. Contractual/Payer Rules**
- Service not covered under plan
- Non-participating provider
- Fee schedule disputes
- Root: Contract knowledge gaps or payer policy changes

**6. Timely Filing**
- Claim submitted after filing deadline
- Corrected claim not filed within appeal window
- Root: Billing workflow delays

### Step 3: Impact Analysis

Quantify the financial and operational impact:

- **Denied amount**: Total dollars at risk
- **Recovery probability**: Likelihood of successful appeal (by denial category)
- **Cost to appeal**: Staff time and resources required
- **Net recovery value**: Denied amount minus appeal cost times recovery probability
- **Denial rate**: Denied claims divided by total claims (benchmark: under 5% is good, under 2% is excellent)

### Step 4: Trend Analysis

When historical data is available, identify patterns:

- **Payer-specific trends**: Which payers deny most, and for what reasons?
- **Service line trends**: Which departments or procedure types have highest denial rates?
- **CARC code trends**: Which denial reasons are increasing/decreasing?
- **Seasonal patterns**: Month-end, year-end, or contract renewal effects
- **Staff patterns**: Specific registration, coding, or billing staff associated with higher denial rates

### Step 5: Corrective Action Plan

Generate targeted corrective actions:

**Prevention Strategies by Root Cause:**

| Root Cause | Prevention Action | Expected Impact |
|-----------|-------------------|-----------------|
| Eligibility | Real-time eligibility verification at registration | Reduce eligibility denials by 60-80% |
| Authorization | Automated auth tracking with expiration alerts | Reduce auth denials by 50-70% |
| Coding | Pre-bill coding audits, NCCI edit checks | Reduce coding denials by 40-60% |
| Documentation | CDI concurrent review, query templates | Reduce medical necessity denials by 30-50% |
| Timely filing | Automated claim submission within 48 hours of coding | Eliminate timely filing denials |
| Contractual | Contract loading in claims system, payer rule updates | Reduce contractual denials by 40% |

## Output Specification

The output includes:

**denial_analysis**: claim_id, date_of_service, billed_amount, denied_amount, carc_codes with descriptions, rarc_codes with descriptions, denial_category

**root_cause**: primary_root_cause, secondary_contributors, specific_failure_point, evidence

**impact_assessment**: denied_amount, recovery_probability, estimated_appeal_cost, net_recovery_value, appeal_recommended (yes/no with rationale)

**appeal_strategy** (if recommended): appeal_type (reconsideration/formal/external), required_documentation, key_arguments, deadline, success_probability

**trend_analysis** (if historical data provided): denial_rate_trend, top_carc_codes by volume and dollars, payer_comparison, service_line_comparison

**corrective_actions**: action, target_root_cause, responsible_team, timeline, expected_denial_reduction, implementation_steps

## Analysis Framework

### Denial Rate Benchmarking

| Metric | Excellent | Good | Needs Improvement | Critical |
|--------|-----------|------|-------------------|----------|
| Initial denial rate | Under 2% | 2-5% | 5-10% | Over 10% |
| Appeal success rate | Over 70% | 50-70% | 30-50% | Under 30% |
| Days to appeal | Under 15 | 15-30 | 30-45 | Over 45 |
| Write-off rate | Under 1% | 1-3% | 3-5% | Over 5% |
| Clean claim rate | Over 98% | 95-98% | 90-95% | Under 90% |

### Appeal Priority Matrix

Prioritize appeals by net recovery value:

- **Priority 1**: High dollar amount and high recovery probability (appeal immediately)
- **Priority 2**: High dollar amount, moderate recovery probability (appeal with strong documentation)
- **Priority 3**: Moderate dollar amount, high recovery probability (batch appeals)
- **Priority 4**: Low dollar amount or low recovery probability (evaluate cost-effectiveness)

## Examples

**Input**: Claim denied for outpatient knee MRI. CARC 197 (precertification/authorization required), RARC N517 (authorization not on file). Billed amount: $1,850. Auth was obtained but under a different procedure code (73721 vs 73723).

**Root Cause Analysis**:
- Primary root cause: Authorization/Precertification — auth obtained for CPT 73721 (MRI knee without contrast) but service performed was CPT 73723 (MRI knee with and without contrast)
- Failure point: Auth request did not match the subsequently ordered procedure
- Recovery probability: HIGH (85%) — auth was obtained; procedure code mismatch is correctable
- Appeal strategy: Submit corrected auth or request retro-auth for 73723; include clinical documentation justifying contrast administration
- Corrective action: Implement auth-to-order reconciliation check before service is performed

## Guidelines

1. **Decode all CARC/RARC codes** — do not rely on payer-provided denial reason text alone
2. **Distinguish true denials from patient responsibility** — CARC 1/2/3 are cost-sharing, not denials
3. **Appeal every viable denial** — many denials are overturned on appeal with proper documentation
4. **Track denial write-offs** — unworked or written-off denials represent permanent revenue loss
5. **Feed findings back to prevention** — every denial analyzed should inform upstream process improvement

## Validation Checklist

- [ ] CARC and RARC codes are correctly decoded and mapped to root causes
- [ ] Root cause classification uses the six-category framework consistently
- [ ] Financial impact is calculated including appeal cost-effectiveness
- [ ] Appeal strategy includes specific documentation requirements and deadlines
- [ ] Trend analysis covers payer, service line, and temporal dimensions
- [ ] Corrective actions target root causes (not symptoms) with measurable expected impact
- [ ] Denial rate is benchmarked against industry standards

## HIPAA Compliance Notes

- Denial management involves PHI (patient names, dates of service, diagnoses, procedures)
- Remittance data (835 transactions) must be stored and transmitted securely
- Appeal correspondence containing clinical information must be encrypted
- Staff accessing denial data must have appropriate authorization and training
- De-identify denial trend data used for operational reporting when possible
- Maintain audit trails for all denial investigation and appeal activities
