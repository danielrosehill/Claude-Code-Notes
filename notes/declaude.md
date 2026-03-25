# Declaude — AI Style Conformity

25-03-2026

[Declaude](https://github.com/danielrosehill/Declaude) is a system for building personal writing rules and enforcing them on AI-generated content via a `/declaude` slash command.

## The Problem

AI-generated technical documentation has a distinctive voice: overly enthusiastic, littered with filler phrases ("Let's dive in!", "Great question!"), loves passive voice, and defaults to corporate-speak. If you're publishing AI-assisted content under your own name, you want it to sound like *you*.

## How It Works

1. **Rules**: Individual markdown files in a `rules/` directory, each defining a writing preference (e.g., "no emojis in technical docs", "prefer active voice", "don't use the word 'leverage'")
2. **Vocabulary**: Avoidance lists in `vocab/` — words and phrases to never use
3. **Consolidation**: An LLM-powered Python script (`consolidate_rules.py`) merges rules and vocab into a versioned prompt (uses OpenRouter API)
4. **Execution**: The output becomes a `/declaude` slash command that rewrites AI-generated content to match your personal style

## The Workflow

Write → Generate AI content → Run `/declaude` → Get content that sounds like you wrote it.

The rules accumulate over time. Every time you spot an AI-ism that annoys you, add a rule file. The consolidated prompt gets better with each addition.

## Practical Takeaway

Even without the full tooling, maintaining a personal "AI style guide" is worth doing. A few lines in your project's `CLAUDE.md` about tone preferences can dramatically improve output quality.

**Disclaimer**: This is highly personal — my rules reflect my pet peeves. Your writing preferences will be completely different.

## Source

- [Declaude](https://github.com/danielrosehill/Declaude)
