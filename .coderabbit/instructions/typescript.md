---
# AGENT: example language document. Keep one document per language or framework this repository uses and
# delete the ones it does not. Five concrete defects, the ones most often caught in human review here, in
# the team's words. No style rules. Under 800 characters.
id: typescript
name: TypeScript and React
paths:
  - "**/*.{ts,tsx}"
---

Flag: hook dependencies that omit a value the effect reads, and effects without cleanup; state derived from props that goes stale; `any` or a cast that hides an API mismatch; a promise whose rejection is not handled; a route handler that trusts the request body without server side validation.
