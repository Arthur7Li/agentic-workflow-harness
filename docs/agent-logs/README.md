# Agent Logs — Permanent Audit Trail

This folder is the durable, version-controlled record of every agent
artifact produced during development (Task Lists, Implementation Plans,
Walkthroughs, or your tool's equivalents). It exists because these artifacts
are not guaranteed to remain accessible indefinitely inside the agent tool's
UI — copying them here makes the project's history auditable independent of
the tool.

## Convention

One folder per unit of work, named:

```
docs/agent-logs/<YYYY-MM-DD>-<issue-number>-<slug>/
  01-task-list.md
  02-implementation-plan.md
  03-walkthrough.md
  screenshots/           (optional — browser/UI subagent captures)
```

Example: `docs/agent-logs/2026-08-11-42-payment-webhook-handler/`

## Rules

- **Append-only.** Never edit a past log entry to "correct" it after the
  fact — if something in a past plan turned out wrong, note the correction in
  a new entry (or the relevant PR) and, if it reveals a durable lesson, add a
  bullet to the relevant Skill's `SKILL.md`.
- Copy artifacts verbatim (or near-verbatim — trimming pure boilerplate is
  fine, trimming substance is not). The point is reconstructability, not
  brevity.
- Every log folder should be referenced from its corresponding PR description
  and, where relevant, its GitHub Issue.
- If a task didn't produce a formal Implementation Plan (trivial/lightweight
  path per `docs/harness/WORKFLOW.md`), it's fine to skip this folder — but
  default to logging when in doubt.
