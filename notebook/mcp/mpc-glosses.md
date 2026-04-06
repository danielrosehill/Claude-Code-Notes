# Anthropic's Claude Code MCP Notes - My Glosses

*October 30, 2025 - Based on version downloaded at that date (in repo)*

## Scope Params

`--user` = User / CLI level MCP
`--project` = Project / repo level MCP

## "Transport"

SSE is deprecated, so these are what will be expected/seen:

**HTTP:**

`--transport http`

**STDIO:**

`--transport stdio`

## Default = Project Specific!

This is a **huge point** about getting MCP to work with Claude in OSes without a desktop GUI that's glossed over in the docs!

The **default** scope for `claude mcp add` is project/repo level. 

Which is why (this has happened many times!):

- In repo 1, you add an MCP
- You go into repo 2 and wonder why Claude seems to have forgotten about the MCP you just configured 

The answer is that the MCP was project-scoped and is therefore not available outside of that repo.

This is expected behavior, of course. But I still argue that it's a little confusing. 

Or maybe it just speaks to the fact that the default behavior expects everyone to be working in a collaborative code repo: many users will be; some users will never be; some users will use it on solo and collaborative projects at different times and places. But currently, however you run `mcp add foo` (without a defined scope), you will be installing the MCP at directory/project level.

Highlight:

If you want some MCPs to be persistent across projects, you **need** to add the `--scope user` param!

## Over MCP-ing - Why It's "Discouraged"

A common problem everyone trying out MCP runs into (regardless of IDE):

- Oh cool, so many amazing MCPs! I want this! I want this! Wait... there's an MCP for that now! I want them all!
- Each MCP then provides a bunch of tools
- Agent is now flooded with task definitions from many MCPs every time it tries to run
- Agent becomes non-functional or runs into context mud after a few turns because it's got a gigantic trailing context of MCP definitions to wade through 

A vital UI parameter that, again, is not highlighted enough (not just Claude, everywhere): enabling/disabling. 

You can *have* a bunch of MCPs (defined, authenticated) but it's not necessarily a problem if you enable them selectively. 

This is (opinionated) a more realistic UI than endlessly creating project-specific MCP configs: toggle the ones you need and don't need on. Or have the project-level config do that (it might).

Either way - it's worth remembering. 

## Plugins With MCPs 

You can configure this by adding `mcp.json` at the plugin **root**.

I'm not using plugins yet so will write more about this when I do.

## What's "Project Scope"? Note For Solo Development Projects

Something that I've noticed:

- As an individual user, I can create my own `mcp.json` at the base of a repo and it works!

So ... why use the CLI then?

If you're flying solo or using a repo for non-dev work, there's nothing inherently wrong with creating MCP.json.

Creating a JSON is what Anthropic call "project scope." As far as I know, there's no matching CLI param for this scope... it's file-defined.

Why/when this is useful:

- Everyone in the repo gets the JSON (i.e., it's not git-ignored)
- Everyone working on the project gets those MCPs 

## Clarifying The Terminology

The terminology for the three scopes currently implemented is just a little confusing:

"Local" and "user" scope sound the same. To recap the difference: user scope will install to the system-level config; local scope is confined to the directory (and is the default). 

Project.json kind of achieves the same thing as local scope but is captured as a JSON with the idea (I presume) that it will escape a git ignore and thus be (by default) visible across the repo by contributors.

If you're using Claude Code on your own repos, the TL;DR is this: user scope installs in the system-wide config and local scope just in the repo. Make sure to pass the user parameter if you want the MCP to be available across projects.

## Claude... Where Are You?

It can be a bit confusing figuring out where Claude's system-level configuration file is.

Basically, `~/.claude` is where the system/OS level configuration is.

At that level you'll find:

```
.credentials.json
history.jsonl
settings.json
settings.local.json
```

System-wide slash commands are:

`~/.claude/commands/*.md`

Subfolders, if used, define namespaces.

## Folder-Level .claude Folders

If you run Claude from the home directory, as anywhere else, it will do its "thing." Namely:

- Creating `./.claude`
- Creating `./.claude/settings.local.json` to hold permissions for that part of the filesystem

If you've done this, just remember that these are not the system-level configurations.