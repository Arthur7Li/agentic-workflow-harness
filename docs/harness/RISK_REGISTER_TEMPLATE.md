# Risk Register

Copy this to `docs/harness/RISK_REGISTER.md` and replace the example rows
with risks specific to your project. Keep it as a living document — add a
row whenever a new risk is identified (by you or the agent); update status
as it's mitigated. Reference relevant ADRs and Issues.

| ID | Risk | Category | Likelihood | Impact | Mitigation | Status | Refs |
|----|------|----------|------------|--------|------------|--------|------|
| R-1 | *Example:* A third-party API's free-tier limits block realistic testing | Technical | Medium | Medium | Use documented sandbox/test accounts; budget extra time; revisit paid tier only once usage justifies it | Open | |
| R-2 | *Example:* Incorrect calculation shown to a user in a domain where correctness matters (pricing, tax, medical, etc.) | Correctness | Medium | High | Mandatory human review gate on this domain's logic (GEMINI.md §4); cite an authoritative source in every such PR | Open | |
| R-3 | *Example:* Accidental commit of real credentials or API keys | Security | Low | Critical | `.gitignore` for secrets; secret-scanning required before merge on high-risk PRs; no real credentials in fixtures | Open | |
| R-4 | *Example:* Agent silently adds a dependency/service outside your tooling constraints | Cost / Governance | Low | Medium | GEMINI.md §2 hard rule; Implementation Plan review checklist includes explicit dependency check | Open | |
| R-5 | *Example:* Agent context drift on long sessions causes it to violate a standing rule | Process | Medium | Medium | Standing-rules file auto-loaded every session; manual artifact review gates at every stage; no autonomous "always proceed" mode | Open | |

Delete the example rows once you've replaced them with your project's actual
risks — keeping stale examples around defeats the purpose of a living
register.
