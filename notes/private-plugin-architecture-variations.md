# Private Plugin Architecture: Workspace, Plugin, MCP Variations

**Date:** 29/04/2026
**Claude Code version at time of writing:** 2.1.123

## Context

After building two private plugins with broadly the same shape (`cloudflare-mgmt`, `podcast-manager`), the same architectural questions kept coming up:

- Where does **user data** live (artwork, drafts, working files) vs. plugin code?
- Does the plugin **bundle an MCP server** or reference a separate one?
- If separate, how does the plugin's `.mcp.json` find the MCP — local path? `npx`? streamable-HTTP via MCP Jungle?

This note captures the variations and the decision tree as of late April 2026. Like everything Claude Code, expect this to age — revisit when the plugin runtime or MCP transport story changes.

## The five observable variations

| # | Pattern | Example | When it fits |
|---|---|---|---|
| 1 | Plugin only | most plugins | Pure helpers — skills + commands, no persistent data, no programmatic tools |
| 2 | Plugin + workspace | `declutter-genie`, `israel-shopping` | Plugin needs user-owned data (inventory, store list) that lives outside the plugin install dir |
| 3 | Plugin + bundled MCP | `cloudflare-mgmt` v0 | Need programmatic tools, want one-step install, OK with the MCP shipping in the plugin repo |
| 4 | Plugin + separate-repo MCP via MCP Jungle | `cloudflare-mgmt` (current) | MCP is reused across plugins / contexts, or runs as a long-lived HTTP server |
| 5 | Plugin + workspace + separate MCP | `podcast-manager` | All of the above — user data, programmatic tools, MCP reusable elsewhere |

The trajectory of `cloudflare-mgmt` (3 → 4) is informative. It started with the MCP bundled in `mcp-server/` for a one-step install, then graduated to a separate streamable-HTTP server on UbuntuVM mounted via MCP Jungle's personal profile once the workflow stabilised. The plugin's `.mcp.json` was deleted in commit `c7321ae` ("Remove plugin .mcp.json — tools surface via MCP Jungle personal profile, not a per-plugin connection").

## Decision tree

```
Does the plugin need any persistent user data (artwork, inventory, drafts, configs beyond pointers)?
├─ NO  → continue
└─ YES → add a workspace repo (variation 2 or 5).
         Workspace = user-owned, separate from plugin install dir.
         Plugin stores only a pointer to the workspace path in $CLAUDE_USER_DATA.

Does the plugin need programmatic tools (uploads, deploys, API calls beyond reading files)?
├─ NO  → variation 1 or 2. Done.
└─ YES → continue.

Will the MCP be reused outside this plugin (other plugins, raw CLI, other agents)?
├─ NO  → bundle it in plugin/mcp-server/ (variation 3). Simplest install.
└─ YES → separate repo (variation 4 or 5). Pick a transport:
         ├─ Streamable-HTTP behind MCP Jungle profile → best long-term
         ├─ stdio via npx -y @scope/mcp-package    → works after npm publish
         └─ stdio via local node path              → works on your dev machine, breaks when the plugin is installed elsewhere
```

## Path resolution rules

Universal regardless of variation:

- **Never** write user data to `~/.claude/plugins/<plugin>/` — that directory is **clobbered on every plugin update**. Whatever's there is gone next time the plugin updates.
- **Never** write to `~/.claude/<anything>` outside Claude Code's own files — that's Anthropic's config surface.
- Plugin-managed data (cache, state, generated artifacts) goes under `$CLAUDE_USER_DATA/<plugin-name>/` with the canonical resolution snippet:

  ```
  ${CLAUDE_USER_DATA:-${XDG_DATA_HOME:-$HOME/.local/share}/claude-plugins}/<plugin-name>/
  ```

- **User-owned data** (the workspace) goes under a path the user picks during onboarding — typically `~/Documents/<workspace>` or `~/repos/<workspace>`. The plugin only stores the *pointer* to that path in its `config.json` under `$CLAUDE_USER_DATA`.

For the full reasoning behind these rules see [Where Should A Claude Code Plugin Store User Data?](plugin-user-data-storage.md).

## `.mcp.json` invocation tradeoffs (variations 3–5)

| Approach | `.mcp.json` shape | Pros | Cons |
|---|---|---|---|
| **Bundled** | `node ${PLUGIN_DIR}/mcp-server/dist/index.js` | One-step install, no external deps | MCP coupled to plugin lifecycle |
| **npx** | `npx -y @scope/mcp-package` | Decoupled, public reuse, version pinning | Requires npm publish, slow cold start |
| **Local path** | `node /home/<user>/repos/.../mcp/dist/index.js` | Works immediately during dev | Hard-coded path; breaks anywhere else |
| **Streamable-HTTP via MCP Jungle** | (not in plugin's `.mcp.json` — mounted via MCP Jungle profile) | Decoupled, reusable across plugins/clients, persistent server | Requires HTTP deployment + MCP Jungle setup |

A reasonable migration path for a new plugin is **bundled → streamable-HTTP via MCP Jungle**: ship variation 3 first to get the workflow working, then extract the MCP to its own repo and deploy as HTTP once it stabilises. Variation 4/5 from day one is fine if you already know the MCP will be reused.

## Marketplace registration

For private plugins, register in `Claude-Code-Plugins-Private/.claude-plugin/marketplace.json` rather than the public marketplace. The skill `create-claude-plugins:new-private-claude-plugin` handles this end-to-end, including:

- pre-flight existence checks (local repo, GitHub remote, marketplace registration, installed cache)
- overlap & subsumption audit against both public and private marketplaces (don't create a new plugin if an existing one already covers the scope)
- private GitHub repo creation
- marketplace JSON entry
- local marketplace cache refresh

## Caveat — this is a snapshot

Claude Code, the plugin runtime, and MCP all move fast. The patterns above reflect what worked as of **2.1.123 (29 April 2026)**. Triggers for revisiting:

- A new MCP transport (e.g. official server discovery) lands and changes the `.mcp.json` story
- Anthropic adds first-class workspace/data-dir support to the plugin runtime, eliminating variation 2's `$CLAUDE_USER_DATA` pointer dance
- The `claude plugins install` UX changes how MCP servers are mounted

Re-read this note when adding the third such plugin — by then the actual decision tree is empirical, not speculative.
