---
name: stakeholder-requirements
description: "Maps each stakeholder's needs, priorities, and concerns from a meeting transcript with multiple stakeholders. Produces a stakeholder roster, per-person needs map, alignment matrix, conflict analysis, and engagement recommendations. Use this skill whenever a transcript from a multi-stakeholder meeting needs to be turned into a per-person strategy for tailoring your approach."
metadata:
  display_name: "Stakeholder Requirements"
  short_description: "Map each stakeholder's needs, priorities, and concerns from meeting transcripts"
  default_prompt: "Map out stakeholder needs and priorities from this meeting transcript"
  icon_path: "assets/icon.webp"
---

# Stakeholder Requirements

## Goal

Take a raw transcript from a meeting with multiple stakeholders and produce a structured stakeholder map — roster, per-person needs, alignment matrix, conflicts, and engagement recommendations — so you can tailor your approach to each person. The output preserves direct quotes, separates stated from inferred needs, and calls out unknowns rather than inventing them.

## When to Use

Activate this skill when any of the following apply:

- A user attaches or pastes a transcript from a meeting with multiple stakeholders and wants each person's needs, priorities, and concerns mapped out
- A user asks to "map stakeholders from this call" or "who cares about what in this meeting"
- A user provides a multi-party meeting transcript and wants a per-stakeholder strategy
- A user references a stakeholder meeting, committee review, or cross-functional discussion and needs to understand each person's angle

Relevant input types:
- Transcribed audio/video recordings of multi-stakeholder meetings
- Chat logs or notes from cross-functional sessions
- Committee or working group transcripts
- Any conversation log where multiple stakeholders expressed views

## How to Use

The user invokes:

- `/stakeholder-requirements <transcript or reference to attached transcript>`

Interpret the input as:
- The full text of a transcript from a meeting with multiple stakeholders
- If a file is attached, read and process that file as the transcript source
- If no transcript is provided, ask the user to attach or paste one

## Steps (STRICT)

1. **Read the full transcript.** Do not skim. Process the entire conversation before extracting anything. If the transcript is attached as a file, use `query_document` or `read_file` to access it.

2. **Build the Stakeholder Roster.** Identify every person who spoke or was discussed. For each, capture:
   - Name and role/title
   - Department or function
   - Decision-making influence: decision-maker, influencer, blocker, end user, or sponsor

3. **Build the Needs Map.** For each stakeholder, produce a card with:
   - **Stated needs**: What they explicitly said they need or want (with direct quotes)
   - **Stated pains**: Problems or frustrations they named (with direct quotes)
   - **Inferred needs**: What they likely care about that they didn't say directly, based on their role and comments
   - **Success criteria**: What "good" looks like for this person — how they'd judge a win
   - **Potential objections**: What might make them push back, based on their concerns

4. **Create the Alignment Matrix.** Build a table with stakeholders as rows and these columns:
   - Top priority (one phrase)
   - What they care most about avoiding
   - What would get them to say yes
   - Risk level (aligned / skeptical / blocker)

5. **Identify Conflicts or Tensions.** Where do stakeholders seem to want different or competing things? Name the tension, who's on each side, and what it means for the solution.

6. **Write Engagement Recommendations.** For each stakeholder, one sentence on how to approach them: what to emphasize, what to prove, and what to avoid bringing up.

7. **Format the output.** Use the exact section structure defined below. Quote the transcript directly wherever possible. If a stakeholder barely spoke, say so and note what's unknown about them — do not invent needs.

## Output Format (STRICT)

Produce a document with exactly these five sections, in this order:

### 1. STAKEHOLDER ROSTER

| # | Name | Role/Title | Department/Function | Decision-Making Influence |
|---|------|------------|---------------------|--------------------------|
| 1 | [name] | [role] | [dept] | [decision-maker/influencer/blocker/end user/sponsor] |

### 2. NEEDS MAP (per stakeholder)

Produce one card per stakeholder:

**[Stakeholder Name] — [Role]**

- **Stated needs**: "[verbatim quote]" — [context]
- **Stated pains**: "[verbatim quote]" — [context]
- **Inferred needs**: [what they likely care about, based on role and comments]
- **Success criteria**: [what "good" looks like for this person]
- **Potential objections**: [what might make them push back]

If a stakeholder barely spoke, write: "Limited participation — [what they said, if anything]. Unknown: [what we don't know about their position]."

### 3. ALIGNMENT MATRIX

| Stakeholder | Top Priority | What They Care Most About Avoiding | What Would Get Them to Say Yes | Risk Level |
|-------------|-------------|-------------------------------------|--------------------------------|------------|
| [name] | [one phrase] | [one phrase] | [one phrase] | [aligned/skeptical/blocker] |

### 4. CONFLICTS OR TENSIONS

Numbered list. For each tension:
- **Tension**: [name the competing priorities]
- **Sides**: [who wants what]
- **Implication**: [what this means for the solution]

### 5. ENGAGEMENT RECOMMENDATIONS

Numbered list, one per stakeholder:
1. **[Stakeholder Name]**: [one sentence — what to emphasize, what to prove, what to avoid]

## Constraints

- **Quote directly.** Use the speaker's exact words in quotation marks for stated needs and pains. Do not paraphrase what was actually said.
- **Don't invent needs.** If a stakeholder barely spoke, say so and note what's unknown. Do not fabricate needs, pains, or objections that aren't supported by the transcript.
- **Separate stated from inferred.** Stated needs and pains get direct quotes. Inferred needs are clearly labeled as inferences based on role and comments — not presented as things the person actually said.
- **One phrase per matrix cell.** The alignment matrix cells should be concise — one phrase each, not paragraphs.
- **One sentence per engagement recommendation.** Keep it tight: what to emphasize, what to prove, what to avoid — all in one sentence.
- **Process the entire transcript.** Do not stop early or skip sections of the conversation.
- **Name the tension.** In the conflicts section, be specific about what's competing and who's on which side. Vague "there may be some tension" statements are not useful.
- **Influence labels.** Use the five categories: decision-maker, influencer, blocker, end user, sponsor. If you're unsure, pick the closest and note the uncertainty.

## Failure Handling

- If no transcript is provided, ask the user to attach or paste one.
- If only one person spoke, produce the roster and needs map for that person and note that a multi-stakeholder analysis wasn't possible.
- If the transcript is too short to extract meaningful stakeholder data, say so and produce what you can with a note about limited input.
- If no conflicts or tensions are apparent, state "No conflicts or tensions were identified in this transcript" rather than forcing one.
- If the transcript is in a language other than English, process it in that language and produce the output in the same language unless the user specifies otherwise.

## Examples

**Example 1**
User: /stakeholder-requirements [attaches multi-stakeholder meeting transcript]

Expected output: A five-section stakeholder map. Roster with all participants and their influence levels. Per-person needs cards with verbatim quotes for stated needs/pains and clearly labeled inferences. Alignment matrix with one-phrase cells. Conflicts section naming specific tensions and who's on each side. Engagement recommendations with one sentence per person.

**Example 2**
User: /stakeholder-requirements [pastes a committee meeting chat log]

Expected output: Same five-section structure. Stakeholders identified from context clues. Needs extracted from the discussion with direct quotes. If someone barely participated, their card notes limited participation and unknowns rather than invented needs.
