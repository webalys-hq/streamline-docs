---
title: Codex
excerpt: Add the Streamline MCP Server to Codex.
deprecated: false
hidden: false
metadata:
  robots: index
---

Go to **Codex > Settings > MCP Servers** and click **Add Server**. Fill the form with the following information:

- **Name:** Streamline MCP Server
- Select the **Streamable HTTP** option
- **URL:** [https://public-api.streamlinehq.com/mcp](https://public-api.streamlinehq.com/mcp "https://public-api.streamlinehq.com/mcp")
- **Headers Key:** `X-API-Key`
- **Headers Value:** `YOUR_API_KEY_HERE` (replace with your actual key)

Then click **Save**.

Don't have a key yet? See [Setup → Authentication](https://docs.streamlinehq.com/reference/mcp-setup) for how to generate one.

![](https://files.readme.io/5d94c07b2ed859c6acd20b7e01796f72e803b77357a2d140bddf2ad545744a85-image.png)

To confirm it's connected, ask Codex to **search for a dog icon** — you should get results from Streamline.
