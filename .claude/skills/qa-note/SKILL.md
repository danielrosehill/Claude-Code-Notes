---
name: qa-note
description: Capture a Q&A exchange as a note. Daniel asks a Claude Code question, you answer, then this skill writes the question + answer into notes/ with the standard date + CC version stamp and updates the README index. Use when Daniel says "make this a note", "Q&A note", or asks a question and wants the answer filed.
---

# Q&A Note

Daniel asks a question about Claude Code. You answer it in chat. This skill turns that exchange into a note in `notes/`.

Unlike `add-note`, the Q&A here is **resolved** — your answer is the body, not a parked "Issue: unresolved" block.

## Steps

1. **Confirm the Q&A pair** — the question Daniel just asked and the answer you just gave (or are about to give). If Daniel invokes this skill before you've answered, answer first, then file.

2. **Capture the stamp** — run `claude --version` and `date +%d/%m/%Y`. Use verbatim. Do not guess.

3. **Pick a filename** — kebab-case, descriptive, in `notes/`. Check for collisions.

4. **Write the note** using this template:

   ```markdown
   # <Title — phrase the question or topic>

   **Date:** DD/MM/YYYY
   **Claude Code version at time of writing:** X.Y.Z

   ## Question

   <Daniel's question, lightly cleaned for transcription artifacts only>

   ## Answer

   <Your answer. Keep it tight — this is a notebook, not docs. Code blocks, links, and concrete examples welcome.>

   ---

   *Claude Code moves fast — this may be outdated by the time you read it.*
   ```

   Style rules:
   - Preserve Daniel's voice in the question. Fix only obvious transcription slips.
   - Answer should match what you said in chat — don't expand into a tutorial.
   - If the answer cited docs or commands, include the links/snippets.

5. **Update `README.md`** — add a row to the appropriate Notes Index table:
   `| [Title](notes/filename.md) | DD/MM/YYYY | One-line summary |`

6. **Show Daniel the draft.** Do NOT commit or push — that's `publish-note`.

## User input

$ARGUMENTS
