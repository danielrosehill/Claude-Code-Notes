# Planning Folder With UUID-Tagged Plans

06-04-2026

A lightweight pattern for keeping plans durable across context resets, without depending on a specific plugin.

## The Setup

Ask Claude to create a `planning/` folder at the repo root with three subfolders:

- `planning/plans/` — written plans for work, current and historical
- `planning/handovers/` — handover notes between sessions (similar to, but distinct from, a dedicated handover plugin)
- `planning/logs/` — running logs of what actually happened

Then add two slash commands:

- `/plan` — create a new plan file in `planning/plans/`
- `/resume` — resume from an existing plan, given its identifier

## The Important Bit: UUIDs

The slash command for creating a plan **must** require that every plan has a UUID in its filename and/or frontmatter. Something like:

```
planning/plans/2026-04-06-refactor-auth-3f7a9c2e.md
```

The UUID becomes the ground-truth reference for that plan. When you later say "resume from plan `3f7a9c2e`", there's zero ambiguity — no fuzzy title matching, no "did you mean…", no risk of Claude grabbing a similarly-named plan from last week.

## The Workflow

1. Start work, run `/plan` — Claude drafts the plan, assigns a UUID, saves it.
2. Work proceeds. Context fills up.
3. When you want to clean context (compact, `/clear`, new session), ask Claude to **document the current state of the plan back into its file** in `planning/plans/`. The UUID makes the target unambiguous.
4. Reset context.
5. Run `/resume <uuid>` — Claude loads that exact plan and picks up where you left off.

Because `/resume` takes an arbitrary UUID, you can also jump back to *any* historical plan, not just the most recent one.

## Why UUIDs Specifically

Dates collide. Titles drift and get rephrased. "The auth plan" is ambiguous once you've worked on auth three times. A UUID is a stable, unique handle that survives rewrites, rephrasings, and Claude's tendency to paraphrase filenames. It's the closest thing to a primary key for a plan.

## Relation To Handover Plugins

This overlaps with dedicated handover tooling (e.g. a `/handover` plugin) but solves a slightly different problem:

- **Handovers** = "here's everything the next agent needs to know right now"
- **Plans** = "here's the durable, addressable artifact for this piece of work"

You can use both. Handovers go in `planning/handovers/`, plans in `planning/plans/`, and they cross-reference each other by UUID.

## Disclaimer

This is a personal pattern, not a recommendation. If your work is short enough to fit in a single session, you don't need any of this.
