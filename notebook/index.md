# Claude Code CLI Reference Notebook

*Last Updated: October 30, 2025*

This notebook contains reference notes, tips, and insights for using Anthropic's Claude Code CLI effectively. The information here comes from personal experience, official Anthropic documentation, and community discussions.

## Table of Contents

### [MCP (Model Context Protocol)](./mcp/)
- [MCP Glosses - Key Concepts and Gotchas](./mcp/mpc-glosses.md)
- [Cloudinary MCP Installation Guide](./mcp/cloudinary-mcp.md)

### [Current Working Directory (CWD)](./cwd/)
- [Understanding and Managing CWD Constraints](./cwd/cwd.md)

### [Configuration Files](./config-files/)
- [Linux Configuration TL;DR](./config-files/linuxtldr.md)

## Quick Reference

### MCP Scopes
- `--scope user` - System-wide MCP configuration
- `--scope project` - Project/repo level (default)
- Project JSON - Team-wide configuration via `mcp.json`

### Key Configuration Locations
- System config: `~/.claude/`
- System settings: `~/.claude/settings.json`
- System commands: `~/.claude/commands/*.md`
- Project config: `./.claude/` (in project directory)

### Essential Links
- [Claude Code Documentation](https://docs.claude.com/en/docs/claude-code/)
- [Cloudinary MCP Servers](https://github.com/cloudinary/mcp-servers)

## Notes on This Notebook

This is a living reference document that evolves as Claude Code develops. All notes include dates to help track when information was current, as the CLI is actively being developed and improved.

When citing Reddit threads or community sources, these are valuable for practical insights that may not be fully covered in official documentation.
