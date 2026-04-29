# Can the cwd constraint be defeated in Claude Code?

**Date:** 29/04/2026
**Claude Code version at time of writing:** 2.1.123

## Question

Can the cwd constraint be defeated in Claude Code, or is it baked into the harness? For my sysadmin use case it's very challenging to constantly work around. What would be ideal for me is if Claude could `cd` once to a directory and then assume position there — so no sandboxing at the FS level, but still some concept of "this is where we are working."

## Answer

It's a harness-level constraint, not something you defeat by tricking the model — but it's configurable, and the "cd once and assume position" model is basically the default.

**What's actually enforced**

- File tools (Read / Write / Edit / Glob / Grep) are gated to the **workspace roots**: the directory you launched `claude` in, plus any additional directories you've explicitly added.
- Bash isn't filesystem-gated the same way — `cd` works and persists between Bash calls in a session — but the structured file tools won't touch paths outside the roots.

**Ways to widen the working set**

1. `cd /where/you/work && claude` — that directory becomes the root for the session. Closest match to "cd once and assume position."
2. `claude --add-dir /etc --add-dir /var/log ...` at launch, or `/add-dir <path>` mid-session, to add more roots without losing the original.
3. Persist roots in settings: `additionalDirectories` in `~/.claude/settings.json` (or project `.claude/settings.json`) — same effect as `--add-dir`, every session.
4. For full-system sysadmin work: launch from `/` (everything is in scope), or run with `--dangerously-skip-permissions` to skip permission prompts entirely. Both trade safety for ergonomics — fine on your own workstation, not on shared boxes.

So for sysadmin sessions: `cd` to your primary working dir, launch `claude` with `--add-dir` for the cross-cutting paths you know you'll hit (`/etc`, `/var/log`, `/usr/local`), and you've got one home base plus the extras without fighting the harness.

---

*Claude Code moves fast — this may be outdated by the time you read it.*
