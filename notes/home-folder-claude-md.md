# Version-Controlling Your Home Folder CLAUDE.md

25-03-2026

[Home-Folder-Claude-MD](https://github.com/danielrosehill/Home-Folder-Claude-MD) is deceptively simple but addresses something important: your `~/CLAUDE.md` (or `~/.claude/CLAUDE.md`) is one of the most consequential files on your system if you use Claude Code regularly, and it deserves version control.

## Why This Matters

Your home-level `CLAUDE.md` is loaded into every Claude Code session on your machine. It shapes how Claude behaves across all your projects. Changes to this file have global impact — and yet most people edit it ad-hoc without any change history, rollback capability, or backup.

## The Setup

A simple repo that:
- Stores your `~/CLAUDE.md` under version control
- Includes a `sync.sh` one-way sync script to copy from the repo to `~/CLAUDE.md`
- Gives you full git history of every change you've made

That's it. Fork it, replace the content with your own, run `sync.sh` when you update.

## Practical Takeaway

Even if you don't use this specific repo, version-control your home-level CLAUDE.md somehow. It's too important to leave as an untracked file. Options:

1. Use this repo pattern (dedicated repo + sync script)
2. Include it in a dotfiles repo
3. At minimum, back it up periodically

The point is: when you break something with an edit, you want to be able to see what changed and roll back.

**Disclaimer**: The sync is one-way (repo → home). If you edit `~/CLAUDE.md` directly, remember to copy changes back to the repo.

## Source

- [Home-Folder-Claude-MD](https://github.com/danielrosehill/Home-Folder-Claude-MD)
