# Brief for your coding agent

Hand this brief, `.coderabbit.yaml` and the `.coderabbit/` folder to your coding agent (Claude Code, Cursor, Codex, or similar) with the repository checked out. Read what comes back, then send it to us before anything is merged.

```
Fill in the attached CodeRabbit configuration for this repository. It has two parts that go at the repository root: `.coderabbit.yaml` (settings) and `.coderabbit/` (Markdown documents: review instructions in `instructions/`, pre-merge checks in `pre-merge-checks/`). This is schema V3: unknown keys and unknown front matter fields are errors, so add nothing that is not already there.

Only change lines marked "# AGENT:" and the examples those lines point at. Do not add, remove or reorder other keys, and do not change any value that is already set. Write globs relative to the repository root. Write instructions as concrete defects to look for, in our own words; never style, naming or formatting rules.

Read the repository first, then work in this order.

In `.coderabbit.yaml`:

1. fun.tone_instructions: replace "authentication, payments or customer data" in the last sentence with the three things that hurt most when they break in our product. Change nothing else in that string. 250 characters at most.

2. reviews.behavior.merge_risk_instructions: rewrite the high-risk and low-risk lists to match what is actually risky to merge in our codebase. Under 3,000 characters.

3. reviews.behavior.path_filters: add generated code, recorded fixtures, large seed or snapshot data, and anything else no human reviews.

4. reviews.behavior.code_guidelines.filePatterns: list every architecture, API or coding-standards document that our agent rule files (AGENTS.md, CLAUDE.md, .cursorrules, .cursor/rules, .claude/rules and similar) reference with a link or "@path", each with the source folders it governs (object form: files and applyTo). Use real paths, not symlinks. Leave the rule files themselves out; they are read by default. Delete the two examples.

5. reviews.behavior.multi_repo_analysis.linked_repositories: if this repository calls, or is called by, another of our repositories, uncomment the block and list each one as owner/repo with one line on what it holds. Leave it commented out if there is none.

In `.coderabbit/instructions/`:

6. Domain documents: replace the two examples (`auth.md`, `payments.md`) with one document per high-stakes area of our product, three or four at most. Each is its own file with front matter `id` (same as the file name, letters, digits and hyphens), `name`, and `paths` (always set; a glob for that area). The body is five to eight concrete defects a senior engineer on this team checks for by hand. Under 1,200 characters.

7. Language documents: keep one document per language or framework this repository uses (`typescript.md`, `python.md` are examples), five concrete defects each, the ones most often caught in our human reviews. Under 800 characters. Keep `migrations.md` only if we have migrations, and adjust its glob. Delete the examples we do not use.

Rules for every document: the body is plain instruction text, so put notes and questions in front matter comments or in your reply, never in the body. Every `id` is unique. Do not create `.coderabbit/` folders anywhere other than the repository root. Remove the "# AGENT:" comment from a document once you have filled it.

Leave these exactly as they are: `instructions/agent-rule-files.md`, everything in `pre-merge-checks/`, and in the YAML `version`, `profile`, `auto_approvals`, `status`, `auto_review` and `output`.

Return the file and the folder with a short list of what you changed and anything you were unsure about. Do not merge them.
```

## For the FE: what to check when it comes back

- Nothing outside the AGENT lines moved. Diff against the starter.
- Every instruction document has `paths`; none applies to the whole repository. Every `id` is unique and matches its file name.
- Each instruction body is defects, not style. Strike anything about naming, formatting, docstrings or "best practices". No `# AGENT:` text or notes left in a body.
- Still one or two pre-merge checks, all `mode: warning`. If the agent added more, remove them and note it for the customer.
- One root `.coderabbit/` folder only; no nested ones.
- Lengths: `tone_instructions` 250 or fewer; `merge_risk_instructions` under 3,000; domain documents under about 1,200 characters.
- Validate the YAML against https://docs.coderabbit.ai/schema/schema.v3.json, and each document's front matter against the allowed fields (`id`, `name`, `paths`, `exclude`, `enabled`, and for checks `mode`, `report`).
