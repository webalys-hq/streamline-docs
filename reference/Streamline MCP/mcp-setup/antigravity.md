---
title: Antigravity
excerpt: Add the Streamline MCP Server to the Antigravity CLI and IDE.
deprecated: false
hidden: false
metadata:
  robots: index
---

Add the Streamline MCP Server to your `~/.gemini/config/mcp_config.json`, replacing `YOUR_API_KEY_HERE` with your Streamline API key. Because this config lives in `~/.gemini/config/mcp_config.json`, it applies to **both the Antigravity CLI and the Antigravity IDE** — configure it once and it's available in both:

```json ~/.gemini/config/mcp_config.json
{
  "mcpServers": {
    "streamline": {
      "serverUrl": "https://public-api.streamlinehq.com/mcp",
      "headers": {
        "X-API-Key": "YOUR_API_KEY_HERE"
      }
    }
  }
}
```

Don't have a key yet? See <Anchor href="https://docs.streamlinehq.com/reference/mcp-setup">Setup → Authentication</Anchor> for how to generate one.

For more details, see the <Anchor target="_blank" href="https://antigravity.google/docs/mcp">Antigravity MCP documentation</Anchor>.

To confirm it's connected, ask Antigravity to **search for a dog icon** — you should get results from Streamline.
