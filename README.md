[![Part of the Claude Code Repos Index](https://img.shields.io/badge/Claude%20Code%20Repos-Index-blue?style=flat-square&logo=github)](https://github.com/danielrosehill/Claude-Code-Repos-Index)

# Claude Code - My Cliff Notes

**Authorship:** Ideas & notes — Daniel. Refinement & writing — Claude Opus 4.6.

Claude Code is a hugely powerful CLI that has made made agentic AI accessible to many.

It is also an incredibly fast-moving product: I saw a joke on X that you would have to be unemployed to keep up with developments. It's true!

I created this repo to jot down a few casual "cliff notes" for using it.

Because of how fast moving Claude Code is, this small store of notes is a kind of self-immolating information store: many of the hacks I put in place just a few months ago are now redundant.

In fact, if we look at the course of evolution so far, the general pattern is something like:

- People use Claude
- The open source community - myself included - finds points of friction and fills those gaps with tooling/bolt-ons. Occasionally, it's heralded as the next big thing and a "Claude-killer"
- Anthropic takes notes or was working on these things anyway. It releases an update.
- Open source world reverts to loving Claude until next set of friction points are discovered.
- Cycle repeats!

From a jaundiced perspective, this might seem silly. But in a way, it's virtuous: we get hot fixes that are then folded back to the product. A more probative question is that of ethics: when open source contributors make Claude better - and Anthropic makes lots of money from the product and charges the very users who spotted those flaws - shouldn't the value be distributed a bit more equitably?

## Notes Index

### CLAUDE.md & Context Configuration

| Note | Date | Summary |
|------|------|---------|
| [CLAUDE.md - Strategic Separation](notes/claude.md) | 25/03/2026 | Why a monolithic CLAUDE.md is a bad idea — the split pattern for user-level context and the turnstile pattern for repos |
| [The CLAUDE.md Turnstile Pattern](notes/claudemd-turnstile-pattern.md) | 25/03/2026 | Role-based routing in CLAUDE.md — dispatch developers and users to different context files |
| [Claude Code Context Toolkit](notes/context-toolkit.md) | 25/03/2026 | Two-file workflow: CONTEXT.md (human scratchpad) and CLAUDE.md (agent-optimised) with conversion commands |
| [Private And Public CLAUDE.md](notes/private-and-public-claude-md.md) | 25/03/2026 | Two-tier CLAUDE.md setup — commit public instructions, gitignore sensitive ones globally |
| [Split Context Setup](notes/split-context-setup.md) | 25/03/2026 | Slash command to automate splitting a bloated CLAUDE.md into a structured context/ store |
| [The Split CLAUDE.md Pattern](notes/split-claude-md-pattern.md) | 25/03/2026 | Keep ~/.claude/CLAUDE.md lean, move topic-specific context to context/ files loaded on demand |
| [Version-Controlling Your Home Folder CLAUDE.md](notes/home-folder-claude-md.md) | 25/03/2026 | Why your home-level CLAUDE.md deserves version control and how to set it up |

### Patterns & Architecture

| Note | Date | Summary |
|------|------|---------|
| [The Agent Picker Pattern](notes/agent-picker-pattern.md) | 25/03/2026 | Solving the "too many subagents" problem with an orchestration agent that selects the right crew |
| [The Claude Agent Workspace Model](notes/agent-workspace-model.md) | 25/03/2026 | Using repos as structured workspaces for non-software work — the most important pattern, with 8 real implementations |
| [Planning Folder With UUID-Tagged Plans](notes/planning-folder-uuid.md) | 06/04/2026 | A planning/ folder with plans, handovers and logs — every plan gets a UUID as ground-truth reference for resume commands |

### Repo & Codebase Tools

| Note | Date | Summary |
|------|------|---------|
| [Claude Repo Jumper](notes/repo-jumper.md) | 25/03/2026 | Slash command concept for automating context handover when spinning up new repos |
| [Claudify-This & Claude-Repo-Retrofitter](notes/claudify-and-retrofit.md) | 25/03/2026 | Tools for getting existing repos ready for Claude Code — single repo or bulk batch |
| [Make Agent Friendly](notes/make-agent-friendly.md) | 25/03/2026 | Plugin for restructuring inherited codebases for agentic development |

### Slash Commands & Plugins

| Note | Date | Summary |
|------|------|---------|
| [Declaude](notes/declaude.md) | 25/03/2026 | Build personal writing rules and enforce them on AI-generated content via a slash command |
| [No Wheel Inventions](notes/no-wheel-inventions.md) | 25/03/2026 | Slash commands to stop Claude reinventing the wheel when good packages exist |
| [Claude Handover Plugin](notes/claude-handover-plugin.md) | 06/04/2026 | Plugin formalising session handover — writes HANDOVER.md and spawns a new Konsole with Claude pre-loaded to resume |

### MCP & Integration

| Note | Date | Summary |
|------|------|---------|
| [Claude MCP Guidelines](notes/claude-mcp-guidelines.md) | 25/03/2026 | CLAUDE.md snippet for deterministic MCP tool selection and conflict resolution |

### Workflow & Task Management

| Note | Date | Summary |
|------|------|---------|
| [Claude Space Self-Ideator](notes/claude-space-self-ideator.md) | 25/03/2026 | A meta workspace that generates ideas for more workspaces — exploratory and self-referential |
| [Claude Task Manager](notes/claude-task-manager.md) | 25/03/2026 | Spec for a sequential task queue to solve context window exhaustion across multi-task projects |

### Reference

| Note | Date | Summary |
|------|------|---------|
| [Claude Code Notebook](notes/claude-code-notebook.md) | 25/03/2026 | Personal reference notebook for Claude Code CLI — config files, CWD behaviour, MCP setup on Linux |

---

For more Claude Code projects, visit my [Claude Code Repos Index](https://github.com/danielrosehill/Claude-Code-Repos-Index).