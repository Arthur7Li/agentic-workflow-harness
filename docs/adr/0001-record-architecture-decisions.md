# ADR-0001: Record architecture decisions with ADRs

- **Status:** Accepted
- **Date:** YYYY-MM-DD (set this to when you adopt this harness)
- **Issue:** N/A (harness bootstrap)
- **Deciders:** <you>

## Context

This project is built with heavy agent-assisted development. Chat-based
approvals are not durable — they aren't searchable, versioned, or visible to
a future contributor (including a future you) trying to understand why a
decision was made. The project needs a lightweight, version-controlled
record of significant technical and product decisions.

## Decision

Every architecturally significant decision (framework/library choice, data
model shape, integration strategy, auth approach, storage choice) is recorded
as a Markdown ADR in `docs/adr/`, using `docs/harness/ADR_TEMPLATE.md`,
numbered sequentially, and referenced from the relevant Implementation Plan
and PR.

## Alternatives considered

- **Rely on PR descriptions only** — rejected; PR descriptions get buried and
  aren't structured for "why" reasoning specifically.
- **Rely on chat history in the agent tool** — rejected; not guaranteed
  durable, not easily shared or diffed, not part of the Git history.

## Consequences

Adds a small amount of overhead per significant decision, but makes the
project's technical history explainable to any future reader. Trivial
decisions do not need an ADR — use judgment per `docs/harness/WORKFLOW.md`.

## References

`docs/harness/OVERVIEW.md`, `docs/harness/WORKFLOW.md`
