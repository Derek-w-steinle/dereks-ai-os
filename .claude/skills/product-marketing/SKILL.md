---
name: product-marketing
description: When the user wants to establish or reuse shared product, audience, and positioning context for Original 7 marketing work. Use this first so other marketing skills inherit consistent positioning. Also use when the user mentions positioning, ICP, audience, value proposition, or messaging. For brand voice, see derek-voice; for conversion work on the pool app, see pool-app-cro.
---

# Product marketing context (anchor skill)

This is the foundation skill. Every other marketing skill reads the shared
context this skill maintains before asking the user to repeat themselves.

## Read shared context first

Check for `docs/product-marketing.md`. If it exists, read it and treat it as the
source of truth for product, audience, and positioning. Only ask the user for
information that is missing or specific to the current task.

In Claude Code, this line auto-injects the context at the top of a session:

```text
Product context: !`cat docs/product-marketing.md 2>/dev/null || echo "No product context file found — ask the user about their product before proceeding."`
```

## What this skill maintains

- **Product** — what O7 sells, core features, and the problem it solves.
- **Audience / ICP** — who buys, their jobs-to-be-done, and objections.
- **Positioning** — the one-sentence value proposition and differentiators.
- **Voice** — tone and phrasing rules (see `derek-voice`).

## When context is missing

If `docs/product-marketing.md` is absent or thin, interview the user in short
rounds (product, then audience, then positioning, then voice), then write the
answers back to `docs/product-marketing.md` so future sessions inherit them.

For writing in O7's voice, see `derek-voice`. For conversion-rate work on the
pool inspection app, see `pool-app-cro`.
