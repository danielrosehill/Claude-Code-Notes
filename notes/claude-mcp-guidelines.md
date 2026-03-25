# Claude MCP Guidelines

25-03-2026

[Claude-MCP-Guidelines](https://github.com/danielrosehill/Claude-MCP-Guidelines) is a snippet for your global `~/.claude/CLAUDE.md` that gives Claude deterministic guidance on which MCPs to prefer and when.

## The Problem

Two issues with MCP usage in Claude Code:

1. **Missing context**: Some MCPs need explanatory guidance that no environment variable provides. Claude might have access to a tool but not know *when* it's the right choice.
2. **Tool conflicts**: When an MCP tool overlaps with Claude's built-in capabilities (e.g., a web-fetch MCP versus Claude's native fetch), which should win? Without guidance, the behaviour is unpredictable.

## The Approach

A structured snippet in your home-level `CLAUDE.md` that:
- Lists available MCPs with one-line descriptions of when to use each
- Defines priority rules for conflicts (e.g., "prefer Context7 MCP for documentation lookups over native web fetch")
- Adds context that helps Claude make better tool selection decisions

## Self-Aware Ephemerality

The author (me) explicitly notes this is a short-lived experiment. The expectation is that Anthropic will eventually build better MCP orchestration into the platform itself, making user-level hacks like this unnecessary. But until then, it meaningfully improves MCP invocation predictability.

## Practical Takeaway

Even a few lines about MCP preferences in your `CLAUDE.md` can reduce the randomness of tool selection. If you've got multiple MCPs with overlapping capabilities, explicit guidance is worth adding.

**Disclaimer**: Experimental snippet. MCP behaviour changes with Claude Code updates, so revisit periodically.

## Source

- [Claude-MCP-Guidelines](https://github.com/danielrosehill/Claude-MCP-Guidelines)
