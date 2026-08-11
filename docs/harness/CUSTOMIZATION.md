# Customizing This Harness For Your Project

This template is deliberately generic. Follow this checklist to adapt it —
most steps are fill-in-the-blank, not rewrites.

## 1. Rename and fill in `GEMINI.md.template`

- Rename to `GEMINI.md` (keep `AGENTS.md` as-is; it just points to it).
- Fill in `{{PROJECT_NAME}}` and `{{ONE_SENTENCE_PROJECT_DESCRIPTION}}`.
- Rewrite **Section 2 (Non-Negotiable Constraints)** with your project's real
  constraints. Ask yourself:
  - What's the budget/tooling ceiling? (free-tier only? specific stack?)
  - What data must never appear in code/logs/tests? (PII, credentials,
    health data, financial data?)
  - What domain(s) need correctness verification beyond "the tests pass"?
    (tax logic, medical logic, legal logic, pricing logic, security logic?)
- Rewrite **Section 4 (High-Risk Changes)** with the specific categories of
  change in your codebase that should never merge on green tests alone.
- Fill in **Section 6** with a short note on your own technical background so
  the agent calibrates explanations appropriately.

## 2. Adapt or replace the example Skills

Two of the four skills included here are templates, not finished skills:

- `skills/domain-rules-example/SKILL.md` — a template for "this project has
  a domain where correctness matters more than velocity" (the original used
  this for Canadian tax rules; yours might be medical dosing, legal
  compliance, pricing/billing logic, or scientific calculations). Rename the
  folder to your actual domain and rewrite the specifics.
- `skills/external-integration-example/SKILL.md` — a template for "this
  project connects to third-party APIs/services." Rename and rewrite for
  your actual integration surface (payment processors, data providers,
  hardware APIs, etc.).

The other two are close to usable as-is:

- `skills/security-reviewer/SKILL.md` — generic OWASP-style checklist; adjust
  only if your stack has unusual security surface area.
- `skills/adr-writer/SKILL.md` — fully generic, no changes needed.

Add more skills as your project reveals recurring capability needs. A skill
is worth creating when you find yourself giving the agent the same
multi-step instructions more than twice.

## 3. Fill in the Risk Register

Copy `docs/harness/RISK_REGISTER_TEMPLATE.md` to `docs/harness/RISK_REGISTER.md`
and replace the example rows with risks specific to your project. Keep
updating it — it's meant to be a living document, not a one-time exercise.

## 4. Bootstrap your ADR log

`docs/adr/0001-record-architecture-decisions.md` is generic and can stay
as-is — it's the ADR that establishes you're using ADRs. Start numbering your
real project decisions from `0002`.

## 5. Adjust Issue/PR templates

The risk-flag checkboxes in `.github/ISSUE_TEMPLATE/*.md` and
`.github/PULL_REQUEST_TEMPLATE.md` currently mirror the generic high-risk
categories from `GEMINI.md.template` §4. Update them to match whatever you
wrote in your actual `GEMINI.md` §4.

## 6. Update `CONTRIBUTING.md`

Replace the placeholder project name and any solo-vs-team framing to match
your situation.

## 7. Delete what you don't need

If a section genuinely doesn't apply (e.g. you have no external integrations
at all), delete the corresponding skill and its references in `GEMINI.md`
rather than leaving unused scaffolding around. A harness that's accurate and
smaller beats one that's comprehensive and stale.

## What NOT to change

The four-layer architecture and the Issue → Task List → Implementation Plan
→ Walkthrough → audit-log → PR → merge loop in `docs/harness/WORKFLOW.md`
are the load-bearing structure. Adapt the content inside each gate to your
project, but keep the gates themselves — they're what makes the system
auditable and keeps a human in the loop on decisions that matter.
