---
name: billing-compliance-checker
description: Ensure healthcare billing compliance with CMS rules, OIG guidelines, False Claims Act requirements, and payer-specific billing policies through systematic claim auditing and risk assessment. Use when auditing billing practices, evaluating compliance risk, preparing for OIG audits, or building billing compliance programs.

metadata:
  display_name: "Billing Compliance Checker"
  short_description: "Audit healthcare billing for regulatory compliance"
  default_prompt: "Check my billing compliance for gaps risks and required fixes"
  version: "1.0.0"
  tags:
    - healthcare
  icon_path: "assets/icon.png"
---

# Billing Compliance Checker

## Overview

Systematically evaluate healthcare billing practices against federal and state regulations, OIG (Office of Inspector General) guidance, CMS billing rules, and payer-specific policies to identify compliance risks, prevent fraud and abuse, and ensure adherence to the False Claims Act, Anti-Kickback Statute, and Stark Law. This skill supports compliance officers, billing managers, and revenue cycle leaders in maintaining compliant billing operations.

## When to Use

- Auditing billing practices for compliance with federal/state regulations
- Evaluating individual claims or claim patterns for compliance risk
- Preparing for external audits (OIG, RAC, MAC, ZPIC/UPIC)
- Building or enhancing a billing compliance program
- Training staff on billing compliance requirements
- Investigating potential billing irregularities or whistleblower concerns

## Required Inputs

| Input | Description | Format |
|-------|-------------|--------|
| Claims data | Billed CPT/ICD-10 codes, modifiers, amounts, dates | Structured array |
| Clinical documentation | Supporting notes and medical records | Document references |
| Provider information | NPI, specialty, employment/contract arrangements | Structured object |
| Billing patterns | Historical claim data for trend analysis | Structured array |
| Compliance program docs | Existing policies, training records, audit history | Document references |

## Methodology

### Step 1: Regulatory Framework Assessment

Identify applicable compliance requirements:

**Federal Compliance Framework:**

| Regulation | What It Covers | Key Risk |
|-----------|----------------|----------|
| False Claims Act (FCA) | Knowingly submitting false claims for payment | Treble damages + per-claim penalties |
| Anti-Kickback Statute (AKS) | Remuneration for referrals of federal healthcare business | Criminal penalties, exclusion |
| Stark Law (Physician Self-Referral) | Physician referrals to entities with financial relationships | Claim denial, refund obligation |
| NCCI Edits | Correct coding to prevent unbundling and incorrect billing | Claim denial, overpayment |
| OIG Compliance Guidance | Industry-specific compliance program elements | Increased scrutiny, exclusion risk |
| 60-Day Overpayment Rule | Obligation to report and return identified overpayments | FCA liability if not returned |

### Step 2: Claim-Level Compliance Audit

Evaluate individual claims against compliance criteria:

**Billing Compliance Checks:**

1. **Documentation supports the code billed** — every code must be justified by clinical documentation
2. **Medical necessity established** — diagnosis supports the procedure or service
3. **Correct code selection** — CPT/HCPCS accurately reflects the service performed
4. **Proper modifier usage** — modifiers used correctly, not to bypass edits inappropriately
5. **No unbundling** — component codes not billed separately when a comprehensive code exists
6. **No upcoding** — E/M level or procedure complexity matches documentation
7. **No duplicate billing** — same service not billed twice for the same date
8. **Correct provider** — billing provider performed or supervised the service as required
9. **Incident-to rules** — services billed incident-to meet all CMS requirements
10. **Place of service accuracy** — POS code reflects where service was actually rendered

### Step 3: Pattern Analysis

Identify billing patterns that may indicate compliance risk:

**High-Risk Billing Patterns:**

| Pattern | Red Flag | OIG Risk Level |
|---------|----------|---------------|
| Consistently billing highest E/M level | Upcoding risk | High |
| High percentage of modifier 25 usage | Separate E/M not supported | Medium-High |
| Unusual modifier 59/XE usage | Unbundling risk | High |
| Same diagnosis on every claim | Cloning/template abuse | Medium |
| Services on every encounter regardless of diagnosis | Routine-ization | High |
| Billing above specialty peers (units, frequency) | Over-utilization | High |
| High volume of after-hours codes | Potential misuse | Medium |
| Bilateral procedures without bilateral diagnosis | Upcoding | Medium |

**Statistical Analysis:**
- Compare provider billing distributions against specialty benchmarks
- Identify outliers (billing greater than 2 standard deviations from peers)
- Analyze procedure frequency per patient against clinical norms
- Review modifier usage rates against specialty averages

### Step 4: Stark Law and AKS Assessment

Evaluate referral patterns and financial arrangements:

**Stark Law Compliance:**
- Are there financial relationships between referring physicians and entities?
- Do referral patterns follow financial interests?
- Are applicable Stark exceptions properly structured and documented?
- Common exceptions: in-office ancillary, employment, personal services, fair market value

**Anti-Kickback Assessment:**
- Are there arrangements that could be construed as remuneration for referrals?
- Do compensation arrangements meet safe harbor requirements?
- Are marketing arrangements, free services, or below-market leases present?
- Common safe harbors: employment, personal services, space rental, equipment rental

### Step 5: Compliance Risk Report

Generate the compliance assessment with risk scoring:

**Risk Severity Levels:**
- CRITICAL: Immediate compliance action needed, potential FCA/AKS exposure
- HIGH: Significant compliance risk, corrective action required within 30 days
- MODERATE: Compliance concern requiring investigation and monitoring
- LOW: Minor issue, address through education and process improvement
- ADVISORY: Best practice recommendation, no current violation

## Output Specification

The output includes:

**compliance_summary**: total_claims_audited, critical_findings, high_risk_findings, moderate_findings, low_findings, overall_compliance_score (0-100)

**claim_level_findings**: claim_id, cpt_codes, icd10_codes, finding_description, compliance_rule_violated, severity, evidence, corrective_action

**pattern_analysis**: pattern_description, affected_claims_count, risk_level, statistical_evidence (provider vs benchmark), recommended_investigation

**stark_aks_assessment**: financial_relationships_evaluated, stark_risks, aks_risks, safe_harbors_documented, recommendations

**overpayment_identification**: claims with potential overpayment, estimated_overpayment_amount, 60_day_rule_deadline, return_obligation

**corrective_action_plan**: prioritized actions with finding, risk_level, corrective_action, responsible_party, deadline, monitoring_plan

**compliance_program_assessment**: seven_elements_evaluation (standards, oversight, training, reporting, enforcement, auditing, response), gaps, recommendations

## Analysis Framework

### OIG Seven Elements of an Effective Compliance Program

1. **Written standards and procedures**: Coding and billing policies, compliance manual
2. **Compliance officer and committee**: Designated leadership with authority
3. **Training and education**: Regular training for all billing and coding staff
4. **Open lines of communication**: Anonymous reporting mechanism (hotline)
5. **Internal monitoring and auditing**: Regular proactive audits
6. **Enforcement through disciplinary guidelines**: Consistent enforcement of standards
7. **Prompt response to detected offenses**: Investigation and corrective action protocols

### Audit Sample Sizing

| Risk Level | Recommended Sample | Frequency |
|-----------|-------------------|-----------|
| High-risk areas | 30+ claims per provider | Quarterly |
| Moderate-risk areas | 10-20 claims per provider | Semi-annually |
| Low-risk areas | 5-10 claims per provider | Annually |
| New providers | 20+ claims | Within first 90 days |
| Post-corrective action | 20+ claims | Monthly for 3 months |

## Examples

**Input**: Dermatology practice audit. Provider bills 99215 on 78% of established patient visits. Modifier 25 used on 85% of E/M claims with same-day procedures. Multiple destruction codes billed per encounter with modifier 59.

**Compliance Assessment**:
1. CRITICAL: E/M upcoding risk — 99215 at 78% far exceeds specialty benchmark of 8-12%. Documentation review needed for sample of 99215 claims
2. HIGH: Modifier 25 overuse — 85% usage exceeds benchmark of 30-40%. Risk of billing separately identifiable E/M without supporting documentation
3. HIGH: Modifier 59 on destruction codes — potential unbundling. Review whether lesions are truly distinct anatomic sites with separate documentation
4. Corrective action: Immediate retrospective audit of 30 claims across each flagged pattern. Provider education on E/M documentation requirements. Implementation of prospective coding review for 90 days

## Guidelines

1. **Apply the FCA knowledge standard** — "knew or should have known" the claim was false
2. **When in doubt, do not bill** — it is safer to under-bill than to over-bill
3. **Document compliance program activities** — evidence of a good-faith compliance program is a mitigating factor
4. **Respond promptly to identified overpayments** — the 60-day clock starts when overpayment is identified
5. **Audit regularly and proactively** — do not wait for external audits to find issues

## Validation Checklist

- [ ] All seven OIG compliance program elements are evaluated
- [ ] Claim-level audits cover documentation support, medical necessity, and code accuracy
- [ ] Billing patterns are statistically compared against specialty benchmarks
- [ ] Stark Law and AKS risk factors are assessed
- [ ] Potential overpayments are identified with 60-day rule deadlines
- [ ] Corrective action plan addresses root causes with specific deadlines and owners
- [ ] Compliance findings are documented and retained for regulatory defense

## HIPAA Compliance Notes

- Compliance audits require access to clinical documentation and claims data containing PHI
- Audit findings should be protected under attorney-client privilege when conducted by or at the direction of legal counsel
- External auditors and consultants must operate under BAA
- Compliance investigation files should be secured with restricted access
- Report compliance findings through appropriate channels (compliance officer, legal counsel)
- Whistleblower protections apply — do not retaliate against individuals who report potential violations
