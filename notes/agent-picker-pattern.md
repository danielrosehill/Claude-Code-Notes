# The Agent Picker Pattern

25-03-2026

[Claude-Agent-Picker-Pattern](https://github.com/danielrosehill/Claude-Agent-Picker-Pattern) addresses the "too many subagents" problem in Claude Code.

## The Problem

If you've built up a library of subagents, loading them all into every project floods the context window and degrades inference quality. But manually selecting which agents to deploy per project is tedious — and you'd have to re-do it every time.

## The Pattern

A "Harsh Team Picker Guy" (HTPG) orchestration agent — yes, really — that:

1. Reads a centralised agent farm (`~/subagents`)
2. Shortlists subagents appropriate for the current project
3. Trims the crew to fit within a user-set context budget
4. Applies variable-based config tweaks
5. Deploys the final crew to `.claude/agents`

The `/agent-picker` slash command triggers the selection process.

## The Analogy

Think of it like casting for a film. You've got a roster of actors (agents) with different specialities. Instead of hiring everyone for every production, the casting director (HTPG) picks the right team for this specific project, within budget.

## Why This Matters

Subagent management is an under-discussed scaling problem. It's fine when you have 3-5 agents, but once you've built 20+ specialists, you need some kind of selection and deployment mechanism. This is one approach.

**Disclaimer**: Primarily a conceptual/design document with a reference implementation. The "Harsh Team Picker Guy" naming is... intentional.

## Source

- [Claude-Agent-Picker-Pattern](https://github.com/danielrosehill/Claude-Agent-Picker-Pattern)
