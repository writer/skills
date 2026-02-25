---
name: fraud-pattern-interpretation
description: Interpret and explain fraud detection signals, model outputs, and suspicious patterns across payment, identity, and account fraud typologies. Use when analyzing fraud alerts, explaining model scores, investigating fraud rings, or documenting fraud case findings for consumer and commercial banking.

metadata:
  display_name: "Fraud Pattern Interpretation"
  short_description: "Interpret banking fraud detection signals and alerts"
  default_prompt: "Interpret my fraud pattern signals in simple words and next steps"
  version: "1.0.0"
  tags:
    - financial-services
  icon_path: "assets/icon.png"
---

# Fraud Pattern Interpretation

## Overview

This skill produces detailed, evidence-based interpretations of fraud detection signals for financial institutions. It covers transaction fraud (card, wire, ACH), identity fraud (synthetic and identity theft), account takeover (ATO), check fraud, and application fraud. Explanations are grounded in industry fraud typologies and aligned with Reg E dispute requirements, network rules (Visa/Mastercard), and law enforcement referral standards.

## When to Use

- Interpreting fraud model scores and feature importance rankings
- Explaining why a transaction or application was flagged as potentially fraudulent
- Documenting fraud investigation findings for case closure
- Identifying fraud ring patterns across linked accounts
- Supporting Reg E provisional credit and liability determination decisions
- Preparing law enforcement referrals (SARs with fraud focus)
- Analyzing false positive patterns to recommend model tuning

## Required Inputs

| Input | Description | Format |
|-------|-------------|--------|
| Alert/case data | Fraud score, rule triggered, alert details | System output |
| Transaction details | Amount, merchant, channel, timestamp, device | Transaction record |
| Customer profile | Account history, authentication method, device fingerprint | CIF/profile data |
| Model output | Score, top features, threshold applied | Model API response |
| Historical fraud data | Prior fraud claims, chargeback history | Case management |
| Peer/network data | Velocity across accounts, shared device/IP | Link analysis output |

## Methodology

### Step 1: Classify the Fraud Typology

Categorize the alert into the appropriate fraud domain:

| Typology | Key Indicators | Typical Channel |
|----------|---------------|-----------------|
| **Card-not-present (CNP)** | Unusual merchant, geo anomaly, velocity | Online/mobile |
| **Card-present counterfeit** | Compromised POS, mag-stripe fallback | In-store |
| **Account takeover (ATO)** | Credential change + transaction, new device | Digital banking |
| **Synthetic identity** | Thin file, SSN/DOB mismatch, credit-building pattern | Application |
| **Check fraud** | Altered MICR, duplicate presentment, remote deposit anomaly | Branch/mobile |
| **ACH/Wire fraud** | BEC pattern, new payee, urgency indicators | Wire/ACH |
| **Application fraud** | Velocity of applications, data inconsistency | New accounts |
| **First-party fraud** | Friendly fraud, bust-out pattern, claim anomaly | Disputes |

### Step 2: Decompose the Detection Signal

For model-based detections, explain the score through feature attribution:

1. **Identify the top contributing features** (e.g., SHAP values, feature importance)
2. **Contextualize each feature**: What does the value mean relative to the customer's baseline?
3. **Quantify the deviation**: "Transaction amount of $2,847 is 4.2 standard deviations above the customer's mean of $127"
4. **Assess feature interactions**: Combinations that individually may be normal but together are suspicious
5. **Compare to known fraud patterns**: Map features to established fraud typology signatures

For rule-based detections:
- State the specific rule triggered and its parameters
- Show which data elements satisfied the rule conditions
- Assess whether the rule is functioning as intended or producing a false positive

### Step 3: Evaluate the Evidence Chain

Build a comprehensive evidence assessment:

**Strong fraud indicators** (high confidence):
- Device fingerprint matches known fraud device
- IP geolocation inconsistent with cardholder location and no travel history
- Transaction velocity exceeds physical possibility (two countries within 1 hour)
- Credential changes (email, phone, address) immediately preceding high-value transactions

**Moderate indicators** (requires corroboration):
- First-time merchant or merchant category
- Transaction amount significantly above historical average
- Time-of-day anomaly (e.g., 3:00 AM local time)
- Shipping address different from billing address

**Weak indicators** (context-dependent):
- Slightly above-average transaction amount
- Weekend or holiday transaction
- New but plausible merchant category

### Step 4: Assess Linkage and Network Patterns

Analyze connections to identify ring activity:
- **Device linkage**: Shared device IDs, browser fingerprints, or IP addresses across accounts
- **Identity linkage**: Common SSN digits, phone numbers, email domains, or physical addresses
- **Behavioral linkage**: Identical transaction patterns, timing, or beneficiaries
- **Financial linkage**: Fund flows between accounts, common funding sources
- Build a link analysis graph showing entity relationships and shared attributes

### Step 5: Determine Liability and Impact

Assess the financial and regulatory implications:
- **Reg E applicability**: Was this an electronic fund transfer subject to consumer liability limits?
- **Reg E timelines**: 10 business days for investigation (20 for new accounts), provisional credit within 10 days
- **Network liability**: Visa/Mastercard chargeback rights and representment windows
- **Customer liability**: Based on notification timing (2 business days = $50 max, 60 days = $500 max, beyond = unlimited under Reg E)
- **Gross and net loss calculation**: Total fraud amount minus recoveries, insurance, and chargebacks

### Step 6: Document Findings

Structure the investigation summary for case closure:
- Chronological event timeline with all relevant data points
- Evidence supporting or refuting fraud determination
- Decision rationale (confirmed fraud, suspected fraud, false positive, inconclusive)
- Recovery actions taken or recommended
- Prevention recommendations (block device, restrict account, update rules)

### Step 7: Recommend Systemic Improvements

Based on the pattern analysis, identify:
- False positive reduction opportunities (rule tuning, threshold adjustment)
- Detection gaps exposed by the fraud pattern
- Customer authentication improvements needed
- Policy or procedure updates warranted

## Output Specification

```markdown
# Fraud Pattern Analysis: Case [ID]

## Alert Summary
- **Case ID**: [ID]
- **Fraud Typology**: [Classification]
- **Detection Method**: [Model score / Rule / Manual referral]
- **Fraud Score**: [Score] (threshold: [threshold])
- **Flagged Amount**: [$Amount]
- **Date of Activity**: [Date range]

## Signal Decomposition
| Feature/Rule | Value | Customer Baseline | Deviation | Risk Contribution |
|-------------|-------|-------------------|-----------|-------------------|
| [Feature 1] | [Value] | [Baseline] | [X sigma / %] | [High/Med/Low] |

## Evidence Assessment
### Strong Indicators
- [Indicator with specific evidence]

### Moderate Indicators
- [Indicator with specific evidence]

### Mitigating Factors
- [Factor reducing fraud likelihood]

## Linkage Analysis
[Connected entities, shared attributes, network visualization description]

## Determination
- **Finding**: [Confirmed Fraud / Suspected Fraud / False Positive / Inconclusive]
- **Confidence**: [High / Medium / Low]
- **Rationale**: [Specific basis for determination]

## Financial Impact
| Metric | Amount |
|--------|--------|
| Gross fraud amount | [$X] |
| Expected recovery | [$X] |
| Net loss | [$X] |

## Actions and Recommendations
- [Immediate actions taken]
- [Systemic recommendations]
```

## Analysis Framework

### Velocity Analysis

Calculate transaction velocity across multiple dimensions:
- Count and sum of transactions per hour, day, and week
- Distinct merchant count in rolling 24-hour window
- Channel switching frequency (mobile → web → in-store)
- Geographic spread (distinct cities or countries per day)

### Behavioral Biometrics Interpretation

When behavioral data is available, assess:
- Typing cadence deviation from enrolled profile
- Navigation pattern anomalies (unfamiliar with interface)
- Session duration relative to transaction complexity
- Mouse movement patterns (bot-like linear movements vs. human curves)

### Bust-Out Detection

For first-party fraud and bust-out patterns:
- Account aging: months since opening vs. credit utilization trajectory
- Payment behavior: consistent minimum payments building to max-out
- Balance transfer patterns: moving credit across products
- Sudden change: shift from responsible usage to rapid cash advances

## Examples

**Example 1 — ATO Pattern**:
"Account #XXXX8832 (customer Jane Smith) triggered ATO-Score 94 on 2025-10-12. At 02:14 AM EST, the registered email was changed from j.smith@email.com to jsmith8832@protonmail.com from a new device (Android, Pixel 7, IP: 185.xx.xx.xx geolocated to Romania). Within 8 minutes, a $4,500 Zelle transfer was initiated to a new recipient. The customer's prior 18 months show no international login, no device changes, and typical daytime-only access from iOS devices in Atlanta, GA. The device, IP geography, email provider change, and rapid fund movement constitute strong evidence of account takeover. Recommended: block account, reverse transaction, credential reset, and SAR filing."

**Example 2 — False Positive Analysis**:
"Alert FP-44291 flagged a $3,200 purchase at an electronics retailer for customer #XXXX1190 (model score: 78, threshold: 75). Top features: amount 2.1σ above mean, new merchant, and weekend timing. Investigation reveals: customer called branch on Friday to advise of planned TV purchase (noted in CRM), merchant is 2 miles from home address, and Apple Pay with biometric authentication was used. Determination: false positive. The pre-notification, proximity, and strong authentication mitigate the statistical anomaly. Recommendation: add merchant pre-notification as a score-suppressing feature in the next model iteration."

## Guidelines

- Never share fraud model scores, thresholds, or detection rules with customers
- Use "unauthorized" rather than "fraudulent" when communicating with customers
- Preserve chain of custody for digital evidence (screenshots, logs, device data)
- Apply Reg E provisional credit timelines strictly; document any extensions
- Distinguish between third-party fraud (victim) and first-party fraud (perpetrator) in findings
- Cross-reference fraud cases against SAR filing obligations
- Use statistical language for deviations (standard deviations, percentiles) rather than subjective terms
- Document both incriminating and exculpatory evidence
- Maintain objectivity; investigation findings inform but do not substitute for legal determinations

## Validation Checklist

- [ ] Fraud typology is explicitly classified
- [ ] Detection signal is decomposed with feature-level attribution
- [ ] Evidence is categorized by strength (strong, moderate, weak)
- [ ] Customer baseline behavior is quantified for comparison
- [ ] Linkage analysis covers device, identity, behavioral, and financial dimensions
- [ ] Reg E applicability and timeline compliance are assessed
- [ ] Financial impact (gross, recovery, net) is calculated
- [ ] Determination includes confidence level and specific rationale
- [ ] Actions are specific and immediately actionable
- [ ] Documentation supports potential law enforcement referral
