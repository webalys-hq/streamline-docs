---
title: MCP Server
excerpt: Streamline MCP server exposing tools and resources via HTTP JSON-RPC.
deprecated: false
hidden: false
metadata:
  robots: index
---
## Overview

<Anchor target="_blank" label="Model Context Protocol (MCP)" href="https://modelcontextprotocol.io/docs/getting-started/intro">Model Context Protocol (MCP)</Anchor> is an open protocol that standardizes how applications provide context to large language models (LLMs). With MCP, AI apps (like Cursor or Claude) can connect to external applications, use their tools, and retrieve data seamlessly.

The Streamline MCP Server provides tools for accessing icons, illustrations, emojis, and other design assets within the Streamline application. It allows MCP-compatible clients to search, retrieve, and download assets in PNG or SVG formats.

## Authentication

The Streamline MCP endpoint supports two ways to authenticate. Use either one on each request to [https://public-api.streamlinehq.com/mcp](https://public-api.streamlinehq.com/mcp) (not both at once).

## Authentication with API Key

Before connecting, make sure you have your Streamline API key ready. Send it in the X-API-Key header with every MCP request. For setup details, see the Authentication section.

## Authentication with OAuth 2.1 (Authorization Code + PKCE)

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

## How to Connect on Cursor

Go to Cursor > Cursor Settings > Tools & MCPs and then click on "New MCP Server" and add the streamlineMCPServer configuration that you can see below:

Add the following configuration to your MCP-compatible client (e.g.,  <Anchor target="_blank" label="Cursor" href="https://cursor.com/docs/context/mcp">Cursor</Anchor>) to connect to Streamline MCP Server:

```json
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

You can see more details about adding MCPs to Cursor here: <Anchor label="https://cursor.com/docs/mcp" title="https://cursor.com/docs/mcp" href="https://cursor.com/docs/mcp">https://cursor.com/docs/mcp</Anchor>

## How to Connect on Claude Code

Run this command replacing the YOUR_API_KEY_HERE part with your Streamline Api Key.

```text
claude mcp add --transport http streamline-mcp https://public-api.streamlinehq.com/mcp --header "X-Api-Key: YOUR_API_KEY_HERE"
```

Run `claude mcp list` to confirm it's up and running.

## How to Connect on Codex

Go to Settings > Settings > MCP Servers and click on "Add Server". Fill the form with the following information: <br />**Name:** Streamline MCP Server<br />Select the **Streamable HTTP** option<br />**URL:** <Anchor label="https://public-api.streamlinehq.com/mcp" title="https://public-api.streamlinehq.com/mcp" href="https://public-api.streamlinehq.com/mcp">https://public-api.streamlinehq.com/mcp</Anchor><br />**Headers Key:** X-API-Key <br />**Headers Value: **YOUR_API_KEY_HERE (Replace with your actual key)<br />Then Click on **Save**

![](https://files.readme.io/5d94c07b2ed859c6acd20b7e01796f72e803b77357a2d140bddf2ad545744a85-image.png)

<br />

## How to Connect to Claude using Connectors

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
4. Review and grant the requested access
   Once authorized, you will be redirected back to Claude automatically.

***

**Step 3 — Verify the Connection**

After being redirected back to Claude, confirm the connector is active:

* Go to **Settings → Connectors**
* The Streamline MCP Server should appear with a **Connected** status

***

**Step 4 — Test It**

1. Start a new chat in Claude
2. Ask Claude to verify the connector is working, for example:
   > _"Check if you are connected to the Streamline MCP Server"_
   > Claude will confirm the connection and list the available tools.

***

**What You Can Do**

Once connected, you can ask Claude to:

* Search for icons, illustrations, or design elements from the Streamline library

* Filter assets by style, type, or pricing tier (free or premium)

* Download assets as PNG with custom size, colors, and stroke width
  **Example prompts:**

* _"Find me a line-style icon for notifications"_

* _"Search for free illustrations related to teamwork"_

* _"Download the settings icon as a 64px PNG"_

<br />

## How to Use

Once connected, you can access tools like [`search`](#search) , [`family_search`](#family_search),  [`get_icon_by_hash`](#get_icon_by_hash), [`download_png`](#download_png), and [`download_svg`](#download_svg) directly through the client AI Chat.

**Example:** You can experiment by asking the AI chat in your client to **search for dog icons**. The client will handle calling the appropriate MCP tool and returning the results.

## Key Features

* Search icons, illustrations, emojis, and elements.
* Retrieve detailed information about specific icons.
* Download assets in PNG or SVG format with customization options (size, colors, background, stroke).
* Fully compatible with MCP protocol clients.

## Use Cases

* Finding icons for web or mobile projects.
* Retrieving and customizing specific assets for design workflows.
* Automating icon-related tasks in applications or scripts.

## Tools

<Accordion title="search" icon="fa-magnifying-glass">
  ### search

  Search for icons, illustrations, or elements across all families. Use when the user asks for a specific asset with no Family/Set preference.

  <div>
    <strong>productType<span>\*</span></strong>\
    Description: Asset type to search.\
    Type: icons | illustrations | elements
  </div>

  <div>
    <strong>query<span>\*</span></strong>\
    Description: Search term.\
    Type: string
  </div>

  <div>
    <strong>offset</strong>\
    Description: Number of items to skip before returning results.\
    Type: number\
    Default value: 0
  </div>

  <div>
    <strong>limit</strong>\
    Description: Maximum number of items to return.\
    Type: number\
    Default value: 10 (max 50)
  </div>

  <div>
    <strong>productTier</strong>\
    Description: Filter by price tier of sets.\
    Type: all | free | premium\
    Default value: all
  </div>

  <div>
    <strong>style</strong>\
    Description: Filter by icon set style. Only applies when `productType` is `icons`.\
    Type: line | solid | flat | duo | handrawn | creative | gradient | remix | neon | pop | light | glyph | minimal | outlined | geometric | bold | stroke | wireframe | filled
  </div>
</Accordion>

<Accordion title="family_group_search" icon="fa-magnifying-glass">
  ### family\_group\_search

  Search for icons, illustrations, or elements within a **Family** (family group) identified by `familyGroupSlug`. Use when you already have a resolved slug from `get_all_family_groups` or `search_family_groups`.

  <div>
    <strong>familyGroupSlug<span>\*</span></strong>\
    Description: Family group slug.\
    Type: string
  </div>

  <div>
    <strong>query<span>\*</span></strong>\
    Description: Search term.\
    Type: string
  </div>

  <div>
    <strong>offset</strong>\
    Description: Number of items to skip before returning results.\
    Type: number\
    Default value: 0
  </div>

  <div>
    <strong>limit</strong>\
    Description: Maximum number of items to return.\
    Type: number\
    Default value: 10 (max 50)
  </div>
</Accordion>

<Accordion title="family_search" icon="fa-magnifying-glass">
  ### family\_search

  Search for icons, illustrations, or elements within a **Set** (family) identified by `familySlug`. Use when you already have a resolved slug from `search_families`, `find_families_by_name`, or `get_all_families_from_family_group`.

  <div>
    <strong>familySlug<span>\*</span></strong>\
    Description: Family (Set) slug.\
    Type: string
  </div>

  <div>
    <strong>query<span>\*</span></strong>\
    Description: Search term.\
    Type: string
  </div>

  <div>
    <strong>offset</strong>\
    Description: Number of items to skip before returning results.\
    Type: number\
    Default value: 0
  </div>

  <div>
    <strong>limit</strong>\
    Description: Maximum number of items to return.\
    Type: number\
    Default value: 10 (max 50)
  </div>
</Accordion>

<Accordion title="search_family_groups" icon="fa-layer-group">
  ### search\_family\_groups

  Semantic (natural-language) search for **family groups** (broad discovery). Use for style- or concept-oriented requests. For listing everything, use `get_all_family_groups`.

  <div>
    <strong>query<span>\*</span></strong>\
    Description: Natural-language search term.\
    Type: string (min 1 character)
  </div>

  <div>
    <strong>offset</strong>\
    Description: Number of items to skip before returning results.\
    Type: number\
    Default value: 0
  </div>

  <div>
    <strong>limit</strong>\
    Description: Maximum number of family groups to return.\
    Type: number\
    Default value: 5 (max 100)
  </div>
</Accordion>

<Accordion title="search_families" icon="fa-shapes">
  ### search\_families

  Semantic search for **families (Sets)** by meaning (not substring on stored names). For partial name match on stored names, use `find_families_by_name` instead. To list all sets in a group without search intent, use `get_all_families_from_family_group`.

  <div>
    <strong>query<span>\*</span></strong>\
    Description: Natural-language search term.\
    Type: string (min 1 character)
  </div>

  <div>
    <strong>familyGroupSlug</strong>\
    Description: When set, only return families in this family group.\
    Type: string\
    Default: (unset)
  </div>

  <div>
    <strong>offset</strong>\
    Description: Number of items to skip before returning results.\
    Type: number\
    Default value: 0
  </div>

  <div>
    <strong>limit</strong>\
    Description: Maximum number of families to return.\
    Type: number\
    Default value: 20 (max 100)
  </div>
</Accordion>

<Accordion title="find_families_by_name" icon="fa-font">
  ### find\_families\_by\_name

  Case-insensitive **substring** match on stored Set (family) names. Minimum 3 characters. For semantic discovery, use `search_families`.

  <div>
    <strong>name<span>\*</span></strong>\
    Description: Substring to match against family names.\
    Type: string (min 3 characters)
  </div>
</Accordion>

<Accordion title="get_all_family_groups" icon="fa-list">
  ### get\_all\_family\_groups

  Returns all family groups (hash, slug, and related fields) for browsing the full catalog.

  <div>
    <em>No parameters.</em>
  </div>
</Accordion>

<Accordion title="get_all_families_from_family_group" icon="fa-list-ul">
  ### get\_all\_families\_from\_family\_group

  Returns all families (Sets) in a family group, with pagination. Use when you already know the group and want a full list (no search).

  <div>
    <strong>familyGroupHash<span>\*</span></strong>\
    Description: Family group hash. Obtain from `get_all_family_groups` or `search_family_groups` results.\
    Type: string (max 80 characters)
  </div>

  <div>
    <strong>offset</strong>\
    Description: Number of items to skip.\
    Type: number\
    Default value: 0
  </div>

  <div>
    <strong>limit</strong>\
    Description: Maximum number of families to return.\
    Type: number\
    Default value: 100 (max 100)
  </div>
</Accordion>

<Accordion title="get_icon_by_hash" icon="fa-info-circle">
  ### get\_icon\_by\_hash

  Full icon metadata (family, variants, preview URLs, tags, etc.) before download.

  <div>
    <strong>iconHash<span>\*</span></strong>\
    Description: Icon ID (hash) from `search`, `family_search`, or `family_group_search` results.\
    Type: string
  </div>
</Accordion>

<Accordion title="download_png" icon="fa-file-image">
  ### download\_png

  Returns **JSON** with a short-lived signed `downloadUrl`, `expiresAt`, `expiresInSeconds`, `mimeType` (`image/png`), and `fileName`. The MCP `tools/call` is authenticated; perform a plain **GET** on `downloadUrl` without `X-API-Key` or Bearer (the URL carries the signed token) to download bytes.

  <div>
    <strong>iconHash<span>\*</span></strong>\
    Description: Icon ID (hash) from search results.\
    Type: string
  </div>

  <div>
    <strong>size<span>\*</span></strong>\
    Description: Square size in pixels (1–4096).\
    Type: number
  </div>

  <div>
    <strong>colors</strong>\
    Description: Array of HEX strings or CSS named colors.\
    Type: array of strings\
    Default value: \[]
  </div>

  <div>
    <strong>backgroundColor</strong>\
    Description: Background color (HEX or CSS name).\
    Type: string\
    Default value: #ffffff00 (transparent)
  </div>

  <div>
    <strong>strokeWidth</strong>\
    Description: Adjust vector path thickness.\
    Type: number
  </div>
</Accordion>

<Accordion title="download_svg" icon="fa-file-code">
  ### download\_svg

  Returns **JSON** with a short-lived signed `downloadUrl`, `expiresAt`, `expiresInSeconds`, `mimeType` (`image/svg+xml`), and `fileName`. The MCP `tools/call` is authenticated; perform a plain **GET** on `downloadUrl` without `X-API-Key` or Bearer to download bytes.

  <div>
    <strong>iconHash<span>\*</span></strong>\
    Description: Icon ID (hash) from search results.\
    Type: string
  </div>

  <div>
    <strong>size<span>\*</span></strong>\
    Description: Square size in pixels (1–4096).\
    Type: number
  </div>

  <div>
    <strong>colors</strong>\
    Description: Array of HEX strings or CSS named colors.\
    Type: array of strings\
    Default value: \[]
  </div>

  <div>
    <strong>backgroundColor</strong>\
    Description: Background color (HEX or CSS name).\
    Type: string\
    Default value: #ffffff00 (transparent)
  </div>

  <div>
    <strong>responsive</strong>\
    Description: If true, SVG uses viewBox and drops fixed width/height for responsive scaling.\
    Type: boolean\
    Default value: false
  </div>

  <div>
    <strong>strokeWidth</strong>\
    Description: Adjust vector path thickness.\
    Type: number
  </div>

  <div>
    <strong>strokeToFill</strong>\
    Description: If true, strokes become fills; `strokeWidth` is not applied.\
    Type: boolean\
    Default value: false
  </div>
</Accordion>

## FAQ

**Which clients can use Streamline MCP Server?**

> Any MCP-compatible client (e.g., Cursor, Claude Desktop) can connect via the JSON-RPC endpoint.

**Can I download icons in multiple formats?**

> Yes, PNG and SVG are both supported, with options for customization.

**Do I need authentication?**

> Yes, see the Authentication section in the docs for API key usage.

<br />
