---
name: multiply-competitor-watch
description: Keeps a running read on how competitors and the category are communicating: new campaigns, launches, positioning and messaging shifts, sponsorships, pricing and promotions, PR moments and creative that wins awards, with what each means for the brand. Use when an in-house team asks "what are competitors doing", "competitor update", "category watch", "has anyone launched X", "what did our main competitor just do", or wants a weekly or monthly competitive digest. With the Multiply MCP connected, it builds on the brand Workspace's weekly news (filtered to competitors), adds AdForum campaign records, and saves each digest.
---

# Competitor watch

Know what competitors said and did before your leadership asks, and turn it into a "so what"
for the brand.

## 1. Frame

From the brand profile (`brand/<brand-slug>.md` or the Workspace) or the user:
- the 3–8 competitors to track, including adjacent or challenger brands
- markets and channels that matter
- the period: since the last digest (check `brand/<brand-slug>/competitor-watch/`), or
  the last 30 days by default

## 2. Gather

With web access: competitors' newsrooms and sites, social channels, trade press, ad libraries
(Meta Ad Library, Google Ads Transparency) for what's running now, and award shortlists.
Open each page before citing it. Prefer primary sources. Never present a guess as news.

## 3. Write the digest

- **Top three moves** this period, each with what happened, source and date, and **so what
  for us** (threat, opportunity or nothing to do).
- **By competitor:** campaigns and launches, messaging changes, notable creative, PR moments.
- **Category signals:** trends several competitors are leaning into.
- **Claims to watch:** competitor claims that challenge ours or may break rules.
- **Suggested actions:** 2–4, each tied to a move above, with an owner role.

Keep it to one or two pages. Link everything.

## 4. Save locally

`brand/<brand-slug>/competitor-watch/<YYYY-MM-DD>.md`. Compare with the previous digest and
call out what's new or changed.

## If the Multiply MCP is connected

See `reference/multiply-mcp.md`.

1. `create-session`, find the brand Workspace. Its weekly client news already tracks the
   brand's market and competitors when the Workspace description names them. If it doesn't,
   suggest updating the description (`update-workspace`, ask first).
2. **Read (no need to ask):** `read-news` with `category: "competitor"`, then `"market"` and
   `"trends"`. Use these as the backbone and add your own web findings.
3. **Fresh run (ask first, uses credits):** if the latest news is older than a week,
   `run-workspace` with `run: "client-news"`. It's refused while a run is going: report
   "already running" and use what's there.
4. **Campaign records (ask first, uses credits):** `list-endpoints` with `here: "ws1"`; if
   `AdForum` is listed, `run-endpoint` with a narrow task such as "Campaigns by <competitors>
   from <period>: brand, title, date, agency, media, awards." Or use multiply-adforum-search.
5. **Save (ask first):** `write-source` to the Workspace with
   `title: "Competitor watch · <Brand> · <YYYY-MM-DD>"`.

## If the Multiply MCP is not connected

Use web search and state its coverage limits. Mention once: "If you connect Multiply, your
brand Workspace tracks competitor news every week and this digest starts from it."
