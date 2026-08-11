# Agentic Workflow Harness — Overview

## Why this harness exists

Agent-assisted coding tools like Antigravity (Gemini), Claude Code, Cursor,
or Copilot Workspace are capable, but capability without structure produces
three specific failure modes this harness is designed to prevent:

1. **Context drift** — the agent forgets project constraints halfway through
   a long session because nothing forces them back into view.
2. **Silent decisions** — the agent makes an architectural or high-stakes
   logic choice that's never reviewed or recorded, so nobody can explain
   later why the system works the way it does.
3. **Unbounded autonomy on high-stakes logic** — every project has some code
   where a confident-but-wrong agent output is genuinely dangerous (money
   math, auth, medical/legal logic, data models, security boundaries), and
   that code deserves a human checkpoint that isn't just "tests passed."

The harness solves this with four layers, each mapped to a concrete agent-tool
feature and a concrete Git/GitHub artifact. Nothing here is aspirational
tooling — every mechanism below maps to a real capability in Antigravity 2.0
(Task Lists, Implementation Plans, Walkthroughs, Skills, Knowledge Base,
subagents), and the GitHub half (Issues, branches, PRs, Copilot review,
secret scanning) is free at small-to-medium usage scale on any Git host.

## The four layers

| Layer | Agent-tool mechanism | Git/GitHub mechanism | Purpose |
|---|---|---|---|
| 1. Standing rules | `GEMINI.md` / `AGENTS.md` (auto-loaded every session) | Committed to `main`, versioned | Constraints that never change per-task: budget/tooling limits, data handling, domain-correctness rules, manual review, definition of done |
| 2. On-demand capabilities | `/skills/*/SKILL.md` (agent activates when relevant) | Committed to `main`, versioned | Reusable "how-to" playbooks for your project's recurring, high-stakes work types |
| 3. Deep reference knowledge | Knowledge Base / RAG index | `/docs/*` committed files | Domain reference material, competitive research, API docs — retrieved on demand, never bloats the prompt |
| 4. Per-task execution & audit trail | Task List → Implementation Plan → Walkthrough artifacts, reviewed manually at each stage | GitHub Issue → branch → PR, artifacts copied into `docs/agent-logs/` | The actual work loop; every step produces a human-reviewable, permanently stored record |

## Why this is auditable and explainable, not just "agents building stuff"

Most agent tools' planning/verification artifacts (Antigravity's Task List,
Implementation Plan, Walkthrough — or equivalents in other tools) are
genuinely useful, but by default they live inside the tool and aren't
guaranteed to persist as a durable, shareable record. This harness closes
that gap: at the end of every task, the agent copies those artifacts verbatim
into `docs/agent-logs/<date>-<issue>-<slug>/`, committed to Git. That gives
you:

- A permanent, greppable history of every plan the agent proposed and every
  verification it ran, independent of the tool that produced it.
- A natural mapping between "why does this code exist" and "which Issue,
  which plan, which verification produced it" — via PR descriptions and
  commit messages that reference the log folder and issue number.
- The ability to reconstruct, months later, exactly what the agent reasoned
  and verified — satisfying "transparent, auditable, explainable" without
  needing an enterprise observability stack.

## Why this keeps agents "in context"

Long-running projects risk two things: (a) the agent re-deriving project
rules every session because nothing persists them, and (b) context bloat from
carrying raw history forward on multi-step tasks. This harness addresses
both:

- The standing-rules file is auto-parsed on every session start, so
  constraints never need to be re-explained.
- Skills are loaded only when the agent's objective matches their
  description, keeping unrelated capability instructions out of the prompt.
- The knowledge base indexes `/docs` for retrieval rather than requiring
  reference material to be pasted into chat every time.
- Implementation Plans compact prior reasoning into a structured artifact
  rather than relying on raw chat history surviving a long session.

## Why this stays efficient rather than bureaucratic

Not every change needs the full loop. `docs/harness/WORKFLOW.md` defines a
lightweight path for trivial, low-risk changes (typos, formatting, docs) and
reserves the full Task List → Plan → Walkthrough → mandatory human gate
sequence for changes touching the high-risk domains you define in Section 4
of your `GEMINI.md`.
