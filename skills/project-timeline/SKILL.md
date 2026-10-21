---
name: project-timeline
description: "Turns proposals, scope docs, statements of work, technical specs, or meeting notes into a structured project timeline formatted as a sprint plan. Produces a project summary, sprint-by-sprint breakdown with work items and dependencies, a dependency map, critical path, gaps and assumptions, and a text-based Gantt visualization. Also generates an interactive HTML project timeline from the analysis. Use this skill whenever a project document needs to be converted into an actionable sprint plan with a visual timeline."
metadata:
  display_name: "Project Timeline"
  short_description: "Turn proposals, scope docs, and specs into structured sprint plans with interactive HTML timelines"
  default_prompt: "Turn this project document into a sprint plan with an interactive timeline"
  icon_path: "assets/icon.png"
---

# Project Timeline

## Goal

Take a project document — a proposal, scope doc, statement of work, technical spec, or meeting notes — and turn it into a structured sprint plan with six sections: project summary, sprint plan, dependency map, critical path, gaps and assumptions, and a text-based Gantt visualization. Then generate an interactive HTML project timeline from the analysis so the user can visualize and share it.

## When to Use

Activate this skill when any of the following apply:

- A user attaches a proposal, scope doc, SOW, technical spec, or meeting notes and wants a project timeline or sprint plan
- A user asks to "turn this document into a timeline" or "break this into sprints"
- A user provides a project document and wants to see dependencies, critical path, or a Gantt chart
- A user asks for a sprint plan, work breakdown, or project schedule from a document
- A user wants an interactive HTML timeline from a project document

Relevant input types:
- Proposals and RFP responses
- Scope documents and statements of work
- Technical specifications and architecture docs
- Meeting notes from planning sessions
- Any document that describes project work, deliverables, or milestones

## How to Use

The user invokes:

- `/project-timeline <document or reference to attached document>`

Interpret the input as:
- The full text of a project document to be converted into a sprint plan
- If a file is attached, use `query_document` or `read_file` to access it
- If no document is provided, ask the user to attach or paste one

## Steps (STRICT)

### 1. Read the Full Document

Process the entire document before extracting anything. Do not skim. If the document is attached as a file, use `query_document` or `read_file` to access it.

### 2. Produce the Project Summary

Write 2-3 sentences covering:
- What the project is
- Who it's for
- The stated end goal

### 3. Build the Sprint Plan

Break the work into sprints (1-2 week increments). For each sprint, produce:

**SPRINT [N] — [Sprint name/theme]**
- **Dates/duration**: estimated start and end, or "Week X-Y"
- **Goal**: one sentence describing what "done" looks like for this sprint
- **Work items**: numbered list, each with:
  - Task description (one line)
  - Owner or role (if stated in the document; otherwise "Unassigned")
  - Dependencies (which prior sprint or task this depends on, if any)
  - Effort estimate (S/M/L if no hours given in the document)
- **Milestones or deliverables** due this sprint
- **Risks or blockers** visible for this sprint

### 4. Build the Dependency Map

List every dependency between work items across sprints. Format as:
```
[Task A] → depends on → [Task B] (Sprint X)
```

### 5. Identify the Critical Path

Identify the longest chain of dependent tasks that determines the project's minimum timeline. List the chain and call out which sprint each task lands in.

### 6. Document Gaps and Assumptions

- Flag anything the document doesn't specify that you had to assume (dates, owners, effort, scope boundaries)
- Flag anything ambiguous that could change the timeline
- Note what's missing that the user should clarify

### 7. Produce the Timeline Visualization Spec

Create a simple text-based Gantt-style view:
- One row per sprint
- Use `|` characters to represent duration proportionally
- Mark milestones with a star icon (★)
- Mark dependencies with arrows between rows (↑↓)

### 8. Generate the Interactive HTML Timeline

After producing the structured analysis, generate an interactive HTML project timeline. Use the `html` skill for this — acquire it before building the HTML. The HTML timeline should include:
- A sprint-by-sprint visual layout with cards for each sprint
- Expandable work items within each sprint
- Visual dependency arrows or indicators between sprints
- Milestone markers
- Critical path highlighting
- Responsive design that works on desktop and mobile
- Clean, professional styling

Present the HTML file as a deliverable using `present_files`.

## Output Format (STRICT)

Format everything as structured sections with tables and numbered lists. Do not write prose paragraphs. If the document doesn't contain enough detail for a section, say so explicitly rather than inventing content.

```
## 1. PROJECT SUMMARY
[2-3 sentences]

## 2. SPRINT PLAN

### SPRINT 1 — [Sprint name/theme]
- **Dates/duration**: [estimated start and end, or "Week X-Y"]
- **Goal**: [one sentence]

**Work items:**
1. [Task description] | Owner: [role/Unassigned] | Dependencies: [none/Sprint X, Task Y] | Effort: [S/M/L]
2. [Task description] | Owner: [role/Unassigned] | Dependencies: [none/Sprint X, Task Y] | Effort: [S/M/L]

- **Milestones/deliverables**: [list or "None specified"]
- **Risks/blockers**: [list or "None visible"]

### SPRINT 2 — [Sprint name/theme]
[Same structure]

[Continue for all sprints]

## 3. DEPENDENCY MAP
1. [Task A] → depends on → [Task B] (Sprint X)
2. [Task C] → depends on → [Task D] (Sprint Y)

## 4. CRITICAL PATH
1. [Task 1] (Sprint 1)
2. [Task 2] (Sprint 2)
3. [Task 3] (Sprint 3)
[Continue — the longest dependent chain]

## 5. GAPS AND ASSUMPTIONS

| # | Type | Item | Assumption/Gap | Impact |
|---|------|------|-----------------|--------|
| 1 | [Assumption/Gap/Ambiguity] | [what] | [details] | [how it affects the timeline] |

## 6. TIMELINE VISUALIZATION

[Text-based Gantt-style view with | characters, ★ for milestones, ↑↓ for dependencies]
```

After the structured output, generate and present the interactive HTML timeline.

## Constraints

- **Don't invent content.** If the document doesn't contain enough detail for a section, say so explicitly. Do not fabricate dates, owners, effort estimates, or scope boundaries.
- **Use what's in the document.** Extract owners, dates, and effort from the document when available. Only mark as "Unassigned" or estimate as S/M/L when the document doesn't specify.
- **Structured output only.** Use tables and numbered lists. No prose paragraphs.
- **Flag gaps explicitly.** The gaps and assumptions section is mandatory — every assumption and ambiguity must be called out.
- **Show dependencies clearly.** Every cross-sprint dependency must appear in the dependency map.
- **Critical path is required.** Identify the longest dependent chain even if it's short.
- **Text Gantt before HTML.** Produce the text-based Gantt first, then generate the HTML timeline from it.
- **HTML timeline is a deliverable.** The interactive HTML file must be presented to the user with `present_files`.

## Failure Handling

- If no document is provided, ask the user to attach or paste one.
- If the document is too vague to break into sprints, say so and produce what you can with a note about insufficient detail.
- If the document has no dates, use relative week numbering (Week 1-2, Week 3-4, etc.) and note the assumption.
- If the document has no clear deliverables or milestones, state "No milestones specified in the document" rather than inventing them.
- If the document is in a language other than English, process it in that language and produce the output in the same language unless the user specifies otherwise.

## Examples

**Example 1**
User: /project-timeline [attaches a statement of work for a website redesign]

Expected output: A six-section structured sprint plan with 4-6 sprints, work items extracted from the SOW, owners from the document, dependencies mapped, critical path identified, gaps flagged (e.g., missing QA timeline), text Gantt, and an interactive HTML timeline presented as a deliverable.

**Example 2**
User: /project-timeline [attaches meeting notes from a project kickoff]

Expected output: Same six-section structure. Sprints inferred from the work discussed. Owners from attendees who claimed work. Many items likely "Unassigned" with gaps flagged. Text Gantt and interactive HTML timeline presented.
