---
title: MCP Server
excerpt: Streamline MCP server exposing tools and resources via HTTP JSON-RPC
deprecated: false
hidden: true
metadata:
  robots: index
---
## Overview

Streamline MCP Server is a Model Context Protocol server that provides access to icons, illustrations, emojis, and other design assets. It allows MCP-compatible clients to search, retrieve, and download assets in PNG or SVG formats.

## How to Connect

Use the HTTP JSON-RPC endpoint:

<br />

<br />

Connect via MCP-compatible clients like Cursor or Claude Desktop by sending JSON-RPC requests to this endpoint.

## How to Use

Call the available MCP tools such as `global_search`, family_search, get_icon_by_hash, download_png, and download_svg to search, retrieve, or download assets.

## Key Features

Search icons, illustrations, emojis, and other assets globally or by family.

Retrieve detailed information about specific icons.

Download assets in PNG or SVG format with customization options (size, colors, background, stroke).

Fully compatible with MCP protocol clients.

## Use Cases

Finding icons for web or mobile projects.

Retrieving and customizing specific assets for design workflows.

Automating icon-related tasks in applications or scripts.

## FAQ

Which clients can use Streamline MCP Server?
Any MCP-compatible client (e.g., Cursor, Claude Desktop) can connect via the JSON-RPC endpoint.

Can I download icons in multiple formats?
Yes, PNG and SVG are both supported, with options for customization.

Do I need authentication?
Yes, see the Authentication section in the docs for API key usage.

<br />
