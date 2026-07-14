---
title: Setup
excerpt: Connect an MCP client to the Streamline MCP Server and authenticate.
deprecated: false
hidden: false
metadata:
  robots: index
---

Point your MCP client at `https://public-api.streamlinehq.com/mcp` and authenticate. The simplest way to connect is **OAuth** — a browser-based sign-in with no keys to copy or paste. Clients that don't support OAuth can use an **API key** instead. Then follow the guide for your specific client below.

## Authentication

The Streamline MCP endpoint supports two ways to authenticate. Use either one on each request to [https://public-api.streamlinehq.com/mcp](https://public-api.streamlinehq.com/mcp) (not both at once).

### OAuth 2.1 — recommended

The simplest way to connect: a browser-based sign-in, with no API key to find, copy, or paste. Clients such as the Claude Desktop and Web apps use this flow — you click **Connect**, sign in to Streamline, and authorize access. See the <Anchor href="https://docs.streamlinehq.com/reference/claude">Claude</Anchor> guide for a step-by-step walkthrough.

Under the hood, the client sends a Streamline-issued access token in the Authorization header:

```
Authorization: Bearer <access_token>
```

The server validates Bearer tokens issued by this API's OAuth endpoints (Authorization Code + PKCE). In this mode, the `X-API-Key` header is not used.

Discovery (machine-readable):

| What                     | URL                                                                                |
| ------------------------ | ---------------------------------------------------------------------------------- |
| Protected resource (MCP) | `GET https://public-api.streamlinehq.com/mcp/.well-known/oauth-protected-resource` |
| Authorization server     | `GET https://public-api.streamlinehq.com/.well-known/oauth-authorization-server`   |

Clients use these endpoints to retrieve the authorization server base URL, registration endpoint, authorize and token URLs, and supported scopes (e.g. `mcp:tools`).

### API Key — alternative

For clients that don't support OAuth — or if you prefer managing keys directly — authenticate with a Streamline API key. Generate one from your <Anchor target="_blank" href="https://www.streamlinehq.com/profile?tab=api_keys">API settings page</Anchor> — see the <Anchor target="_blank" href="https://docs.streamlinehq.com/reference/quick-start-guide">Quick start guide</Anchor> for step-by-step instructions. Send it in the `X-API-Key` header with every MCP request.

## Connect a client

Follow the guide for your client:

- <Anchor href="https://docs.streamlinehq.com/reference/universal-setup">Universal setup</Anchor> — generic config that works with most clients
- <Anchor href="https://docs.streamlinehq.com/reference/claude">Claude</Anchor> — Desktop, Web, and Claude Code (CLI)
- <Anchor href="https://docs.streamlinehq.com/reference/cursor">Cursor</Anchor>
- <Anchor href="https://docs.streamlinehq.com/reference/codex">Codex</Anchor>
- <Anchor href="https://docs.streamlinehq.com/reference/gemini-cli">Gemini CLI</Anchor>
- <Anchor href="https://docs.streamlinehq.com/reference/antigravity">Antigravity</Anchor>

## Need help?

Want direct access to the Streamline dev team? <a href="https://go.streamlinehq.com/mcp-support" target="_blank">Join our public Slack channel</a> to ask questions, share feedback, and get help setting up the MCP server straight from the people building it.
