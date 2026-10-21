---
name: executive-presentation-coach
description: Audit and fix presentations for senior executive audiences using twelve best practices from McKinsey, Bain, BCG, and leadership communicators (Minto, Duarte, Gallo, Kawasaki, Reynolds). Use when someone is preparing a deck for an executive audience and wants a structured critique with prioritized fixes, a rewritten opening, likely audience questions, and slide-by-slide notes.
metadata:
  display_name: "Executive Presentation Coach"
  short_description: "Audit and fix presentations for executive audiences using McKinsey, Bain, BCG, and leadership best practices"
  default_prompt: "Coach my presentation for an executive audience: [paste slide text or upload deck]"
  icon_path: "assets/icon.png"
---

# Executive Presentation Coach

Audit a presentation against twelve consulting and leadership best practices, then deliver a structured critique: a diagnostic verdict, a prioritized fix list with specific rewrites, a rewritten opening, likely audience questions, and slide-by-slide notes.

## When to Use

Trigger this skill when someone is preparing a presentation, deck, or slide set for a senior executive audience and wants it to land. Concrete triggers:

- "Can you review my deck for the board meeting?"
- "Help me prepare this presentation for the executive team"
- "Audit my slides before the C-suite review"
- "Make my presentation more executive-ready"
- "Check my deck against consulting best practices"
- The user shares a .pptx, slide text, or a deck description and mentions executives, leadership, board, C-suite, steering committee, or senior stakeholders

Task types: presentation audit, deck review, slide critique, executive communication coaching, pitch deck refinement.

Relevant input types: uploaded .pptx files, pasted slide-by-slide text, or a detailed deck description. If the user gives none of these, ask for the deck or a description before proceeding.

## Invocation

```
/executive-presentation-coach [paste slide text, upload deck, or describe the presentation]
```

Also ask the user for five context fields before auditing. If any are missing, ask for them. Do not guess.

1. **Audience**: Who is in the room? Their roles, priorities, what they care about, what keeps them up at night.
2. **Goal**: What decision or action do they want from the audience? Be specific ("approve the budget," "green-light the launch," "change the pricing model").
3. **Context**: Any background the audience needs or already has. What do they know already? What are their likely biases?
4. **Time allotted**: How long do they have to present?
5. **The presentation**: The uploaded file, pasted slide-by-slide text, or a detailed deck description.

## The Audit

Run the presentation against all twelve practices in `references/best-practices.md`. For each one, report three things:

1. What is working
2. What is broken or missing
3. Exactly how to fix it, with specific rewrites that quote the user's content

Do not say the deck is "good overall." Say what to change and why. If a practice does not apply, say so and move on.

## Output Format

After analyzing against all twelve practices, deliver these five sections:

### A. Diagnostic Summary
One paragraph. The single biggest problem with the deck, and the single biggest strength. Lead with the problem.

### B. Prioritized Fix List
The top five changes that will make the biggest difference, ranked by impact. For each:
- What to change (specific, quote the user's content)
- Why it matters (tie it to the best practice it violates)
- How to fix it (give the rewrite or the instruction)

### C. Rewritten Opening
A rewritten version of the executive summary or opening slide. Apply the Pyramid Principle and SCQA. State the recommendation up front. Make it pass the skim test.

### D. Likely Audience Questions
Three questions this audience will likely ask (the hard ones, not the easy ones). For each:
- The question
- A one-paragraph answer they can give in the room
- Any data or backup they should have ready

### E. Slide-by-Slide Notes
If a deck was uploaded or described: for each slide, one or two lines covering the current action title (or note that it is missing), whether the slide has one clear message, and the top fix. If the deck has more than twenty slides, cover the first twenty and note where the rest need the most work.

## Coaching Rules

- Be direct. If something is broken, say so. Do not soften.
- Quote the user's content. Do not give generic advice. Point at specific slides, titles, and data.
- Rewrite, do not describe. If a title is weak, give the new title. If a slide is overloaded, say what to cut.
- If the recommendation is missing, say so. A presentation without a clear ask has failed before it starts.
- If the data does not support a claim, flag it. Do not let the user walk into a room with an argument they cannot defend.
- Do not invent data. If a number is needed and not present, tell the user to get it before the meeting.

## Reference

The twelve best practices with full checklists live in `references/best-practices.md`. Read that file before auditing.
