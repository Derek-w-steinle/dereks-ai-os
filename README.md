# Derek's AI OS

This is a Claude Code workspace I built and use as a personal AI operating
system. It's one Git-tracked folder that turns Claude Code into a repeatable
assistant for the marketing work I did at Original 7, the residential pool
company where I ran service operations and marketing. It did real work, 
and the structure itself, not any one output, is the point.

I taught myself to build this. The goal was simple: stop re-explaining the same
context to a chat window every day, and encode it once in a way Claude loads and
follows on its own. What's here is the result, organized so anyone can open it
and see how I think about building with AI.

## The four-layer architecture

Everything in this repo belongs to one of four layers. Each has a distinct job,
and they stack:

```text
Layer 1 · CLAUDE.md ............ persistent context, loaded every session
Layer 2 · .claude/skills/ ...... knowledge Claude auto-invokes by relevance
Layer 3 · .claude/agents/ ...... scoped subagents for delegated work
Layer 4 · .claude/settings.json  permissions now, hooks next
```

- **CLAUDE.md**: the context Claude loads at the start of every session. The
  kernel of the whole thing.
- **Skills** (`.claude/skills/`): focused knowledge Claude pulls in only when
  it's relevant, so the context window stays clean.
- **Agents** (`.claude/agents/`): subagents with scoped, read-only tools for
  delegated tasks like code review.
- **Settings** (`.claude/settings.json`): a permissions allowlist that keeps
  Claude to safe, read-only commands. Deterministic hooks are the next layer
  I'm adding.

## A skill in action: derek-voice

The clearest example of how this works is `derek-voice`. The problem it solves
is simple: AI writes in a generic, recognizable voice, and I send a lot of
customer texts, emails, and internal messages that need to sound like me, not
like a chatbot.

The skill is two parts. `.claude/skills/derek-voice/SKILL.md` holds the rules
and triggers and stays short, so it's cheap to keep loaded.
`docs/writing-samples.md` holds the real, name-stripped examples, organized by
who I'm writing to: customers, my team, and social. The skill loads the samples
only when it fires. That's progressive disclosure, the pattern Anthropic
recommends for skills, working in a real folder.

What it does in practice: I paste in a rough message or a customer email and say
nothing else. Claude recognizes it should write in my voice, reads the samples,
picks the right register, and writes it the way I would. No em dashes, no
corporate filler, no AI tells. That last part is the whole point.

Read `.claude/skills/derek-voice/SKILL.md` and `docs/writing-samples.md`
together. That pair is the system at its most complete.

## Read it in five minutes

In order:

1. `CLAUDE.md`: the kernel. It stays under 120 lines with exactly five sections,
   so Claude follows it instead of skimming it.
2. `.claude/skills/derek-voice/SKILL.md` with `docs/writing-samples.md`: the
   most complete skill and its backing context. Start here to see the pattern
   end to end.
3. `.claude/skills/product-marketing/SKILL.md`: the anchor skill the other
   marketing skills read first for shared positioning.
4. `.claude/skills/pool-app-cro/SKILL.md`: a scoped skill for conversion work on
   the pool inspection app.
5. `goals/`: reusable `/goal` templates whose finish line is mechanically
   verifiable. A lint exit code, a file count, a clean tree, not "looks good."
6. `.claude/agents/code-reviewer.md`: a subagent with a read-only, scoped tool
   list.

## Repository layout

```text
dereks-ai-os/
├── CLAUDE.md             # persistent context (the kernel)
├── README.md             # you are here
├── .gitignore            # excludes local notes, secrets, node_modules
├── .markdownlint.json    # markdown lint config
├── .claude/
│   ├── settings.json     # permissions allowlist (committed)
│   ├── skills/           # auto-invoked skills
│   │   ├── derek-voice/
│   │   ├── product-marketing/
│   │   └── pool-app-cro/
│   └── agents/
│       └── code-reviewer.md
├── docs/                 # shared reference the skills read
│   ├── writing-samples.md
│   └── product-marketing.md
└── goals/                # reusable /goal templates
```

## What I learned building it

Three things did most of the work.

A CLAUDE.md should read like code, not documentation. Short, specific, checkable
lines beat prose, and keeping it under about 120 lines is what makes Claude
actually follow it.

A skill's `description` is the load-bearing part. It's what Claude reads to
decide whether to use the skill at all, so getting the trigger right matters
more than the body. I write each one as "when the user wants X," plus a pointer
to the related skill.

`/goal` only works when "done" is something the transcript can prove and the
turns are capped. A lint exit code or a file count is a finish line. "Looks
good" is not.

The payoff is leverage. One folder does real work and, at a glance, shows how I
build with AI.

## Status and roadmap

This is a live workspace, pinned to the Claude Code features and model lineup
current as of mid-2026. Client data and secrets stay in gitignored local files
(`CLAUDE.local.md` and `.claude/settings.local.json`), never in anything
committed here.

Live now: the kernel, the `derek-voice` skill with its full sample library, the
skill and agent structure, a read-only permissions allowlist, and the `/goal`
templates.

On the roadmap: deterministic hooks in `settings.json` (auto-format on save,
lint must pass before a task counts as done), fleshing out the
`product-marketing` context file, and a redesign pass on the pool inspection app
driven by `pool-app-cro`.
