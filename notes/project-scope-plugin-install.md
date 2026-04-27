# Intentional Project-Level Plugin Installation

**Date:** 27/04/2026
**Claude Code version at time of writing:** 2.1.119

**Companion note:** `shipping-plugins-with-a-repo.md` covers the same mechanism from the *publisher's* angle (declaring a plugin dependency in a repo for other contributors). This note is the *consumer's* angle: deliberately limiting a plugin to one project so it doesn't auto-load globally.

## The use case

You have a plugin that's useful in **one specific repo** but irrelevant — and possibly noisy — everywhere else. Examples:

- A `programmatic-doc-generation` plugin that's only relevant in the repo where you're building a doc-gen pipeline.
- A `kde-plasmoid-dev` plugin you only want loaded inside KDE widget repos.
- A heavy domain-specific plugin (lots of skills, big context surface) that you don't want polluting auto-trigger candidates in unrelated projects.

The default `claude plugins install <plugin>@<marketplace>` writes the install into `~/.claude/settings.json` at **user scope** — meaning it loads for every project on your machine. That's the wrong default for these cases.

The fix: install at **project scope** so the plugin only loads when Claude Code is started from inside that specific repo.

## Procedure

From inside the target repo:

```bash
cd /path/to/your-repo
claude plugins install <plugin-name>@<marketplace-name> --scope project
```

This writes `.claude/settings.json` inside the repo:

```json
{
  "enabledPlugins": {
    "<plugin-name>@<marketplace-name>": true
  }
}
```

If you don't want this committed (e.g. it's a personal preference, not a project dependency), use `--scope local` instead — that writes to `.claude/settings.local.json`, which is gitignored by convention.

| Want | Scope flag | File written | Committed? |
|---|---|---|---|
| Plugin only when *I* work in this repo | `--scope local` | `.claude/settings.local.json` | No (gitignore) |
| Plugin for anyone who clones this repo | `--scope project` | `.claude/settings.json` | Yes |
| Plugin for me everywhere | `--scope user` (default) | `~/.claude/settings.json` | n/a |

Pick `local` for "intentional project-level for myself", `project` for "ship as a dep with the repo".

## Verifying

After installing at project scope, you can confirm with:

```bash
cat .claude/settings.json
# or, for local-scope:
cat .claude/settings.local.json
```

The plugin will load when you run `claude` from inside that repo and **not** when you run `claude` from anywhere else.

To check what's loaded in the current session, look at the available skills/commands list — the project-scoped plugin's skills will only appear when the working directory is the repo (or a descendant of it).

## Removing later

```bash
cd /path/to/your-repo
claude plugins uninstall <plugin-name>@<marketplace-name>
```

This will remove the entry from whichever scope it was installed under. If you have it installed at multiple scopes (rare, but possible), uninstall is scope-targeted — repeat per scope.

You can also just edit `.claude/settings.json` (or `.local.json`) and delete the entry — but using the CLI is the supported path.

## Reasons to prefer this over user-scope install

1. **Context window hygiene.** Every loaded plugin contributes skill descriptions to the session's skill list. A plugin with 8 skills × 200-character descriptions = ~1.6k tokens of skill metadata loaded in *every* session, even when you'll never invoke it. Project-scoping confines that cost to the projects where it's actually useful.
2. **Trigger noise.** Skill auto-trigger phrases compete. A `programmatic-doc-generation` skill that triggers on "create a template" can fire spuriously in an unrelated repo. Scoping eliminates that.
3. **Clear intent.** The `.claude/settings.json` (or `.local.json`) file becomes a record of "this project uses these plugins" — useful for handover and for future-you trying to remember why a particular skill was available here.

## Gotchas

- **The marketplace must already be added** (or the install will prompt to add it). For Daniel's marketplaces this is a one-off; once `danielrosehill` and `danielrosehill-private` are added at user scope, project-scope installs of plugins from those marketplaces are silent.
- **`--scope local` files must be gitignored.** Most repos already have `.claude/settings.local.json` in `.gitignore`. Verify before adding personal-preference installs there.
- **The plugin code is not copied into the repo** — only the *enable* flag. Resolution still happens against the marketplace at session start. If the plugin or its repo is deleted upstream, the install silently breaks.
- **Project scope sticks to the working directory tree.** Running `claude` from a subdirectory of the repo still picks it up; running `claude` from a sibling directory doesn't.

## Pattern for the doc-gen workflow specifically

For the `programmatic-doc-generation` plugin (the one Daniel just built but doesn't want loaded globally):

```bash
cd /path/to/repo-where-i-need-doc-gen
claude plugins install programmatic-doc-generation@danielrosehill --scope local
```

This loads the plugin only in that repo, only for Daniel's user, without committing the preference. When the doc-gen work is done and the plugin's no longer wanted there, `claude plugins uninstall programmatic-doc-generation@danielrosehill` removes it.
