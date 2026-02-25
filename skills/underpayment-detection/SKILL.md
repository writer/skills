---
name: underpayment-detection
description: Identify payer underpayments by comparing actual reimbursements against contracted rates, fee schedules, and expected payment calculations. Use when auditing payer payments, validating ERA/835 remittances, identifying payment variances, or supporting contract compliance monitoring.

metadata:
  display_name: "Underpayment Detection"
  short_description: "Detect payer underpayments versus contracted rate schedules"
  default_prompt: "Review my detect payer underpayments versus contracted rate and highlight top risks and next actions"
  version: "1.0.0"
  tags:
    - healthcare
  icon_path: "assets/icon.png"
---

# Underpayment Detection

## Overview

Systematically identify instances where payers have reimbursed healthcare claims below contracted rates or expected payment amounts. This skill compares actual payments against fee schedules, contract terms, Medicare/Medicaid rates, and expected payment calculations to surface underpayments, incorrect adjustments, and contractual non-compliance — recovering revenue that would otherwise be lost.

## When to Use

- Auditing payer remittances (835/ERA) against contracted rates
- Identifying systemic underpayment patterns by payer or service line
- Validating payment accuracy for high-dollar claims
- Supporting payer contract negotiations with payment variance data
- Performing retrospective payment audits for revenue recovery
- Monitoring contract compliance across payer portfolio

## Required Inputs

| Input | Description | Format |
|-------|-------------|--------|
| Remittance data | 835/ERA with payment amounts and adjustment codes | Structured transaction data |
| Contracted rates | Fee schedule or contract terms by CPT/payer | Rate table |
| Claim details | Billed CPT/HCPCS, units, modifiers, billed amount | Claim object |
| Payer contract | Contract terms including reimbursement methodology | Contract summary |
| Medicare fee schedule | CMS MPFS or OPPS rates for benchmarking | Rate table |

## Methodology

### Step 1: Expected Payment Calculation

Calculate the expected payment for each claim line:

**Reimbursement Methodologies:**

| Methodology | Calculation | Common Payers |
|-------------|-------------|---------------|
| Fee schedule | Contracted rate per CPT code | Most commercial |
| Percent of Medicare | Medicare rate times contracted percentage (e.g., 120% of Medicare) | Many commercial |
| Percent of billed | Billed charges times contracted percentage | Some commercial |
| DRG-based | MS-DRG weight times base rate (inpatient) | All payers (inpatient) |
| APC-based | APC relative weight times conversion factor (outpatient) | Medicare OPPS |
| Case rate | Flat rate per case/episode | Bundled payment contracts |
| Per diem | Daily rate times LOS | Some inpatient contracts |
| Capitation | Fixed PMPM regardless of services | Capitated contracts |

**Key Calculation Factors:**
- Multiple procedure payment reduction (MPPR) for applicable services
- Bilateral procedure adjustment (modifier 50)
- Assistant surgeon reduction (modifier 80/82)
- Sequestration reduction (Medicare: currently 2%)
- Timely filing discount (if applicable per contract)
- Out-of-network rate methodology

### Step 2: Payment Variance Analysis

Compare expected vs. actual payment for each claim line:

**Variance Classification:**
- UNDERPAID: Actual payment is less than expected (beyond acceptable tolerance, typically 1-2%)
- CORRECTLY PAID: Payment matches expected within tolerance
- OVERPAID: Actual payment exceeds expected (flag for compliance, do not retain knowingly)
- ZERO PAID: No payment made (may be denial, not underpayment)
- PARTIALLY PAID: Some lines paid, others denied or reduced

**Variance Calculation:**
- Dollar variance = Expected payment - Actual payment
- Percentage variance = (Expected - Actual) / Expected times 100
- Material threshold: Flag variances exceeding tolerance (e.g., greater than $25 or greater than 2%)

### Step 3: Root Cause Classification

Identify why the underpayment occurred:

**Common Underpayment Causes:**

| Cause | Description | Recovery Approach |
|-------|-------------|-------------------|
| Wrong fee schedule applied | Payer used outdated or incorrect rate | Appeal with contract reference |
| Incorrect procedure grouping | Payer bundled services incorrectly | Appeal with unbundling justification |
| Missing contract escalator | Annual rate increase not applied | Appeal with contract amendment |
| Incorrect modifier processing | Modifier reduction applied incorrectly | Appeal with modifier rationale |
| Wrong reimbursement methodology | Percent-of-Medicare calculated wrong | Appeal with rate recalculation |
| Coordination of benefits error | Primary/secondary payment split incorrect | Resubmit with correct COB |
| Sequestration overapplied | Reduction applied when it should not be | Appeal with exemption evidence |
| Patient responsibility miscalculated | Deductible/coinsurance applied incorrectly | Appeal with benefit verification |

### Step 4: Recovery Prioritization

Prioritize underpayments for recovery action:

**Priority Matrix:**
- Tier 1 (Immediate): Large dollar variance, clear contract violation, within appeal deadline
- Tier 2 (High): Moderate dollar variance, strong recovery evidence, approaching deadline
- Tier 3 (Batch): Small dollar variance but high volume (systemic issue), batch appeal
- Tier 4 (Monitor): Borderline variances, track for pattern confirmation

**Recovery ROI Calculation:**
- Potential recovery = Sum of identified underpayments
- Recovery cost = Staff time for appeals and follow-up
- Expected recovery rate = Historical success rate by payer and cause
- Net recovery = Potential times expected rate minus recovery cost

### Step 5: Reporting and Trending

Generate comprehensive underpayment reports:

**Report Dimensions:**
- By payer: Which payers have the highest underpayment rates?
- By CPT/service line: Which services are most frequently underpaid?
- By cause: What are the primary drivers of underpayments?
- By time period: Are underpayments increasing or decreasing?
- By contract: Which contracts have the most payment variances?

## Output Specification

The output includes:

**underpayment_summary**: total_claims_analyzed, underpaid_count, total_underpayment_amount, average_variance_percent, underpayment_rate

**underpaid_claims**: claim_id, date_of_service, cpt_code, billed_amount, expected_payment, actual_payment, variance_amount, variance_percent, root_cause, recovery_priority, appeal_deadline

**systemic_patterns**: pattern_description, affected_claims_count, total_variance, root_cause, payer, service_line, recommended_action

**recovery_plan**: prioritized actions with underpayment_target, recovery_amount, appeal_type, required_documentation, expected_success_rate, deadline

**payer_scorecard**: by payer — total claims, underpayment rate, average variance, top underpayment causes, contract compliance score

**trending**: underpayment trends over time by payer, cause, and service line

## Analysis Framework

### Underpayment Benchmarks

| Metric | Target | Warning | Critical |
|--------|--------|---------|----------|
| Underpayment rate (by volume) | Under 3% | 3-8% | Over 8% |
| Underpayment rate (by dollars) | Under 2% | 2-5% | Over 5% |
| Recovery rate | Over 70% | 50-70% | Under 50% |
| Days to recover | Under 45 | 45-90 | Over 90 |
| Appeal success rate | Over 65% | 40-65% | Under 40% |

### Contract Compliance Monitoring

Track payment accuracy by contract provision:
- Base rate accuracy
- Annual escalator application
- Carve-out/exclusion compliance
- Stop-loss/outlier payment triggers
- Multi-procedure reduction accuracy
- Modifier payment adjustments

## Examples

**Input**: Orthopedic surgery claim. CPT 27447 (total knee arthroplasty). Contract: 140% of Medicare. Medicare rate: $1,542.38. Expected payment: $2,159.33. Actual payment: $1,695.00. CARC 45 (charges exceed contracted amount).

**Analysis**:
- Expected: $1,542.38 times 140% = $2,159.33
- Actual: $1,695.00
- Variance: $464.33 underpaid (21.5%)
- Root cause: Payer appears to have applied 110% of Medicare instead of 140%
- Recovery priority: Tier 1 (large dollar, clear contract violation)
- Appeal strategy: Submit with contract page showing 140% of Medicare methodology, Medicare fee schedule showing base rate, and calculation showing correct expected payment

## Guidelines

1. **Maintain current contract terms** — load and update fee schedules when contracts are renewed
2. **Set appropriate tolerance thresholds** — minor rounding differences are not actionable
3. **Focus on systemic patterns** — one-off variances matter less than recurring underpayment patterns
4. **Track appeal deadlines** — most payers have 90-180 day appeal windows for payment disputes
5. **Document everything** — maintain detailed records of underpayment identification, appeals, and outcomes

## Validation Checklist

- [ ] Expected payment calculation uses current contracted rates
- [ ] Medicare fee schedule rates are current (updated annually, sometimes quarterly)
- [ ] Variance calculations account for legitimate adjustments (deductible, coinsurance, sequestration)
- [ ] Root causes are correctly classified (not all variances are underpayments)
- [ ] Recovery prioritization accounts for appeal deadlines and dollar thresholds
- [ ] Systemic patterns are identified across multiple claims
- [ ] Payer scorecard provides actionable contract compliance insights

## HIPAA Compliance Notes

- Payment data (835 transactions) contains PHI and must be secured appropriately
- Underpayment analysis shared with external consultants requires BAA
- Payment dispute correspondence may contain clinical information subject to minimum necessary
- De-identify underpayment trend data used for operational reporting when feasible
- Maintain audit trails for all payment review and appeal activities
- Overpayment identification triggers reporting obligations under the 60-day rule (ACA Section 6402)
