# Contributing to {{PROJECT_NAME}}

This project is built with heavy agent-assisted development. This document
exists so the human-in-the-loop process is explicit and repeatable.

## Before doing any work

Read, in order:

1. `GEMINI.md` — standing rules the agent (and you) must follow
2. `docs/harness/OVERVIEW.md` — why the harness is structured this way
3. `docs/harness/WORKFLOW.md` — the step-by-step loop to follow for every task

## The short version

1. Open a GitHub Issue.
2. Branch: `issue/<number>-<slug>`.
3. Work the task through Task List → Implementation Plan → Execution →
   Walkthrough, approving manually at each artifact gate.
4. Copy artifacts to `docs/agent-logs/`.
5. Open a PR with the template filled out completely.
6. Merge only after human review — no auto-merge regardless of CI or
   automated review status, per `GEMINI.md`.

## Tooling constraints

See `GEMINI.md` §2 for this project's actual constraints (budget, data
handling, domain correctness). If a request conflicts with them, open an
Issue tagged `needs-decision` rather than working around it silently.

## Getting unstuck

If an agent's Task List or Implementation Plan doesn't make sense, don't
approve it hoping it'll become clear later — ask it to re-explain. The entire
point of the manual review gates is to understand the system as it's built,
not just to confirm that it works.
