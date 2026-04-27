# Shipping A Claude Code Plugin With A Repo (Project-Scope Install)

**Date:** 27/04/2026
**Claude Code version at time of writing:** 2.1.119

**Source:** https://code.claude.com/docs/en/plugins-reference, https://code.claude.com/docs/en/plugin-marketplaces

## The use case

You have a repo that benefits from a specific Claude Code plugin — domain-specific skills, slash commands, or agent definitions that are useful when working in that codebase but irrelevant elsewhere.

Concrete example: a KDE plasmoid repo (`Hebrew-Date-KDE-Widget`) where the workflow benefits from the `kde-plasmoid-dev` plugin (Plasma 6 scaffolding, dev-tool installer, OpenCode mirror). Users contributing to that repo should get the plugin without having to know it exists.

The trick is **project-scope plugin installation**, persisted into the repo via `.claude/settings.json`.

## How it works on the publishing side

Run from inside the repo:

```bash
cd /path/to/your-repo
claude plugins install <plugin-name>@<marketplace-name> --scope project
```

This writes (or updates) `.claude/settings.json` in the repo:

```json
{
  "enabledPlugins": {
    "kde-plasmoid-dev@danielrosehill": true
  }
}
```

That file is meant to be **committed and pushed**. It declares the plugin dependency for that project, the same way `package.json` declares an npm dep.

The three scopes:

| Scope | File | Who sees it |
|---|---|---|
| `user` (default) | `~/.claude/settings.json` | Just you, on every project |
| `project` | `<repo>/.claude/settings.json` | Anyone who clones the repo |
| `local` | `<repo>/.claude/settings.local.json` (gitignored by convention) | Just you, only in this repo |

For shipping with a repo, you want `project`.

## What the receiving user has to do

Short answer: **almost nothing — but they do have to consent.**

When a user opens the repo in Claude Code:

1. Claude Code reads `.claude/settings.json` and sees the `enabledPlugins` entry.
2. If the referenced marketplace (`danielrosehill` in the example) is **not already added** to the user's Claude Code, it prompts: "This project uses plugins from marketplace X. Trust it?"
3. If they accept, Claude Code adds the marketplace, installs the plugin, and enables it for that project.
4. If they decline, the plugin simply doesn't load — Claude Code keeps working without it. Nothing breaks.

Marketplace trust is **per-marketplace, not per-plugin**. Once they trust your marketplace, every project that references the same marketplace works without re-prompting.

If the marketplace was already added (e.g. they trusted it for a previous project), the install happens silently with no prompt.

### What it looks like to the user

- They `git clone` the repo, `cd` into it, run `claude`.
- Claude Code shows a one-time prompt naming the marketplace and the plugin.
- They press "y" — done. The plugin is now installed at project scope.

That's it. No `.claude` folder management, no manual marketplace adds, no plugin-install commands.

## Practical recipe

For a repo where you want to ship plugin X from your marketplace M:

```bash
cd /path/to/repo
claude plugins install X@M --scope project
git add .claude/settings.json
git commit -m "Enable $X plugin at project scope"
git push
```

A README note doesn't hurt:

> This repo uses the `<plugin-name>` plugin from the `<marketplace-name>` Claude Code marketplace. Claude Code will prompt you to trust the marketplace on first open — accept and the plugin installs automatically.

## Caveats and gotchas

- **The plugin must be on a public marketplace.** If your plugin lives in a private marketplace the user can't access, the install will fail — they'll just see Claude Code without the plugin.
- **Marketplace name matters in the reference.** `kde-plasmoid-dev@danielrosehill` is `<plugin-name>@<marketplace-name>`, where `marketplace-name` is the `name` field in the marketplace's `.claude-plugin/marketplace.json`, not a GitHub repo name.
- **Project scope ≠ vendored.** The plugin code is **not** copied into the repo. Claude Code resolves and downloads it on demand from the marketplace. If the plugin's upstream repo disappears, the install breaks. If you need true reproducibility, vendor the plugin into the repo and reference it as a local plugin instead — but you lose update propagation.
- **Don't manually edit `.claude/settings.json`** unless you know the schema. The `--scope project` install flag is the supported way to write it.
- **`.claude/settings.local.json` should stay gitignored** — it's for personal overrides. Add `.claude/settings.local.json` to `.gitignore` if you're shipping `.claude/settings.json`.

## Why this is nice

It's a clean dependency model. Instead of "to use this repo properly, follow these 8 setup instructions in the README and remember to install plugin Y," the repo declares its plugin dependency declaratively, the user's tooling resolves it on first open, and contributors get a uniform experience.

Same pattern as `package.json` for npm or `requirements.txt` for pip — the tool reads the manifest and installs what's needed.
