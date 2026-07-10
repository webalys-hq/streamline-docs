---
title: Search guide
excerpt: Get better results from the Streamline MCP search tools.
deprecated: false
hidden: false
metadata:
  robots: index
---

Streamline exposes two complementary search tools. Picking the right one — and scoping it correctly — makes results dramatically better.

## Terminology

- **Family** — a top-level bundle (e.g. "Ultimate").
- **Set** — a style variant within a Family (e.g. "Ultimate Regular").

## Assets vs. Sets

- Use `search_assets` to find individual **icons, illustrations, or elements**.
- Use `search_sets` to find a **Set** (a style) by meaning, then search assets scoped to it.

## Scope your `search_assets` call

`search_assets` runs in one of three scopes, from broadest to narrowest:

| Scope       | When                                         | Notes                                                                              |
| ----------- | -------------------------------------------- | ---------------------------------------------------------------------------------- |
| Global      | Neither `setSlug` nor `familySlug` provided  | `productType` (`icons` / `illustrations` / `elements`) is **required** here.        |
| Family      | `familySlug` provided, `setSlug` omitted     | Searches within one Family.                                                         |
| Set         | `setSlug` provided                           | Narrowest — takes precedence over `familySlug`.                                     |

> 📘 Only pass a `setSlug` or `familySlug` you obtained from a tool result (`search_sets`, `find_sets_by_name`, `get_all_sets_from_family`, or `get_all_families`). Never invent slugs.

## Write better queries

- **Use concrete visual nouns.** Translate abstract concepts into things you can actually draw — search `shield` or `padlock`, not `security`.
- **One concept per query.** Don't mix unrelated ideas (e.g. `dog cloud settings`) in a single search; run separate queries.
- **Don't over-specify.** Pass the natural phrasing of what you want rather than a distilled keyword list.

## Filter global searches

When searching globally (`productType` set), you can narrow results:

- `productTier` — `all`, `free`, or `premium`.
- `style` — for `icons`, restrict to a Set style such as `line`, `solid`, `flat`, `duo`, `gradient`, and more.

## Finding a Set or Family first

- `search_sets` — semantic search for a Set by meaning.
- `find_sets_by_name` — case-insensitive **substring** match on stored Set names (minimum 3 characters).
- `get_all_families` — browse the full catalog of Families.
- `get_family_extra_details` — richer semantic context to choose between Families.

See the <Anchor href="https://docs.streamlinehq.com/reference/tools">Tools</Anchor> page for the full parameter list of each tool.
