# Make Agent Friendly

25-03-2026

[Make-Agent-Friendly](https://github.com/danielrosehill/Make-Agent-Friendly) is a Claude Code plugin for preparing inherited or human-built codebases for agentic development.

## The Problem

You've inherited a codebase — or you built something before AI coding tools existed — and now you want to use Claude Code on it. The repo has no `CLAUDE.md`, no context directory, no slash commands, and the folder structure wasn't designed with agent navigation in mind. Claude *can* work in this repo, but it's going to spend a lot of context figuring out the basics.

## What It Does

Run `/make-agent-friendly` in any repo and Claude:

1. Analyses the existing structure
2. Asks intake questions about the project
3. Restructures folders for agent navigability
4. Creates `CLAUDE.md` and `/context/` infrastructure
5. Updates documentation
6. Validates before committing

The key word is "refactoring for agentic readiness" — it's not adding features or changing logic, just making the codebase navigable and contextualised for AI tools.

## How It Differs From Claudify-This

[Claudify-This](claudify-and-retrofit.md) audits and fills in Claude Code scaffolding (CLAUDE.md, commands, settings). Make-Agent-Friendly goes deeper — it actually restructures the repo's directory layout and documentation to be more agent-friendly. It's about the codebase itself, not just the Claude Code config on top of it.

## Practical Takeaway

The broader principle: the structure of your codebase affects how well AI tools work with it. Clear directory organisation, good README files, and explicit architecture documentation aren't just good engineering practices — they're performance optimisations for agentic workflows.

Available as a Claude Code plugin or legacy slash command.

**Disclaimer**: Restructuring a codebase is a significant operation. Review the changes carefully before committing.

## Source

- [Make-Agent-Friendly](https://github.com/danielrosehill/Make-Agent-Friendly)
