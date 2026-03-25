# Split Context Setup — Automating The Split

25-03-2026

If the [Split CLAUDE.md Pattern](split-claude-md-pattern.md) is the theory, [Split-Context-Setup](https://github.com/danielrosehill/Split-Context-Setup) is the automation.

## What It Does

It's a slash command (`/chunk-claude`) that converts a bloated repo-level `CLAUDE.md` into a lean entrypoint backed by a structured `context/` store. Instead of manually extracting sections and creating files, you run the command and it handles the whole migration.

## The Sequence

1. Prunes `CLAUDE.md` to essentials
2. Scaffolds `context/` with topic subfolders
3. Creates `context/pipeline/` with `audio/` and `documents/` directories for raw context ingestion
4. Adds subagent templates (`pipeline-processor`, `context-organizer`) in `context/agents/`
5. Creates a `MEMORY.md` to distinguish working patterns from project context

## The Pipeline Concept

The interesting addition beyond simple splitting is the `pipeline/` directory. This is designed for dumping raw inputs — voice note transcripts, document excerpts, unstructured notes — that the subagents then process and route into the appropriate context files. It's a lightweight ingestion system.

## When To Use This

If you've got a repo with an unwieldy `CLAUDE.md` that's grown organically over time, this is the quick fix. Run `/chunk-claude`, review what it produced, and you're done.

**Disclaimer**: The scaffolding it generates reflects my preferred directory structure. You'll likely want to adjust the categories and subfolders to match your own organisation.

## Source

- [Split-Context-Setup](https://github.com/danielrosehill/Split-Context-Setup)
