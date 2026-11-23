# Brief for your coding agent

Hand this brief, `.coderabbit.yaml` and the `.coderabbit/` folder to your coding agent (Claude Code, Cursor, Codex, or similar) with your repositories checked out. It asks you which repositories to set up, fills in the configuration for each, and hands it back. Read what comes back, then send it to us before anything is merged.

```
Set up the attached CodeRabbit configuration. It has two parts that go at a repository's root: `.coderabbit.yaml` (settings) and `.coderabbit/` (Markdown documents: review instructions in `instructions/`, pre-merge checks in `pre-merge-checks/`). This is schema V3: unknown keys and unknown front matter fields are errors, so add nothing that is not already there or listed in the V3 reference (https://docs.coderabbit.ai/reference/configuration-v3).

BEFORE YOU CHANGE ANYTHING

A. Ask me which repositories to set this up in. The configuration applies only to the repository it is committed to. List the repositories you can see (the ones checked out next to this one, or `gh repo list <owner>` if the GitHub CLI is available), most recently active first, and let me pick. Recommend starting with the one or two where a bug costs the most. Then do the chosen repositories one at a time, each on its own branch, repeating the steps below in each.

B. In each repository, look for an existing `.coderabbit.yaml`, `.coderabbit.yml` or `.coderabbit/` folder. If there is one, do not overwrite it. Merge:
   - Keep every setting the team already chose, for example the base branches under auto_review, labels, path filters, tool settings, linked repositories and tone. Where the existing value and the starter disagree, the existing value wins.
   - If the existing file is V2 (no `version: 3`), move each kept setting to its V3 key using https://docs.coderabbit.ai/configuration/guides/migrate-to-v3. Do not copy V2 keys under `version: 3`.
   - Turn each existing `path_instructions` block into its own document in `.coderabbit/instructions/` and each existing custom check into a document in `.coderabbit/pre-merge-checks/`, then remove the inline copy so it does not apply twice.
   - Keep existing documents in `.coderabbit/`. If one covers the same area as a starter example, keep theirs and delete the example. Every `id` stays unique.
   - Settings with no V3 key (finishing touches, ignoring pull requests by title or author, learnings scope, early access, chat integrations) cannot go in the file. List them with their current values in your reply so we can set them in the web app.
   - In your reply, list what was kept, what was moved and anything you could not carry over.

THEN FILL IN THE STARTER

Only change lines marked "# AGENT:" and the examples those lines point at (plus the merge above). Do not add, remove or reorder other keys, and do not change any value that is already set. Write globs relative to the repository root. Write instructions as concrete defects to look for, in our own words; never style, naming or formatting rules.

In `.coderabbit.yaml`:

1. fun.tone_instructions: replace "authentication, payments or customer data" in the last sentence with the three things that hurt most when they break in our product. Change nothing else in that string. 250 characters at most.

2. reviews.behavior.merge_risk_instructions: rewrite the high-risk and low-risk lists to match what is actually risky to merge in our codebase. Under 3,000 characters.

3. reviews.behavior.path_filters: add generated code, recorded fixtures, large seed or snapshot data, and anything else no human reviews.

4. reviews.behavior.code_guidelines.filePatterns: list every architecture, API or coding-standards document that our agent rule files (AGENTS.md, CLAUDE.md, .cursorrules, .cursor/rules, .claude/rules and similar) reference with a link or "@path", each with the source folders it governs (object form: files and applyTo). Use real paths, not symlinks. Leave the rule files themselves out; they are read by default. Delete the two examples.

5. reviews.behavior.multi_repo_analysis.linked_repositories: if this repository calls, or is called by, another of our repositories, uncomment the block and list each one as owner/repo with one line on what it holds. Leave it commented out if there is none.

In `.coderabbit/instructions/`:

6. Domain documents: replace the two examples (`auth.md`, `payments.md`) with one document per high-stakes area of our product, three or four at most. Each is its own file with front matter `id` (same as the file name, letters, digits and hyphens), `name`, and `paths` (always set; a glob for that area). The body is five to eight concrete defects a senior engineer on this team checks for by hand. Under 1,200 characters.

7. Language documents: keep one document per language or framework this repository uses (`typescript.md`, `python.md` are examples), five concrete defects each, the ones most often caught in our human reviews. Under 800 characters. Keep `migrations.md` only if we have migrations, and adjust its glob. Delete the examples we do not use.

In `.coderabbit/pre-merge-checks/`:

8. `no-personal-data-in-logs.md`: rewrite the list of personal data in the body to the fields this product actually handles, and name the logging, analytics and error reporting helpers this repository uses. Keep it a pass or fail condition and keep `mode: warning`. Delete the document if this repository handles no personal data. Do not add a third check.

Rules for every document: the body is plain instruction text, so put notes and questions in front matter comments or in your reply, never in the body. Every `id` is unique. Do not create `.coderabbit/` folders anywhere other than the repository root. Remove the "# AGENT:" comment from a document once you have filled it.

Leave these exactly as they are unless the merge in step B says otherwise: `instructions/agent-rule-files.md`, `pre-merge-checks/scope-matches-description.md`, and in the YAML `version`, `profile`, `auto_approvals`, `status`, `auto_review` and `output`.

Return the file and the folder for each repository with a short list of what you changed, what you kept from an existing configuration, and anything you were unsure about. Do not merge them.
```

## For the FE: what to check when it comes back

- Nothing outside the AGENT lines moved, except settings carried over from an existing configuration. Diff against the starter.
- Existing configuration: every setting the team had is still there under its V3 key (base branches, labels, filters, tools), no inline `path_instructions` or `pre_merge_checks` left in the YAML, and the list of web app settings came back.
- Every instruction document has `paths`; none applies to the whole repository. Every `id` is unique and matches its file name.
- Each instruction body is defects, not style. Strike anything about naming, formatting, docstrings or "best practices". No `# AGENT:` text or notes left in a body.
- One or two pre-merge checks, all `mode: warning`. If the agent added more, remove them and note it for the customer.
- One root `.coderabbit/` folder per repository; no nested ones.
- Lengths: `tone_instructions` 250 or fewer; `merge_risk_instructions` under 3,000; domain documents under about 1,200 characters.
- Validate the YAML against https://docs.coderabbit.ai/schema/schema.v3.json, and each document's front matter against the allowed fields (`id`, `name`, `paths`, `exclude`, `enabled`, and for checks `mode`, `report`).
