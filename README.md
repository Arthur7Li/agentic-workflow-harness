# Agentic Workflow Harness

A reusable, auditable harness for building software with heavy agentic
assistance (designed around Google Antigravity 2.0 running Gemini, but the
core ideas transfer to any agent tool that supports persistent rules files,
skills/plugins, and reviewable plan/execution artifacts — e.g. Claude Code,
Cursor, Copilot Workspace).

This started as the harness for a specific project ([MapleFolio](https://github.com/Arthur7Li/maplefolio),
a Canadian personal finance tracker) and was generalized here so it can be
dropped into any project that wants agent-assisted development to stay
**transparent, auditable, and human-gated** rather than a black box.

## What problem this solves

Agentic coding tools are capable, but without structure they tend to fail in
three specific ways:

1. **Context drift** — the agent forgets project constraints partway through
   a long session because nothing forces those constraints back into view.
2. **Silent decisions** — the agent makes an architectural or high-stakes
   logic choice that's never reviewed or recorded, so nobody can explain
   later why the system works the way it does.
3. **Unbounded autonomy on high-stakes code** — some parts of any codebase
   (money math, auth, data models, security-sensitive logic) are exactly
   where a confident-but-wrong agent output is dangerous, and deserve a human
   checkpoint that isn't just "tests passed."

This harness is four layers that address each failure mode with a concrete
mechanism, not a vague policy. See [`docs/harness/OVERVIEW.md`](docs/harness/OVERVIEW.md)
for the full explanation.

## Quickstart — adopting this in your own project

1. Use this repo as a template (GitHub's "Use this template" button) or copy
   the folders listed below into your project.
2. Read [`docs/harness/CUSTOMIZATION.md`](docs/harness/CUSTOMIZATION.md) and
   fill in every `{{PLACEHOLDER}}` — it's a checklist, not a rewrite.
3. Rename/edit the example Skills in `/skills` to match your project's actual
   high-risk domains (see below for what "high-risk domain" means).
4. Commit the result, then follow [`docs/harness/WORKFLOW.md`](docs/harness/WORKFLOW.md)
   for every unit of work going forward.

## What's included

```
GEMINI.md.template          # standing rules the agent auto-loads every session
AGENTS.md                   # compatibility pointer to GEMINI.md
docs/harness/OVERVIEW.md    # the four-layer architecture, explained
docs/harness/WORKFLOW.md    # the step-by-step loop with human approval gates
docs/harness/CUSTOMIZATION.md  # how to adapt this template to your project
docs/harness/ADR_TEMPLATE.md
docs/harness/RISK_REGISTER_TEMPLATE.md
docs/adr/0001-record-architecture-decisions.md   # example ADR
docs/agent-logs/README.md   # convention for a permanent, versioned audit trail
skills/domain-rules-example/SKILL.md         # template: domain-specific correctness rules
skills/external-integration-example/SKILL.md # template: third-party integration rules
skills/security-reviewer/SKILL.md            # generic, usable mostly as-is
skills/adr-writer/SKILL.md                   # generic, usable mostly as-is
.github/ISSUE_TEMPLATE/feature_request.md
.github/ISSUE_TEMPLATE/task.md
.github/PULL_REQUEST_TEMPLATE.md
CONTRIBUTING.md
```

## Design principles (kept from the original)

- **Every agent capability maps to a concrete artifact.** Task Lists,
  Implementation Plans, and Walkthroughs aren't just chat — they get copied
  into `docs/agent-logs/` so the reasoning survives independent of whatever
  tool produced it.
- **Not everything needs the full loop.** Trivial changes get a lightweight
  path; anything touching the domains you flag as high-risk gets mandatory
  human review regardless of test results.
- **Standing rules stay standing.** Project constraints live in one
  auto-loaded file (`GEMINI.md`) so the agent doesn't have to be reminded
  every session, and doesn't silently drift from them either.
- **Decisions get recorded, not just approved in chat.** Anything
  architecturally significant becomes an ADR — a durable, version-controlled
  record of *why*, not just *what*.

## License

MIT — use, fork, and adapt freely. See [`LICENSE`](LICENSE).
