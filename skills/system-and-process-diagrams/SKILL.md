---
name: system-and-process-diagrams
description: Turns a description, a codebase, or pasted Mermaid into a polished, validated, interactive diagram, delivered as one standalone HTML file with inline SVG, dark and light themes, and PNG/JPEG/WebP/SVG/WebM export. Five diagram types — architecture (components, services, cloud, security and network topology), workflow (processes, approvals, runbooks, CI/CD), sequence (API call chains, request lifecycles, back-and-forth between parties), dataflow (pipelines, ETL/ELT, lineage, where money or documents go) and lifecycle (state machines, order or application status). Use it whenever the user asks to diagram, draw, map or visualize a system, architecture, process, flow, pipeline or set of states, wants to convert or beautify a Mermaid flowchart, sequenceDiagram or stateDiagram, or describes an everyday plan or process with steps, parts or states. Not for numeric charts or dashboards.
license: MIT (see NOTICE.md at the repository root)
---

# System and Process Diagrams

The diagram is typed JSON, rendered and checked by the bundled engine (Archify) into a standalone HTML file. The quality comes from the gates: schema validation, layout and route checks, and a real-browser check. A diagram is delivered only when `finalize` passes. Output is static unless the user asks for motion.

## Setup

- **Engine path.** Every command below runs `bin/archify.mjs` from this skill's folder. Replace it with that file's absolute path, or its path relative to the working directory. Input and output paths resolve from the working directory. Node 18+ is the only requirement, with no install.
- **Output folder.** Unless the user names another location, give each new diagram request its own folder `.archify/<type>-<slug>-<YYYYMMDD-HHMMSS>/` in the working directory (local time, chosen once when the request starts). Keep `candidate.json` and `<slug>.html` in it, set `meta.output` to that relative HTML path, and reuse the folder for every repair rerun. A later request gets a new folder, so earlier versions stay intact.
- **Diagnosis.** If setup looks broken, run `node bin/archify.mjs doctor` and `node bin/archify.mjs demo <output-directory>`.
- **No shell.** Hand-place architecture SVG into `assets/template.html`, use the CSS semantic classes rather than inline colors, and follow the visual review contract in `references/delivery-contract.md`.

## Choose the type

| Type | Use for | Schema | Example |
|---|---|---|---|
| `architecture` | Components, services, cloud/security boundaries, infrastructure; what something everyday is made of | `schemas/architecture.schema.json` | Systems, services, libraries, CLI repos: `examples/web-app.architecture.json`. Deployment repos: `examples/production-deployment.architecture.json` |
| `workflow` | Processes, approval gates, tool calls, runbooks, CI/CD; plans and step-by-step life processes | `schemas/workflow.schema.json` | `examples/agent-tool-call.workflow.json` |
| `sequence` | API call chains, request lifecycles, async traces, returns; back-and-forth between people | `schemas/sequence.schema.json` | `examples/cache-miss-request.sequence.json` |
| `dataflow` | Pipelines, ETL/ELT, lineage, governance, consumers; where money or documents go | `schemas/dataflow.schema.json` | `examples/product-analytics.dataflow.json` |
| `lifecycle` | State/status transitions, retries, waiting and terminal states; where an application or order stands | `schemas/lifecycle.schema.json` | `examples/deployment-release.lifecycle.json` |

- **Ambiguous?** Run `node bin/archify.mjs guide "<scenario>" --json`. Its scenario examples are structural references, not facts to copy.
- **Everyday subjects** use the same five types and semantic node types, named for the reader: everyday `icon` values and `meta.legend` labels, as in [Node icons](references/authoring-contract.md#node-icons). Ask for missing personal facts. Never invent dates, amounts or rules.
- **Mermaid input.** Read it for topology and meaning, then author fresh JSON. Don't carry over Mermaid styling.
  - `flowchart` / `graph` → `workflow`, or `architecture` for a component map.
  - `sequenceDiagram` → `sequence`. Participants become semantic participants; arrows become messages.
  - `stateDiagram` → `lifecycle`. States and transitions keep their meaning, not their style.
- **Real codebase.** Read [Repository authoring](references/repository-authoring.md) while tracing the requested behavior, and attach source evidence from the first draft.
- **Existing JSON supplied by the user.** Treat it as a frozen candidate: go straight to `finalize` (step 4) as one invocation. For repair, follow step 5.

## Author and deliver

Read a branch reference only when its stated trigger applies. Before the first candidate, use the authoring references and the relevant repository source, not the engine's implementation. Inspect the implementation only if diagnostics stay unactionable after focused repairs.

1. **Pick the type** from the question.
2. **Read in bounded batches.** Use the exact schema and example paths in the table; don't list directories. Read [Authoring defaults](references/authoring-defaults.md) and the type's example in one batch, separate from project documents and complete schemas so neither is truncated; recover any missing section before writing.
   - Architecture: use the matching example above.
   - Sequence, Dataflow, Lifecycle: also read the type's schema and `schemas/common.schema.json`.
   - Read the schema definition before choosing any new field, enum or constrained text, especially boundary kinds.
   - Examples teach shape, not facts. Use fresh IDs, wording and layout.
   - Go straight to the candidate: no preliminary `help`, `doctor`, starter validation, temporary diagrams or output-path listing.
   - Brand marks: query them only when a mark is explicitly requested. For an unknown mark with a user-provided URL, read [Brand marks](references/brand-marks.md).
3. **Write the complete candidate** once the requested scope (and, for a codebase, the source evidence) is covered. Don't plan coordinates in prose.
   - For Architecture, choose abstraction and connected placement with Authoring defaults before coordinates: show the main user journey and necessary branches, keep control roles and behavior-changing conditions, and leave room for the real relationship labels.
   - No count of nodes, relationships, sources, views, cards or boundaries is a target or a ceiling.
   - Use automatic routes first. Add explicit routing only for a necessary branch, a return, supplied geometry or a measured repair.
   - Set `meta.quality_profile` to `"showcase"` unless the user asks for dense `standard`.
4. **Run `finalize` directly** on the first complete candidate, and keep the candidate unchanged while it runs. Its first gate is showcase validation, so no separate pre-validation is needed.

   ```bash
   node bin/archify.mjs finalize <type> <candidate.json> <output.html> --quality showcase --json
   # repository-backed:
   node bin/archify.mjs finalize <type> <candidate.json> <output.html> --repo-root <repo-root> --quality showcase --json
   ```

   A passing receipt proves the `validate`, `deliver`, strict `check` and real-browser `browser-check` gates. Use its compact summary. Run standalone commands only for a separate request or to diagnose a specific failure.
5. **A non-zero exit is never success.** Read the compact stdout or `evidence.summaryReceipt`, then [repair the failed gate](references/delivery-contract.md#failed-finalize-and-candidate-repair) within its repair limit. Preserve the requested meaning and source evidence. Edit the connected neighborhood and rerun the complete step-4 command.
   - Several tangled Architecture routes: [Architecture layout repair](references/architecture-layout-repair.md).
   - Measured field or geometry failures: [Authoring contract](references/authoring-contract.md).
   - Workflow viewport overflow: [Workflow viewport repair](references/authoring-contract.md#workflow-viewport-repair), before the next layout edit.

## After a passing finalize

`finalize` stops at the first failing gate. Its compact stdout and `<output-stem>.finalize-summary.json` are the evidence. A passing run creates no screenshots and reports `visualReview: "not-requested"`.

- **Resolved crossovers (Architecture).** When the receipt reports `visualReviewRecommendation.signals.resolvedCrossovers`, copy the candidate aside and apply the hints in one edit that changes only node positions and sizes. Every node, relationship (including `from` and `to`), label and source stays as it was. Rerun the complete `finalize` once with `--out-dir <folder>/review-2`, because the previous HTML already owns its browser evidence. If that run fails or reports more crossings, restore the copy and finalize it with `--out-dir <folder>/review-3`. No second placement round. Hints about extra bends alone are optional.
- **Sequence width.** When `layoutReviewRecommendation.action` is `inspect-sequence-width`, follow [Sequence width review](references/delivery-contract.md#sequence-width-review) before handing off a new Sequence.
- **Perceptual review** is optional for ordinary generation, including a newly positioned Architecture, and `visualReviewRecommendation` is advisory. When the user asks for visual review, during development audits, or for a concrete route or browser concern, use [Optional capture evidence](references/delivery-contract.md#optional-capture-evidence) with `--out-dir <folder>/visual-check`. Inspect the captures before claiming visual quality; otherwise report automated checks only.
- **Everything else** — failed gates, standalone commands, provenance and recovery, repeat delivery, exports, opening — is in the [Delivery contract](references/delivery-contract.md). Recovery runs `deliver` → strict provenance `check` → `browser-check`; captures require strict provenance. For an explicitly requested preview or live desktop loop, see [Optional opening](references/delivery-contract.md#optional-opening).

## Viewer features (opt-in)

`meta.animation: "trace"` turns on motion. Read `references/viewer-runtime.md` only when the user explicitly asks for Share Cards, Route/Reach cards, motion, deep links, presentation, search/focus or another viewer feature.

## Report back

Give the checked HTML as an absolute path, the diagram type, the validation summary, the specification/artifact receipt, the browser-evidence status and a truthful visual-review status. Report artifact checks, browser evidence, captures and actual perceptual review as separate results. Never claim success for a non-zero command, or a visual inspection you didn't perform.
