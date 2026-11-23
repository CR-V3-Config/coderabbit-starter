---
# AGENT: example. Keep this document only if the repository has database migrations, and adjust the glob
# to where they live. Delete it otherwise.
id: migrations
name: Database migrations
paths:
  - "**/{migrations,migrate,schema,prisma,drizzle,alembic}*/**"
---

Flag a column dropped, renamed, retyped or made required without a compatibility path; a new NOT NULL column with no default or backfill; a data move on a large table that is not batched; a migration that is not safe to run twice; an index added without CONCURRENTLY (or the equivalent) on a hot table.
