# Claude Repo Jumper

25-03-2026

[Claude-Repo-Jumper](https://github.com/danielrosehill/Claude-Repo-Jumper) is a slash command idea for automating the "repo handover" workflow in multi-repo projects.

## The Problem

When you're building a multi-component system across several repos, spinning up a new repo involves a lot of manual context transfer: secrets, webhook URLs, config values, architecture decisions from the parent project. You end up copy-pasting between terminals and manually writing `CLAUDE.md` files that reference the other repos.

## The Concept

Run a slash command in your current repo and it:

1. Creates a new private GitHub repo
2. Gathers context from the current repo (secrets, webhook URLs, config)
3. Generates a `CLAUDE.md` in the new repo pre-loaded with that context
4. Pushes to initialise it

Essentially a clean handover — the new repo starts life already knowing about the system it's joining.

## Status

This is currently at the planning/idea capture stage. The system prompt is documented but the implementation is pending. It's a good example of the kind of workflow friction that could be solved with a well-designed slash command.

**Disclaimer**: Placeholder repo — the concept is solid but execution hasn't landed yet.

## Source

- [Claude-Repo-Jumper](https://github.com/danielrosehill/Claude-Repo-Jumper)
