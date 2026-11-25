---
name: multiply-creative-precedents
description: Maps how a category has advertised, covering its dominant codes and clichés, standout and award-winning campaigns (Cannes Lions, D&AD, One Show, Effies), and white space, before ideation. Use when the user asks for reference campaigns, precedents, "what has been done in X", category codes or clichés, award winners, an agency's or brand's creative track record, or inspiration before ideation. To test a specific idea or creative direction ("has this been done?", "is this original?"), use multiply-idea-test instead. Standalone it uses web search with honest caveats. When the Multiply MCP is connected and AdForum is enabled for the organisation, it searches AdForum's campaign and awards archive and saves the map to the client's Project.
---

# Creative precedents

Know the category's creative history before you add to it.

To test a specific idea or creative direction against existing work, use **multiply-idea-test**.

## Non-negotiables

- **Never invent a campaign, agency, award or year.** If you can't verify something, leave it out or
  label it "unverified". A short honest list beats a long made-up one.
- Every campaign entry has the brand, campaign title, year, agency (if known), market, what it did,
  its recognition (exact award and level, for example "Gold Lion, Outdoor, 2024"), and a source.
- Be clear about coverage. Web search finds famous and recent work well. It misses older,
  non-English and less publicised work, and its award data is patchy. Say so in the output.

## Category map

1. **Frame:** category, markets, time window (default: the last 5–10 years), the
   purpose (pre-ideation, pitch, competitor audit) and any client brief. Read the client
   profile (`clients/<client-slug>.md`) or Multiply Workspace if available.
2. **Search:** award-show winner archives, Effie case studies, trade press (Ad Age, Campaign,
   The Drum, Adweek, LBBOnline, Contagious), agency case pages, brand channels, and ad libraries
   (Meta Ad Library, Google Ads Transparency) for what is running now. Run many narrow
   searches, open each page before citing it, and prefer primary sources.
3. **Analyse:**
   - **Category codes:** the visual, verbal and narrative conventions most brands follow.
   - **Clichés to avoid:** codes so overused that they make work invisible.
   - **Standout work:** 6–12 campaigns that broke the codes, grouped by approach, each with
     why it worked.
   - **Adjacent inspiration:** brands outside the category that solved the same audience
     problem.
   - **White space:** what nobody in the category is doing or saying.
   - **Implications:** 3–5 "so we should…" statements for the brief.
4. **Write** it up with `templates/precedent-map.md`.

## Testing an idea

If the user shares a specific idea, route or concept and asks whether it has been done or how it
compares, hand over to **multiply-idea-test**, passing on the category map if you have just made
one.

## Save locally

Save to `clients/<client-slug>/<YYYY-MM-DD>-precedents-<topic>.md`, or output Markdown if
you can't write files.

## If the Multiply MCP is connected

When results come from Multiply, present them as `reference/multiply-mcp.md` describes under
*Presenting results from Multiply*: every source as an embedded link, and the data visualised
where it fits.

See `reference/multiply-mcp.md` for every tool's arguments.

1. `create-session`, then find the client: `list-workspaces` (`title-contains`) and
   `list-projects` (`principals: ["ws1"]`).
2. **Read what is already known (you don't need to ask):** call `read-intelligence` on the
   Project. Its `competitors`, `category` and `campaign-history` areas, where present, are
   your starting point. Then `read-news` on the Workspace with `category: "competitor"`.
3. **AdForum:** call `list-endpoints` with `here: "prj1"`.
   - If `AdForum` is listed: AdForum's archive covers campaigns with brand, agency, country,
     media and industry data, the award records behind them, and AdForum's own trend
     write-ups. Ask first, because it takes a few minutes and uses Multiply credits. Then call
     `run-endpoint` with `endpoint: "AdForum"`, `here: "prj1"`, and a self-contained `task`
     (the driver sees nothing of this conversation). For example: "Award-winning campaigns from 2018 to 2025 for
     plant-based dairy brands in Europe and the US. For each, give the brand, title, year, agency, country,
     media, and awards with their level. Include each campaign's image." Add `context` (a
     brief summary) and `focus` (for example "Gold and above").
   - Keep each run narrow, limited to one category, market or time window. A single search returns about
     250 records at most. For a track record, ask for awards grouped by level or year.
   - `await` an `op1` if one is returned, then `read-source` (`account: "acc1"`) the report handle.
     Merge it with your web findings. Credit AdForum's trend write-ups to AdForum.
   - If `AdForum` isn't listed, say so once and continue with web search.
4. **Save (ask first):** `write-source` with `to: "prj1"` (or `ws1` for a category map that serves the
   whole client) and `title: "Creative precedents · <topic> · <YYYY-MM-DD>"`. Sources are
   append-only, so each new run is a new dated document. Use plain links, and use `【N】` only
   for source handles from this session, such as the AdForum report.

## If the Multiply MCP is not connected

Use web search and state its limits in a "Coverage" line. Without web access, work only from
what you reliably know, mark every entry "verify before use", and keep the list short.
Mention once: "If you connect Multiply with AdForum enabled, this can search a licensed archive
of campaigns and award records instead of the open web."
