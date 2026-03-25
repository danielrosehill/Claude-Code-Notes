# No Wheel Inventions

25-03-2026

[No-Wheel-Inventions](https://github.com/danielrosehill/No-Wheel-Inventions) tackles one of the most annoying tendencies of AI coding assistants: writing custom code when perfectly good open source libraries exist.

## The Problem

Claude (and every other LLM) has a bad habit of implementing things from scratch rather than reaching for well-maintained packages. You ask for CSV parsing and get a hand-rolled regex parser. You ask for date handling and get artisanal string manipulation. It's technically impressive and practically terrible.

## The Toolkit

Two modes of operation:

**Prevention**: Inject a philosophy snippet into `CLAUDE.md` or run `/DevUtils:starting-instruction` at the start of a project. This primes Claude to check for existing packages before writing custom code.

**Remediation**: Run `/DevUtils:retrospective` to audit an existing codebase for wheel-reinvention. It identifies code that could be replaced with established libraries.

Installs to `~/.claude/commands/DevUtils/` and `~/.claude/agents/`.

## Practical Takeaway

This is one of those tools where the concept is almost more valuable than the implementation. Even if you don't install the slash commands, the underlying principle — explicitly telling Claude to prefer existing packages — should be in every project's `CLAUDE.md`. Something like: "Before writing utility code, check if a well-maintained npm/pip package exists for this."

**Disclaimer**: The definition of "wheel reinvention" is subjective. Sometimes a 5-line utility function really is better than adding a dependency. Use judgement.

## Source

- [No-Wheel-Inventions](https://github.com/danielrosehill/No-Wheel-Inventions)
