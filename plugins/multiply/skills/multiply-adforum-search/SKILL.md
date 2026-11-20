---
name: multiply-adforum-search
description: Searches AdForum's archive of advertising campaigns and award records (Cannes Lions, D&AD, The One Show, Effies and more) through Multiply, and returns verified campaigns with brand, title, year, agency, country, media and awards. Use when the user asks for campaigns or award winners by brand, agency, category, market, year or award show, "what has X done", "who won Gold in Y", "find reference campaigns for Z", an agency's or brand's creative track record, or wants AdForum data specifically. Needs the Multiply MCP. For a full category map or "has this idea been done?", use multiply-creative-precedents, which calls this search as one step.
---

# AdForum search

Answer a campaign or awards question from a licensed archive, not from memory or a web guess.

## 1. Frame the query

Turn the request into one narrow, self-contained search. Pin down, inferring where you can:

- **Who:** brands, agencies, or a category (for example "plant-based dairy").
- **Where and when:** markets and a year range. Default to the last 5 years if unsaid.
- **Recognition:** shows and levels if they matter (for example "Gold and above at Cannes").
- **What comes back:** brand, title, year, agency, country, media, awards with level, and a
  one-line description of the idea. Add images only if asked.

One run returns about 250 records at most. If the request is broad ("all FMCG awards since
2015"), split it into a few runs by category, market or period and say so.

## 2. Check access (reads)

1. `create-session`. Keep `org1` and `acc1`.
2. Choose where the report lands (`here`):
   - The client's Project or Workspace if the search is for a known client (`list-workspaces`
     with `title-contains`, then `list-projects`).
   - Otherwise a private task: `create-task` with `parent: "acc1"` and a title such as
     `AdForum · <topic> · <YYYY-MM-DD>`. It is only visible to the user.
3. `list-endpoints` with that `here`. If `AdForum` isn't listed, say so in one line, offer a
   web search with an honest coverage caveat instead, and stop.

## 3. Run (ask first: it uses Multiply credits and takes a few minutes)

Tell the user the query and where the report will be saved, then call `run-endpoint`:

- `endpoint: "AdForum"`, `here`, and a `task` that stands alone: the driver sees nothing
  of this conversation.
- `focus` for what matters most (for example "award level and the core mechanic").
- `context` for a short client or brief summary when it helps rank results.
- `wait: 300`. If an `op1` comes back, `await` it.

Then `read-source` (`account: "acc1"`) on the report handle.

## 4. Hand back

- Lead with the answer to the question in two or three lines.
- Then a table: Brand · Campaign · Year · Agency · Market · Media · Awards.
- Group by approach or award level when there are more than ~10.
- Credit AdForum as the source, and AdForum's own trend write-ups to AdForum.
- **Never add campaigns from memory to the table.** If you know of something AdForum didn't
  return, list it separately as "not in this AdForum result, verify".
- Say where the full report is saved in Multiply.

Offer one follow-up: a narrower run, a related category, or multiply-creative-precedents for the full
category map.

See `reference/multiply-mcp.md` for every tool's arguments.
