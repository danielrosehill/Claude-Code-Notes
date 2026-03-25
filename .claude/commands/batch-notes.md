Create multiple notes from a batch of sources.

The user will provide multiple sources (repos, voice notes, URLs, descriptions). Process each one into a separate note, then update the index once at the end.

## Instructions

1. Parse the user's input to identify each distinct source/topic.
2. For each source:
   - Read/transcribe/fetch the source material
   - Create a note in `notes/` following the same conventions as `/new-note`:
     - Kebab-case filename
     - `# Title` on first line
     - Date (DD-MM-YYYY) on second line
     - Casual, opinionated tone with practical takeaways
     - Disclaimers where subjective
     - Links to sources
3. After all notes are created, rebuild the README index (newest first).
4. Show a summary of all created notes before committing.

## User input

$ARGUMENTS
