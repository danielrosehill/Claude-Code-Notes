# Current Working Directory (CWD)

I've spent much of the last week on a frantic quest to debug just about every desktop and local network issue that exists in my house (the list was long). 

This has been possible thanks to the fact that Claude has high reasoning and is extremely versatile: all you need to use Claude for local Linux desktop stuff is a terminal - and by extension, you can get it to work on just about any other computer on the planet if you have an SSH connection to it. 

This approach is great but also flies in the face of the main "use case" for Claude Code, at least as it stands today - which is collaborative development in which sandboxing an agent to within the bounds of a repository (or even a level of the repo / filesystem) is desirable and standard best practice.

The arch nemesis of the YOLO method is the CWD constraint. At the time of writing, it's also kind of a clunky thing to work around: Claude *can* break out of the CWD but even in the most permissive setting possible you tend to get reminders and noisy messages. 

## The add-dir Flag

There are generally two methods of passing parameters in CLIs - Claude being only one example:

- Launch parameters or command parameters 
- Persistent configs 

Claude (and Codex and Gemini) tend to have an `--adddir` flag (or similar) for extending the sandbox on the fly (appropriate when the use for sandboxing is agent supervision rather than security, of course). 

So one option is to do *that* and open up the whole FS (!) or home when you need it. 

## Persistent Approach: Settings 

Settings are discussed here in the docs: https://docs.claude.com/en/docs/claude-code/settings

In Linux the file is: `~/.claude/settings.json`.

### Adding Home Dir As Trusted

Within the JSON array you can add:

```
  "trustedFolders": [
    "~"
  ]
```
### Trust The Whole Filesystem / Free Access

```
  "trustedFolders": [
    "/"
  ]