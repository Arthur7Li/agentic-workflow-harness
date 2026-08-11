---
name: adr-writer
description: Use when a task involves a significant, hard-to-reverse technical or architectural decision (framework choice, data model shape, storage layer, auth approach, new provider integration). Activates to draft an Architecture Decision Record before or alongside the Implementation Plan.
---

# ADR Writer

## When to use this skill

Whenever a decision meets any of these criteria:

- Hard to reverse later without significant rework
- Affects multiple future features, not just the current task
- Involves choosing between genuinely competing alternatives (not an obvious
  default)
- Introduces a new dependency, service, or architectural layer

## Approach

1. Draft the ADR using `docs/harness/ADR_TEMPLATE.md`, numbered sequentially
   after the highest existing ADR number in `docs/adr/`.
2. Fill in Context, Decision, at least two Alternatives considered (even if
   one is "do nothing"), Consequences, and References.
3. Reference the ADR number from the Implementation Plan and the PR
   description.
4. Do not mark an ADR "Accepted" yourself — draft it as "Proposed" and let
   a human change the status upon review, since ADR acceptance is itself a
   human decision gate.

## Output

A new file at `docs/adr/00XX-<slug>.md`, referenced in the current task's
Implementation Plan and PR.
