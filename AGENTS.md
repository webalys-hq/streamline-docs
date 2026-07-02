# AGENTS.md

Guidance for AI agents (and humans) working in this repository.

## What this repo is

This is the **Streamline documentation**, authored for and synced with **[ReadMe](https://readme.com) (readme.com)** — a hosted developer-docs platform. The published site is <https://docs.streamlinehq.com>.

Because pages are rendered by ReadMe's Markdown engine (**not** GitHub, not a static-site generator), they use **ReadMe-specific (RDMD) syntax and custom components**. Plain CommonMark assumptions do not always hold. When editing, preserve the existing patterns rather than "normalizing" them to standard Markdown.

## Repository layout

```
docs/        # "Guides" — free-form narrative documentation
reference/   # "API Reference" — endpoint & MCP docs, grouped into categories
```

- Each folder can contain an **`_order.yaml`** listing its child pages/categories **by slug**, in display order. When you add, remove, or rename a page, update the relevant `_order.yaml` or it may not appear (or appear in the wrong place) in the sidebar.
- A page's slug is its filename without `.md` (e.g. `mcp-server.md` → `mcp-server`), and that slug is also its URL path under the section (e.g. `https://docs.streamlinehq.com/reference/mcp-server`).

## Page frontmatter

Every page starts with YAML frontmatter. Common keys used here:

```yaml
---
title: MCP Server
excerpt: Short summary shown in listings and meta description.
deprecated: false
hidden: false          # true = unpublished/draft, hidden from the live site
metadata:
  robots: index        # index | noindex for search engines
---
```

Keep `hidden`/`deprecated` intact — flipping them changes what is publicly visible.

## ReadMe-specific syntax to preserve

- **Custom React-style components** (uppercase tags). These are ReadMe features, not raw HTML — do not "fix" or remove them:
  - `<Anchor target="_blank" href="...">link text</Anchor>` — used for links (often external). The repo prefers this over `[text](url)` in many places; match the surrounding style.
  - `<Accordion title="search_assets" icon="fa-magnifying-glass"> ... </Accordion>` — collapsible sections. `icon` is a **Font Awesome** class (e.g. `fa-list`, `fa-file-arrow-down`). Content inside is regular Markdown.
- **Code block "tab" labels**: the text after the language is a named tab, not a filename. Examples in this repo:
  - ` ```json Cursor ` and ` ```json Zed ` — two labeled config variants shown as tabs.
  - ` ```node node `, ` ```shell shell `, ` ```json 200 OK ` — label doubles as the tab title. Keep these labels.
- **Callouts** use blockquotes, sometimes with a leading emoji, e.g. `> ❗️ Do not share your API key...`. ReadMe renders these as styled callout boxes.
- **Raw HTML is allowed and used**: `<br />`, `<div>`, `<strong>`, `<span>`, `<em>`, and inline tables. The `<div>`-based parameter lists inside `<Accordion>`s are intentional formatting — preserve their structure.
- **Escaped characters**: you'll see `\*`, `\_`, `\[`, and `\` at end-of-line (a hard line break). These escapes are deliberate (e.g. `YOUR\_API\_KEY\_HERE` prevents italics). Don't strip them.
- **Horizontal rules** `***` are used as visual dividers between steps.
- **In-page anchor links** like `[search_assets](#search_assets)` jump to a heading/accordion on the same page.
- **Images** are hosted on ReadMe's CDN (`https://files.readme.io/...`). Add new images through ReadMe (or keep existing URLs); don't expect local image files.

## Editing conventions

- **Heading levels matter for the on-page TOC.** `##` (H2) entries become top-level TOC items; `###` (H3) nest under the preceding H2. Use H3 to group related subsections (e.g. individual client setup guides under one "Connecting a Client" H2) rather than a flat list of H2s.
- Match the **existing link style** on the page (`<Anchor>` vs Markdown links) instead of mixing.
- Keep changes **content-focused**; avoid mass whitespace/reflow edits that bloat diffs and obscure the real change.
- This repo is **synced with ReadMe** (see the `Update reference` commit history). Content is authored in ReadMe's UI and mirrored here, so keep formatting compatible with ReadMe's editor round-tripping.

## Reference

- ReadMe-Flavored Markdown (RDMD) — getting started: <https://docs.readme.com/rdmd/docs/getting-started>
- RDMD flavored syntax (code tabs, callouts, embeds, components): <https://docs.readme.com/rdmd/docs/syntax-extensions>
