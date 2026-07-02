---
title: MCP Server
excerpt: Streamline MCP server exposing tools and resources via HTTP JSON-RPC.
deprecated: false
hidden: false
metadata:
  robots: index
---
## Overview

<Anchor target="_blank" href="https://modelcontextprotocol.io/docs/getting-started/intro">Model Context Protocol (MCP)</Anchor> is an open protocol that standardizes how applications provide context to large language models (LLMs). With MCP, AI apps (like Cursor or Claude) can connect to external applications, use their tools, and retrieve data seamlessly.

The Streamline MCP Server provides tools for accessing icons, illustrations, emojis, and other design assets within the Streamline application. It allows MCP-compatible clients to search, retrieve, and download assets in PNG or SVG formats.

## Key Features

- Search icons, illustrations, emojis, and elements.
- Retrieve detailed information about specific icons.
- Download assets in PNG or SVG format with customization options (size, colors, background, stroke).
- Fully compatible with MCP protocol clients.

## Use Cases

- Finding icons for web or mobile projects.
- Retrieving and customizing specific assets for design workflows.
- Automating icon-related tasks in applications or scripts.

## Pricing

Access via the Public API and MCP Server is included with **Pro plans** (up to **1,000 assets/week**).

For full plan details and current pricing, see the <Anchor target="_blank" href="https://home.streamlinehq.com/pricing">Streamline pricing page</Anchor>.

## Authentication

The Streamline MCP endpoint supports two ways to authenticate. Use either one on each request to [https://public-api.streamlinehq.com/mcp](https://public-api.streamlinehq.com/mcp) (not both at once).

### API Key

Before connecting, make sure you have your Streamline API key ready. You can generate one from your <Anchor target="_blank" href="https://www.streamlinehq.com/profile?tab=api_keys">API settings page</Anchor> — see the <Anchor target="_blank" href="https://docs.streamlinehq.com/reference/quick-start-guide">Quick start guide</Anchor> for step-by-step instructions. Send it in the X-API-Key header with every MCP request.

### OAuth 2.1 (Authorization Code + PKCE)

Send a Streamline-issued access token in the Authorization header:

```
Authorization: Bearer <access_token>
```

The server validates Bearer tokens issued by this API's OAuth endpoints. In this mode, the X-API-Key header is not used.

Discovery (machine-readable):

| What                     | URL                                                                                |
| ------------------------ | ---------------------------------------------------------------------------------- |
| Protected resource (MCP) | `GET https://public-api.streamlinehq.com/mcp/.well-known/oauth-protected-resource` |
| Authorization server     | `GET https://public-api.streamlinehq.com/.well-known/oauth-authorization-server`   |

Clients use these endpoints to retrieve the authorization server base URL, registration endpoint, authorize and token URLs, and supported scopes (e.g. `mcp:tools`).

## Connecting a Client

Point your MCP client at `https://public-api.streamlinehq.com/mcp` and authenticate with your API key (or, for Claude Connectors, the OAuth sign-in flow). Follow the guide for your client below.

### Cursor

Go to Cursor > Cursor Settings > Tools & MCPs and then click on "New MCP Server" and add the streamlineMCPServer configuration that you can see below:

Add the following configuration to your MCP-compatible client (e.g., <Anchor target="_blank" href="https://cursor.com/docs/context/mcp">Cursor</Anchor>, [Zed](https://zed.dev/docs/ai/mcp#as-custom-servers)) to connect to Streamline MCP Server:

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

```json Zed
"streamline": {
    /// The URL of the remote MCP server
    "url": "https://public-api.streamlinehq.com/mcp",
    "headers": {
     /// Any headers to send along
     "X-API-Key": "YOUR_API_KEY_HERE"
    }
}
```

You can see more details about adding MCPs to Cursor here: [https://cursor.com/docs/mcp](https://cursor.com/docs/mcp "https://cursor.com/docs/mcp")

### Claude Code (CLI)

Run this command replacing the YOUR\_API\_KEY\_HERE part with your Streamline Api Key.

```shell
claude mcp add --transport http streamline-mcp https://public-api.streamlinehq.com/mcp --header "X-API-Key: YOUR_API_KEY_HERE"
```

Run `claude mcp list` to confirm it's up and running.

### Codex

Go to Settings > Settings > MCP Servers and click on "Add Server". Fill the form with the following information: <br />**Name:** Streamline MCP Server<br />Select the **Streamable HTTP** option<br />**URL:** [https://public-api.streamlinehq.com/mcp](https://public-api.streamlinehq.com/mcp "https://public-api.streamlinehq.com/mcp")<br />**Headers Key:** X-API-Key <br />**Headers Value:** YOUR\_API\_KEY\_HERE (Replace with your actual key)<br />Then Click on **Save**

![](https://files.readme.io/5d94c07b2ed859c6acd20b7e01796f72e803b77357a2d140bddf2ad545744a85-image.png)

<br />

### Claude (via Connectors)

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

<br />

## How to Use

Once connected, you can access tools like `search_assets`, `search_sets`, `get_icon_by_hash`, `download_asset` and others directly through the client AI Chat. See the [Tools](#tools) section below for the full list and their parameters.

**Example:** You can experiment by asking the AI chat in your client to **search for dog icons**. The client will handle calling the appropriate MCP tool and returning the results.

## Tools

<Accordion title="search_assets" icon="fa-magnifying-glass">

Search for icons, illustrations, or elements. With a non-empty `setSlug`, search within that Set. With a non-empty `familySlug` (and no `setSlug`), search within that Family. Otherwise performs a global search — `productType` is required for global search.

| Parameter            | Type                                   | Description                                                                                                                                                                                                                                                                        |
| -------------------- | -------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `query` _(required)_ | string                                 | Search term. Translate abstract concepts into concrete visual nouns when searching globally. Never mix different concepts in the same query.                                                                                                                                       |
| `setSlug`            | string                                 | Set slug from `search_sets`, `find_sets_by_name`, or `get_all_sets_from_family`. When provided, search is scoped to this Set (takes precedence over `familySlug`).                                                                                                                 |
| `familySlug`         | string                                 | Family slug from `get_all_families`. When provided and `setSlug` is omitted, search is scoped to this Family.                                                                                                                                                                      |
| `productType`        | `icons` / `illustrations` / `elements` | Required for global search only (when both `setSlug` and `familySlug` are omitted). Asset type to search.                                                                                                                                                                          |
| `offset`             | number                                 | Number of items to skip before returning results. Default: `0`.                                                                                                                                                                                                                    |
| `limit`              | number                                 | Maximum number of items to return. Default: `20` (max `100`).                                                                                                                                                                                                                      |
| `productTier`        | `all` / `free` / `premium`             | Filter by price tier of Sets (e.g. `free` limits results to free Sets). Used for global search only. Default: `all`.                                                                                                                                                               |
| `style`              | enum                                   | Filter by Set style. Global search only; applies when `productType` is `icons`. One of: `line`, `solid`, `flat`, `duo`, `handrawn`, `creative`, `gradient`, `remix`, `neon`, `pop`, `light`, `glyph`, `minimal`, `outlined`, `geometric`, `bold`, `stroke`, `wireframe`, `filled`. |

</Accordion>

<Accordion title="search_sets" icon="fa-shapes">

Semantic search for **Sets** by meaning (not substring on stored names). For partial name match on stored Set names, use `find_sets_by_name`. To list all Sets in a Family without search intent, use `get_all_sets_from_family`.

| Parameter            | Type   | Description                                                                                                                                            |
| -------------------- | ------ | ------------------------------------------------------------------------------------------------------------------------------------------------------ |
| `query` _(required)_ | string | Natural-language search term. Minimum 1 character.                                                                                                     |
| `familySlug`         | string | When set, only return Sets belonging to this Family. Use the Family `slug` from `get_all_families`. Minimum 1 character when provided. Default: unset. |
| `limit`              | number | Maximum number of Sets to return. Default: `20` (max `100`).                                                                                           |

</Accordion>

<Accordion title="find_sets_by_name" icon="fa-font">

Case-insensitive **substring** match on stored **Set** names. Minimum 3 characters. For semantic discovery, use `search_sets`.

| Parameter           | Type   | Description                                                 |
| ------------------- | ------ | ----------------------------------------------------------- |
| `name` _(required)_ | string | Substring to match against Set names. Minimum 3 characters. |

</Accordion>

<Accordion title="get_all_families" icon="fa-list">

Returns all Families (e.g. hash, slug, and related fields) for browsing the full catalog.

_No parameters._

</Accordion>

<Accordion title="get_all_sets_from_family" icon="fa-list-ul">

Returns all Sets in a Family, with pagination. Use when you already know the Family and want a full list (no search).

| Parameter                 | Type   | Description                                                                                                                 |
| ------------------------- | ------ | --------------------------------------------------------------------------------------------------------------------------- |
| `familyHash` _(required)_ | string | Family hash. Use `hash` from `get_all_families` or `familyHash` from `find_sets_by_name` when available. Max 80 characters. |
| `offset`                  | number | Number of items to skip. Default: `0`.                                                                                      |
| `limit`                   | number | Maximum number of Sets to return. Default: `100` (max `100`).                                                               |

</Accordion>

<Accordion title="get_family_extra_details" icon="fa-circle-info">

Returns full semantic text for a Family in four sections: fit & recommendations, brand & cultural identity, visual & technical specs, and pairing & compatibility. Use when you need richer metadata to choose between Families after `search_sets` or `get_all_families`. Pass the exact `familySlug` from those results — do not invent slugs.

| Parameter                 | Type   | Description                          |
| ------------------------- | ------ | ------------------------------------ |
| `familySlug` _(required)_ | string | Family slug from `get_all_families`. |

</Accordion>

<Accordion title="get_icon_by_hash" icon="fa-info-circle">

Full icon metadata (Set, variants, preview URLs, tags, etc.) before download.

| Parameter               | Type   | Description                                  |
| ----------------------- | ------ | -------------------------------------------- |
| `iconHash` _(required)_ | string | Icon ID (hash) from `search_assets` results. |

</Accordion>

<Accordion title="download_asset" icon="fa-file-arrow-down">

Returns **JSON** with a short-lived signed `downloadUrl`, `expiresAt`, `expiresInSeconds`, `mimeType`, and `fileName`. The MCP `tools/call` is authenticated; perform a plain **GET** on `downloadUrl` without `X-API-Key` or Bearer (the URL carries the signed token) to download bytes. SVG-only params: `responsive`, `strokeToFill`.

| Parameter               | Type          | Description                                                                                                |
| ----------------------- | ------------- | ---------------------------------------------------------------------------------------------------------- |
| `format` _(required)_   | `png` / `svg` | Export format.                                                                                             |
| `iconHash` _(required)_ | string        | Icon ID (hash) from `search_assets` results.                                                               |
| `size` _(required)_     | number        | Square size in pixels.                                                                                     |
| `colors`                | string[]      | Array of HEX strings or CSS named colors. Default: `[]`.                                                   |
| `backgroundColor`       | string        | Background color (HEX or CSS name). Default: `#ffffff00` (transparent).                                    |
| `strokeWidth`           | number        | Adjust vector path thickness. Optional.                                                                    |
| `responsive`            | boolean       | SVG only. If true, SVG uses viewBox and drops fixed width/height for responsive scaling. Default: `false`. |
| `strokeToFill`          | boolean       | SVG only. If true, strokes become fills; `strokeWidth` is not applied. Default: `false`.                   |

</Accordion>

## FAQ

**Which clients can use Streamline MCP Server?**

> Any MCP-compatible client (e.g., Cursor, Claude Desktop) can connect via the JSON-RPC endpoint.

**Can I download icons in multiple formats?**

> Yes, PNG and SVG are both supported, with options for customization.

**Do I need authentication?**

> Yes, see the Authentication section in the docs for API key usage.

<br />
