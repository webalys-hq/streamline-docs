---
title: Claude Code (CLI)
excerpt: Add the Streamline MCP Server to Claude Code.
deprecated: false
hidden: false
metadata:
  robots: index
---

Run this command, replacing `YOUR_API_KEY_HERE` with your Streamline API key:

```shell
claude mcp add --transport http streamline-mcp https://public-api.streamlinehq.com/mcp --header "X-API-Key: YOUR_API_KEY_HERE"
```

Run `claude mcp list` to confirm it's up and running.
