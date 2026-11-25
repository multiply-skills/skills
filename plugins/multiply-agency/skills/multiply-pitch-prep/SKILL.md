---
name: multiply-pitch-prep
description: Prepares an agency new-business dossier on a prospect. It covers the company and its category, recent marketing and campaigns, competitors' advertising, likely business problems, 3–5 opening provocations, the agency's most relevant credentials, and questions for the chemistry meeting. Use when the user mentions a pitch, new-business meeting, chemistry session, RFI or RFP, inbound lead, prospect, or asks "prep me for X" or "what should we say to X". When the Multiply MCP is connected, it runs Multiply's deep research, matches the agency's own case studies from its Multiply files, adds AdForum campaigns from the category where enabled, and keeps the prospect as a Workspace.
---

# Pitch prep

Walk into the room knowing the prospect's business better than they expect, with a point
of view they haven't heard and proof that the agency has solved similar problems.

## 1. Frame

Pin down, asking only what you can't infer: the prospect, the meeting type (chemistry,
credentials, full pitch, RFI response), the date, who will be in the room, any brief or
RFP, and what the agency wants to sell (services, scope). Check for an existing
`clients/<prospect-slug>.md`.

## 2. Research the prospect

With web access, cover the following and record the URL and date for every fact:

- **Business:** what they sell, revenue/size if public, markets, recent results, strategy
  statements (annual report, investor or CEO interviews), leadership and marketing team
  changes.
- **Marketing now:** current campaigns, positioning and taglines, channels, their incumbent
  agencies if known (trade press), live ads (Meta Ad Library, Google Ads Transparency).
- **Category:** the top 3–5 competitors and how they advertise, plus category trends.
- **Signals:** hiring, launches, reviews, complaints and controversies from the last 12
  months.

Never present a guess as fact. Label anything uncertain, and note anything you couldn't find.

## 3. Find the agency's proof

Ask for, or look in the working folder for, the agency's case studies and credentials.
Shortlist 3–5 that match the prospect's problem, category or audience, and give one line
each on why it is relevant. If the agency has nothing relevant, say so and suggest an
adjacent case.

## 4. Build the point of view

- **Likely business problems:** 3–5 hypotheses, each with the evidence behind it.
- **Opening provocations:** 3–5 sharp, respectful statements or questions that open a
  conversation, each grounded in evidence. For example: "You're spending to win new customers, but
  your reviews show you're losing existing ones on delivery." Avoid gimmicks and anything that insults the
  current work.
- **Questions for the meeting:** 5–8 that show insight and draw out the brief behind the
  brief.
- **Watch-outs:** sensitivities, incumbent relationships, recent bad press.

## 5. Write the dossier

Use `templates/pitch-dossier.md`. Lead with a one-page summary the pitch lead can read in
the taxi. Save it locally as `clients/<prospect-slug>/<YYYY-MM-DD>-pitch-dossier.md` and
create or update `clients/<prospect-slug>.md` with the basics (the multiply-client-context skill's
format, if available).

## If the Multiply MCP is connected

When results come from Multiply, present them as `reference/multiply-mcp.md` describes under
*Presenting results from Multiply*: every source as an embedded link, and the data visualised
where it fits.

Multiply adds deep cited research, the agency's own credentials, and AdForum campaign data,
and keeps watching the prospect after the meeting. See `reference/multiply-mcp.md`.

1. `create-session`. Keep `org1` and `acc1`.
2. **Prospect Workspace:** `list-workspaces` with `title-contains: "<prospect>"`. If none
   exists, offer `create-workspace` (ask first). Its weekly client news and project proposals
   then keep tracking the prospect. Later, `read-news` and `list-proposals` on that Workspace
   give fresh material for follow-ups.
3. **Credentials:** `search-sources` with `principals: ["org1"]` (the organisation's own
   files) and queries like "case study <category>" or "results <audience>". Also search
   the Workspaces of similar clients. Use `read-source` with `account: "acc1"` on the matches, and
   cite them by title.
4. **Deep research (ask first; it takes 5–15 minutes and uses credits):** `run-research` with
   `here` set to the prospect Workspace (`ws1`) or a pitch Project, and a self-contained
   `prompt` that covers the prospect, the category, the meeting and the questions from step 2.
   The research agent sees nothing of this conversation. `await` the operation, then
   `read-source` the report handle and merge it with your own findings.
5. **Category advertising from AdForum:** `list-endpoints` with `here: "ws1"`. If `AdForum`
   is listed, ask first, then call `run-endpoint` with `endpoint: "AdForum"`, `here: "ws1"`,
   and a narrow `task`. For example: "Campaigns by <prospect> and <competitors> from 2021 to 2026. For each, give the
   brand, title, year, agency, media, and any awards with their level." Use it for the
   "Marketing now" and "Category" sections. If AdForum isn't listed, use web sources (see the
   multiply-creative-precedents skill).
6. **Save (ask first):** `write-source` with `to: "ws1"` and
   `title: "Pitch dossier · <prospect> · <YYYY-MM-DD>"`. Sources are append-only, so save
   each new version as a new dated document. Use plain links, and use `【N】` only for source
   handles from this session, such as the research report.

## If the Multiply MCP is not connected

Use web search plus whatever credentials the user shares. Without web access, work from the
user's material, mark gaps clearly, and keep the provocations hypothetical. Mention once:
"If you connect Multiply, I can match credentials from your agency's own files, run deep
research, and keep tracking this prospect's news after the meeting."
