---
name: domain-rules-example
description: TEMPLATE — rename this skill and folder to your project's actual high-stakes domain (e.g. tax-calculation-rules, medical-dosing-rules, pricing-engine-rules). Use whenever a task touches logic where correctness matters more than velocity and a wrong answer would be genuinely harmful, not just buggy.
---

# Domain Rules — TEMPLATE (rename me)

> This is a template. The original harness this was generalized from used a
> skill exactly this shape for Canadian tax-account rules (TFSA/RRSP
> contribution limits, marginal tax rates). Replace the domain, the
> non-negotiable rule, and the decision tree below with your own project's
> equivalent, then rename this folder to something specific
> (e.g. `skills/pricing-rules/`, `skills/clinical-dosing-rules/`).

## When to use this skill

Any time a task touches: {{list the specific rules, calculations, or
regulated behaviors in your domain that need this level of scrutiny}}.

## Non-negotiable rule

**Never assert a specific number, rate, or rule from memory without flagging
it for verification**, if that number changes over time (regulatory limits,
prices, rates, thresholds) or has real-world consequences if wrong. If the
exact current figure isn't confirmed against an indexed, authoritative source,
the Implementation Plan must say so explicitly and mark it as "needs
verification" rather than presenting it as fact.

## Approach

1. Identify exactly which rule(s) or calculation(s) are involved.
2. Check your indexed reference docs for an authoritative, dated source. If
   none exists, say so and propose adding one — don't fabricate a citation.
3. Keep this logic isolated behind a clearly named module/function (not
   inlined into UI or general business logic) so it can be updated in one
   place when the underlying rule changes.
4. Write a unit test per rule with the cited value hardcoded as a test
   fixture, with a comment noting the date/version it applies to.
5. Flag any such change as high-risk per your `GEMINI.md` §4 — it requires a
   human approval gate regardless of test coverage.

## Decision tree (example shape — adapt the categories)

- Is this a *display* of a user-entered value? → Low risk, standard review.
- Is this a *calculated* or *derived* value based on domain rules? → High
  risk. Cite source, isolate logic, mandatory human gate.
- Is this a *recommendation or decision* made on the user's behalf? → Treat
  as high risk and be explicit about the limits of what the system is
  qualified to assert (e.g. "informational only, not professional advice.")
