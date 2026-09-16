# Implementation Log

> Created: 2026-09-15

## Decisions

### 2026-09-15 — Continuity and cost

- Keep at most 20 session entries, each owning its answer, draft, scroll position and cancellable chat request. Background replies attach to their original entry, never to the newly viewed card.
- Keep at most one automatic card waiting for the user. Stop automatic generation while it waits; manual next consumes newer history before requesting another card.
- Add summary as the default layout while respecting explicit widget/overlay choices. Settings writes carry only edited fields and an explicit destination.
- Economical mode uses text cards at a slower automatic cadence; it does not skip quiz correctness review. No real-provider quality claims from offline tests.
- Work remains uncommitted in the existing checkout.

### 2026-09-15 — Verified continuity and input behavior

- Type checks and 39 offline tests pass, including entry-owned late replies, retries without duplicate questions, bounded history cancellation, small-screen summary, scoped settings and the knowledge wizard.
- Use `[` for previous-card navigation because B must remain a quiz answer key. D expands detail only after an answer is revealed.
- Card scrolling may place an answer heading at the top even when fewer lines remain than the viewport; chat scrolling retains the latest full viewport. This avoids pushing the correct answer below the original question again.
- Native pi menu verification is still in progress; the automated selector sequence needs fresh UI state between nested dialogs. Final completion requires a passing real-terminal run.

### 2026-09-15 — Native terminal completion

- Native pi testing exposed stale selector focus after a passive overlay was mounted during settings. Menus explicitly suspend widgets for their full lifetime; settings remounts remain suspended until menu exit. Regression coverage verifies this lifecycle.
- Real pi smoke passes summary rendering, quiz selection, background reply after dismissal, favorites, main completion, power toggles, scoped layout persistence/readback, and returning from history to the original conversation.
- Tiny focused panels use compact footer hints and retain an exit control; manual card scrolling no longer gets forced back to the selected option.
- README and JSON examples were rewritten for the final controls and persistence rules. Earlier handoff remains a historical snapshot; the restart pointer and task index identify this milestone as current. No wiki exists, so durable guidance stays in README.

### 2026-09-15 — Concrete examples and ASCII explanations

- Keep diagrams inside the existing answer Markdown so parsing, history and favorites remain compatible; knowledge-card diagrams appear in expanded detail, follow-up diagrams appear in chat.
- Preserve fenced-block spacing. If a block exceeds the viewport, keep prose readable and show a resize/favorite hint; never wrap connectors into a misleading diagram.
- New explanation rules ask for grounded examples and short vertical flows where useful. Validation: type check, 45 offline tests, real-pi smoke and inspected diagram preview pass; no real-provider quality claim.

### 2026-09-15 — Explain behavior and conditions before detail

- The actual “拒绝再次委派的文本” example showed that prompt-only plain-language advice could still produce jargon repetition. New generation requires a structured lesson with summary, scope and concrete example; optional diagrams remain raw text until rendering/export. Length failures trigger a bounded rewrite, never silent truncation of conditions. Legacy cards without a lesson remain readable.
- Display the short lesson by default, move extra explanation to `d`, and avoid repeating the correct option explanation when the summary already fills that role. Short-window footers expose detail and feedback after answering.
- Targeted clarification is a current-card conversation action, not a learning preference. Cancellation, blank input and stale dialogs send nothing; busy replies are preserved. No pending card is discarded just because a user asks for a word definition.
- Split card-only formatting rules from follow-up rules so a term-definition question does not inherit a requirement to output a full lesson object. The optional sequential article-learning feature is outside this clarity slice and remains follow-up work.

- Validation for this slice: type check and 52 tests pass; offline native-pi smoke passes including the nested feedback term-input workflow. Actual component previews confirm default examples/diagrams and adjacent scope. No real-provider semantic quality claim; work remains uncommitted.
