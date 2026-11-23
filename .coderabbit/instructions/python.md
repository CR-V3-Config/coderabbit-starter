---
# AGENT: example language document. Keep one document per language or framework this repository uses and
# delete the ones it does not. Five concrete defects, the ones most often caught in human review here, in
# the team's words. No style rules. Under 800 characters.
id: python
name: Python
paths:
  - "**/*.py"
---

Flag: swallowed exceptions; blocking I/O inside async code; mutable default arguments; SQL or shell built from string formatting; an outbound call with no timeout.
