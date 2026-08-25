---
title: Tools
excerpt: The tools exposed by the Streamline MCP Server and their parameters.
deprecated: false
hidden: false
metadata:
  robots: index
---

Once connected, these tools are available through your client's AI chat. For guidance on choosing the right tool and writing effective queries, see the <Anchor href="https://docs.streamlinehq.com/reference/how-to-search">Search guide</Anchor>.

<Accordion title="get_user_context" icon="fa-user">

Returns the profile of the authenticated session. Call this **before** `search_assets` — that tool requires the `userContext` string this one returns.

_No parameters._

Returns two strings:

| Field             | Description                                                                                                                         |
| ----------------- | ----------------------------------------------------------------------------------------------------------------------------------- |
| `userContext`     | One-line summary of the signed-in account, e.g. `you@example.com is on the free plan`. Pass it straight through to `search_assets`. |
| `llmInstructions` | Presentation guidance for the assistant — how to lay out catalog results, and how to handle premium assets for this account.        |

</Accordion>

<Accordion title="search_assets" icon="fa-magnifying-glass">

Search for icons, illustrations, or elements.

How wide the search goes depends on which slug you pass. The first rule that matches wins:

- **One Set** — pass `setSlug`. Narrowest scope, and it overrides `familySlug` if you pass both.
- **One Family** — pass `familySlug` and leave `setSlug` out.
- **The whole catalog** — leave both out. `productType` is then required, so the search knows whether to look at icons, illustrations, or elements.

An empty or blank slug counts as "not passed".

| Parameter                  | Type                                   | Description                                                                                                                                                                                                                                                                          |
| -------------------------- | -------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| `query` _(required)_       | string                                 | Search term, 1–100 characters. Translate abstract concepts into concrete visual nouns when searching globally. Never mix different concepts in the same query.                                                                                                                       |
| `language`                 | enum                                   | Source language of `query`. When set, the query is machine-translated to English before searching. One of: `en`, `fr`, `de`, `es` (Spain), `es-MX` (Latin America), `pt` (Brazil), `pt-PT`, `hi`, `ko`, `ja`. Omit for English. Default: unset.                                      |
| `setSlug`                  | string                                 | Set slug from `search_sets`, `find_sets_by_name`, or `get_all_sets_from_family`. When provided, search is scoped to this Set (takes precedence over `familySlug`).                                                                                                                   |
| `familySlug`               | string                                 | Family slug from `get_all_families`. When provided and `setSlug` is omitted, search is scoped to this Family.                                                                                                                                                                        |
| `productType`              | `icons` / `illustrations` / `elements` | Required for global search only (when both `setSlug` and `familySlug` are omitted). Asset type to search.                                                                                                                                                                            |
| `offset`                   | number                                 | Number of items to skip before returning results. Default: `0`.                                                                                                                                                                                                                      |
| `limit`                    | number                                 | Maximum number of items to return. Default: `20` (max `100`).                                                                                                                                                                                                                        |
| `productTier`              | `all` / `free` / `premium`             | Filter by price tier of Sets (e.g. `free` limits results to free Sets). Used for global search only. Default: `all`. On ChatGPT this is forced to `free` for accounts without a premium entitlement (see note below).                                                                |
| `style`                    | enum                                   | Filter by Set style. Global search only; applies when `productType` is `icons`. One of: `line`, `solid`, `flat`, `duo`, `hand-drawn`, `creative`, `gradient`, `remix`, `neon`, `pop`, `light`, `glyph`, `minimal`, `outlined`, `geometric`, `bold`, `stroke`, `wireframe`, `filled`. |
| `userContext` _(required)_ | string                                 | The `userContext` string returned by `get_user_context`. Call that tool first — do not invent or guess this value.                                                                                                                                                                   |

</Accordion>

<Accordion title="search_sets" icon="fa-shapes">

Semantic search for **Sets** by meaning (not substring on stored names). For partial name match on stored Set names, use `find_sets_by_name`. To list all Sets in a Family without search intent, use `get_all_sets_from_family`.

| Parameter            | Type   | Description                                                                                                                                            |
| -------------------- | ------ | ------------------------------------------------------------------------------------------------------------------------------------------------------ |
| `query` _(required)_ | string | Natural-language search term, 1–100 characters. Preserve the full intent (questions, negatives); don't compress it into a keyword stack.               |
| `familySlug`         | string | When set, only return Sets belonging to this Family. Use the Family `slug` from `get_all_families`. Minimum 1 character when provided. Default: unset. |
| `limit`              | number | Maximum number of Sets to return. Default: `20` (min `1`, max `100`).                                                                                  |

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
| `limit`                   | number | Maximum number of Sets to return. Default: `100` (min `1`, max `100`).                                                      |

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
| `size` _(required)_     | number        | Square size in pixels. Between `1` and `4096`.                                                             |
| `colors`                | string[]      | Array of HEX strings or CSS named colors. Default: `[]`.                                                   |
| `backgroundColor`       | string        | Background color (HEX or CSS name). Default: `#ffffff00` (transparent).                                    |
| `strokeWidth`           | number        | Adjust vector path thickness. Optional.                                                                    |
| `responsive`            | boolean       | SVG only. If true, SVG uses viewBox and drops fixed width/height for responsive scaling. Default: `false`. |
| `strokeToFill`          | boolean       | SVG only. If true, strokes become fills; `strokeWidth` is not applied. Default: `false`.                   |

</Accordion>

<Accordion title="download_multiple_assets" icon="fa-download">

Batch version of `download_asset`: export **up to 50 icons** in a single call, all sharing the same `format`, `size`, and render options. Returns **JSON** with a `downloads` array — one entry per requested hash, each with its `iconHash`, a short-lived signed `downloadUrl`, `expiresAt`, `expiresInSeconds`, `mimeType`, and `fileName`. The MCP `tools/call` is authenticated; perform a plain **GET** on each `downloadUrl` without `X-API-Key` or Bearer (the URL carries the signed token) to download bytes. SVG-only params: `responsive`, `strokeToFill`.

| Parameter                 | Type          | Description                                                                                                |
| ------------------------- | ------------- | ---------------------------------------------------------------------------------------------------------- |
| `format` _(required)_     | `png` / `svg` | Export format. Applies to every hash in the batch.                                                         |
| `iconHashes` _(required)_ | string[]      | Icon IDs (hashes) from `search_assets` results, one per array element. Between `1` and `50` items.         |
| `size` _(required)_       | number        | Square size in pixels. Between `1` and `4096`. Applies to every hash in the batch.                         |
| `colors`                  | string[]      | Array of HEX strings or CSS named colors. Default: `[]`.                                                   |
| `backgroundColor`         | string        | Background color (HEX or CSS name). Default: `#ffffff00` (transparent).                                    |
| `strokeWidth`             | number        | Adjust vector path thickness. Optional.                                                                    |
| `responsive`              | boolean       | SVG only. If true, SVG uses viewBox and drops fixed width/height for responsive scaling. Default: `false`. |
| `strokeToFill`            | boolean       | SVG only. If true, strokes become fills; `strokeWidth` is not applied. Default: `false`.                   |

> 📘 Bulk downloads and rate limits
>
> Every hash in `iconHashes` is exported and metered **individually**: a request for 50 hashes counts as 50 downloads against your plan's download allowance (see <Anchor href="https://docs.streamlinehq.com/reference/mcp">Overview</Anchor> and <Anchor href="https://docs.streamlinehq.com/reference/rate-limit">Rate Limit</Anchor>), not as a single download.
>
> All signed URLs are returned up front, but your allowance is only spent when each `downloadUrl` is fetched. On a large pull that crosses your remaining allowance, the earlier fetches succeed while later ones return `429 Too Many Requests` with the date your limit resets.
>
> A separate per-hour request limit applies to the MCP tool calls themselves, so a single `download_multiple_assets` call is far more efficient for bulk exports than many `download_asset` calls.

</Accordion>
