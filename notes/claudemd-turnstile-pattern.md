# The CLAUDE.md Turnstile Pattern

25-03-2026

The "turnstile" pattern is an idea I documented in [ClaudeMD-Turnstile](https://github.com/danielrosehill/ClaudeMD-Turnstile) for handling repos where different audiences need different instructions.

## The Problem

A lot of repos serve multiple audiences. Developers contributing code need one set of instructions; end users setting up the software need completely different guidance. If you dump all of that into a single monolithic `CLAUDE.md`, Claude ingests everything regardless of who's using it. A developer gets buried in deployment instructions they don't need; a user gets confused by internal architecture notes.

## The Pattern

The root `CLAUDE.md` acts as a lightweight dispatcher — a turnstile — rather than a monolithic instruction set. It routes the agent toward role-specific context files in subdirectories:

```
CLAUDE.md              ← "Who are you? Developer or user?"
context/developer/     ← Architecture, coding conventions, PR guidelines
context/user/          ← Setup instructions, configuration, troubleshooting
```

The turnstile file itself is minimal. It just needs enough to help Claude determine which path to take based on the conversation context.

## When This Is Useful

This is especially valuable for open source projects with both contributor and consumer audiences, internal tools with both developer and ops personas, or any repo where the instruction surface area is large enough that loading everything would waste context.

**Disclaimer**: This is a pattern I've been experimenting with. It works well for my use cases, but YMMV depending on how your repos are structured and who's using them.

## Source

- [ClaudeMD-Turnstile](https://github.com/danielrosehill/ClaudeMD-Turnstile)
