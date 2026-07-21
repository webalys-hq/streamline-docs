---
title: Setup
excerpt: Connect an MCP client to the Streamline MCP Server and authenticate.
deprecated: false
hidden: false
metadata:
  robots: index
---

Point your MCP client at `https://public-api.streamlinehq.com/mcp` and authenticate. Pick your client below and copy its config to get started.

## Connect a client

Each guide has the exact config to copy and paste:

- <Anchor href="https://docs.streamlinehq.com/reference/claude">Claude</Anchor> — Desktop, Web, and Claude Code (CLI)
- <Anchor href="https://docs.streamlinehq.com/reference/cursor">Cursor</Anchor>
- <Anchor href="https://docs.streamlinehq.com/reference/codex">Codex</Anchor>
- <Anchor href="https://docs.streamlinehq.com/reference/gemini-cli">Gemini CLI</Anchor>
- <Anchor href="https://docs.streamlinehq.com/reference/antigravity">Antigravity</Anchor>
- <Anchor href="https://docs.streamlinehq.com/reference/universal-setup">Universal setup</Anchor> — generic config that works with most other clients

## Authentication

Authenticate each request to `https://public-api.streamlinehq.com/mcp` with **one** of these — your client's guide above tells you which it uses:

- **OAuth (recommended)** — a browser-based sign-in with no API key to copy or paste. You click **Connect**, sign in to Streamline, and authorize access. Clients like the Claude Desktop and Web apps use this flow.
- **API key** — for clients that don't support OAuth. Generate one from your <Anchor target="_blank" href="https://www.streamlinehq.com/profile?tab=api_keys">API settings page</Anchor> (see the <Anchor target="_blank" href="https://docs.streamlinehq.com/reference/quick-start-guide">Quick start guide</Anchor>) and send it in the `X-API-Key` header.

## Need help?

Want direct access to the Streamline dev team? <a href="https://go.streamlinehq.com/mcp-support" target="_blank">Join our public Slack channel</a> to ask questions, share feedback, and get help setting up the MCP server straight from the people building it.
