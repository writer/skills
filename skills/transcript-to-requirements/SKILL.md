---
name: transcript-to-requirements
description: "Extracts and structures discovery call, working session, or stakeholder interview transcripts into formal requirements documents with six defined sections: meeting context, stated requirements, inferred requirements, constraints, open questions, and assumptions. Use this skill whenever a transcript from a requirements-gathering conversation needs to be turned into a structured requirements document."
metadata:
  display_name: "Transcript to Requirements"
  short_description: "Transform discovery call and stakeholder interview transcripts into formal requirements documents"
  default_prompt: "Extract a formal requirements document from this discovery call transcript"
  icon_path: "assets/icon.png"
---

# Transcript to Requirements

## Goal

Take a raw transcript from a discovery call, working session, or stakeholder interview and produce a structured, formal requirements document with six standardized sections. The output preserves direct quotes, separates explicit from inferred requirements, and flags ambiguity rather than papering over it.

## When to Use

Activate this skill when any of the following apply:

- A user attaches or pastes a transcript from a discovery call, working session, or stakeholder interview and wants it structured into requirements
- A user asks to "extract requirements from this call" or "turn this transcript into a requirements doc"
- A user provides meeting notes or interview recordings (transcribed) and wants formal requirements captured
- A user references a discovery session, stakeholder interview, or requirements-gathering conversation and needs the output structured

Relevant input types:
- Transcribed audio/video recordings of meetings
- Chat logs or notes from working sessions
- Interview transcripts with stakeholders
- Any free-form conversation log where requirements were discussed

## How to Use

The user invokes:

- `/transcript-to-requirements <transcript or reference to attached transcript>`

Interpret the input as:
- The full text of a transcript from a discovery call, working session, or stakeholder interview
- If a file is attached, read and process that file as the transcript source
- If no transcript is provided, ask the user to attach or paste one

## Steps (STRICT)

1. **Read the full transcript.** Do not skim. Process the entire conversation before extracting anything. If the transcript is attached as a file, use `query_document` or `read_file` to access it.

2. **Extract Meeting Context.** Identify the date, participants (by role, not just name), and the stated purpose of the conversation. If the date is not mentioned, flag it as an open question rather than guessing.

3. **Extract Stated Requirements.** Go through the transcript line by line. Capture every explicit requirement or need mentioned. For each one, record:
   - **Requirement** (one sentence, active voice)
   - **Who stated it** (by role)
   - **Priority** if mentioned (must-have, should-have, nice-to-have) — leave blank if not stated
   - **Direct quote** from the transcript supporting it (verbatim, in quotation marks)

4. **Identify Inferred Requirements.** Look for things strongly implied but not stated outright. For each:
   - **Inferred requirement** (one sentence)
   - **Evidence** from the transcript supporting the inference (quote or paraphrase)
   - **Confidence level** (high / medium / low)

5. **Extract Constraints.** Capture technical, organizational, or timeline constraints mentioned — budget, existing systems, deadlines, compliance requirements, team size, etc. Quote the transcript directly.

6. **Identify Open Questions.** List things that came up but were left unanswered or ambiguous. Phrase each as a specific question to ask the stakeholder.

7. **List Assumptions.** Note anything you had to assume to fill in gaps. For each assumption, explain why you made it.

8. **Format the output.** Use tables for stated and inferred requirements. Use the exact section structure defined below. Quote the transcript directly — do not paraphrase what was actually said. If something is unclear, flag it rather than guessing.

## Output Format (STRICT)

Produce a document with exactly these six sections, in this order:

### 1. MEETING CONTEXT
- Date
- Participants (by role, not just name)
- Stated purpose of the conversation

### 2. STATED REQUIREMENTS

| # | Requirement | Stated By | Priority | Direct Quote |
|---|-------------|-----------|----------|--------------|
| 1 | [one sentence, active voice] | [role] | [must/should/nice — or blank] | "[verbatim quote]" |

### 3. INFERRED REQUIREMENTS

| # | Inferred Requirement | Evidence | Confidence |
|---|----------------------|----------|------------|
| 1 | [one sentence] | [quote or paraphrase from transcript] | [high/medium/low] |

### 4. CONSTRAINTS
List each constraint with a direct quote. Categorize as technical, organizational, or timeline.

### 5. OPEN QUESTIONS
Numbered list of specific questions to ask stakeholders.

### 6. ASSUMPTIONS
Numbered list. Each assumption paired with the reason it was made.

## Constraints

- **Quote directly.** Use the speaker's exact words in quotation marks for stated requirements, constraints, and evidence. Do not paraphrase what was actually said.
- **Flag, don't guess.** If something is unclear or missing, flag it as an open question or assumption. Do not fabricate information.
- **Role, not just name.** Identify participants by their role (e.g., "Product Manager," "Engineering Lead") in addition to their name when available.
- **Active voice.** Write each requirement as a single sentence in active voice (e.g., "The system shall support single sign-on" not "SSO support is needed").
- **Separate stated from inferred.** Do not blend explicit and inferred requirements. If it wasn't said outright, it goes in the inferred section with a confidence level.
- **Priority only if stated.** Do not assign priority levels that weren't mentioned in the transcript. Leave the field blank if no priority was given.
- **Process the entire transcript.** Do not stop early or skip sections of the conversation.
- **One requirement per row.** Do not bundle multiple requirements into a single row.

## Failure Handling

- If no transcript is provided, ask the user to attach or paste one.
- If the transcript is too short to extract meaningful requirements, say so and produce what you can with a note about limited input.
- If the transcript is in a language other than English, process it in that language and produce the requirements document in the same language unless the user specifies otherwise.
- If a section has no entries (e.g., no constraints were mentioned), state "No [section name] were identified in this transcript" rather than leaving it blank.

## Examples

**Example 1**
User: /transcript-to-requirements [attaches discovery call transcript]

Expected output: A structured requirements document with all six sections. Stated requirements in a table with verbatim quotes. Inferred requirements with confidence levels. Constraints with quotes. Open questions phrased as specific questions. Assumptions with reasoning.

**Example 2**
User: /transcript-to-requirements [pastes a working session chat log]

Expected output: Same six-section structure. Participants identified by role from context clues in the chat. Requirements extracted from the discussion with direct quotes from the chat log.
