# CodeRabbit starter configuration (schema V3)

A starting point for configuring CodeRabbit on a repository, tuned for signal over noise: reviews lead with defects, the walkthrough stays small, and nothing blocks a merge.

## What is here

```text
.
├── .coderabbit.yaml                      settings: profile, when reviews run, what the summary shows
├── .coderabbit/
│   ├── instructions/                     what to look for, one Markdown document per area
│   │   ├── agent-rule-files.md           keep as is
│   │   ├── auth.md                       example domain document
│   │   ├── payments.md                   example domain document
│   │   ├── typescript.md                 example language document
│   │   ├── python.md                     example language document
│   │   └── migrations.md                 example, keep if you have migrations
│   └── pre-merge-checks/
│       └── scope-matches-description.md  one check, warning mode, never blocks
└── AGENT_BRIEF.md                        instructions for your coding agent
```

## Requirements

- The repository is on GitHub.com and reviewed by CodeRabbit Cloud.
- V3 configuration is enabled for your organization. Adding `version: 3` does not enable it; confirm with your CodeRabbit contact.
- Custom pre-merge checks are a plan feature. If your plan does not include them, delete `.coderabbit/pre-merge-checks/`.

## How to use it

1. Copy `.coderabbit.yaml` and the `.coderabbit/` folder to the root of your repository, on a branch.
2. Give your coding agent the block in `AGENT_BRIEF.md` with the repository checked out. It fills in the lines marked `# AGENT:` and replaces the example documents with ones for your product.
3. Read what comes back, then open a pull request. On that pull request, comment `@coderabbitai configuration` and check that the reply names your V3 file as the source.
4. Merge to the default branch. Pull requests from forks and from authors outside the repository read the configuration from the target branch, so it applies to everyone only once it is merged.
5. To cover another repository, copy the same file and folder into it. The folder is only read from the repository under review.

## How the folder works

- Each document is Markdown with YAML front matter. `id` is required and must be unique; `paths` says which files it applies to, relative to the repository root.
- Documents with different ids apply together, so adding a rule for one area is a new file with a new id.
- A document with no `paths` applies to every file. Every instruction here sets `paths` on purpose: general defects are the default review's job.
- Keep everything in this one root folder so there is a single place to look.
- One invalid document stops all of them from loading. Unknown front matter fields, a duplicate id or an empty body all count as invalid.
- Limits: 100 documents per repository, 20,000 characters per instruction, 10,000 per check.

## Set in the CodeRabbit web app, not in these files

V3 keeps these out of the file: finishing touches (docstrings, unit tests, autofix), skipping reviews by pull request title or author, learnings and issue scope, chat integrations, and early access.

## Reference

- [Configuration V3 reference](https://docs.coderabbit.ai/reference/configuration-v3)
- [Instruction and check documents](https://docs.coderabbit.ai/configuration/documents)
- [Migrate configuration to V3](https://docs.coderabbit.ai/configuration/guides/migrate-to-v3)
