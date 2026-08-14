---
title: Cursor
excerpt: Connect Cursor to the Streamline MCP Server.
deprecated: false
hidden: false
metadata:
  robots: index
---

Go to **Cursor > Cursor Settings > Tools & MCPs**, then click **New MCP Server** and add the `streamlineMCPServer` configuration below. There's no API key to paste — you sign in with OAuth:

```json Cursor
{
  "mcpServers": {
    "streamlineMCPServer": {
      "name": "Streamline MCP Server",
      "url": "https://public-api.streamlinehq.com/mcp"
    }
  }
}
```

Back in **Tools & MCPs**, the server appears as needing login: click **Login**, sign in to Streamline in your browser, and grant access. Cursor stores and refreshes the token for you.

You can see more details about adding MCPs to Cursor here: [https://cursor.com/docs/mcp](https://cursor.com/docs/mcp "https://cursor.com/docs/mcp")

To confirm it's connected, ask Cursor to **search for a dog icon** — you should get results from Streamline.
