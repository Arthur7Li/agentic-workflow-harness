---
name: external-integration-example
description: TEMPLATE — rename this skill and folder to your project's actual integration surface (e.g. payment-processor-connector, institution-connector, hardware-api-connector). Use whenever building or modifying a connector to a third-party API, data provider, or aggregator.
---

# External Integration — TEMPLATE (rename me)

> This is a template. The original harness this was generalized from used a
> skill exactly this shape for Canadian financial institution connectors
> (Plaid/Flinks bank aggregation). Replace the specifics below with your own
> project's integration surface, then rename this folder
> (e.g. `skills/payment-connector/`, `skills/iot-device-connector/`).

## When to use this skill

Building any code path that connects your project to an external system:
third-party APIs, data providers, payment processors, hardware interfaces, or
aggregator services.

## Non-negotiable rules

- **Sandbox/mock only, until an explicit human-approved production
  credentials plan exists.** Never use real credentials in development,
  tests, or fixtures.
- **Respect your tooling constraints.** Verify the provider's free-tier
  limits (or cost structure) before proposing it; state those limits in the
  Implementation Plan.
- **Provider-agnostic interface where feasible.** If there's a realistic
  chance you'll need to swap providers later, design a shared interface
  (e.g. `ExternalConnector`) so calling code doesn't need to change.

## Approach

1. Confirm which provider and why, with at least one alternative considered
   — log this as an ADR if it's a new provider integration.
2. Design against the sandbox/test environment first; write integration
   tests against sandbox test accounts/fixtures.
3. Never log or persist sensitive identifiers in plaintext — even in sandbox
   mode, build the habit now.
4. Handle partial failures gracefully (one integration being down shouldn't
   break the whole feature) — make this a testable requirement.
5. Document required scopes/permissions in the connector's own README so a
   future reviewer can see exactly what access is requested and why.
6. Flag as high-risk per your `GEMINI.md` §4 — mandatory human approval gate
   and a secret-scanning pass before merge.

## Decision tree

- Is this a **new provider integration**? → Write an ADR first.
- Is this a **new endpoint/resource within an existing provider**? → Standard
  review, but confirm sandbox coverage exists.
- Is this **file/manual import parsing** (CSV, etc.)? → Lower risk than live
  API connectors, but still validate and sanitize all parsed input before it
  touches the data model.
