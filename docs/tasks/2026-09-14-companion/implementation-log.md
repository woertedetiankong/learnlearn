# Implementation Log

> Created: 2026-09-14

## Task

Implement the accepted pi companion plan, including ABCD questions and independent follow-up chat.

## Assumptions

- Local Markdown directories are the first knowledge provider; no Obsidian-specific integration is necessary.
- Menu configuration changes become user defaults; command and shortcut power toggles remain session-only unless explicitly saved.

## Initial Approach

Use supported pi extension events, independent model-registry calls, a widget and optional passive overlay, with filesystem sources behind interfaces.

## Log

### 2026-09-14

- Installed pi 0.85.1 uses the @earendil-works packages. Its TUI is an interface with TuiMainScreen as the concrete regular-terminal implementation. Production code consumes the host TUI; tests instantiate the real implementation.
- Passive overlays do not allocate a side column. Default to the above-editor widget; only enable right overlay at 120 columns and 30 rows. This preserves the approved scope without modifying pi core.
- Use modelRegistry.complete with separate bounded context. Event handlers schedule background work without awaiting it; cancellation generations protect against providers returning after an abort.
- Knowledge questions require one validated correct option; judgment questions deliberately omit a correct answer. Models cannot cite source IDs not supplied by the source adapter.
- The real-PTY favorite test exposed that a focused chat overlay covers native select/input dialogs. Temporarily hide the chat overlay while saving, then restore visibility and focus. Expanded the smoke test to verify the saved follow-up transcript.
- Task start now requests a fresh card, including when a prior task left a card visible. Pinning and interaction still suppress replacement.
- Indexing is bounded to 5000 files and 32 MiB, with per-file size limits and cancellation checks. Prompt excerpts are bounded and no tool outputs or complete sessions are sent to the companion model.
- Work remains uncommitted in the repository. The project-local installation is recorded in ignored .pi/settings.json; no global package installation, credential edits or publication occurred.

- Layout feedback follow-up: the user reported Enter did not save; the actual user configuration already contained overlay. Added a current-option marker and success notification, plus persistent terminal-size fallback feedback. Extended the PTY smoke to assert Enter writes the setting and reopening the menu reflects it.

- Reference-driven refinement: default top-right overlay, full frame and structured metadata; lower fallback threshold to 96 columns / 22 rows while retaining existing saved preferences. Both passive and focused views share the card renderer and width.
- Separate browsing from chat: answer in place, t opens follow-up, Esc returns one level at a time. Added full-row selection, numeric quick answers, scrolling and n/s/p actions without capturing the main editor's normal letters.
- Stop sending tool-completion telemetry as card-generation context. Meta/refusal cards and malformed task-card responses use explicitly labeled curated warmups. Wander mode retains selected-source semantics and does not silently switch topics.
- Visual inspection caught ellipses in border rules; border padding now clips without ellipses. Long-content testing caught the last line being replaced by the scroll indicator; the indicator now reserves its own row.
- PTY tests use explicit Kitty escape events for two-level dismissal, avoiding ambiguity from adjacent lone escape bytes. UTF-8 decoding is incremental. Type checks, 19 tests, and real-pi offline flow are the completion gates.

### 2026-09-15

- Added required phase, goal and constraints for generated quizzes; judgment choices include a current-scenario verdict and personalized feedback. Chosen feedback is rendered before the general explanation and scrolls into view.
- A separate model review checks semantic consistency, including emergency versus prevention, unique-answer validity, and contradictory per-choice explanations. Strict review parsing fails closed; one rewrite and re-review are allowed within the existing 45-second gate. This increases quiz requests to two normally and four at most, with no extra calls for text cards.
- Persistent failures fall back to labeled curated questions only in task mode. Wander mode preserves the current card and selected-source semantics. Added regressions for rejected drafts, review feedback propagation, malformed reports, bounded retries and cancellation.
