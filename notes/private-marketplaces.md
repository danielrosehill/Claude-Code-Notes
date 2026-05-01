# Private Claude Code Marketplaces

**Date:** 01/05/2026
**Claude Code version at time of writing:** 2.1.126

This isn't documented by Anthropic, but it's not hard to do and it's very useful — so worth a note.

## The catch-22

You can install plugins directly from a repo, one by one. That's fine for a single machine. But if you work across a few machines and you want a private collection of plugins to follow you around, doing that manually gets old fast.

A marketplace solves it. The thing people don't always realise is that **a marketplace doesn't have to be public**. Neither the marketplace repo nor the plugin repos it points at need to be public. The whole chain can be private and it just works.

## My setup: parallel public + private marketplaces

What I do personally is run **parallel marketplaces** — one public, one private:

- **Public marketplace** — for the plugins I'm happy to open-source. Most of them, in my case.
- **Private marketplace** — for the ones that are too process-specific to me, or just internal-only.

You can attach as many marketplaces as you want, so they sit side by side. On a new machine I just attach both and pull what I need.

## Why this is useful

It gives a clean split between things you want to share and things you don't, without forcing you to pick. For individual users it means your private tooling syncs across machines without manual installs. For teams it's the same idea — internal plugins live in the private marketplace, and anything generally useful can be promoted to the public one.

The flexibility is the point. You can open-source what makes sense and keep what doesn't, on the same plugin-management substrate.

## Status

Not in the docs, but I've validated it works and I use it daily. Fully private chains (private marketplace repo → private plugin repos) work fine.

---

*Claude Code moves fast — this may be outdated by the time you read it.*
