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

For more details, see the <Anchor target="_blank" href="https://geminicli.com/docs/tools/mcp-server/">Gemini CLI MCP documentation</Anchor>.
