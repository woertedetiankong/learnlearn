---
title: Handoff 2026-09-15 - Companion UX
status: Complete
updated: 2026-09-15
supersedes: ../2026-09-14-companion/handoff.md
---

# Handoff

## Summary

Completed the continuity UX and explanation-clarity follow-up: short structured lessons, explicit scope, examples/diagrams visible by default, optional detail, and targeted clarification. History, background chat, scoped settings and knowledge onboarding remain available.

## Current State

Implementation is complete with 52 automated tests and an offline real-pi terminal workflow passing. Real-provider content quality remains an empirical follow-up.

## Git And Persistent State

- Existing master checkout; files remain uncommitted. No publication or global installation.
- Generated UI previews and smoke transcript are under ignored artifacts; smoke uses disposable configuration and an offline provider.

## Key Decisions

- Each history entry owns its chat request, messages, draft and reading position. Dismissal and navigation preserve them; eviction, disable, branch/session reset cancel relevant requests.
- One waiting automatic card caps background requests until consumed. History and learning preferences are session-local; favorites provide durable storage.
- Settings write only changed fields to the explicitly chosen scope. Native menus suspend widgets to prevent stale selector focus during layout changes.
- Generated cards require lesson.summary/scope/example; diagram is optional raw text. Parsing retains support for legacy cards without lessons. Oversized lesson text triggers repair rather than condition-truncation. UI and favorites consume the same fields.
- Targeted clarification sends a card-specific question without changing preferences or pending cards; cancellation, empty input, stale-card dialogs and busy replies do not send duplicate requests.
- Summary is the default; explicit saved layouts remain respected. Economy uses text and a minimum 600-second cadence without bypassing quiz review.

## Cross-Module References

- Builds on [initial companion](../2026-09-14-companion/handoff.md).
- Runtime contracts and commands: [README](../../../README.md).
- Scope and acceptance criteria: [task brief](task-brief.md).

## Validation

- `npm run check`: passes; `npm test`: 52 tests pass.
- `python3 test/smoke.py`: PASS for native menus, summary, quiz, background chat, favorites, history, settings readback and the nested word-definition feedback/input flow.
- Actual component SVG previews inspected for explicit answers, adjacent scope and visible examples/diagrams. Diagram indentation, width fallback, legacy cards and Markdown exports have regression coverage.
- `npm pack --dry-run`: includes menus module and excludes the test provider.

## Restart Verify

```bash
npm run check && npm test  # expected 52 passes; mismatch means implementation or dependency drift
python3 test/smoke.py  # expected PASS; failure writes artifacts/smoke-transcript.txt for diagnosis
```

## Next Steps

1. Restart pi to load changes; select summary in settings if a previous explicit layout is saved.
2. Observe real-model clarity, scope accuracy and repetition using actual cards; offline tests establish structure and interaction, not teaching quality.
3. Consider ordered article learning with durable progress as a later feature; this slice does not add it.

## Docs And Wiki

README, task brief, task index and restart entry reconciled; examples need no config changes. No wiki was created; durable operating guidance is in README.

## Implementation Log

[Decisions, focus discovery and verification](implementation-log.md).

