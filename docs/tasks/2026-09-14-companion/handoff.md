---
title: Handoff 2026-09-14 - pi Curiosity Companion
status: Complete
updated: 2026-09-15
---

# Handoff

## Summary

Implemented a pi package with persistent text/ABCD cards, isolated follow-up chat, configurable Markdown collections, and explicit favorites. Main task execution remains independent.

## Current State

Visual and interaction refinement implemented and verified with type checks, 23 automated tests, and an offline real-pi PTY workflow.

## Git And Persistent State

- Branch: master; initial implementation is uncommitted, no PR or remote publication.
- Persistent state: project-local package installation in ignored .pi/settings.json; ignored .pi/companion.json provides an unselected software-design example collection. Dependencies installed in node_modules.

## Key Decisions

- Use pi 0.85.1 extension APIs; default passive top-right overlay with full borders and a 96-column / 22-row fallback threshold; existing saved layouts are respected.
- Separate model contexts and cancellable requests; no main-session injection, tool execution, or automatic knowledge writes.
- Collections map names to multiple directories; user/project settings merge by collection name. Model and collection selection are independent of card format.
- Native save dialogs temporarily hide the discussion overlay; the actual PTY smoke covers this focus interaction.
- Focused cards use full-row selection, in-place reveal, n/s/p actions and explicit t-to-chat. Esc returns from chat to card, then to the main editor.
- AI quiz generation requires scenario and per-choice judgments, then a separate semantic review. One rewrite maximum, within the existing request timeout; failed task quizzes use curated fallback, wander preserves the current card.
- Chosen-option feedback appears before the overall explanation and is scrolled into view on answer.
- Task card generation excludes tool status metadata and substitutes labeled curated warmups for meta/refusal or malformed output.
- Layout selection marks the current option and confirms saving; undersized terminals explain why the saved overlay layout temporarily appears above the editor.

## Validation

- `npm run check`: passed.
- Actual component SVG previews rendered and visually inspected for borders, Chinese wrapping, selection and answer layout.
- `npm test`: 23 passed, including real TUI focus, cadence, cancellation, knowledge refresh, favorites, and non-TUI inactivity.
- `python3 test/smoke.py`: actual pi package discovery, quiz during main run, B confirmation, independent follow-up, saved transcript, main completion, power toggles, and Enter layout persistence with current-option readback; offline model, no external service calls.
- `npm pack --dry-run`: package includes extension sources, examples and README, excludes test model and local settings.
- `pi list --approve`: project package resolves to this repository.

## Restart Verify

```bash
npm run check && npm test  # expected: clean type check and 23 passes; mismatch means source/dependency regression
python3 test/smoke.py  # expected: PASS for actual pi workflow; mismatch means host API or terminal integration changed
pi list --approve  # expected: this repository under Project packages; mismatch means local installation missing
```

## Known Risks

- Real provider answer quality and provider-specific concurrency have not been assessed; integration tests use an offline provider.
- Terminal support for Ctrl+Alt shortcuts varies; slash commands remain available. Right overlay may obscure output by design.

## Docs And Wiki

- Created README with setup, settings, sources, limits, extension interfaces and validation commands.
- No wiki existed; reusable knowledge is in README instead.

## Next Steps

1. Use pi in this repository and select the example collection in /companion; point additional collections to preferred project or Obsidian directories.
2. Evaluate pacing and answer quality with the user's chosen real model before publishing a release.

## Implementation Log

- [implementation-log.md](implementation-log.md) records API constraints, layout and cancellation decisions, and the save-dialog issue found by integration testing.
