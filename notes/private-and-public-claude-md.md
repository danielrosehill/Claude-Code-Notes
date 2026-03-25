# Private And Public CLAUDE.md

25-03-2026

[Private-And-Public-Claude-MD](https://github.com/danielrosehill/Private-And-Public-Claude-MD) addresses a real tension: you want to commit your `CLAUDE.md` to share project context with collaborators, but some of your instructions contain sensitive information.

## The Two-Tier Setup

- **`CLAUDE.md`** — Safe to commit. Project-level instructions, architecture notes, coding conventions.
- **`CLAUDE_PRIVATE.md`** — Never committed. API keys, personal preferences, sensitive system details, internal URLs.

## The Tooling

A `setup-claude-private-gitignore.sh` script that adds `CLAUDE_PRIVATE.md` to your **global** gitignore, applying the exclusion across all repositories system-wide. No per-repo `.gitignore` editing needed.

Also includes a Claude Code slash command to automate the setup.

## Why Global Gitignore

The clever bit is using the global gitignore rather than per-repo. Once you run the setup script, `CLAUDE_PRIVATE.md` is excluded from every repo on your machine. You can freely create it in any project directory without worrying about accidentally committing secrets.

## Practical Takeaway

If you work on public repos or collaborate with others, some form of public/private CLAUDE.md separation is essential. The specific mechanism (global gitignore, per-repo gitignore, `.claude/` private directory) matters less than the principle: never commit sensitive instructions to a shared repo.

This is also relevant if you put API keys or personal preferences in your CLAUDE.md — easy to do by accident, especially when Claude itself helps edit the file.

**Disclaimer**: The `CLAUDE_PRIVATE.md` filename isn't officially recognised by Claude Code (as of writing) — it's a convention. You'd need to reference it from your main `CLAUDE.md` with a pointer so Claude knows to read it.

## Source

- [Private-And-Public-Claude-MD](https://github.com/danielrosehill/Private-And-Public-Claude-MD)
