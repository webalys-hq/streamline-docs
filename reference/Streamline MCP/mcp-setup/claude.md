---
title: Claude
excerpt: Add the Streamline MCP Server to Claude — Desktop, Web, or Claude Code (CLI).
deprecated: false
hidden: false
metadata:
  robots: index
---

Claude connects to the Streamline MCP Server in two ways. Pick the one that matches how you use Claude:

- **Desktop & Web app** — install the official Streamline connector from the Claude directory and sign in with OAuth.
- **Claude Code (CLI)** — add the server with a single `claude mcp add` command, then sign in with OAuth.

<Accordion title="Desktop & Web app (Connectors)" icon="fa-desktop" defaultState="open">

**Prerequisites**

Before you begin, make sure you have a Streamline account. You will be prompted to sign in and authorize access during the connection flow.

---

**Step 1 — Add the Streamline Connector**

Streamline is available as an official connector in the Claude directory:

1. Open <Anchor target="_blank" href="https://claude.ai/directory/connectors/streamline-icons">Streamline in the Claude connector directory</Anchor>
2. Click **Add** (or **Connect**) to add it to your Claude account

You can also find it from inside Claude under **Settings → Connectors → Browse connectors**, then search for `Streamline`.

> 📘 Don't see it in the directory?\
> On some Claude plans the directory is managed by your workspace admin. In that case, add Streamline manually: go to **Settings → Connectors → Add custom connector**, name it (e.g., `Streamline MCP`), set the MCP Server URL to `https://public-api.streamlinehq.com/mcp`, and click **Add**.

---

**Step 2 — Authenticate and Authorize**

1. After adding the connector, click **Connect**
2. You will be redirected to the Streamline web app
3. Sign in to your account if prompted
4. Review and grant the requested access. Once authorized, you will be redirected back to Claude automatically.

---

**Step 3 — Verify the Connection**

After being redirected back to Claude, confirm the connector is active:

- Go to **Settings → Connectors**
- The Streamline MCP Server should appear with a **Connected** status

---

**Step 4 — Test It**

1. Start a new chat in Claude
2. Ask Claude to verify the connector is working, for example:

   > _"Check if you are connected to the Streamline MCP Server"_

   Claude will confirm the connection and list the available tools.

---

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

Add the server — no API key needed, you sign in with OAuth:

```shell
claude mcp add --transport http streamline-mcp https://public-api.streamlinehq.com/mcp
```

Then start Claude Code and run `/mcp`, select **streamline-mcp**, and choose **Authenticate**. Your browser opens the Streamline sign-in page; grant access and you'll be returned to the terminal, already connected.

Run `claude mcp list` to confirm it's up and running.

</Accordion>
