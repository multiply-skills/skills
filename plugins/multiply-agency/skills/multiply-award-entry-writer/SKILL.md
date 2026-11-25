---
name: multiply-award-entry-writer
description: Drafts advertising and marketing award entries and case studies (Cannes Lions, D&AD, The One Show, Effies, Epica, regional shows) covering background, challenge, idea, strategy, execution and results. It adapts each entry to a show's category criteria, scoring weights and word limits, flags missing or weak evidence and over-claiming, and writes case-film scripts and short summaries. Use when the user mentions an award entry, awards submission, case study for awards, entry form, jury, effectiveness paper, or asks to "write up this campaign for Cannes / Effies / D&AD". Works from the case material the user provides. When the Multiply MCP is connected, it pulls the Project's brief and sources, benchmarks against past winners in the category via AdForum where enabled, and saves the entry back to the Project.
---

# Award entry writer

Juries read hundreds of entries. Write the one that is clear in 30 seconds, proves every claim,
and fits exactly what that show and category reward.

## 1. Pin down the target

Ask for, or confirm: the show, the year, the category (for example Creative Effectiveness, Film,
Social & Creator, Brand Experience), the entry deadline, and the **current entry kit**: its
questions, word or character limits and judging criteria. Rules change every year. If the user
can't provide the kit and you have web access, look it up on the show's own site. Otherwise use
`reference/award-criteria.md` as a starting point and label every limit "verify against this
year's entry kit".

One campaign entered in several categories needs a different angle for each. Ask which
categories are planned.

## 2. Gather the evidence

Collect the brief, strategy deck, creative, media plan, results reports, client quotes and
press coverage. Build an **evidence table**: each claim, its number, its source, the period
it covers, its baseline, and whether the client has approved it.

Flag:
- **Missing:** no baseline, no control or comparison, no business result (only reach and
  impressions), no time period, no source.
- **Weak:** vanity metrics, earned-media values with no stated method, "trending" with no data,
  results that could have other causes (price cuts, distribution, seasonality) that aren't
  addressed.
- **Over-claiming:** superlatives without proof ("record-breaking", "viral"), results credited
  to the campaign that came from other factors, rounding up. Juries penalise this.

List what is missing as **questions for the client or data team**, ranked by how much each
answer would lift the score.

## 3. Draft

Use `templates/award-entry.md`. Standard structure, mapped onto the show's own questions:

1. **Background:** the brand, market and situation, briefly.
2. **Challenge / objectives:** what had to change, with measurable objectives set *before* the
   campaign. Note that juries check whether objectives were set in advance.
3. **Insight & strategy:** the human or cultural truth and the strategic choice it led to.
4. **Idea:** one sentence. If the jury can't repeat it, rewrite it.
5. **Execution:** how it came to life, covering channels, timing, scale and craft, plus spend if required.
6. **Results:** tied back to each objective, business results first, each with its
   source, period and baseline. Address other factors that could explain them.

Rules:
- Write to the show's **word or character limits** and give the count per section.
- Put the effort where the scoring weight is. For effectiveness shows, results usually
  carry the most weight.
- Plain, confident language. No jargon, no superlatives without proof, no unexplained
  acronyms.
- Also give a **one-line summary**, a **50-word summary**, and if requested a **case film
  script** (about 2 minutes: problem, insight, idea, execution, results, end card).

## 4. Review like a juror

Score the draft against the category's criteria (1–10 each, with a reason), then list the
three edits that would raise the score most. Run the over-claiming check again on the final
text.

## 5. Save locally

Save to `clients/<client-slug>/<YYYY-MM-DD>-award-entry-<show>-<category>.md`, keeping each
show and category as its own file. If you can't write files, output Markdown.

## If the Multiply MCP is connected

When results come from Multiply, present them as `reference/multiply-mcp.md` describes under
*Presenting results from Multiply*: every source as an embedded link, and the data visualised
where it fits.

See `reference/multiply-mcp.md` for every tool's arguments.

1. `create-session`, then find the client's Workspace and the campaign's Project
   (`list-workspaces`, `list-projects`).
2. **Pull the case material (reads, no need to ask):** `read-intelligence` on the Project gives
   the original Brief and objectives, which is useful proof that objectives were set in advance. Then
   `search-sources` with `principals: ["ws1", "prj1"]` and queries such as "results",
   "post-campaign report", "media plan", "brand tracker", "client quote". Call `read-source`
   (`account: "acc1"`) on the matches and add every figure to the evidence table with its
   source title.
3. **Benchmark against past winners (ask first, because it uses credits):** call
   `list-endpoints` with `here: "prj1"`. If `AdForum` is listed, call `run-endpoint` with
   `endpoint: "AdForum"`, `here: "prj1"`, and a `task` such as: "Campaigns that won at
   <show> in <category> from 2021 to 2025, especially in <client's category>. For each, give the brand, title,
   year, agency, award level, and a one-line description of the idea." Use the results to
   show what has won, how the work compares, and which angles are already well-worn. Never
   copy their wording. If AdForum isn't listed, use the show's own winners archive on the
   web.
4. **Save (ask first):** `write-source` with `to: "prj1"` and
   `title: "Award entry · <show> <year> · <category> · <YYYY-MM-DD>"`. Sources are
   append-only, so every revision is a new dated document whose first line reads "Supersedes …".
   Use `【N】` only for source handles from this session, such as the results report, which
   lets the team trace every claim.

## If the Multiply MCP is not connected

Work from the material the user provides and, if available, web access to the show's rules and
winners. Mention once: "If you connect Multiply, I can pull the brief and results straight from
the campaign's Project and benchmark against past winners in AdForum."
