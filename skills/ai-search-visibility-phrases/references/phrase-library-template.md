# Phrase Library Template

The phrase library is the only source of target phrases. Keep it in the project's sources of truth beside the proof library, re-validate it each quarter, and update it in place, so the skill always uses the current set. Treat it as internal: it reveals which buyer questions the company is not yet winning.

## Building it

1. **Pick the target prompts.** The questions buyers ask AI assistants where the company should appear but doesn't yet, or appears weakly. Base the list on tracked AI answers (each prompt run across the main assistants, recording whether and how the brand appears), not on guesses. Typically 10–20 prompts.
2. **Prioritize.** High for the biggest gaps on the most commercially important questions, then Medium and Low. List in priority order.
3. **Turn each prompt into a tight phrase:**
   1. Strip the question word ("Which", "How", "What are", "How can"). What's left is the semantic core.
   2. Tighten to a dense, quotable phrase of 5–9 words.
   3. Check it can sit naturally in a sentence beside the brand name.

   Example: "Which AI platforms automate compliance and legal review for marketing content?" → "automate compliance and legal review for marketing content".
4. **Map each phrase** to the content types where it fits, the brand mode for each, and the messaging pillar whose proof points support it (from the messaging house in `positioning-and-messaging`; proof points from the proof library).
5. **List topic signals:** the words and themes in a draft that suggest the phrase fits.

## Entry format

```
### [#]. [Short name] — [HIGH | MEDIUM | LOW] priority ([why: gap size, launch tie-in])

| Field | Value |
|---|---|
| Target prompt | [the full buyer question; never pasted into content] |
| Tight phrase | "...[5–9 word phrase]..." |
| Content types | [e.g. press releases, thought leadership, social posts, third-party articles] |
| Brand mode | [mode per content type, e.g. Product (press releases) / Editorial (thought leadership)] |
| Pillar mapping | [pillar name(s) from the messaging house] |
| Topic signals | [comma-separated themes that indicate a fit] |
```

## Header to keep at the top

```
# [Quarter] Phrase Library
Valid through: [date]. Owner: [name]. Last validated against tracked AI answers: [date].
Brand name as written: [exact form, e.g. capitalization]
```

If the library is past its "valid through" date, tell the user it may be stale, and ask whether to proceed with it.
