---
name: payment-failure-diagnosis
description: Diagnose and explain payment processing failures across ACH, wire transfer, check, and real-time payment rails. Use when investigating rejected, returned, or delayed payments, analyzing payment exception patterns, or troubleshooting payment processing system issues in banking operations.

metadata:
  display_name: "Payment Failure Diagnosis"
  short_description: "Diagnose payment processing failures across all payment rails"
  default_prompt: "Analyze my payment failure diagnosis and recommend clear next actions"
  version: "1.0.0"
  tags:
    - financial-services
  icon_path: "assets/icon.png"
---

# Payment Failure Diagnosis

## Overview

This skill produces structured diagnostic analyses of payment processing failures across all major payment rails. It covers ACH (NACHA), Fedwire, SWIFT, CHIPS, check clearing (Check 21), real-time payments (RTP/FedNow), and card networks. Diagnoses identify the failure point, root cause, applicable return/reject codes, regulatory implications, and corrective actions. Output supports operations teams, customer communication, and regulatory compliance.

## When to Use

- Investigating why a specific payment was rejected, returned, or delayed
- Diagnosing patterns of payment failures in operations exception queues
- Explaining payment processing errors to customers or relationship managers
- Troubleshooting payment system connectivity or processing issues
- Analyzing payment return rates for compliance with NACHA thresholds
- Supporting Reg E error resolution for electronic payment disputes
- Preparing root cause analysis for material payment processing incidents

## Required Inputs

| Input | Description | Format |
|-------|-------------|--------|
| Payment details | Amount, date, parties, payment type, reference | Payment record |
| Error/return code | NACHA return reason code, Fedwire reject code, SWIFT error | System output |
| Processing timeline | Timestamps from initiation to failure point | Audit trail |
| Account status | Originator and receiver account status and balances | Account data |
| System logs | Application and middleware processing logs | Technical logs |
| Routing information | ABA routing numbers, SWIFT BICs, account numbers | Payment instructions |
| Compliance screening | OFAC, fraud screening results | Screening output |

## Methodology

### Step 1: Identify the Payment Rail and Failure Type

Classify the payment and failure:

| Rail | Settlement | Common Failure Types |
|------|-----------|---------------------|
| **ACH (NACHA)** | T+1 (standard), T+0 (same-day) | Returns (R01-R85), NOCs, rejects |
| **Fedwire** | Real-time, final | Rejects (format, routing, OFAC hold) |
| **SWIFT** | Varies by correspondent | NAK, MT199 inquiry, compliance hold |
| **CHIPS** | End-of-day net settlement | Release failures, queue management |
| **Check 21/Image** | T+1 (local), T+2 (non-local) | Return unpaid, duplicate presentment |
| **RTP (TCH)** | Real-time, final | Reject (timeout, account, limit) |
| **FedNow** | Real-time, final | Reject (routing, account, OFAC) |
| **Card (Visa/MC)** | T+1 to T+3 | Decline, chargeback, reversal |

### Step 2: Decode the Error/Return Code

Interpret the specific failure code:

**ACH Return Reason Codes (most common)**:

| Code | Meaning | Root Cause Category |
|------|---------|-------------------|
| R01 | Insufficient funds | Account balance |
| R02 | Account closed | Account status |
| R03 | No account/unable to locate | Routing/account error |
| R04 | Invalid account number | Data quality |
| R05 | Unauthorized debit (consumer) | Authorization dispute |
| R06 | ODFI requested return | Originator recall |
| R07 | Authorization revoked | Customer action |
| R08 | Payment stopped | Stop payment |
| R10 | Customer advises not authorized | Reg E dispute |
| R16 | Account frozen | Legal/compliance |
| R20 | Non-transaction account | Account type mismatch |
| R29 | Corporate customer advises not authorized | Corporate dispute |

**Fedwire Reject Codes**:
- Format errors (invalid field content)
- Routing errors (invalid receiving ABA)
- OFAC holds (sanctions screening match)
- Business reason rejects (beneficiary bank rejection)

**SWIFT Error Categories**:
- NAK (negative acknowledgment): Message format failure
- MT199: Free-format inquiry from correspondent
- Compliance hold: Sanctions/AML screening at intermediary bank

### Step 3: Trace the Processing Path

Map the payment's journey and identify where it failed:

```
Originator → Originating Bank (ODFI) → [Fed/Clearing House] → Receiving Bank (RDFI) → Beneficiary
     ↓              ↓                        ↓                      ↓                    ↓
  Initiation    Validation &           Clearing &              Receipt &            Credit to
  & capture     OFAC screening         settlement              OFAC screening       account
```

For each node, verify:
- Was the payment received? (timestamp and confirmation)
- Were validation checks passed? (format, routing, compliance)
- Was the payment forwarded? (outbound confirmation)
- What was the elapsed time at each node? (latency analysis)

### Step 4: Diagnose the Root Cause

Apply diagnostic logic by failure category:

**Account-related failures (R01, R02, R03, R04, R16, R20)**:
- Verify account number and routing number accuracy
- Check account status (open, closed, frozen, restricted)
- Confirm account type supports the transaction type
- Verify available balance at time of debit (for R01)
- Check for recent account changes (closure, ownership change)

**Authorization-related failures (R05, R07, R08, R10, R29)**:
- Verify originator's authorization (agreement, mandate)
- Check for customer-initiated stop payments or revocations
- Assess whether Reg E rights are applicable (consumer accounts)
- Review originator's authorization retention and evidence

**Technical failures (format errors, timeouts, system rejects)**:
- Review message format against specification (NACHA, ISO 20022, SWIFT MT)
- Check field length, data type, and character set compliance
- Verify routing number validity against Federal Reserve E-Payments directory
- Assess system availability and processing capacity at time of failure
- Check for middleware or integration failures between systems

**Compliance-related failures (OFAC holds, fraud blocks)**:
- Review OFAC screening results and match details
- Determine if hold is a true match or false positive requiring release
- Check for fraud detection triggers requiring review
- Assess regulatory reporting requirements (blocking report, SAR)

### Step 5: Assess Regulatory and Financial Impact

Evaluate the consequences of the failure:

**NACHA compliance**:
- Overall return rate threshold: 15% (administrative + unauthorized)
- Unauthorized return rate threshold: 0.5%
- Exceeding thresholds may result in NACHA enforcement (fine, restricted origination)
- Monitor return rates by originator and SEC code

**Reg E implications** (consumer electronic fund transfers):
- R10 returns trigger Reg E error resolution obligations
- RDFI must accept returns within 60 days of settlement
- Consumer liability limits apply based on timing of notification

**Financial impact**:
- Return item fees assessed or absorbed
- Interest cost of delayed settlement
- Customer relationship impact and complaint risk
- Operational cost of manual exception handling

### Step 6: Prescribe Corrective Actions

Provide specific, actionable remediation:

**For the immediate failure**:
- Re-route or re-initiate the payment with corrected information
- Contact receiving institution for resolution (if routing/account issue)
- Release from compliance hold with documented disposition (if false positive)
- Communicate status and timeline to customer or originator

**For recurring patterns**:
- Implement pre-validation checks (account verification services, routing number validation)
- Enhance data quality controls at payment initiation
- Tune OFAC screening to reduce false positive rates
- Upgrade to current message format standards (ISO 20022)
- Implement real-time balance checks before debit origination

### Step 7: Document for Audit Trail

Record the complete diagnostic for operational and regulatory retention:
- Payment reference details (trace number, IMAD/OMAD, Fedwire reference)
- Complete timeline from initiation to failure to resolution
- Root cause classification and evidence
- Customer communication record
- Corrective actions taken with completion confirmation
- Regulatory filing requirements met (if applicable)

## Output Specification

```markdown
# Payment Failure Diagnosis: [Reference/Trace Number]

## Payment Details
- **Payment Type**: [ACH/Wire/Check/RTP]
- **Amount**: [$Amount]
- **Origination Date**: [Date]
- **Originator**: [Name, account, routing]
- **Beneficiary**: [Name, account, routing]
- **Status**: [Rejected/Returned/Delayed/Held]

## Failure Information
- **Error Code**: [Code]
- **Error Description**: [Description]
- **Failure Point**: [Where in the processing chain]
- **Failure Timestamp**: [Date/time]

## Diagnosis
### Root Cause
[Specific root cause with evidence]

### Root Cause Category
[Account / Authorization / Technical / Compliance]

### Processing Path Analysis
[Node-by-node trace showing where failure occurred]

## Impact Assessment
- **Customer Impact**: [Description]
- **Financial Impact**: [$Amount, fees, interest]
- **Regulatory Risk**: [Reg E, NACHA compliance, sanctions]

## Resolution
- **Immediate Action**: [What was done to resolve this specific failure]
- **Prevention**: [What changes prevent recurrence]
- **Customer Communication**: [What was communicated and when]

## Audit Trail
[Timestamps, reference numbers, and documentation for retention]
```

## Analysis Framework

### Return Rate Monitoring

Track NACHA return rates for compliance:

| Metric | Current Rate | Threshold | Status |
|--------|-------------|-----------|--------|
| Overall return rate (admin + unauthorized) | [X.X%] | 15.0% | [OK/Warning/Breach] |
| Unauthorized return rate | [X.X%] | 0.5% | [OK/Warning/Breach] |
| WEB debit return rate | [X.X%] | 15.0% | [OK/Warning/Breach] |

Set internal early warning at 50% of NACHA threshold.

### Payment Exception Trend Analysis

Identify patterns in payment failures:
- Failure rate by payment rail, originator, SEC code, and time period
- Top 10 return reason codes with volume trends
- Correlation between volume spikes and failure rates
- System availability impact on failure rates

### Same-Day ACH Performance

Monitor same-day ACH compliance:
- File submission by cutoff time (2:45 PM ET for current window)
- Processing window utilization
- Same-day vs. next-day return rates

## Examples

**Example 1 — ACH Return Diagnosis**:
"ACH credit (payroll) trace #0214XXXXXXXX, $3,247.82, originated 2025-10-01 by ABC Corp (ODFI: First National Bank) to employee account #XXXX5591 at Second State Bank, returned R03 (No Account/Unable to Locate) on 2025-10-02. Diagnosis: The employee's account was closed on 2025-09-28 due to the employee's voluntary account closure after opening an account at a competitor. The pre-notification (prenote) on file was validated in June 2024 and did not reflect the recent closure. Corrective action: (1) Notify ABC Corp payroll department of the return with updated information request (Wire Ops, same day); (2) Recommend ABC Corp implement account validation service (Accuity/Early Warning) for all payroll ACH origination to pre-validate accounts before origination; (3) Update prenote refresh cycle from annual to semi-annual for all payroll originators."

**Example 2 — Wire Transfer Compliance Hold**:
"Fedwire #20251015XXXXXXX, $425,000 outbound wire from customer account #XXXX2237 to intermediary bank (Deutsche Bank AG) for ultimate beneficiary 'Meridian Trading FZE' (Dubai, UAE). Wire held by OFAC screening at 10:47 AM ET. Match: Beneficiary name scored 82% against SDN entry 'Meridian Trade FZE' (SDN ID 34782, Iran-related). Diagnosis: The screening match is a near-name match. Due diligence reveals: (1) Customer's beneficiary is a UAE-incorporated electronics distributor established in 2012 with verifiable trade licenses; (2) SDN entity was added in 2019 and is associated with Iranian petrochemical transactions; (3) No matching identifiers (address, registration number, beneficial owners). Disposition: False positive — names are similar but entities are distinct. Wire released at 2:15 PM ET after BSA Officer approval. Total hold time: 3 hours 28 minutes. Customer notified of delay."

## Guidelines

- Always cite the specific return/reject code and its standard definition
- Trace the complete processing path before concluding root cause
- For OFAC holds, never release without documented false positive determination
- Monitor NACHA return rate thresholds and alert when approaching 50% of limit
- Reg E electronic fund transfers require strict adherence to error resolution timelines
- Preserve all diagnostic documentation for minimum 5 years (BSA recordkeeping)
- Communicate payment status to customers proactively; do not wait for inquiry
- Distinguish between sender-side and receiver-side failures in the diagnosis
- For recurring failures from the same originator, escalate to relationship management
- Document the complete audit trail including all timestamps and reference numbers

## Validation Checklist

- [ ] Payment rail and type are correctly identified
- [ ] Error/return code is decoded with standard definition
- [ ] Processing path is traced to the specific failure point
- [ ] Root cause is categorized (account, authorization, technical, compliance)
- [ ] Regulatory implications are assessed (Reg E, NACHA thresholds, OFAC)
- [ ] Financial impact is quantified (fees, interest, customer impact)
- [ ] Corrective action addresses both the immediate failure and recurrence prevention
- [ ] Customer communication is documented with timestamps
- [ ] Audit trail includes all reference numbers and processing timestamps
- [ ] Pattern analysis checks for systemic vs. isolated failure
