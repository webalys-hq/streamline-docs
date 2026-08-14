---
title: Antigravity
excerpt: Add the Streamline MCP Server to Antigravity (CLI and IDE) and the Gemini CLI.
deprecated: false
hidden: false
metadata:
  robots: index
---

Both of Google's clients connect to the Streamline MCP Server with OAuth — there is no API key to copy or paste. Pick the one you use:

<Accordion title="Antigravity (CLI & IDE)" icon="fa-rocket" defaultState="open">

Add the Streamline MCP Server to your `~/.gemini/config/mcp_config.json`. Because this config lives in `~/.gemini/config/mcp_config.json`, it applies to **both the Antigravity CLI and the Antigravity IDE** — configure it once and it's available in both:

```json ~/.gemini/config/mcp_config.json
{
  "mcpServers": {
    "streamline": {
      "serverUrl": "https://public-api.streamlinehq.com/mcp"
    }
  }
}
```

No `headers` block is needed — Streamline supports dynamic client registration, so Antigravity discovers the OAuth endpoints on its own.

Then authenticate:

1. Open **Agent Settings** (`Cmd+,` on macOS, `Ctrl+,` on Windows/Linux)
2. Go to the **Customizations** tab and click **Authenticate** next to `streamline`
3. Sign in to Streamline in your browser and grant access
4. Copy the authorization code back into the settings panel and click **Submit**

Access tokens are stored and refreshed automatically.

For more details, see the <Anchor target="_blank" href="https://antigravity.google/docs/mcp">Antigravity MCP documentation</Anchor>.

To confirm it's connected, ask Antigravity to **search for a dog icon** — you should get results from Streamline.

</Accordion>

<Accordion title="Gemini CLI" icon="fa-terminal">

Add the Streamline MCP Server to your `.gemini/settings.json`:

```json .gemini/settings.json
{
  "mcpServers": {
    "streamline": {
      "httpUrl": "https://public-api.streamlinehq.com/mcp",
      "authProviderType": "dynamic_discovery"
    }
  }
}
```

Use `httpUrl` (streamable HTTP), not `url` — `url` is for SSE endpoints.

Then start the Gemini CLI and run:

```shell
/mcp auth streamline
```

Sign in to Streamline in your browser and grant access. Tokens are stored and refreshed for you.

For more details, see the <Anchor target="_blank" href="https://geminicli.com/docs/tools/mcp-server/">Gemini CLI MCP documentation</Anchor>.

To confirm it's connected, ask the Gemini CLI to **search for a dog icon** — you should get results from Streamline.

</Accordion>
