# Configuration Files

*Last Updated: October 30, 2025*

This section covers Claude Code configuration files and their hierarchy, particularly for Linux users.

## Documents in This Section

### [Linux Configuration TL;DR](./linuxtldr.md)
Quick reference for where Claude Code stores configuration on Linux systems:
- Key configuration directory: `~/.claude/`
- Master settings file: `~/.claude/settings.json`
- Understanding the configuration hierarchy

## Key Takeaways

**Configuration Home**: `~/.claude/` is your system-level configuration directory.

**Master Settings**: `~/.claude/settings.json` is the top-level settings file for system-wide configuration.

**Three Scopes**: Anthropic uses three configuration scopes:
1. System/User level (`~/.claude/`)
2. Project level (`./.claude/` in project directory)
3. Repository level (`mcp.json` in project root for team collaboration)

**Quick Access**: Bookmark `~/.claude/` to save time when troubleshooting or configuring Claude Code.
