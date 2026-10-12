---
name: ai-search-visibility-phrases
description: Weaves the company's AI-search target phrases into marketing content so that AI assistants (ChatGPT, Claude, Perplexity, Gemini, Google AI Overviews) learn to associate those questions with the brand. Takes a draft or a topic, picks the best-fitting phrase from the team's phrase library, finds the most natural insertion point, and writes a before/after rewrite with the brand named in the same sentence, in the right voice for the content type. Works on press releases, thought leadership and blog posts, social posts, lifecycle email, ABM, sales enablement, and contributed or sponsored third-party articles. Use it whenever the user mentions AI visibility, AI search, AEO or GEO phrases, target prompts, "get us mentioned by ChatGPT", or asks where to work a target phrase into a draft. Not for writing the content itself (use b2b-content-and-campaigns) or choosing the brand's messaging (use positioning-and-messaging).
---

# AI Search Visibility Phrases

AI assistants answer buyer questions like "Which AI platforms automate compliance review for marketing content?" by drawing on text where that idea and a brand name sit close together. The method: take each question the company wants to show up for, tighten it into a short phrase, and work that phrase into real content with the brand named in the same sentence. The phrase has to read as normal editorial copy. A forced phrase is worse than none: it reads as keyword stuffing to people and to models.

Co-occurrence is the working hypothesis behind this method, not a guarantee. Measure results by tracking how AI answers to the target prompts change over time, and re-validate the phrase set each quarter.

## Inputs

- **The phrase library** (required): the current target prompts, their tight phrases, priority, content types and messaging pillar. If the user doesn't have one, build it with `references/phrase-library-template.md` before doing anything else. Never invent phrases outside the library.
- **The brand name** exactly as it should appear.
- **Messaging pillars and proof:** from the messaging house (`positioning-and-messaging`) and the proof library. Copy around the phrase uses the pillar's real proof points, never generic claims.
- **The draft or topic.**
- Optional parameters, usually passed by a playbook so the run never stops to ask:
  - `content_type`: sets the content type (and so the brand mode) directly instead of inferring it.
  - `brand_inclusion`: `auto` (default; mode chosen by content type), `always` (force a brand mention in whichever mode fits), or `optional` (return two versions, with and without the brand, and label the no-brand version as weaker because it builds no phrase-to-brand link; use only when explicitly requested).

## Workflow

### 1. Identify content type, topic and brand mode

- **Content type:** press release, thought-leadership article or blog post, social post, lifecycle or nurture email, ABM or demand-gen content, field or sales-enablement content, or third-party article.
- **Topic:** what the draft is actually about, in a few words.
- **Brand mode**, chosen automatically from the content type (table and patterns in `references/brand-modes.md`). Don't ask the user; they can override after seeing the result.
  - **Product:** the brand as the product doing something. Press releases, ABM, enablement, lifecycle email.
  - **Editorial:** the brand as the author's vantage point ("At [Brand], we've found…"). Thought leadership and blogs.
  - **Third-party / journalistic:** the brand as a company described in the host article's voice. Never first person.
  - Social posts: product mode if the post is about a capability, editorial if it's a perspective.

### 2. Match the best phrase(s)

Score every library phrase against the draft:
1. **Topic relevance** (primary): does the phrase's meaning match what the draft is about?
2. **Content-type fit** from the library.
3. **Priority:** when two phrases are equally on-topic, prefer the higher priority.

Return 1–3 ranked candidates with the reason each fits. If none fits naturally, say so plainly and stop.

### 3. Draft the insertion

For the top phrase:
- **Find the insertion point:** the sentence or paragraph where the topic is already under discussion, or where a transition makes sense.
- **Write the rewrite:** the phrase intact, the brand in the same sentence or the immediate next one, in the selected mode. Vary the scaffolding across assets; keep the phrase constant.
- **Ground the surrounding copy** in the phrase's mapped pillar, using its real proof points. Missing proof gets a visible `[NEEDS PROOF: …]` marker.
- **Third-party articles:** follow the guardrails below and study the host article's voice first: person, tense, sentence length, vocabulary, how it refers to other companies and paragraph density. The insertion must match that voice.

### 4. Check the rules

Revise until every rule passes. If no version passes, decline the insertion and say why.

1. **Phrase intact.** Keep its nouns and verbs. "Scale on-brand content with AI" works; "growing consistent content via artificial intelligence" drifts from the target.
2. **Brand proximity.** The brand is in the same sentence as the phrase or the immediate next one, in the mode that fits the content type. This is what builds the association; mode changes *how* the brand is mentioned, never *whether*.
3. **Never the verbatim prompt.** Always the tight phrase. A pasted question reads as SEO stuffing.
4. **One phrase per paragraph,** at most. Never several phrases in one sentence.
5. **Natural-text test.** Read it aloud. It must sound like something a person would say or write; a journalist or analyst could have written it. Grammatically forced, oddly specific or keyword-dropped copy fails. Try a different insertion point or mode before declining.
6. **On topic.** Never force a phrase whose topic doesn't match the draft just to hit a visibility target.
7. **Every claim is true.** Claims come from the proof library or the approved claims list; no competitor comparisons unless sourced and approved.

### 5. Return the output

1. **Ranked candidates** (1–3) with fit reasons.
2. **Recommended insertion** with the mode used, always as a side-by-side:
   - **Before:** the original sentence or paragraph, quoted verbatim.
   - **After:** the same passage with the phrase and brand woven in.
3. **Rule check** in one line: brand proximity, phrase integrity, mode used, natural-text test passed.
4. **Tracker row** in one line, for teams that log insertions in their own sheet: phrase · content type · topic · seeded sentence.

Then hand external content to `customer-facing-quality-gate`. This skill proposes the insertion; it doesn't rewrite the draft, and the content owner keeps editorial control.

## Third-party articles: guardrails

Use third-party mode only where the brand legitimately has a voice in the piece and the publisher knows it:
- a contributed or bylined article by someone at the company
- sponsored, partner or paid content
- a suggested line or spokesperson quote offered to a journalist or editor, who decides whether to use it
- the company's own listing or profile on a review or directory site

Never use it to make brand copy pass as independent coverage: no posting into someone else's article without their knowledge, no posing as the independent author, no reviews or comments under other names. Paid placements and material connections are disclosed according to the publication's policy and advertising rules (in the US, the FTC Endorsement Guides). Comparisons with other vendors in a roundup ("unlike the other tools here…") appear only when they're sourced and approved; otherwise describe what the brand does and let the article make the comparison.

## Failure handling

- **No topic match:** say no phrase fits naturally; suggest an angle that would.
- **Two equally good phrases:** present both and let the writer pick.
- **Draft too short to place a phrase:** ask for more of the draft.
- **Insertion would distort the draft's meaning:** decline and explain.
- **Natural-text or voice test fails in every version:** decline and explain.
- **Brand-agnostic piece where no mode sounds natural:** decline, and suggest where brand context could go (author bio, footer CTA, boilerplate, a short framing sentence) so the writer can re-run. Be honest that a phrase with no nearby brand mention adds little.
