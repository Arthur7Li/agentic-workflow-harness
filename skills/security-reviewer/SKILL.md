---
name: security-reviewer
description: Use before merging any change that touches authentication, credential handling, data storage/encryption, new third-party dependencies, or external API integrations. Activates for a pre-merge OWASP-oriented review pass on high-risk changes.
---

# Security Reviewer

## When to use this skill

Any change flagged high-risk under your `GEMINI.md` §4: auth flows,
credential storage, encryption, new dependencies, new external integrations,
or anything handling sensitive data at rest or in transit.

## Approach (OWASP-oriented checklist)

1. **Secrets:** Run a secret-scanning tool on the diff. Confirm no API keys,
   tokens, or credentials are present, including in test fixtures and
   comments.
2. **Injection:** For any code touching a database or shell command, confirm
   parameterized queries / safe APIs are used — no string-concatenated SQL,
   no unsanitized shell invocation.
3. **AuthN/AuthZ:** Confirm session/token handling follows a standard,
   well-reviewed library rather than custom crypto or custom session logic.
4. **Data exposure:** Confirm sensitive data isn't logged in plaintext, isn't
   exposed in error messages/stack traces returned to the client, and isn't
   over-fetched beyond what a view needs.
5. **Dependency risk:** For any new dependency, check it's actively
   maintained, has no known critical CVEs, and satisfies your tooling
   constraints. Note findings in the Implementation Plan.
6. **Transport:** Confirm any external API call uses HTTPS/TLS and validates
   certificates — no disabled cert verification "to make it work."

## Output

Record findings — including "none found" — directly in the Walkthrough
artifact and the PR description. A high-risk PR with no documented security
pass is incomplete, not just lower quality.
