# Derek's AI OS

A Claude Code workspace built as a personal "AI operating system": a single,
Git-tracked folder that turns Claude Code into a repeatable marketing
assistant for Original 7 (O7). It is a live workspace used for real marketing
work, and the structure itself — not any single output — is the portfolio piece.

## The four-layer architecture

Everything here belongs to one of four layers. Each has a distinct job, and
they compose:

```text
   ┌─ Layer 1 · CLAUDE.md ............. persistent context, every session
   │
   ├─ Layer 2 · .claude/skills/ ...... auto-invoked knowledge (progressive)
   │
   ├─ Layer 3 · .claude/agents/ ...... delegated sub-tasks, isolated context
   │
   └─ Layer 4 · .claude/settings.json  deterministic hooks + permissions
```

- **CLAUDE.md** — persistent context loaded at the start of every session.
- **Skills** (`.claude/skills/`) — knowledge Claude auto-invokes by relevance.
- **Agents** (`.claude/agents/`) — subagents with scoped tools for delegation.
- **Hooks** (`.claude/settings.json`) — deterministic safety and automation.

## How to read this repo

With five minutes, read these in order:

1. `CLAUDE.md` — the kernel. It stays under 120 lines with exactly five
   sections, so Claude follows it instead of skimming.
2. `.claude/skills/product-marketing/SKILL.md` — the anchor skill every other
   skill reads first for shared product and audience context.
3. `.claude/skills/derek-voice/SKILL.md` and
   `.claude/skills/pool-app-cro/SKILL.md` — two custom skills layered on top.
4. `goals/` — reusable `/goal` templates whose "done" is mechanically
   verifiable: a lint exit code, a file count, a clean tree.
5. `.claude/agents/code-reviewer.md` — a read-only subagent with a scoped
   tool list.
6. `docs/` — shared reference material skills read via `@docs/<file>.md`.

## Repository layout

```text
dereks-ai-os/
├── CLAUDE.md            # persistent context (the kernel)
├── README.md           # you are here
├── .gitignore          # excludes local/secret files and node_modules
├── .markdownlint.json  # markdown lint configuration
├── .claude/
│   ├── settings.json   # hooks + permissions (committed)
│   ├── skills/         # auto-invoked skills
│   └── agents/         # scoped subagents
├── goals/              # reusable /goal templates
└── docs/               # shared reference context
```

## What I learned

Three ideas did most of the work. First, a CLAUDE.md reads like code, not
documentation: short, specific, verifiable lines beat prose, and staying under
~120 lines keeps Claude actually following it. Second, a skill's `description`
is load-bearing — it is what Claude reads to decide whether to invoke a skill,
so "When the user wants…" plus a "For X, see Y" cross-reference matters more
than the body. Third, `/goal` is only safe when "done" is something the
transcript can prove and turns are capped; "looks good" is not a finish line.
The payoff is leverage: one folder does real O7 marketing work and, at a
glance, shows how I build with AI.

## Status

A live workspace, pinned to the Claude Code features and model lineup current
as of mid-2026. Client data and secrets stay in gitignored local files
(`CLAUDE.local.md` and `.claude/settings.local.json`).
