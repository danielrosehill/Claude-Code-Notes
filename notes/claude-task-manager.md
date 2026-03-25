# Claude Task Manager

25-03-2026

[Claude-Task-Manager](https://github.com/danielrosehill/Claude-Task-Manager) is a spec for a sequential task queue for Claude Code and other agentic coding tools.

## The Problem It Solves

Context window exhaustion is real. When you're working on a multi-task project, each task eats into the context window, and by task three or four, Claude starts losing track of earlier work. The manual workaround is to keep clearing context and re-briefing — tedious and error-prone.

## The Design

A queue system that:
- Accepts freeform or voice input, parsed into discrete tasks
- Auto-prioritises (fixes before features)
- Executes one task at a time with a fresh context per task
- Is tool-agnostic (Claude Code, Open Code, etc.)

The key design decision: **no parallel workers**. The spec deliberately avoids worktree-based parallelism due to merge conflict risks and API rate-limit issues. Sequential execution with fresh context per task is the bet.

## Status

Planning/spec stage — includes voice notes, transcripts, and a SPEC.md. No functional implementation yet.

## Why This Matters

The underlying insight is correct: context window management is one of the biggest practical bottlenecks in agentic coding. Whether the solution is a queue system, better context compression, or something else entirely — this is a real friction point that needs addressing.

**Disclaimer**: This is at the idea/spec stage. Whether sequential single-task execution actually outperforms parallel approaches in practice remains to be proven.

## Source

- [Claude-Task-Manager](https://github.com/danielrosehill/Claude-Task-Manager)
