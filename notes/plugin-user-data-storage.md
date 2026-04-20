# Where Should A Claude Code Plugin Store User Data?

**Date:** 21/04/2026
**Claude Code version at time of writing:** 2.1.116

**Source:** https://code.claude.com/docs/en/plugins-reference

## Question

Daniel wants to develop a Claude Code plugin. He figures it might be useful for other users so wants to release it on his public marketplace.

The plugin provides some functions for document typesetting with typst.

Daniel thinks: "well... it would be super useful if there was an onboarding slash and Claude could save the user's data and reference it on future runs."

Here are our challenges:

- This means that Claude is going to need memory to run this plugin effectively
- Every user is unique and will want their own data store
- Daniel will maintain and push updates so the plugin and user memory data have to be decoupled

### Question 1: Can we define a workspace folder at random or is there a "proper" place?

**Answer 1:** The docs have this (intended for plugin.json):

> "workspaceFolder — Workspace folder path for the server"

In my experience, if you're using Claude Code to develop Claude Code plugins, Claude will suggest random and inconsistent paths but bias towards nesting these under `~/.claude`.

Is `~/.claude/plugin-data/foo` safe?

Daniel isn't sure. The worry is that this would be overwritten on updates.

A problem with this approach is as follows: it's machine-bound. Unless you're syncing your `.claude` across machines.

**Potential solutions:**

1. Roll your own filesystem base for Claude plugin data that is removed from `~/.claude` like `~/.claude-user-data` or `~/.claude-my-data` or whatever you want. Consistently reference this as your base. Version control and sync with YADM etc. Cumbersome but doable.

2. Make the base directory of your user-data something mounted with rclone. Sync across machines. Assuming path consistency, data store should work across environments.

Pitfalls: the usual ones with Linux. OS and distro differences could break this.

Best model? Maybe MCP: data lives in the cloud and the plugin reads/writes it dynamically with database lookups.

**Issue: unresolved**

---

## Postscript — resolved answer

After thinking this through a bit more, the above has a few misunderstandings worth flagging. Corrected version:

**`workspaceFolder` is the wrong field.** That key in `plugin.json` is under the MCP server config — it sets the CWD for a bundled MCP server process. It has nothing to do with a plugin's user-data directory. Quoting it as an answer to "where do I store user data" is a category error.

**There's already a "proper" place, and it isn't `~/.claude`.** The cross-platform answer is the XDG Base Directory spec (and its macOS / Windows equivalents):

- **Linux**: `$XDG_DATA_HOME/<plugin-name>/` — default `~/.local/share/<plugin-name>/` for data; `$XDG_CONFIG_HOME/<plugin-name>/` (default `~/.config/<plugin-name>/`) for config
- **macOS**: `~/Library/Application Support/<plugin-name>/`
- **Windows**: `%APPDATA%\<plugin-name>\`

This is the standard. Not a roll-your-own `~/.claude-my-data`. Third-party plugins should never write user data inside `~/.claude/plugins/<plugin>/` — that directory is owned by the marketplace installer and is blown away on update. `~/.claude/plugin-data/<plugin>/` (a sibling of the install dir) would survive updates, but it's still the wrong location on principle — `~/.claude` is Claude Code's own directory, not a free-for-all for third-party plugin data.

**"Overwritten on update" dissolves once data lives outside the plugin install dir.** Updates only touch `~/.claude/plugins/<plugin>/`. Anywhere outside that is safe.

**Machine-bound is not a problem to solve at the plugin level.** Every dotfile on Linux is machine-bound until the user syncs it. Correct layering: plugin writes to XDG path → user decides whether to sync that path with Syncthing / yadm / symlink-to-cloud. Baking rclone into the plugin is overreach and fragile.

**"MCP as the memory layer" is confused.** MCP is a tool protocol, not storage. You'd still need a backing store (SQLite, Postgres, whatever) and you'd be forcing every user to provision cloud infra just to remember their name and default paper size for a typst plugin. Massive overkill. For onboarding-style plugins the right model is: local XDG file (JSON / TOML / SQLite), optional export/import commands if users want to move between machines.

### Suggested setup for plugin authors

1. **Detect** `$XDG_DATA_HOME` — if unset, fall back to `~/.local/share/`.
2. **Use it consistently** as the default base for your plugin's user data — `$BASE/<plugin-name>/`.
3. **Document the default** in user-level `CLAUDE.md` so Claude picks the same location across future sessions when extending the plugin.
4. **Sync optionally** via rclone, a private git repo, Syncthing — user's call, not the plugin's.
5. **Onboarding flow**: on first run, the plugin checks for the XDG variable, creates its directory, and writes an initial config. Subsequent runs read from that path.

### Related

- Filed as a Claude Code model-behavior issue: [anthropics/claude-code#51342](https://github.com/anthropics/claude-code/issues/51342) — the `~/.claude` path bias is the reproducible pattern.

---

*Claude Code moves fast — this may be outdated by the time you read it.*
