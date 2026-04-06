# Cloudinary MCP Installation - Claude Code

30 Oct 2025

## Cloudinary MCPs

Cloudinary maintains a list of MCP servers here:

https://github.com/cloudinary/mcp-servers

The asset management repo is https://github.com/cloudinary/asset-management-js

## JSON 

The JSON model for adding the asset management MCP is:

```
{
  "mcpServers": {
    "cloudinary-asset-mgmt": {
      "command": "npx",
      "args": [
        "-y", "--package", "@cloudinary/asset-management",
        "--",
        "mcp", "start",
        "--cloud-name", "cloud_name",
        "--api-key", "api_key",
        "--api-secret", "api_secret"
      ]
    }
  }
}
```

Replace secret placeholders with secrets, of course. 

## Add With Bash Command

This is the bash:

```
claude mcp add --transport stdio cloudinary-asset-mgmt --scope user \
  -- npx -y --package @cloudinary/asset-management -- mcp start \
  --api-key 123456789012345 --api-secret aBcDeFgHiJkLmNoPqRsTuVwXyZ --cloud-name examplecloud
  ```