# Claude Space Self-Ideator

25-03-2026

This one is meta and I love it: [Claude-Space-Self-ideator](https://github.com/danielrosehill/Claude-Space-Self-ideator) is a Claude workspace for generating ideas for more Claude workspaces.

## The Concept

A "Claude Space" is a version-controlled repo acting as a miniaturised agentic workspace (see [Agent Workspace Model](agent-workspace-model.md)). This repo uses that exact pattern to brainstorm new workspace ideas across categories like personal development, relationships, home life, mental wellbeing, and creative projects.

Run `/develop-idea` with a rough concept and it generates a structured Claude Space specification document.

## What's In There

Around 30 structured idea documents, each describing a potential workspace with its purpose, suggested slash commands, context files, and expected workflows. It also includes `the-idea.md` with the detailed rationale for the workspace concept, plus docs on agent portability and development patterns.

## The Pitch

The underlying argument is that folder structure + Markdown files provide lightweight RAG without any database or vector infrastructure. Git gives you versioning for free. This is Claude's own analysis of why the pattern works, documented within the workspace itself.

## Why This Is Interesting

It's exploratory and self-referential — using the pattern to generate more instances of itself. Whether you find that delightful or absurd probably says something about your relationship with AI tooling.

**Disclaimer**: Very much an experimental/exploratory repo. The workspace ideas range from practical to whimsical.

## Source

- [Claude-Space-Self-ideator](https://github.com/danielrosehill/Claude-Space-Self-ideator)
