# CLAUDE.md - Strategic Separation!

25-03-2026

CLAUDE.md serves as the system prompt in Claude Code. Other agentic frameworks mirror the approach with their own markdown file.

One of the most underconsidered aspects of Claude Code (IMO!) is how the chaining (I call it concatenation) of these instructions work.

Palo Perrone, writing in Hackernoon had [this](https://hackernoon.com/the-complete-guide-to-ai-agent-memory-files-claudemd-agentsmd-and-beyond) to say about this critical question - which is clearer than Anthropic's own documentation:

"The hierarchy loads bottom-up. Enterprise policies load first, then your personal preferences, **then project-level, then subdirectory-level. More specific instructions override broader ones**."

I've added the highlight for emphasis.

## Practical Takeaways

I use Claude Code as a general purpose assistant. The idea of thinking of an agentic CLI as purely a tool for code generation within repos never connected with me. I run Ubuntu. Hence, I pop Claude open all the time at arbitrary positions on my filesystem - disproportionately the home folder but also .... random nooks and crannies.

This doesn't gel very intuitively with how Anthropic has designed the tool, but it is something worth doing deliberately and carefully because the point in the file system at which you open Claude has important ramifications for how freely the agent will be able to move. Although if you run Claude with dangerous permissions, these concerns are mostly negated.

Coming back to Peronne's point above, this is where there is an enormous risk of not only context bloat, but also Claude ingesting conflicting instructions before it's even received the first user prompt, degrading reasoning and task performance.

For example, let's say you have a setup like mine:

`/daniel/CLAUDE.md` - General OS-level instructions
`/daniel/programs/CLAUDE.md` - "Hey Claude, this is where and how I like to store programs on this OS!"
`/daniel/programs/ai-ml/CLAUDE.md` - "This is where I put my AI and ML projects"
`/daniel/programs/ai-ml/voice-typer-v1/CLAUDE.md` - Detailed project specific context for a repo I'm working on.

Then:

If Perrone's understanding and mine is correct, Claude will have to process all four CLAUDE.md files before every single user prompt. Even with prompt caching, it seems like a lot of potential bloat.

## The Split Pattern

This is why I have shifted to creating a folder structure that - wherever possible - tries to use the base level CLAUDE.md merely as an entrypoint pointing to deeper context - so that the agent only ingests it when needed.

So instead of my home folder being a huge CLAUDE.md monolith, it's a lightweight file that looks something like this:

`~/CLAUDE.md` - I'm Daniel. This is my computer. The programs I prefer are in `~/.claude/context/program-preferences.md`

I've documented this user-level approach more formally in [Split-Claude-MD-Pattern](https://github.com/danielrosehill/Split-Claude-MD-Pattern). The core idea: keep `~/.claude/CLAUDE.md` as a minimal entrypoint (30–50 lines) and put topic-specific context in `~/.claude/context/` files that Claude reads on demand. One important detail documented there: use `~/.claude/CLAUDE.md`, **not** `~/CLAUDE.md` — both are recognised by Claude Code, but using both creates redundant overlapping contexts.

To make this concrete, here's what my `~/.claude/context/` directory currently looks like:

| File | Purpose |
|------|---------|
| `system-environment.md` | OS, hardware, storage, network layout, audio/input devices |
| `development-environment.md` | Languages, toolchains, containers, Python strategy, git config |
| `file-organization.md` | Where repos, scripts, programs, backups, and Obsidian vaults live |
| `mcp-usage.md` | Which MCP servers are configured and how to use them |
| `mcp-provisioning.md` | Rules for creating/configuring new MCP connections |
| `media-tools.md` | Audio, video, image processing tools and AI/ML media utilities |
| `troubleshooting.md` | Known quirks — audio, display, KDE/Plasma, USB devices |
| `contacts.md` | Family and shared email addresses |
| `auth-and-security.md` | SSH, GPG, API keys, sudo policy |
| `tools.md` | Preferred CLI tools and utilities |
| `preferences.md` | Date formats, naming conventions, index repo formats |

The key principle: none of this gets loaded unless Claude actually needs it. The entrypoint CLAUDE.md just has a table pointing to these files with one-line descriptions, so the agent knows *where* to look without having to *read* everything upfront.

## The Turnstile Pattern (For Repos)

For repos, I've experimented with creating a similar bifurcation — which I've called the "turnstile" pattern and documented in [ClaudeMD-Turnstile](https://github.com/danielrosehill/ClaudeMD-Turnstile).

The idea is the same: the root `CLAUDE.md` in a repo acts as a routing mechanism rather than a monolithic instruction set. It points the agent toward context files in a `context/` directory within the repo, so that different concerns (project architecture, coding conventions, deployment notes, etc.) are separated and only loaded when relevant. This is especially useful when different users — developers vs. end users, for instance — need different instructions from the same repository.