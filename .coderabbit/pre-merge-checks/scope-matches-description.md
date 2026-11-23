---
# Keep as is. Warning mode: it reports in the walkthrough and never blocks a merge.
# Every extra check adds to review time, so this folder stops at two checks.
# The dials for later: `report: platform` posts the result as a GitHub check; `mode: error` makes it fail.
id: scope-matches-description
name: Scope matches description
mode: warning
report: coderabbit
---

Pass when every changed file is accounted for by the pull request title, description or linked issue. Fail when any of these is changed without the description saying so: an agent rule file (AGENTS.md, CLAUDE.md, .cursorrules and similar), a CI workflow, deployment or infrastructure configuration, a database migration or schema, a dependency manifest or lockfile with a non-patch change, or a file under a folder the description does not mention at all. List the unaccounted-for files.
