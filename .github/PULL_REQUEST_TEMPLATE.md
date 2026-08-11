## Summary

<!-- What changed, in plain language. -->

## Linked

- Issue: #
- Agent log folder: `docs/agent-logs/<date>-<issue>-<slug>/`
- ADR (if applicable): `docs/adr/00XX-....md`

## Risk flags (check any that apply — adapt these to match your GEMINI.md §4)

- [ ] Touches a high-stakes domain calculation/rule
- [ ] Adds a new dependency or third-party service
- [ ] Touches authentication or credential storage
- [ ] Changes a core data model
- [ ] Adds a new external integration/connector

If any box above is checked, confirm before requesting review:

- [ ] `security-reviewer` skill pass completed and findings recorded below
- [ ] Secret-scanning run against this diff, no findings (or findings resolved)
- [ ] Relevant authoritative source cited for any domain-specific figure or rule

## Security review findings (if applicable)

<!-- "None found" is a valid answer, but must be stated explicitly. -->

## How this was verified

<!-- Test results, screenshots/recordings from a browser/UI subagent, etc. -->

## Human review checklist

- [ ] I understand what changed and why, in my own words
- [ ] I reviewed the Implementation Plan / ADR, not just the diff
- [ ] I'm comfortable this doesn't violate the constraints in GEMINI.md
