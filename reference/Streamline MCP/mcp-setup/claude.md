---
title: Claude
excerpt: Add the Streamline MCP Server to Claude — Desktop, Web, or Claude Code (CLI).
deprecated: false
hidden: false
metadata:
  robots: index
---

Claude connects to the Streamline MCP Server in two ways. Pick the one that matches how you use Claude:

- **Desktop & Web app** — add Streamline as a custom connector and sign in with OAuth.
- **Claude Code (CLI)** — add the server with a single `claude mcp add` command using your API key.

<Accordion title="Desktop & Web app (Connectors)" icon="fa-desktop" defaultState="open">

**Prerequisites**

Before you begin, make sure you have a Streamline account. You will be prompted to sign in and authorize access during the connection flow.

***

**Step 1 — Add the Custom Connector**

1. Open Claude and go to **Settings → Connectors → Add custom connector**
2. Enter a name for the connector (e.g., `Streamline MCP`)
3. Set the MCP Server URL to your Streamline endpoint:
   ```
   https://public-api.streamlinehq.com/mcp
   ```
4. Click **Add**

***

**Step 2 — Authenticate and Authorize**

1. After adding the connector, click **Connect**
2. You will be redirected to the Streamline web app
3. Sign in to your account if prompted
4. Review and grant the requested access. Once authorized, you will be redirected back to Claude automatically.

***

**Step 3 — Verify the Connection**

After being redirected back to Claude, confirm the connector is active:

- Go to **Settings → Connectors**
- The Streamline MCP Server should appear with a **Connected** status

***

**Step 4 — Test It**

1. Start a new chat in Claude
2. Ask Claude to verify the connector is working, for example:

   > _"Check if you are connected to the Streamline MCP Server"_

   Claude will confirm the connection and list the available tools.

***

**What You Can Do**

Once connected, you can ask Claude to:

- Search for icons, illustrations, or design elements from the Streamline library

- Filter assets by style, type, or pricing tier (free or premium)

- Download assets as PNG with custom size, colors, and stroke width

**Example prompts:**

- _"Find me a line-style icon for notifications"_
- _"Search for free illustrations related to teamwork"_
- _"Download the settings icon as a 64px PNG"_

</Accordion>

<Accordion title="Claude Code (CLI)" icon="fa-terminal">

Run this command, replacing `YOUR_API_KEY_HERE` with your Streamline API key:

```shell
claude mcp add --transport http streamline-mcp https://public-api.streamlinehq.com/mcp --header "X-API-Key: YOUR_API_KEY_HERE"
```

Run `claude mcp list` to confirm it's up and running.

</Accordion>
