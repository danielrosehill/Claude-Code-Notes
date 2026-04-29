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
| [Private Plugin Architecture: Workspace, Plugin, MCP Variations](notes/private-plugin-architecture-variations.md) | 29/04/2026 | Five variations for private plugins (plugin-only, +workspace, +bundled MCP, +separate MCP via MCP Jungle, +workspace +MCP), decision tree, .mcp.json invocation tradeoffs |

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
| [Claude Slash Commands](notes/claude-slash-commands.md) | 06/04/2026 | Index repo for 350+ custom slash commands across dev, docs, security, and sysadmin categories |
| [Claude Document This](notes/document-this.md) | 06/04/2026 | Plugin for capturing sysadmin fixes and routing the writeup to Notion, Obsidian, or email |
| [Claude Janitor](notes/claude-janitor.md) | 06/04/2026 | Plugin for tidying up repos from Claude-related artefacts and stray scaffolding |
| [Plugin User-Data Storage](notes/plugin-user-data-storage.md) | 21/04/2026 | Where plugins should persist per-user state — why `~/.claude/` is wrong, why XDG Base Directory is right, and how to set it up |

### Hooks

| Note | Date | Summary |
|------|------|---------|
| [New Turn Claude Hook](notes/new-turn-hook.md) | 06/04/2026 | Concept hook for auto-deciding when to start a fresh conversation vs continue the current one |

### Desktop Utilities

| Note | Date | Summary |
|------|------|---------|
| [Claude Konsole Launcher](notes/konsole-launcher.md) | 06/04/2026 | WIP launcher for spinning up Claude Code inside Konsole on KDE Plasma |
| [Claude Linux Desktop Manager](notes/linux-desktop-manager.md) | 06/04/2026 | GUI wrapper exposing sysadmin tasks as buttons backed by Claude Code slash commands |

### Templates & Scaffolds

| Note | Date | Summary |
|------|------|---------|
| [Claude Deep Research Template](notes/deep-research-template.md) | 06/04/2026 | Workspace template for phased research projects — context, plan, execute, synthesise |
| [Claude Spec Starter](notes/spec-starter.md) | 06/04/2026 | Template that turns free-form project descriptions into structured specs and context files |
| [Claude Workspace Setup Helper](notes/workspace-setup-helper.md) | 06/04/2026 | Interactive picker for cloning pre-built Claude Workspace templates by use case |

### Repository Sculpting

| Note | Date | Summary |
|------|------|---------|
| [Claude Repo Creator](notes/repo-creator.md) | 06/04/2026 | Workspace for generating GitHub repos from natural language — local, remote, and scaffolding in one shot |

### Harnessing & Guidance

| Note | Date | Summary |
|------|------|---------|
| [Claude MD Chunk](notes/md-chunk.md) | 06/04/2026 | CLI tool that prunes bloated CLAUDE.md and offloads detail into an agent-context/ folder |

### Workarounds

| Note | Date | Summary |
|------|------|---------|
| [Claude Model Identifier](notes/model-identifier.md) | 06/04/2026 | Prompt snippet for verifying which model is actually serving the session |
| [The cwd Constraint and Workspace Roots](notes/cwd-constraint-and-workspace-roots.md) | 29/04/2026 | The cwd lock is harness-level but configurable — `--add-dir`, `additionalDirectories`, or launch from `/` for sysadmin work |

### Bash & Shell

| Note | Date | Summary |
|------|------|---------|
| [Claude Code Bash Aliases](notes/bash-aliases.md) | 06/04/2026 | Curated bash aliases for Claude Code workflows on Linux, version-controlled with YADM |

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

### Reference Notebook

Longer-form reference material (folded in from the former `Claude-Code-Notebook` repo):

- [Notebook Index](notebook/index.md)
- [Config Files](notebook/config-files/) — including the [Linux TL;DR](notebook/config-files/linuxtldr.md)
- [Current Working Directory (CWD)](notebook/cwd/cwd.md)
- [MCP](notebook/mcp/index.md) — [add from JSON](notebook/mcp/add-from-json.md), [list MCP names](notebook/mcp/get-mcp-names.md), [Anthropic MCP glosses](notebook/mcp/mpc-glosses.md), [STT MCP](notebook/mcp/stt.md)
- Individual MCP configs: [Cloudinary](notebook/mcp/individual-configs/cloudinary-mcp.md) · [Context7](notebook/mcp/individual-configs/context7.md) · [Firecrawl](notebook/mcp/individual-configs/firecraw.md) · [GitHub Gists](notebook/mcp/individual-configs/github-gists.md) · [Hugging Face](notebook/mcp/individual-configs/hugging-face.md) · [Notion](notebook/mcp/individual-configs/notion.md) · [Resend](notebook/mcp/individual-configs/resend.md) · [Time Awareness](notebook/mcp/individual-configs/time-awarendess.md) · [Todoist](notebook/mcp/individual-configs/todoist.md) · [Vercel](notebook/mcp/individual-configs/vercel.md)
- [Useful Links](notebook/links.md) · [Other Notebooks](notebook/ref/other-notebooks.md) · [Resources](notebook/ref/resources.md)

---

For more Claude Code projects, visit my [Claude Code Repos Index](https://github.com/danielrosehill/Claude-Code-Repos-Index).