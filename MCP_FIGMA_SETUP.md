### Connect Cursor to Figma via MCP

Follow these steps to enable Figma access in MCP-enabled IDEs (Cursor, Claude Desktop, etc.).

- **Prereqs**
  - Node.js 18+
  - Figma Personal Access Token (PAT)

- **1) Create a Figma token**
  - In Figma: Profile menu → Settings → Personal access tokens
  - Generate a token with access to files you need. Copy it.

- **2) Configure the MCP server**
  - We use the community `mcp-figma` server (stdio via npx).
  - In this repo, `mcp.config.json` is provided as a template.
  - Update the token placeholder:

```json
{
  "mcpServers": {
    "figma": {
      "command": "npx",
      "args": ["-y", "mcp-figma"],
      "env": {
        "FIGMA_API_KEY": "figd_xxxxxxxxxxxxxxxxx"
      }
    }
  }
}
```

- **3) Add to Cursor**
  - Open Cursor Settings → MCP (or Tools & Integrations) → Add server
  - Paste the JSON above into your MCP config, or add an entry named `figma` with the same fields.
  - Alternatively, place `mcp.config.json` in your global MCP config location and point Cursor to it.

- **4) Install and test (optional)**
  - You can prefetch the server binary:
  ```bash
  npm i -g mcp-figma
  ```
  - Then in your IDE, ask the agent to "list MCP tools" or run a simple call like "get file by key" once connected.

- **Troubleshooting**
  - Invalid token → regenerate in Figma and update `FIGMA_API_KEY`.
  - No tools listed → ensure Node 18+, internet access, and that `npx mcp-figma` works locally.
  - Enterprise Figma permissions may restrict file access; verify your account can open the file in browser.

- **Security**
  - Treat your Figma PAT as secret. Prefer environment variables over committing tokens to files.

