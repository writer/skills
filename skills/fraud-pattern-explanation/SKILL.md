---
name: Fraud Pattern Explanation
description: Explain transaction fraud signals by analyzing payment, behavioral, and contextual patterns to produce human-readable explanations of why transactions are flagged, enabling faster review and better fraud rule calibration.

metadata:
  display_name: "Fraud Pattern Explanation"
  short_description: "Explain why transactions are flagged as potential fraud"
  default_prompt: "Explain my fraud pattern drivers in simple words and next steps"
  version: "1.0.0"
  tags:
    - cpg-retail
  icon_path: "assets/icon.png"
---

# Fraud Pattern Explanation

## Overview

This skill translates complex fraud detection signals into clear, human-readable explanations that fraud analysts, operations managers, and customer service teams can understand and act upon. It bridges the gap between black-box fraud scoring models and the human judgment required for manual review queues, chargeback disputes, and fraud rule optimization. For each flagged transaction, it produces a structured explanation of which signals triggered, why they are suspicious, and what the recommended action is.

## When to Use

- When fraud analysts need to review flagged transactions and require clear explanations of why each was flagged
- When tuning fraud detection rules and needing to understand false positive vs. true positive patterns
- When customer service agents need to explain holds or declines to legitimate customers
- During chargeback representment when documenting fraud evidence
- When reporting fraud trends to leadership and needing narrative context beyond statistics
- When training new fraud analysts on pattern recognition
- After fraud model updates to validate that new signals behave as expected

## Required Inputs

| Input | Description | Format |
|-------|-------------|--------|
| `flagged_transactions` | Transactions flagged by the fraud detection system with risk scores | Tabular |
| `fraud_signals` | Individual signals or features that contributed to the flag (from the scoring model) | Array per transaction |
| `customer_history` | Customer's transaction history, account age, prior fraud flags, device history | Object per customer |
| `order_details` | Items ordered, quantities, prices, shipping address, billing address | Object per transaction |
| `device_data` | Device fingerprint, IP geolocation, proxy/VPN detection, browser attributes | Object per transaction |
| `velocity_data` | Transaction frequency, amount patterns, address change recency | Object per customer |
| `fraud_rules` | Active rule set with descriptions and thresholds | Reference data |
| `historical_fraud` | Confirmed fraud cases for pattern matching | Tabular (optional) |
| `chargeback_data` | Chargeback history and reason codes | Tabular (optional) |

## Methodology

### Step 1 — Signal Decomposition

Break down the fraud flag into its component signals:

1. **Score Contribution Analysis**: For model-based fraud scoring, extract the top contributing features using SHAP values, feature importance, or logistic regression coefficients. Rank signals by their contribution to the overall risk score.
2. **Rule Trigger Identification**: For rule-based systems, identify which specific rules triggered and the parameter values that exceeded thresholds.
3. **Signal Categorization**: Group signals into intuitive categories:
   - **Payment Signals**: Card type mismatch, BIN country mismatch, velocity on payment instrument, multiple cards on single account.
   - **Identity Signals**: New account with high-value order, mismatched name variations, email pattern anomalies (random string emails), phone number inconsistencies.
   - **Behavioral Signals**: Unusual browsing pattern (skipped product pages, went directly to checkout), session duration anomalies, cart composition inconsistencies.
   - **Device/Network Signals**: Known fraudulent device fingerprint, proxy or VPN usage, geolocation mismatch with billing/shipping, emulator detection.
   - **Velocity Signals**: Multiple orders in short timeframe, rapid address changes, multiple shipping addresses, amount escalation pattern.
   - **Address Signals**: Billing and shipping address mismatch, freight forwarder address, P.O. box for high-value electronics, address previously associated with fraud.

### Step 2 — Contextual Enrichment

Add context that helps analysts assess signal severity:

1. **Baseline Comparison**: For each signal, provide the normal range for legitimate customers and this customer's position relative to it. Example: "Average time between account creation and first order is 14 days; this account placed a $1,200 order within 23 minutes of creation."
2. **Historical Pattern Matching**: Compare the flagged transaction's signal combination against confirmed fraud cases. Calculate the similarity score to known fraud patterns (e.g., "This signal combination matches 78% of confirmed account takeover cases from the past 6 months").
3. **False Positive Indicators**: Also highlight signals that suggest the transaction may be legitimate despite the flag — long customer tenure, prior successful orders, consistent device, shipping to previously used address.
4. **Risk Calibration**: Provide the historical true positive rate for transactions with similar risk scores. Example: "Transactions scoring 75-85 in our model have a historical true positive rate of 34%."

### Step 3 — Narrative Explanation Generation

Produce a human-readable explanation for each flagged transaction:

1. **Risk Summary**: One-sentence statement of the primary concern. Example: "This transaction exhibits strong account takeover indicators: new device, changed shipping address, and high-value electronics order inconsistent with purchase history."
2. **Signal-by-Signal Explanation**: For each contributing signal, explain:
   - What was detected (the factual observation).
   - Why it is suspicious (the fraud pattern it aligns with).
   - How unusual it is (statistical context).
3. **Mitigating Factors**: Any signals that reduce suspicion, clearly separated from the risk signals.
4. **Recommended Action**: Based on the signal combination and risk level:
   - **Auto-Decline**: Confidence is high, matches known fraud pattern with greater than 80% true positive rate.
   - **Manual Review**: Mixed signals require human judgment. Specify what additional verification to perform.
   - **Step-Up Authentication**: Moderate risk — trigger additional verification (SMS OTP, email confirmation, callback) before approving.
   - **Monitor**: Low risk but unusual — approve but flag for post-transaction monitoring.

### Step 4 — Pattern Aggregation

When analyzing multiple flagged transactions, identify patterns:

1. **Attack Vector Identification**: Group related flags into attack patterns. Example: "12 flagged transactions in the past 24 hours share a common device fingerprint and rotate through prepaid Visa cards, suggesting a single actor using a card testing bot."
2. **Fraud Ring Detection**: Identify shared attributes across flagged transactions that suggest coordinated fraud (shared devices, shipping addresses, BIN ranges, email patterns).
3. **Trend Analysis**: Track fraud flag volume, type distribution, and true positive rates over time. Identify emerging fraud vectors.
4. **Rule Performance Assessment**: For each active rule, calculate precision (true positives / total flags) and recall (true positives / total fraud). Recommend rule threshold adjustments where precision is low.

### Step 5 — Analyst Decision Support

Provide tools for the analyst to make and document decisions:

1. **Decision Checklist**: For manual review transactions, provide a checklist of verification steps:
   - Contact customer via phone on file (not phone provided with order).
   - Verify recent account changes with customer.
   - Check if shipping address is a known drop point or freight forwarder.
   - Review order contents against customer's purchase history.
2. **Evidence Documentation**: Structure the explanation for use in chargeback representment if the transaction is approved and later disputed.
3. **Feedback Loop**: Capture analyst decisions (approve, decline, escalate) and outcomes (was it fraud?) to improve model and rule calibration.

## Output Specification

Produce a fraud explanation report per transaction containing:

- `transaction_id`: Unique transaction identifier
- `risk_score`: Numeric risk score from the fraud model
- `risk_level`: Categorical risk assessment (low, medium, high, critical)
- `risk_summary`: One-sentence human-readable explanation of the primary concern
- `contributing_signals`: Array of signals, each with:
  - `signal_category`: Payment, Identity, Behavioral, Device/Network, Velocity, Address
  - `signal_name`: Specific signal identifier
  - `observation`: What was detected (factual)
  - `suspicion_rationale`: Why this is suspicious (pattern context)
  - `severity`: Impact on overall risk (low, medium, high)
  - `statistical_context`: How unusual this is relative to baseline
- `mitigating_factors`: Array of signals suggesting legitimacy
- `pattern_match`: Similarity to known fraud patterns with match percentage and pattern name
- `historical_tp_rate`: True positive rate for transactions with similar risk profile
- `recommended_action`: Auto-decline, manual review, step-up authentication, or monitor
- `verification_checklist`: Steps for manual review if applicable
- `evidence_package`: Structured evidence for chargeback representment

For aggregated pattern reports:

- `attack_vectors`: Identified coordinated attack patterns with shared attributes and affected transactions
- `fraud_ring_indicators`: Shared attributes suggesting coordinated fraud activity
- `rule_performance`: Precision and recall for each active rule with threshold adjustment recommendations
- `trend_summary`: Volume, type distribution, and true positive rate trends

## Analysis Framework

Apply the **Fraud Signal Triangle**:

Every fraud transaction exhibits signals across three dimensions. Strong fraud cases show signals in all three; ambiguous cases may only show one or two:

1. **Identity Anomaly**: Something is wrong with who is transacting — account is new, credentials were recently changed, identity elements are inconsistent.
2. **Behavioral Anomaly**: Something is wrong with how the transaction is being conducted — unusual speed, unusual product selection, unusual navigation pattern, unusual time of day.
3. **Contextual Anomaly**: Something is wrong with the transaction circumstances — device mismatch, geolocation mismatch, velocity spike, address risk.

When explaining a fraud flag, always assess all three dimensions and note which are present and which are absent. A transaction with all three dimensions flagged is high-confidence fraud. A transaction with only one dimension flagged is more likely a false positive.

## Examples

**Example Fraud Explanation**:

Transaction #TXN-98234. Risk score: 82/100. Risk level: High.

Risk Summary: This transaction exhibits strong account takeover indicators — the customer's shipping address was changed 2 hours before a high-value electronics order placed from an unrecognized device in a different geographic region.

Contributing Signals:
1. [Device/Network - HIGH] Transaction placed from a device never previously associated with this account. Prior 23 orders all from the same iPhone in Dallas, TX. This order placed from an Android device with IP geolocating to Lagos, Nigeria.
2. [Velocity - HIGH] Shipping address changed to a freight forwarder in Miami, FL, 2 hours before order placement. Prior 23 orders shipped to a residential address in Dallas, TX.
3. [Behavioral - MEDIUM] Order contains 3x PlayStation 5 consoles ($1,497). Customer's prior purchase history is entirely apparel and home goods, with average order value of $67. High-value electronics with no category history is consistent with account takeover patterns.
4. [Identity - MEDIUM] Account password was reset via email 6 hours before the address change. Email account may be compromised.

Mitigating Factors: Account is 3 years old with clean history. Loyalty member with 4,200 points.

Pattern Match: 87% similarity to confirmed Account Takeover pattern (ATO-DEVICE-GEO-RESHIPPER).

Recommended Action: Auto-decline. Trigger account security alert to the customer via the phone number on file (not the one on the order). Lock account pending customer verification.

## Guidelines

- Explain fraud signals in plain language that non-technical reviewers can understand. Avoid jargon like "BIN" without explaining it means "Bank Identification Number — the first 6 digits of the card."
- Always include mitigating factors alongside risk signals. Analysts need both to make balanced decisions.
- Provide statistical context for every signal — "this is unusual" is not actionable; "this occurs in only 2% of legitimate transactions but 68% of confirmed fraud" is.
- Respect customer privacy in explanations. Document enough detail for fraud decisions but do not include unnecessary personal information.
- Acknowledge model limitations. If the model's true positive rate at a given score threshold is only 30%, the analyst should know that 70% of transactions at that score are legitimate.
- Differentiate between fraud types in explanations — account takeover, synthetic identity, card testing, and friendly fraud require different response protocols.
- Calibrate recommended actions to the retailer's risk tolerance and false positive cost. A luxury retailer with high margins may accept higher false positive rates; a grocery delivery service with thin margins cannot.
- Document analyst decisions and outcomes to create a feedback loop for model improvement.
- Never disclose specific fraud detection rules or thresholds in customer-facing communications.

## Validation Checklist

- [ ] All contributing signals include factual observation, suspicion rationale, and statistical context
- [ ] Mitigating factors are documented alongside risk signals for balanced assessment
- [ ] Risk summary is written in plain language understandable by non-technical stakeholders
- [ ] Pattern matching references confirmed fraud cases, not just flagged transactions
- [ ] Historical true positive rate is provided for the relevant risk score range
- [ ] Recommended action is appropriate to the risk level and signal confidence
- [ ] Verification checklist for manual review is specific and actionable
- [ ] Evidence package is structured for potential chargeback representment use
- [ ] Customer privacy is maintained — no unnecessary PII in explanations
- [ ] Fraud type classification (ATO, synthetic, card testing, friendly fraud) is specified for each case
