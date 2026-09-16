# Task Brief: pi Curiosity Companion

> Created: 2026-09-14
> Parent plan: Accepted conversation plan, including ABCD cards
> Status: Complete

## Goal

Deliver a pi package with persistent curiosity cards, optional quizzes, independent follow-up chat, configurable local knowledge collections and explicit Markdown favorites.

## Success Criteria

- Card work never blocks or modifies the main agent conversation.
- Support task / wander / mixed modes and text / quiz / mixed formats independently.
- Support multiple named Markdown collections and user-selected favorite destinations.
- Verify lifecycle, cancellation, keyboard focus, model failures and source integrity.
- Match the reference interaction: bordered top-right card, full-row choice highlight, in-place reveal and optional follow-up; filter meta-content and supply labeled warmups.

## Scope

In scope: extension, scheduler, model adapter, local knowledge, terminal UI, favorites, tests and README.
Out of scope: remote knowledge connectors, desktop app, pi core changes, automatic knowledge writes.

## Constraints

Target installed pi 0.85.1. Use supported extension APIs. No subagents requested. No publication or credentials changes.

## Expected Knowledge Updates

- README: installation, configuration, interfaces, limits and manual validation.
- Task index: docs/tasks/INDEX.md.
