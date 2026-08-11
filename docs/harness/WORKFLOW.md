# Workflow — Step by Step

This is the loop to run for every unit of work. Follow it in order. Steps
marked **[GATE]** require explicit human approval before the agent continues.

## 0. Before you start a session

- Open your agent tool (Antigravity, etc.) and confirm the workspace's
  **Artifact/Autonomy Review Policy is set to manual review**, not an
  autonomous "always proceed" mode. Re-check this after tool updates —
  settings occasionally reset.
- Confirm `GEMINI.md` (or your tool's equivalent rules file) is present at
  the workspace root and current.

## 1. Define the work as a GitHub Issue

Use `.github/ISSUE_TEMPLATE/feature_request.md` or `task.md`. Every task the
agent works on should trace back to an Issue number — this is what makes the
audit trail queryable later ("why does this exist" → Issue #N).

Small, low-risk items (typo, copy change, formatting) don't strictly need an
Issue, but still get a branch and PR.

## 2. Create the branch

`issue/<number>-<slug>`. Either you or the agent creates this before any file
changes.

## 3. Agent context loading (automatic)

Your rules file auto-loads. If the task needs a specific Skill, reference it
explicitly in your prompt to make sure it activates: *"Use the
[skill-name] skill to build X for Issue #N."* If the task needs deep
reference material, make sure it's indexed in the knowledge base and mention
it by name.

## 4. Task List artifact — **[GATE 1]**

The agent proposes a structured breakdown before writing any code. Read it.
Check for:

- Does it match the Issue's actual scope, or is it doing more/less than asked?
- Does it surface any high-risk item (per your `GEMINI.md` §4) that needs
  flagging?

Comment directly on the artifact to redirect scope if needed. Do not approve a
Task List you don't understand — ask the agent to explain any step first.

## 5. Implementation Plan artifact — **[GATE 2]**

Once the Task List is approved, the agent produces a technical plan: files
touched, new dependencies, data model changes, logic overrides. This is the
single most important review point. Check for:

- **New dependency?** Verify it satisfies your tooling constraints (e.g.
  free-tier only). Ask the agent to justify the choice against at least one
  alternative if unsure.
- **Touches a high-risk domain from `GEMINI.md` §4?** Require a cited source
  or an ADR before approving.
- **New external integration?** Confirm it targets a sandbox/mock endpoint,
  not production credentials, unless you've explicitly approved otherwise.
- **Architecturally significant?** (new service boundary, new storage layer,
  new auth flow) → needs an ADR. Ask the agent to draft one using the
  `adr-writer` skill, or draft it yourself and reference it.

Only approve once you can explain, in your own words, what is about to change
and why. If you can't, ask the agent to re-explain — this is the entire point
of the harness.

## 6. Execution

The agent implements the approved plan. For UI-facing work, direct it to use
a browser subagent to verify rendering and capture screenshots/recordings as
part of verification. For backend logic, require unit tests written
*alongside* the implementation, not after.

## 7. Test and self-heal loop

If tests fail, allow the agent a bounded number of self-correction attempts
(2-3 is a reasonable default). If still failing, stop and escalate — do not
let the agent loop indefinitely or silently weaken a test to make it pass.

## 8. Walkthrough artifact — **[GATE 3]**

The agent summarizes what changed and how it was verified. Read it before
merging anything. If it doesn't clearly explain *how* correctness was
verified, it's incomplete — ask for the missing verification before
proceeding.

## 9. Security pass (required for high-risk changes)

For anything flagged high-risk in `GEMINI.md` §4:

1. Run a secret-scanning tool against the diff.
2. Invoke the `security-reviewer` skill for a structured review pass.
3. Record findings (even "none found") in the Walkthrough.

## 10. Persist the audit trail

Copy the Task List, Implementation Plan, and Walkthrough verbatim into:

```
docs/agent-logs/<YYYY-MM-DD>-<issue-number>-<slug>/
  01-task-list.md
  02-implementation-plan.md
  03-walkthrough.md
```

This step is not optional — it's what makes the project auditable after the
fact, independent of what's still visible in the agent tool's UI.

## 11. Commit and open the PR

- Commit message: Conventional Commits, referencing `#<issue-number>`.
- Open the PR using `.github/PULL_REQUEST_TEMPLATE.md`. Link the agent-log
  folder and the Issue.
- Request an automated code review (e.g. GitHub Copilot review) as a second
  pass before your own review, where available — it catches mechanical
  issues your manual review might not prioritize.

## 12. Human merge gate — **[GATE 4]**

Review the PR diff, any automated review comments, and the linked
Walkthrough. Merge only when satisfied. High-risk items should never be
merged solely because tests passed — a human is the final check on
correctness for anything that matters, not the test suite.

## 13. Close the loop

- Close the Issue, referencing the PR.
- If the task produced a new architectural decision, confirm the ADR is
  merged in `docs/adr/`.
- If you caught a mistake the agent made, add a short "Lesson" bullet to the
  relevant Skill's `SKILL.md` — this is a manual substitute for an automated
  learning flywheel, since most agent tools don't yet persist cross-session
  corrections automatically.

## Lightweight path for trivial changes

Typo fixes, formatting, comment updates, README edits: skip the Task List /
Plan gates, but still open a PR (even a tiny one) so it's in the Git history.
Use judgment — when in doubt, use the full loop.
