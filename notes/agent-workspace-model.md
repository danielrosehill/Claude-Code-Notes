# The Claude Agent Workspace Model

25-03-2026

This is probably the most important pattern I've developed for Claude Code. The reference specification lives at [Claude-Agent-Workspace-Model](https://github.com/danielrosehill/Claude-Agent-Workspace-Model).

## The Big Idea

A Claude Code repo doesn't have to be a software project. It can be a *workspace* — a structured directory that gives Claude persistent context and structured operations for any domain of work: home management, research, business ops, system administration, creative projects.

The pattern: create a version-controlled repo with a `CLAUDE.md` (environment briefing), `.claude/commands/` (slash commands as task definitions), optionally `.claude/agents/` (subagents for complex workflows), and `context/` (domain knowledge). Open Claude Code in that directory and you have a purpose-built AI assistant with full context about the domain.

## The Canonical Structure

```
workspace-name/
├── CLAUDE.md                    ← Lightweight entrypoint
├── context/
│   ├── for-agent/               ← Detailed instructions
│   └── reference/               ← Domain knowledge
├── .claude/
│   ├── commands/                ← Slash commands
│   └── agents/                  ← Subagents
├── work-log/                    ← Session outputs
├── planning/                    ← Plans and strategies
├── user-docs/                   ← Human-facing documentation
└── manifest.json                ← Agentic entry point
```

Three lifecycle stages: **Scaffold** (create the structure) → **Personalise** (via `/onboard`) → **Operate** (use it).

## Real-World Implementations

This isn't just theory. Here are working examples across different domains:

### System Administration
- **[Claude-LAN-Manager-0126](https://github.com/danielrosehill/Claude-LAN-Manager-0126)** — Python GUI for managing LAN devices through isolated Claude spaces. Each device gets its own MCP server; Claude launched in a space sees only that device's MCPs. Effectively an AI-mediated SSH replacement.
- **[Claude-Proxmox-Manager-Template](https://github.com/danielrosehill/Claude-Proxmox-Manager-Template)** — 38 slash commands and 10 subagents for Proxmox server management. Fork once per machine, customise with `/claude-setup`.
- **[Claude-Home-Assistant-Manager-Template](https://github.com/danielrosehill/Claude-Home-Assistant-Manager-Template)** — Same pattern for Home Assistant: 20+ commands covering health monitoring, Zigbee/Z-Wave/MQTT, backup, config validation.
- **[Claude-Linux-Server-Manager](https://github.com/danielrosehill/Claude-Linux-Server-Manager)** — Generic Linux server template: Docker, XFS/RAID storage, Cloudflare Tunnels, security auditing, backups.
- **[Claude-Code-LAN-Manager](https://github.com/danielrosehill/Claude-Code-LAN-Manager)** — Lighter-weight LAN admin launchpad with ARP scanning, network topology context, and ad-hoc device management.

### Desktop & Environment Management
- **[Claude-Code-Linux-Desktop-Slash-Commands](https://github.com/danielrosehill/Claude-Code-Linux-Desktop-Slash-Commands)** — Library of 93+ slash commands for Linux desktop sysadmin, across 20+ categories. The source library that desktop workspaces draw from.
- **[Claude-Linux-Desktop-Manager](https://github.com/danielrosehill/Claude-Linux-Desktop-Manager)** — WIP: GUI wrapper exposing the slash command library as clickable tasks with visual feedback and log management.
- **[Claude-Conda-Manager](https://github.com/danielrosehill/Claude-Conda-Manager)** — Workspace for managing Conda environments on an AMD ROCm workstation. Handles env audits, ROCm dependency resolution, and documentation of working package combos.

## Why This Matters

The insight is that folder structure + Markdown files provide lightweight RAG without any database or vector infrastructure. Git gives you versioning. Slash commands give you structured operations. `CLAUDE.md` gives you persistent context. You don't need a framework or platform — just a well-organised directory.

The repo catalogues 70 workspace ideas (7 implemented, 63 conceptual). The pattern is also framework-agnostic — it can be adapted for Aider, Goose, Codex, or any agent that reads from the filesystem.

**Disclaimer**: This is a very opinionated approach to using Claude Code. It works brilliantly for my use cases (sysadmin, home management, research), but it's a significant departure from using Claude Code purely as a coding assistant.

## Source

- [Claude-Agent-Workspace-Model](https://github.com/danielrosehill/Claude-Agent-Workspace-Model) (reference spec)
