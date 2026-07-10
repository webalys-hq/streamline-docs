---
title: Cursor
excerpt: Connect Cursor to the Streamline MCP Server.
deprecated: false
hidden: false
metadata:
  robots: index
---

Go to **Cursor > Cursor Settings > Tools & MCPs**, then click **New MCP Server** and add the `streamlineMCPServer` configuration below, replacing `YOUR_API_KEY_HERE` with your Streamline API key:

```json Cursor
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

You can see more details about adding MCPs to Cursor here: [https://cursor.com/docs/mcp](https://cursor.com/docs/mcp "https://cursor.com/docs/mcp")
