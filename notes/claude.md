# CLAUDE.md - Strategic Separation!

25-03-2026

CLAUDE.md serves as the system prompt in Claude Code. Other agentic frameworks mirror the approach with their own markdown file. 

One of the most underconsidered aspects of Claude Code (IMO!) is how the chaining (I call it concatenation) of these instructions work.

Palo Perrone, writing in Hackernoon had [this])https://hackernoon.com/the-complete-guide-to-ai-agent-memory-files-claudemd-agentsmd-and-beyond) to say about this critical question - which is clearer than Anthropic's own documentation:

"The hierarchy loads bottom-up. Enterprise policies load first, then your personal preferences, **then project-level, then subdirectory-level. More specific instructions override broader ones**."

I've added the highlight for emphasis. 

## Practical Takeaways

I use Claude Code as a general purpose assistant. The idea of thinking of an agentic CLI as purely a tool for code generation within repos never connected with me. I run Ubuntu. Hence, I pop Claude open all the time at arbitrary positions on my filesystem - disproportionately the home folder but also .... random nooks and crannies. 

This doesn't gel very intuitively with how Anthropic has designed the tool, but it is something worth doing deliberately and carefully because the point in the file system at which you open Claude has important ramifications for how freely the agent will be able to move. Although if you run Claude with dangerous permissions, these concerns are mostly negated.

Coming back to Peronne's point above, this is where there is an enormous risk of not only context bloat, but also Claude ingesting conflicting instructions before it's even received the first user prompt, degrading reasoning and task performance. 

For example, let's say you have a setup like mind:

`/daniel/CLAUDE.md` - General OS-level instructions 
`/daniel/programs/CLAUDE.md` - "Hey Claude, this is where and how I like to store programs on this OS!" 
`/daniel/programs/ai-ml/CLAUDE.md` - "This is where I put my AI and ML projects"
`/daniel/programs/ai-ml/voice-typer-v1/CLAUDE.md` - Detailed project specific context for a repo I'm working on.

Then:

If Perrone's understanding and mine is correct, Claude will have to process all four CLAUDE.md files before every single user prompt. Even with prompt caching, it seems like a lot of potential bloat. 

This is why I have shifted to creating a folder structure that - wherever posisible - tries to use the base level CLAUDE.md merely as an entrypoint pointing to deeper context - so that the agent only ingests it when needed. 

So instead of my home folder being a huge CLAUDE.md monolith, it's a lightweight file that looks something like this:

`~/CLAUDE.md` - I'm Daniel. This is my computer. The programs I prefer are in ~/.claude/ai-context/program-preferences.md` 

Etc. 

For repos, I've experimented with creating a similar bifurcation. 