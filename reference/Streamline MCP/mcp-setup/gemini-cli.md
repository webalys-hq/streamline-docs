---
title: Gemini CLI
excerpt: Add the Streamline MCP Server to the Gemini CLI.
deprecated: false
hidden: false
metadata:
  robots: index
---

Add the Streamline MCP Server to your `.gemini/settings.json`, replacing `YOUR_API_KEY_HERE` with your Streamline API key:

```json .gemini/settings.json
{
  "mcpServers": {
    "streamline": {
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

For more details, see the <Anchor target="_blank" href="https://geminicli.com/docs/tools/mcp-server/">Gemini CLI MCP documentation</Anchor>.

To confirm it's connected, ask the Gemini CLI to **search for a dog icon** — you should get results from Streamline.
