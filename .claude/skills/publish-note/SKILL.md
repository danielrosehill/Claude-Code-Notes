---
name: publish-note
description: Commit and push the current state of the Claude-Code-Notes repo — use after Daniel approves a drafted note (or batch of notes) and says "publish", "ship it", "push", or similar. Follows Daniel's git rule — commit everything, push immediately.
---

# Publish Note

Release whatever is staged/unstaged in the notes repo. Daniel's git rule: always commit ALL changes and push immediately — no splitting, no leaving unpushed work.

## Steps

1. `cd` into `~/repos/github/my-repos/Claude-Code-Notes` (use absolute paths in commands).

2. `git status` — show Daniel what's about to ship. If nothing to commit, say so and stop.

3. Stage everything: `git add -A` (scoped to this repo — safe here, it's a notes repo with no secrets).

4. Commit with a concise message describing the note(s) added/updated. Message format:
   - Single note: `Add note: <Title>`
   - Multiple notes: `Add <N> notes: <short, comma-separated titles>`
   - Updates to existing note: `Update note: <Title>`

5. `git push`.

6. Report the short SHA and the pushed message back to Daniel.

## Notes

- Do not amend. New commit every time.
- Do not use `--no-verify`.
- If the push fails, surface the error — don't retry blindly.

## User input

$ARGUMENTS
