---
title: MCP Server
excerpt: Streamline MCP server exposing tools and resources via HTTP JSON-RPC.
deprecated: false
hidden: false
metadata:
  robots: index
---
## Overview

<Anchor target="_blank" label="Model Context Protocol (MCP)" href="https://modelcontextprotocol.io/docs/getting-started/intro">Model Context Protocol (MCP)</Anchor> is an open protocol that standardizes how applications provide context to large language models (LLMs). With MCP, AI apps (like Cursor or Claude Desktop) can connect to external applications, use their tools, and retrieve data seamlessly.

The Streamline MCP Server provides tools to access icons, illustrations, emojis, and other design assets. It allows MCP-compatible clients to search, retrieve, and download assets in PNG or SVG formats.

## Authentication

The Streamline MCP endpoint supports two ways to authenticate. Use either one on each request to [https://public-api.streamlinehq.com/mcp](https://public-api.streamlinehq.com/mcp) (not both at once).

## Authentication with API Key

Before connecting, make sure you have your API key ready for authentication. See the <Anchor target="_blank" label="Authentication" href="https://streamline-api.readme.io/reference/authentication-1#/">Authentication</Anchor> section for details.

Send your Streamline API key in the X-API-Key header on every MCP request. This matches the setup examples above (Cursor, Claude Code, Codex).

**When to use:** quick setup, scripts, and clients that only support static headers.

## Authentication with OAuth 2.1 (Authorization Code + PKCE)

Send a Streamline-issued access token in the Authorization header:

```
Authorization: Bearer <access_token>
```

The server validates Bearer tokens issued by this API’s OAuth endpoints. There is no X-API-Key header in this mode.

**When to use:** MCP clients or apps that implement OAuth (browser login, refresh tokens, dynamic client registration), as required by some hosted or enterprise setups.

Discovery (machine-readable):

| What                     | URL                                                                                |
| ------------------------ | ---------------------------------------------------------------------------------- |
| Protected resource (MCP) | `GET https://public-api.streamlinehq.com/mcp/.well-known/oauth-protected-resource` |
| Authorization server     | `GET https://public-api.streamlinehq.com/.well-known/oauth-authorization-server`   |

From there, clients learn the authorization server base URL, registration endpoint, authorize and token URLs, and supported scope (e.g. mcp:tools).

Typical flow (summary):

1. Register an OAuth client (e.g. `POST /oauth/register` with redirect URIs), if your client uses dynamic client registration.
2. Send the user through `GET /oauth/authorize` with PKCE (code_challenge / code_challenge_method=S256) and the registered client_id / redirect_uri.
3. After the user signs in and consents, exchange the authorization code at `POST /oauth/token` for access_token (and usually refresh_token).
4. Call the MCP JSON-RPC endpoint with `Authorization: Bearer <access_token>`.

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

  Search for icons, illustrations, emojis, or elements from all families.

  <div>
    <strong>productType<span>\*</span></strong>\
    Description: Product type for the search.\
    Type: icons | illustrations | emojis | elements
  </div>

  <div>
    <strong>query<span>\*</span></strong>\
    Description: Search term to find icons.\
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
    Description: Filter by price tier (free, premium, all).\
    Type: all | free | premium\
    Default value: all
  </div>

  <div>
    <strong>style</strong>\
    Description: Filter for the style of the sets.\
    Type: line | solid | flat | duo | handrawn | creative | gradient | remix | neon | pop | light | glyph | minimal | outlined | geometric | bold | stroke | wireframe | filled
  </div>
</Accordion>

<Accordion title="family_search" icon="fa-magnifying-glass">
  ### family\_search

  Search for icons, illustrations, emojis, or elements from a specific family.

  <div>
    <strong>familySlug<span>\*</span></strong>\
    Description: Family slug obtained from a global search or family group.\
    Type: string
  </div>

  <div>
    <strong>query<span>\*</span></strong>\
    Description: Search term to find icons.\
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

<Accordion title="get_icon_by_hash" icon="fa-info-circle">
  ### get\_icon\_by\_hash

  Retrieves detailed information about a specific icon.

  <div>
    <strong>iconHash<span>\*</span></strong>\
    Description: Icon hash obtained from a global search response.\
    Type: string
  </div>
</Accordion>

<Accordion title="download_png" icon="fa-file-image">
  ### download\_png

  Apply modifications (size, colors, background, stroke) and download the icon as PNG.

  <div>
    <strong>iconHash<span>\*</span></strong>\
    Description: Icon hash obtained from a global search response.\
    Type: string
  </div>

  <div>
    <strong>size<span>\*</span></strong>\
    Description: Image size in pixels (square).\
    Type: number
  </div>

  <div>
    <strong>colors</strong>\
    Description: List of HEX or named colors for export.\
    Type: array of strings
  </div>

  <div>
    <strong>backgroundColor</strong>\
    Description: Background color in HEX or named color.\
    Type: string\
    Default value: #ffffff00
  </div>

  <div>
    <strong>strokeWidth</strong>\
    Description: Adjusts vector path thickness.\
    Type: number
  </div>
</Accordion>

<Accordion title="download_svg" icon="fa-file-code">
  ### download\_svg

  Apply modifications (size, colors, background, stroke, responsive, stroke-to-fill) and download the icon as SVG.

  <div>
    <strong>iconHash<span>\*</span></strong>\
    Description: Icon hash obtained from a global search response.\
    Type: string
  </div>

  <div>
    <strong>size<span>\*</span></strong>\
    Description: Image size in pixels (square).\
    Type: number
  </div>

  <div>
    <strong>colors</strong>\
    Description: List of HEX or named colors for export.\
    Type: array of strings
  </div>

  <div>
    <strong>backgroundColor</strong>\
    Description: Background color in HEX or named color.\
    Type: string\
    Default value: #ffffff00
  </div>

  <div>
    <strong>responsive</strong>\
    Description: Scales SVG with container; removes width/height.\
    Type: boolean\
    Default value: false
  </div>

  <div>
    <strong>strokeWidth</strong>\
    Description: Adjusts vector path thickness.\
    Type: number
  </div>

  <div>
    <strong>strokeToFill</strong>\
    Description: Converts strokes to fills; strokeWidth ignored if true.\
    Type: boolean\
    Default value: false
  </div>

  <div>
    <strong>base64</strong>\
    Description: Return SVG as base64 string instead of raw data.\
    Type: boolean
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
