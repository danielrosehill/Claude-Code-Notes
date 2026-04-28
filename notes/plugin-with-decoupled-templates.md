# Plugins With Decoupled Templates

**Date:** 28/04/2026
**Claude Code version at time of writing:** 2.1.121

## The shape

Some plugins are wrappers around an external project — they scaffold a workspace from it, run it, and offer convenience operations on top. The naive approach is to copy the project's files into the plugin itself, but that couples plugin updates to template updates and makes the plugin repo bloat with code it doesn't own.

Cleaner shape: the plugin is a *thin orchestrator*, and the templates it scaffolds from live in **separate upstream repos**. The plugin holds only:

- A `templates/` registry — one entry per supported template (name, repo URL, short description, cost/depth tradeoff blurb, run command, sentinel file path)
- Skills that read the registry and act on it

## Why this is good

- **Independent release cadences.** Push template improvements to the upstream repo whenever; the plugin doesn't need a version bump. Push plugin improvements (new skills, better UX) without touching templates.
- **Multi-template from day one.** Adding a new template later is a registry entry — no skill rewrites.
- **User picks at scaffold time.** The scaffold skill presents the registry as a menu with the tradeoff blurbs, so the user makes an informed choice instead of the plugin guessing.
- **No vendoring drift.** The user always gets `git clone` of the live upstream, never a stale snapshot baked into the plugin.

## Required skills

A plugin in this shape wants four skills, minimum:

1. **`scaffold-<thing>`** — interactive menu over the template registry, clones the chosen template into a new workspace dir, wires `.env` (ideally from 1Password), drops a sentinel file like `.template-id` so other skills know which template this workspace is.
2. **`run-<thing>`** — reads the sentinel, dispatches to the template's run command (which differs per template — e.g. `python -m forecast` vs `uv run geopol forecast`).
3. **`update-templates`** — `git pull` inside each template's local clone (or re-clone if missing), so users get upstream improvements without reinstalling the plugin. Reports what changed per template.
4. **Domain-specific skills** — anything else the plugin layer adds (e.g. "edit actor personas" for one template, "swap council models" for another). These should branch on the sentinel and fail gracefully when the active workspace's template doesn't support the operation.

## Sentinel file

The sentinel is what makes one workspace distinguishable from another at the plugin layer. Keep it dead simple — a `.template-id` file at workspace root containing the registry key (e.g. `geopol-forecaster` or `geopol-council`). Skills that operate on a workspace `cat .template-id` to dispatch.

## Example

The pattern emerged from `Geopol-Sim-Plugin`, which wraps two unrelated upstream simulators (`Geopol-Forecast-Council` and `Geopol-Forecaster`) with very different cost profiles, run commands, and editable surfaces. A third can be added later with a registry entry plus dispatch branches in skills 2–4 — no touching skill 1.

## When NOT to use this

- The "template" is one or two files — just inline them in the plugin.
- The template is genuinely owned by the plugin and has no independent life — vendoring is fine.
- Users would never want the upstream's latest — pin a commit instead.
