# Claude Handover Plugin

06-04-2026

[Claude-Handover](https://github.com/danielrosehill/Claude-Handover) is a plugin that formalises the session-handover procedure between Claude Code agents — including spawning a fresh Konsole window with Claude already running and pre-loaded to resume, so the handoff is as seamless as possible.

## The Problem

You hit context limits, or you want to end a session, or a long-running task is half-done. The next agent (you, tomorrow, or a fresh `claude` invocation) shouldn't have to reverse-engineer where things stood. Ad-hoc "let me write a HANDOVER.md" works, but it's inconsistent and easy to skip.

## The Plugin

Three commands:

- `/handover:create` — spawns a dedicated `handover-writer` subagent that inspects git status, recent commits, diffs, active plans, failing tests, and key files, then writes a structured `HANDOVER.md` at the repo root. The doc is written **for another AI agent**, not a human — precise, actionable, self-contained.
- `/handover:resume` — reads `HANDOVER.md`, internalises it, deletes the file, and continues work.
- `/handover:handoff` — the full one-shot sequence: writes the handover, then **opens a new Konsole terminal with Claude Code already running and pre-loaded with `/handover:resume`**. One command ends a session and spawns a fresh agent that's already picking up where you left off.

## Why The Konsole Spawn Matters

The Konsole-spawn step is the bit that turns this from "another markdown convention" into an actual workflow. You don't have to remember to start a new session, navigate to the repo, run the resume command, etc. One command, fresh context window, work continues.

(KDE/Konsole-specific — would need adapting for other terminals.)

## Relation To The Planning Folder Pattern

This overlaps with the [planning folder + UUID pattern](planning-folder-uuid.md) but solves a different slice:

- **Handover plugin** = "end this session cleanly and resume in a new one, automatically"
- **Planning folder** = "durable, addressable plan artifacts I can return to whenever"

Use both: the handover captures *right-now* state at session end; the planning folder holds the longer-lived plan that handovers reference.

## Source

- [Claude-Handover](https://github.com/danielrosehill/Claude-Handover)
