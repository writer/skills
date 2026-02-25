---
name: Patient Feedback Analysis
description: Analyze patient complaints, grievances, and survey free-text responses using NLP-driven sentiment analysis, CAHPS-aligned thematic coding, and root cause classification to drive systematic experience improvement.

metadata:
  display_name: "Patient Feedback Analysis"
  short_description: "Analyze patient complaints and survey feedback themes"
  default_prompt: "Analyze my patient feedback and recommend clear next actions"
  version: "1.0.0"
  tags:
    - healthcare
  icon_path: "assets/icon.png"
---

# Patient Feedback Analysis

## Overview

This skill systematically analyzes patient feedback data (complaints, grievances, survey comments, online reviews, and patient advisory council input) to extract actionable themes, quantify sentiment, and identify systemic root causes. It applies CAHPS-aligned thematic coding, NLP-based sentiment analysis, and healthcare-specific complaint taxonomy to transform unstructured patient voice data into prioritized improvement opportunities. CMS Conditions of Participation require hospitals to have a grievance process (42 CFR 482.13), and feedback analysis is essential for CAHPS improvement, risk mitigation, and patient safety event detection.

## When to Use

- Analyzing quarterly or annual patient complaint and grievance trends
- Investigating root causes behind declining CAHPS scores
- Mining patient survey free-text comments for improvement opportunities
- Monitoring online reputation (Google, Healthgrades, Yelp) for emerging themes
- Preparing patient experience reports for board or quality committee review
- Identifying potential patient safety events reported through complaint channels
- Supporting Magnet designation or other nursing excellence programs

## Required Inputs

| Input | Description | Format |
|-------|-------------|--------|
| `complaint_data` | Patient complaints and grievances with dates, categories, departments | De-identified JSON/CSV |
| `survey_comments` | Free-text responses from CAHPS, Press Ganey, or internal surveys | De-identified JSON array |
| `online_reviews` | Reviews from public platforms (Google, Healthgrades) | JSON array |
| `department_mapping` | Organizational structure mapping departments to service lines | JSON object |
| `historical_cahps` | CAHPS composite and individual item scores over time | JSON object |
| `resolution_data` | Complaint resolution status, time-to-resolution, actions taken | JSON array |

## Methodology

### Step 1: Data Ingestion and Normalization
- Aggregate feedback from all channels into unified format
- De-identify all patient-level data (remove names, MRN, dates of birth, specific dates of service)
- Normalize date formats, department names, and category labels
- Flag and separate potential patient safety events for immediate escalation
- Apply data quality checks: completeness, duplicates, and encoding errors

### Step 2: Thematic Coding (CAHPS-Aligned)
- Code each feedback item against CAHPS composite domains:
  - Communication with Doctors (listening, explaining, respect)
  - Communication with Nurses (responsiveness, courtesy, explanation)
  - Responsiveness of Hospital Staff (help timeliness, call button)
  - Pain Management (pain control, medication communication)
  - Communication about Medicines (purpose, side effects)
  - Discharge Information (self-care instructions, symptoms to watch)
  - Care Transitions (preferences considered, understanding of care plan)
  - Cleanliness and Quietness (environment of care)
- Apply additional healthcare-specific categories:
  - Billing and Financial (surprise bills, insurance confusion, collections)
  - Access and Scheduling (wait times, appointment availability, referral delays)
  - Staff Behavior (rudeness, dismissiveness, discrimination)
  - Care Quality (perceived errors, missed diagnoses, complications)
  - Facilities and Environment (wayfinding, parking, food, temperature)
- Allow multi-coding: single feedback items may span multiple themes

### Step 3: Sentiment Analysis
- Apply healthcare-tuned sentiment analysis:
  - Positive: Expressions of gratitude, praise, satisfaction, trust
  - Neutral: Factual statements, suggestions without emotional valence
  - Negative: Complaints, frustration, fear, anger, disappointment
  - Mixed: Contains both positive and negative elements
- Calculate sentiment scores on a -1.0 to +1.0 scale
- Identify intensity modifiers (use of capitals, exclamation marks, extreme language)
- Flag high-intensity negative sentiment for priority review

### Step 4: Root Cause Classification
- Apply root cause taxonomy to negative feedback:
  - **Process failure**: Broken workflow, policy gap, system error
  - **Communication failure**: Information not shared, miscommunication, language barrier
  - **Competency gap**: Knowledge or skill deficit, training need
  - **Resource constraint**: Staffing shortage, equipment unavailable, time pressure
  - **Culture issue**: Attitude, empathy deficit, bias, discrimination
  - **System/technology failure**: EHR issue, portal outage, equipment malfunction
- Map root causes to responsible departments and leaders
- Identify recurring root causes (same cause across 3 or more complaints = systemic)

### Step 5: Trend Analysis and Benchmarking
- Analyze trends over time:
  - Volume trends by theme, department, and severity
  - Seasonal patterns (post-holiday, flu season, summer staffing)
  - Correlation with operational changes (new EHR, staff turnover, construction)
- Benchmark against national CAHPS percentiles and peer organizations
- Calculate complaint rate per 1,000 patient encounters by department
- Identify statistically significant changes using control charts

### Step 6: Priority Ranking and Action Planning
- Score each theme using Impact-Prevalence-Detectability matrix:
  - Impact: Severity of patient harm or dissatisfaction (1-5)
  - Prevalence: Frequency of occurrence (1-5)
  - Detectability: Likelihood issue is captured in feedback (1-5, inverse)
  - Priority score = Impact x Prevalence x Detectability
- Generate prioritized action recommendations with:
  - Specific improvement actions tied to root causes
  - Responsible owner and timeline
  - Expected impact on CAHPS scores
  - Resource requirements

## Output Specification

```yaml
feedback_analysis:
  analysis_period: string
  total_feedback_items: number
  channels:
    complaints: number
    survey_comments: number
    online_reviews: number
  sentiment_distribution:
    positive: number
    neutral: number
    negative: number
    mixed: number
    average_sentiment_score: number
  theme_summary:
    - theme: string
      cahps_domain: string
      count: number
      percentage: number
      avg_sentiment: number
      trend: string
  root_causes:
    - cause_category: string
      count: number
      departments: array
      systemic: boolean
  priority_actions:
    - action: string
      theme: string
      root_cause: string
      priority_score: number
      responsible_owner: string
      timeline: string
      expected_cahps_impact: string
  safety_escalations:
    - description: string
      severity: string
      status: string
```

## Analysis Framework

Use the **Voice of the Patient (VoP) Triangulation Model**:
1. **Quantitative signal**: CAHPS and survey scores identify WHAT is underperforming
2. **Qualitative context**: Free-text comments and complaints explain WHY
3. **Operational correlation**: Process and staffing data reveals the ROOT CAUSE
4. **Action mapping**: Evidence-based interventions target specific root causes
5. **Outcome tracking**: Monitor improvement through ongoing feedback loops

## Examples

**Example: Quarterly Feedback Analysis for 200-Bed Community Hospital**
- Total feedback items: 1,847 (complaints: 312, survey comments: 1,203, online reviews: 332)
- Top themes: Communication with Nurses (23%), Wait Times (18%), Billing (15%), Cleanliness (11%)
- Sentiment: 34% positive, 12% neutral, 48% negative, 6% mixed
- Root causes: Staffing shortage in Med-Surg (systemic), billing process redesign needed, EVS schedule gaps
- Priority action 1: Implement hourly rounding protocol on Med-Surg (impact on nurse communication CAHPS: +4 percentile points estimated)
- Safety escalations: 3 items flagged for patient safety review

## Guidelines

- **HIPAA Compliance**: All feedback data must be de-identified before analysis. Remove patient names, MRN, provider names (unless analyzing provider-specific patterns with appropriate authorization), and dates of service. Use aggregate reporting only in outputs shared beyond quality leadership.
- **CMS Grievance Requirements**: Ensure analysis distinguishes between complaints (resolved at point of service) and grievances (require written response per 42 CFR 482.13). Track grievance response timeliness (CMS requires written response within 7 days).
- **Bias Awareness**: Feedback channels over-represent certain demographics (English-speaking, digitally connected, higher education). Acknowledge sampling bias and supplement with targeted outreach to underrepresented populations.
- **Provider Sensitivity**: When analysis reveals individual provider patterns, handle through established peer review and performance management channels with appropriate confidentiality protections.
- **Action Accountability**: Every analysis cycle must produce specific, assigned, time-bound actions. Analysis without action erodes trust in the feedback process.

## Validation Checklist

- [ ] All feedback channels included in analysis
- [ ] Data de-identified and PHI removed
- [ ] Thematic coding aligned to CAHPS domains
- [ ] Sentiment analysis calibrated for healthcare context
- [ ] Root causes classified using structured taxonomy
- [ ] Trends analyzed with statistical significance testing
- [ ] Benchmarking against national CAHPS percentiles completed
- [ ] Priority actions scored and ranked
- [ ] Safety events escalated through appropriate channels
- [ ] Grievance compliance requirements tracked
- [ ] Sampling bias acknowledged and mitigation documented
- [ ] Report formatted for quality committee presentation
