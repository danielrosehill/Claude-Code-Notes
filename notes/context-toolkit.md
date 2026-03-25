# Claude Code Context Toolkit

25-03-2026

[Claude-Code-Context-Toolkit](https://github.com/danielrosehill/Claude-Code-Context-Toolkit) is a plugin implementing a two-file context workflow.

## The Two Files

- **`CONTEXT.md`** — Human-friendly scratchpad. Conversational, messy, voice-transcription-ready. This is where *you* dump context in whatever form it arrives.
- **`CLAUDE.md`** — Structured, agent-optimised briefing. Auto-read by Claude Code. This is what the *agent* consumes.

## The Insight

Humans and LLMs express and process information differently. You might voice-dictate a rambling description of what you're building. Claude needs structured, categorised instructions. The toolkit bridges that gap with slash commands that convert between the two formats.

## Key Commands

- `/context-to-claude` — Transform human scratchpad into agent instructions
- `/claude-to-context` — Reverse: extract human-readable context from structured CLAUDE.md
- `/add-to-context` — Append to the scratchpad
- `/remove-from-context` — Remove from the scratchpad
- `/chunk-repo-context` — Break up large context into manageable pieces

Plus hooks that auto-remind you when the two files go out of sync.

## Practical Takeaway

The separation of "how I think about this project" from "how I instruct the agent about this project" is genuinely useful. Even without the full toolkit, maintaining a `CONTEXT.md` scratchpad alongside your `CLAUDE.md` is a pattern worth adopting — especially if you use voice input.

**Disclaimer**: This plugin reflects a specific workflow (voice input → structured output). If you type everything precisely from the start, the two-file pattern may be overhead you don't need.

## Source

- [Claude-Code-Context-Toolkit](https://github.com/danielrosehill/Claude-Code-Context-Toolkit)
