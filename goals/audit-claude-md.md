# Goal: audit CLAUDE.md

Paste the block below after `/goal`, with auto mode on and a clean tree.

```text
Audit CLAUDE.md against the workspace standard.
Done when:
- CLAUDE.md is between 60 and 120 lines (verify: wc -l CLAUDE.md)
- it has exactly 5 level-2 headings (verify: grep -c "^## " CLAUDE.md returns 5)
- no personality directive is present
- every "Do not X" is rewritten as "Prefer Y over X"
- CLAUDE.md.backup exists with the original
Report the output of each verify command before declaring done.
Stop after 10 turns.
```
