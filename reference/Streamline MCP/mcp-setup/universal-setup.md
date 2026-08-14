---
title: Universal setup
excerpt: Generic MCP configuration that works with most MCP-compatible clients.
deprecated: false
hidden: false
metadata:
  robots: index
---

Most MCP-compatible clients accept a JSON configuration block. If your client supports OAuth — most do — add the following and let it walk you through signing in to Streamline:

```json
{
  "mcpServers": {
    "streamlineMCPServer": {
      "name": "Streamline MCP Server",
      "url": "https://public-api.streamlinehq.com/mcp"
    }
  }
}
```

Streamline supports dynamic client registration, so there are no client credentials to configure. The first time the client connects, it opens your browser to sign in and authorize access.

For clients that don't support OAuth, add your Streamline API key as a header instead, replacing `YOUR_API_KEY_HERE`:

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

To confirm it's connected, ask your client to **search for a dog icon** — you should get results from Streamline.

For step-by-step instructions tailored to a specific client, see the dedicated guides: <Anchor href="https://docs.streamlinehq.com/reference/claude">Claude</Anchor>, <Anchor href="https://docs.streamlinehq.com/reference/cursor">Cursor</Anchor>, <Anchor href="https://docs.streamlinehq.com/reference/chatgpt">ChatGPT</Anchor>, and <Anchor href="https://docs.streamlinehq.com/reference/antigravity">Antigravity</Anchor> (also covers the Gemini CLI).
