# Claudify-This & Claude-Repo-Retrofitter

25-03-2026

Two related tools for the same broad problem: getting repos ready for Claude Code when they weren't built with it in mind.

## Claudify-This

[Claudify-This](https://github.com/danielrosehill/Claudify-This) is a slash command (`/claudify-repo`) that audits a repo's Claude Code setup and fills in what's missing — `CLAUDE.md`, slash commands, subagents, settings, MCP config. It's positioned as a smarter alternative to Claude Code's built-in `/init` because it actually inspects the project type and tailors its suggestions rather than generating a generic baseline.

Install it with `./install.sh` after cloning; the command becomes available globally.

## Claude-Repo-Retrofitter

[Claude-Repo-Retrofitter](https://github.com/danielrosehill/Claude-Repo-Retrofitter) takes this idea and scales it up for bulk operations. If you've got hundreds of repos and want to batch-retrofit them with Claude Code scaffolding, this is the tool.

Key skills:
- `/repo-retrofitter:scan` — inventory a directory of repos
- `/repo-retrofitter:auto` — fully autonomous scan + retrofit
- `/repo-retrofitter:interactive` — guided per-repo approval

What gets added: `CLAUDE.md`, `AGENTS.md`, scaffold folders (`context-data/`, `planning/`, `pm/`, `from-ai/`, `user-docs/`), slash commands, subagents, and MCP recommendations tailored to the tech stack.

It runs `git pull` before changes, never touches source code, and tracks processed repos in `scan-log.json` to avoid redundant re-visits.

## The Broader Point

Most of us have repos that predate Claude Code. The friction of onboarding an AI agent into a repo that wasn't designed for agents is real. These tools automate what would otherwise be tedious manual scaffolding across many projects.

**Disclaimer**: These are my tools for my workflow. The scaffolding they generate reflects my preferences for directory structure and context organisation — fork and adapt as needed.

## Sources

- [Claudify-This](https://github.com/danielrosehill/Claudify-This)
- [Claude-Repo-Retrofitter](https://github.com/danielrosehill/Claude-Repo-Retrofitter)
