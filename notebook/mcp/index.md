# Model Context Protocol (MCP)

*Last Updated: October 30, 2025*

This section covers the Model Context Protocol (MCP) implementation in Claude Code CLI, including scope management, installation patterns, and common gotchas.

## Documents in This Section

### [MCP Glosses - Key Concepts and Gotchas](./mpc-glosses.md)
Personal notes and clarifications on MCP concepts that aren't always obvious from the documentation:
- Understanding scope parameters (`--scope user` vs default project scope)
- Transport types (HTTP vs STDIO)
- Why MCPs sometimes "disappear" between projects
- The importance of selective MCP enabling to avoid context overload
- Terminology clarifications (local vs user vs project scope)
- Configuration file locations

### [Cloudinary MCP Installation Guide](./cloudinary-mcp.md)
Step-by-step guide for installing the Cloudinary Asset Management MCP:
- JSON configuration format
- Bash command installation
- Authentication setup

## Key Takeaways

**Most Important**: The default scope for `claude mcp add` is **project level**, not user level. If you want an MCP available across all projects, you must explicitly add `--scope user`.

**Configuration Location**: System-wide MCP configuration lives in `~/.claude/`, while project-specific configuration is in `./.claude/` within each repository.

**Selective Enabling**: Having many MCPs defined is fine, but enable them selectively to avoid overwhelming the agent with too many tool definitions at once.
