# Current Working Directory (CWD) Management

*Last Updated: October 30, 2025*

This section covers working with Claude Code's current working directory constraints, particularly relevant when using Claude Code for system administration or non-traditional development tasks.

## Documents in This Section

### [Understanding and Managing CWD Constraints](./cwd.md)
Insights on working with (or around) CWD restrictions in Claude Code:
- Why CWD constraints exist (sandboxing for collaborative development)
- The tension between YOLO system administration and repository sandboxing
- Using the `--adddir` flag for temporary directory access
- Persistent configuration via `settings.json`
- Adding home directory or entire filesystem to trusted folders

## Key Takeaways

**For System Administration**: Claude Code is primarily designed for collaborative repository development, but it's powerful for system administration too. The CWD constraint can feel restrictive for these use cases.

**Quick Access**: Use the `--adddir` flag when you need temporary broader filesystem access.

**Persistent Access**: Add directories to `trustedFolders` in `~/.claude/settings.json`:
- Add `~` for home directory access
- Add `/` for full filesystem access (use with caution)

**Trade-offs**: Opening up filesystem access is appropriate when sandboxing is for agent supervision rather than security, but be aware of the implications.
