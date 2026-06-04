# /goal templates

Reusable `/goal` conditions with mechanically verifiable end states. Each one
caps turns and states how "done" is proven from the transcript.

- `audit-claude-md.md` — keep CLAUDE.md within its size and section limits.
- `redesign-screen.md` — redesign a screen against a checkable visual spec.

Use a template only when "done" is something the transcript can prove (a lint
exit code, a file count, a clean tree), never for "looks good."
