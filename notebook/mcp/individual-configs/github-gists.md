# Github Gists (Gistpad)

Project:

https://github.com/lostintangent/gistpad-mcp

CLI Syntax:

```
claude mcp add --transport stdio --scope user  github-gists --env GITHUB_TOKEN="your-token-here" -- npx -y gistpad-mcp
```

## Explanation

Refer: docs

https://code.claude.com/docs/en/mcp

The two double-dashes (--) divides between the Claude params and the MCP run commands 

Hence it's:

``-- npx``

and not:

``--npx``

Even though - to Linux folks - the first looks wrong!

Note: this is for User scope.

Recommendation: create a PAT just for gists.