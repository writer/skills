---
name: Associate Enablement Coach
description: Generate store-level playbooks that translate performance gaps into actionable coaching scripts, training priorities, and behavioral nudges tailored to individual store contexts and associate skill profiles.

metadata:
  display_name: "Associate Enablement Coach"
  short_description: "Create coaching playbooks for store associate enablement"
  default_prompt: "Help me with associate enablement and give clear next steps"
  version: "1.0.0"
  tags:
    - cpg-retail
  icon_path: "assets/icon.png"
---

# Associate Enablement Coach

## Overview

This skill generates targeted, store-level enablement playbooks that bridge the gap between performance analytics and frontline execution. It translates KPI shortfalls into specific coaching conversations, training module recommendations, role-play scenarios, and daily behavioral nudges that store managers can immediately deploy. The playbooks are contextualized to each store's unique performance profile, staffing mix, and customer demographics.

## When to Use

- After store performance reviews reveal execution gaps (conversion, UPT, ATV)
- When onboarding new store managers who need structured coaching frameworks
- During seasonal ramp-up periods requiring rapid skill-building (holiday, back-to-school)
- When rolling out new selling programs, loyalty initiatives, or product launches
- To address specific behavioral deficits identified through mystery shop or customer feedback
- As part of ongoing associate development and performance management cycles

## Required Inputs

| Input | Description | Format |
|-------|-------------|--------|
| `store_performance` | Current KPIs vs. benchmark (conversion, UPT, ATV, CSAT) | JSON object |
| `associate_profiles` | Tenure, role, certifications, skill assessment scores | Array of objects |
| `performance_gaps` | Ranked list of KPI gaps from store performance analysis | Array |
| `customer_segments` | Primary shopper demographics and behavioral profiles | Object |
| `training_catalog` | Available training modules and completion status by associate | Reference data |
| `mystery_shop_results` | Most recent mystery shop scores by evaluation category | Object (optional) |
| `schedule_data` | Weekly schedule with peak/off-peak coverage | Tabular (optional) |

## Methodology

### Step 1 — Gap-to-Behavior Mapping

Translate each KPI gap into the specific frontline behaviors that drive it:

- **Low Conversion**: Map to greeting timing (under 30 seconds), needs assessment depth, fitting room engagement, objection handling, and closing techniques.
- **Low UPT**: Map to outfit-building suggestions, accessory attachment prompts, loyalty program enrollment pitches, and complementary category awareness.
- **Low ATV**: Map to trade-up selling, premium product storytelling, bundle value articulation, and full-price selling confidence.
- **Low CSAT**: Map to active listening, empathy language, resolution authority usage, and follow-up commitment delivery.
- **Low Labor Productivity**: Map to zone coverage optimization, task batching during off-peak, and proactive customer engagement during downtime.

### Step 2 — Associate Skill Assessment

Profile each associate against the required behaviors:

1. **Skill Matrix Construction**: Rate each associate on the behavioral competencies identified in Step 1, using data from mystery shops, manager observations, and transactional data (personal conversion rate, personal UPT where trackable).
2. **Tenure-Based Expectations**: Set differentiated expectations — associates under 90 days focus on foundational behaviors; 90-day to 1-year associates build consistency; tenured associates develop mentoring and advanced selling skills.
3. **Strength Identification**: Identify each associate's top 2 strengths for peer teaching opportunities and morale reinforcement.

### Step 3 — Playbook Construction

Build the store-level playbook with these components:

1. **Weekly Focus Behavior**: Select the single highest-impact behavior to improve based on the largest controllable KPI gap. Narrow focus drives adoption.
2. **Daily Huddle Script**: A 3-minute pre-shift script for the store manager covering the focus behavior, a specific customer scenario, and a measurable goal for the shift.
3. **Coaching Conversation Guides**: Structured one-on-one conversation templates using the SBI (Situation-Behavior-Impact) model for addressing gaps and the STAR (Situation-Task-Action-Result) model for reinforcing strengths.
4. **Role-Play Scenarios**: 2-3 realistic customer interaction scenarios tailored to the store's product mix and customer demographics. Include ideal dialogue flow, common pitfalls, and evaluation criteria.
5. **Micro-Learning Assignments**: Map specific training modules (under 10 minutes each) from the catalog to associates who need them, with completion deadlines.
6. **Recognition Triggers**: Define measurable thresholds that trigger real-time recognition (e.g., "When an associate achieves 3+ UPT on a transaction, acknowledge within the shift").

### Step 4 — Schedule-Aware Deployment

Align coaching activities with operational reality:

- Place role-play practice during low-traffic windows (typically Tuesday/Wednesday 2-4 PM).
- Schedule one-on-ones during overlap shifts to avoid floor coverage gaps.
- Front-load coaching for associates scheduled on highest-traffic days.
- Assign peer mentoring pairs on shared shifts where both the mentor and mentee are present.

### Step 5 — Progress Tracking Framework

Define how to measure coaching effectiveness:

- **Leading Indicators** (weekly): Behavior observation checklist completion rate, training module completion, role-play participation.
- **Lagging Indicators** (bi-weekly): Shift-level conversion rate change, UPT trend, mystery shop score improvement, CSAT movement.
- **Feedback Loop**: Weekly 5-minute manager reflection on what coaching tactics worked and what to adjust.

## Output Specification

Produce a structured playbook containing:

- `store_id`: Store identifier
- `playbook_period`: Week or date range covered
- `priority_gap`: The primary KPI gap being addressed, with current value, target value, and gap magnitude
- `focus_behavior`: The single behavior to emphasize, with description and rationale
- `daily_huddle_scripts`: Array of 5-7 daily scripts, each with a theme, key message, customer scenario, and shift goal
- `coaching_guides`: Array of associate-specific coaching conversation outlines using SBI/STAR frameworks
- `role_play_scenarios`: Array of 2-3 scenarios with customer profile, ideal flow, common mistakes, and evaluation rubric
- `training_assignments`: Array of associate-module pairings with completion deadlines
- `recognition_plan`: Triggers and recognition methods for positive reinforcement
- `progress_metrics`: Leading and lagging indicators with measurement cadence and targets

## Analysis Framework

Apply the **Coaching Impact Chain**:

1. **Identify**: Performance data reveals the KPI gap.
2. **Diagnose**: Gap-to-behavior mapping isolates the root behavior.
3. **Prescribe**: Specific coaching interventions are selected.
4. **Execute**: Manager delivers coaching using playbook scripts and tools.
5. **Observe**: Behavior change is monitored through leading indicators.
6. **Measure**: KPI improvement is validated through lagging indicators.
7. **Iterate**: Playbook is updated based on what moved the needle.

At each stage, the playbook must provide the store manager with clear, unambiguous guidance — no interpretation required.

## Examples

**Example — Low Conversion Store Playbook Excerpt**:

Weekly Focus: Greeting and Needs Assessment (targeting conversion rate improvement from 16.8% to 19.0%)

Daily Huddle — Monday: "This week we are focused on connecting with every customer within 30 seconds of entry. Today's scenario: A customer walks in and heads straight to the clearance section. Instead of waiting, approach with 'I see you found our new markdowns — are you shopping for yourself or looking for a gift?' This opens the conversation beyond price. Goal for today: every associate initiates contact with at least 80% of customers in their zone."

Coaching Guide — Associate A (tenure: 45 days): SBI framework conversation. Situation: "During Saturday's shift, I observed three customers browse your zone for over 2 minutes without engagement." Behavior: "You were focused on refolding the table display and didn't look up." Impact: "Those customers left without trying anything on, which directly affects our conversion. Let's practice a transition from tasking to engaging — you can refold while positioned to make eye contact."

## Guidelines

- Limit each playbook to ONE primary focus behavior per week. Attempting to fix everything simultaneously dilutes impact and overwhelms managers.
- Write huddle scripts in natural, conversational language — not corporate jargon. Managers will read these aloud.
- Respect associate dignity in all coaching language. Frame gaps as development opportunities, not failures.
- Tailor scenarios to the store's actual product categories and customer base. Generic scripts feel inauthentic.
- Account for manager coaching skill level — new managers need more scripted guidance; experienced managers need frameworks and flexibility.
- Never recommend disciplinary action in playbooks — this is an enablement tool, not a performance management instrument.
- Include at least one strength-based recognition element per playbook to maintain associate morale.
- Ensure training module recommendations are actually available and accessible on the store's devices.

## Validation Checklist

- [ ] Focus behavior directly maps to the largest controllable KPI gap
- [ ] Huddle scripts are under 3 minutes when read aloud at natural pace
- [ ] Coaching conversations follow SBI or STAR structure completely
- [ ] Role-play scenarios reflect the store's actual product assortment and customer mix
- [ ] Training assignments are matched to individual associate skill gaps, not blanket-assigned
- [ ] Schedule conflicts are checked — coaching activities do not overlap with peak traffic
- [ ] Progress metrics include both leading (behavioral) and lagging (KPI) indicators
- [ ] Language is inclusive, respectful, and free of corporate jargon
- [ ] Playbook is actionable by a store manager without additional interpretation
- [ ] Recognition triggers are specific and measurable, not subjective
