Rebuild the Notes Index table in README.md by scanning all markdown files in `notes/`.

## Instructions

1. Read every `.md` file in `notes/`.
2. Extract from each:
   - The title (first `#` heading)
   - The date (second line, DD-MM-YYYY format)
   - A one-line summary (first substantive paragraph or the user-provided summary)
3. Rebuild the `## Notes Index` table in README.md, sorted by date (newest first).
4. Format: `| [Title](notes/filename.md) | DD/MM/YYYY | Summary |`
5. Show the updated table to the user.
