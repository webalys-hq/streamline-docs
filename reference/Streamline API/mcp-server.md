---
title: MCP Server
excerpt: Streamline MCP server exposing tools and resources via HTTP JSON-RPC.
deprecated: false
hidden: true
metadata:
  robots: index
---
## Overview

Streamline MCP Server is a Model Context Protocol server that provides access to icons, illustrations, emojis, and other design assets. It allows MCP-compatible clients to search, retrieve, and download assets in PNG or SVG formats.

## How to Connect

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

Once connected, you can access tools like `global_search` `family_search`, `get_icon_by_hash`, `download_png`, and `download_svg` directly through the client AI Chat.

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

<Tabs>
  <Tab title="Search icons">
    Search for icons, illustrations, emojis or elements from all families.

    | Parameter     | Type                     | Description                                                | Default     |
    | ------------- | ------------------------ | ---------------------------------------------------------- | ----------- |
    | `productType` | enum (`ProductTypeEnum`) | Product type for the search.                               | —           |
    | `query`       | string                   | Search term to find icons.                                 | —           |
    | `offset`      | number                   | Number of items to skip before returning results.          | 0           |
    | `limit`       | number                   | Maximum number of items to return.                         | 10 (max 50) |
    | `productTier` | enum (`PriceFilterEnum`) | Filter by price tier. E.g., `free` returns only free sets. | `ALL`       |
    | `style`       | enum (`StyleFilterEnum`) | Filter for the style of the sets.                          | —           |
  </Tab>

  <Tab title="Family search">
    Search for icons, illustrations, emojis or elements from a specific family.
  </Tab>

  <Tab title="Get icon by hash">
    Retrieves detailed information about the requested icon.
  </Tab>

  <Tab title="Download icon as PNG">
    Apply the required modifications to the asset such as size as color and returns the PNG.
  </Tab>

  <Tab title="Download icon as SVG">
    Apply the required modifications to the asset such as size as color and returns the SVG.
  </Tab>
</Tabs>

## FAQ

**Which clients can use Streamline MCP Server?**

> Any MCP-compatible client (e.g., Cursor, Claude Desktop) can connect via the JSON-RPC endpoint.

**Can I download icons in multiple formats?**

> Yes, PNG and SVG are both supported, with options for customization.

**Do I need authentication?**

> Yes, see the Authentication section in the docs for API key usage.

<br />
