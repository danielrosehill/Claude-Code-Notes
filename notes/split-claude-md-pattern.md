# The Split CLAUDE.md Pattern

25-03-2026

I documented this pattern in [Split-Claude-MD-Pattern](https://github.com/danielrosehill/Split-Claude-MD-Pattern) and it's become central to how I use Claude Code on my desktop.

## The Core Idea

Your `~/.claude/CLAUDE.md` loads into *every single Claude Code session* on your machine. If it's a 500-line monolith covering your hardware specs, Python environment, MCP configs, network topology, and personal preferences — all of that gets injected before you've even typed a word, every time.

The split pattern keeps `~/.claude/CLAUDE.md` as a lean entrypoint (30-50 lines) and moves topic-specific context into `~/.claude/context/` files that Claude reads on demand.

## Important Detail

Use `~/.claude/CLAUDE.md`, **not** `~/CLAUDE.md`. Both are recognised by Claude Code, but using both creates redundant overlapping contexts. Pick one — the `.claude` directory path is cleaner.

## What The Entrypoint Looks Like

Just a table of pointers:

```markdown
I'm Daniel. This is my Ubuntu workstation.

| File | Contents |
|------|----------|
| `context/system-environment.md` | OS, hardware, network |
| `context/development-environment.md` | Languages, tools, git |
| `context/media-tools.md` | Audio, video, image tools |
```

None of those files get loaded unless Claude actually needs them. The agent knows *where* to look without having to *read* everything upfront.

## The Template

The repo includes a full demo with a synthetic persona ("Alex Chen") so you can fork it and replace with your own details rather than starting from scratch.

**Disclaimer**: This is very much my personal approach. Some people prefer keeping everything in one file for simplicity — that's valid too, especially if your context is small enough.

## Source

- [Split-Claude-MD-Pattern](https://github.com/danielrosehill/Split-Claude-MD-Pattern)
