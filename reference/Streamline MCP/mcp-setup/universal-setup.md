---
title: Universal setup
excerpt: Generic MCP configuration that works with most MCP-compatible clients.
deprecated: false
hidden: false
metadata:
  robots: index
---

Most MCP-compatible clients accept a JSON configuration block. Add the following to your client, replacing `YOUR_API_KEY_HERE` with your Streamline API key:

```json
{
  "mcpServers": {
    "streamlineMCPServer": {
      "name": "Streamline MCP Server",
      "url": "https://public-api.streamlinehq.com/mcp",
      "headers": {
        "X-API-Key": "YOUR_API_KEY_HERE"
      }
    }
  }
}
```

Don't have a key yet? See <Anchor href="https://docs.streamlinehq.com/reference/mcp-setup">Setup → Authentication</Anchor> for how to generate one.

For step-by-step instructions tailored to a specific client, see the dedicated guides: <Anchor href="https://docs.streamlinehq.com/reference/claude">Claude</Anchor>, <Anchor href="https://docs.streamlinehq.com/reference/cursor">Cursor</Anchor>, <Anchor href="https://docs.streamlinehq.com/reference/codex">Codex</Anchor>, <Anchor href="https://docs.streamlinehq.com/reference/gemini-cli">Gemini CLI</Anchor>, and <Anchor href="https://docs.streamlinehq.com/reference/antigravity">Antigravity</Anchor>.
