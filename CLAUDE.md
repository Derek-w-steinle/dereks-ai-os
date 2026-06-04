# Derek's AI OS — Claude Code workspace

This is a live Claude Code workspace for Original 7 (O7) marketing work that
also serves as a public portfolio. It is organized in four layers: this
CLAUDE.md (persistent context), `.claude/skills/` (auto-invoked knowledge),
`.claude/agents/` (delegated sub-tasks), and `.claude/settings.json`
(deterministic hooks and permissions). Client data and secrets stay out of
every committed file.

## Build and verification commands

This repo is content and configuration, not a compiled app. Common checks:

- Lint the README: `npx markdownlint-cli2 README.md`
- Lint every markdown file: `npx markdownlint-cli2 "**/*.md"`
- Count CLAUDE.md lines (target 60–120): `wc -l CLAUDE.md`
- Count CLAUDE.md H2 sections (expect 5): `grep -c "^## " CLAUDE.md`
- List the tree: `ls -R`
- Check the working tree: `git status`

When a skill or doc adds a build step, record the exact command here so this is
the first place to look.

## Project layout

- `CLAUDE.md` — this file; the context loaded every session.
- `CLAUDE.local.md` — personal notes and scratch context (gitignored).
- `README.md` — the portfolio entry point and reading guide.
- `.claude/skills/` — auto-invoked skills, one folder per skill, each with a
  `SKILL.md`. Anchored by `product-marketing` (shared positioning context).
- `.claude/agents/` — subagents with scoped tools for delegated work.
- `.claude/settings.json` — committed hooks and permissions.
- `.claude/settings.local.json` — personal overrides (gitignored).
- `goals/` — reusable `/goal` templates with verifiable end states.
- `docs/` — reference material skills read via `@docs/<file>.md`.

## Conventions

- Skill folders use kebab-case names; each `SKILL.md` stays under 500 lines.
- Every skill `description` starts with "When the user wants…" and ends with a
  "For X, see other-skill" cross-reference for scope.
- Skills read `docs/product-marketing.md` for shared product and audience
  context before asking the user to repeat it.
- Markdown uses `-` for bullets, fenced code blocks with a language tag, and
  one H1 per file.
- Keep CLAUDE.md between 60 and 120 lines with exactly five H2 sections.
- Commit messages use the imperative mood, e.g. "Add pool-app-cro skill".

## Always-do and never-do rules

- Prefer `CLAUDE.local.md` and `.claude/settings.local.json` over committing
  client names, account data, or secrets.
- Prefer editing an existing skill over creating a near-duplicate one.
- Prefer positive instructions ("Prefer X over Y") over negative phrasing in
  every committed file.
- Prefer scoped, read-only agent tool lists over granting write access by
  default.
- Always run the verification commands above and report their output before
  declaring a task done.
- Always review third-party skills before installing: read each `SKILL.md` and
  script, and prefer pinned commits over floating versions.

## Workflow

- Start each session in this directory so Claude loads CLAUDE.md automatically.
- For non-trivial tasks, use Plan Mode and `AskUserQuestion` to confirm scope
  before writing files.
- Use `/goal` only when "done" is something the transcript can prove (a lint
  exit code, a file count, a clean tree), and always cap turns.
- Use `/clear` between unrelated tasks; prefer fresh sessions over `/compact`.
- Commit in small, reviewable steps; keep `git status` clean before stopping.
- After finishing, note durable learnings in `docs/` or a skill so the next
  session inherits them.
