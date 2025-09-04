---
title: MCP Server
excerpt: Streamline MCP server exposing tools and resources via HTTP JSON-RPC.
deprecated: false
hidden: true
metadata:
  robots: index
---
## Overview

[Model Context Protocol (MCP)](https://modelcontextprotocol.io/docs/getting-started/intro) is an open protocol that standardizes how applications provide context to large language models (LLMs). With MCP, AI apps (like Cursor or Claude Desktop) can connect to external applications, use their tools, and retrieve data seamlessly.

The Streamline MCP Server provides tools to access icons, illustrations, emojis, and other design assets. It allows MCP-compatible clients to search, retrieve, and download assets in PNG or SVG formats.

## How to Connect

Before connecting, make sure you have your API key ready for authentication. See the [Authentication](https://streamline-api.readme.io/reference/authentication-1#/) section for details.

Add the following configuration to your MCP-compatible client (e.g., Cursor or Claude Desktop) to connect to Streamline MCP Server:

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

## How to Use

Once connected, you can access tools like `search` `family_search`, `get_icon_by_hash`, `download_png`, and `download_svg` [`download_svg`](#download_svg) directly through the client AI Chat.

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
  Search for icons, illustrations, emojis, or elements from all families.

  <div>
    <strong>productType<span style={{color: 'red'}}>\*</span></strong>\
    Description: Product type for the search.\
    Type: icons | illustrations | emojis | elements
  </div>

  <div>
    <strong>query<span style={{color: 'red'}}>\*</span></strong>\
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
  Search for icons, illustrations, emojis, or elements from a specific family.

  <div>
    <strong>familySlug<span style={{color: 'red'}}>\*</span></strong>\
    Description: Family slug obtained from a global search or family group.\
    Type: string
  </div>

  <div>
    <strong>query<span style={{color: 'red'}}>\*</span></strong>\
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
  Retrieves detailed information about a specific icon.

  <div>
    <strong>iconHash<span style={{color: 'red'}}>\*</span></strong>\
    Description: Icon hash obtained from a global search response.\
    Type: string
  </div>
</Accordion>

<Accordion title="download_png" icon="fa-file-image">
  Apply modifications (size, colors, background, stroke) and download the icon as PNG.

  <div>
    <strong>iconHash<span style={{color: 'red'}}>\*</span></strong>\
    Description: Icon hash obtained from a global search response.\
    Type: string
  </div>

  <div>
    <strong>size<span style={{color: 'red'}}>\*</span></strong>\
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
  Apply modifications (size, colors, background, stroke, responsive, stroke-to-fill) and download the icon as SVG.

  <div>
    <strong>iconHash<span style={{color: 'red'}}>\*</span></strong>\
    Description: Icon hash obtained from a global search response.\
    Type: string
  </div>

  <div>
    <strong>size<span style={{color: 'red'}}>\*</span></strong>\
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
