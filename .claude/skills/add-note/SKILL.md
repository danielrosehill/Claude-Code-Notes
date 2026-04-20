---
name: add-note
description: Turn Daniel's rough notes (text, voice, URL, repo path, or unresolved Q&A) into a note in notes/, stamped with the date and Claude Code version. Edits are light — these are rough cliff notes, not polished docs. Use when Daniel says "add a note", "new note", or drops rough material for this repo.
---

# Add Note

Daniel drops rough material; you file it in `notes/` with a date + CC version stamp and update the README index. Claude Code changes fast, so every note records the CC version at write-time.

**Edit lightly.** These notes are supposed to feel rough — first-person, opinionated, sometimes unresolved. Your job is typo fixes, obvious grammar, and structure (headings if missing). Do NOT rewrite Daniel's voice, smooth out the prose, or pad it out.

## Inputs

Daniel's rough input may be:
- Free-form prose / bullets pasted into chat
- A path to a voice note → transcribe first
- A URL → fetch and skim
- A repo path → read CLAUDE.md / README

## Steps

1. **Capture the stamp** — run `claude --version` and `date +%d/%m/%Y`. Use these verbatim in the note frontmatter block (see template below). Do not guess the version.

2. **Pick a filename** — kebab-case, descriptive, in `notes/`. Check `notes/` first to avoid collisions.

3. **Write the note** using this header template:

   ```markdown
   # <Title>

   **Date:** DD/MM/YYYY
   **Claude Code version at time of writing:** X.Y.Z

   <body>

   ---

   *Claude Code moves fast — this may be outdated by the time you read it.*
   ```

   Two common body shapes:

   **Prose / pattern note** — lede paragraph, then sections as needed, concrete examples, links.

   **Unresolved Q&A note** — Daniel often drops these: a Source link, then `Question:` framing, then `Question 1 / Answer 1 / ...` blocks, often ending with "Issue: unresolved". Keep this structure as-is. Do not flatten it into prose. If Daniel asked you to push back or add a resolved answer, append it as a clearly labelled section at the bottom (e.g. `## Postscript — resolved answer`) rather than editing his Q&A body.

   Style rules:
   - Preserve Daniel's voice. First-person, opinionated, sometimes unfinished.
   - Typo and obvious-grammar fixes only. No rewriting, no smoothing, no padding.
   - If the rough note is short, the final note is short.

4. **Update `README.md`** — add a row to the appropriate Notes Index table (or create a new section if none fits). Format:
   `| [Title](notes/filename.md) | DD/MM/YYYY | One-line summary |`

5. **Show Daniel the draft** before doing anything else. Do NOT commit or push — that's the `publish-note` skill's job.

## User input

$ARGUMENTS
