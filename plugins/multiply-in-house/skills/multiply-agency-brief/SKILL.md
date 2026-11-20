---
name: multiply-agency-brief
description: For in-house teams working with external agencies. Writes a clear brief to send to an agency (creative, media, PR, digital, production), with objectives, audience, proposition, mandatories, budget, timings and how the work will be judged. Then scores what the agency sends back against that brief and drafts consolidated feedback. Use when the user says "brief an agency", "write the agency brief", "brief for our PR agency", "RFP for agencies", "review the agency's response", "score these pitches", or "give feedback on the agency's work". Reads the brand profile; with the Multiply MCP connected, it grounds the brief in the brand Workspace and keeps brief, responses and scores together in a Project.
---

# Agency brief

A good agency brief is the cheapest way to better work. Write one the agency can't
misread, then judge what comes back against it, not against taste.

## Mode A: write the brief

1. **Collect:** the internal request or job brief (from multiply-intake-triage if used), the
   brand profile, budget, timings, and which agency or agencies it's going to.
2. **Write** with these sections, one page if possible:
   - **Background:** the business situation in plain words.
   - **Objective chain:** business objective, communication objective, KPI with baseline
     and target (or "TBC").
   - **Audience:** a person with a tension or need.
   - **Single-minded proposition:** one sentence, 20 words or fewer.
   - **Reasons to believe:** approved claims only, from the brand profile.
   - **Deliverables:** formats, channels, markets, languages.
   - **Mandatories and no-gos:** brand, legal, partner.
   - **Budget and timings:** including review rounds and decision dates.
   - **What we'll judge it on:** 4–6 criteria with weights, shared with the agency upfront.
   - **Who decides:** names and roles.
3. **Check it** like an agency planner would: list anything vague, contradictory or missing,
   and fix it or flag it. Mark inferred items `(proposed)`.
4. Offer a short cover email to the agency.

## Mode B: score the response

1. Load the brief and its judging criteria. If they weren't set, agree them with the user
   before reading the work, so the scoring is fair.
2. For each response (or each route in one response), score every criterion 1–5 with a
   reason that quotes or points to the work. Weighted total at the end.
3. Check the work against the brand rules (or run multiply-brand-guardian) and flag claims
   that need approval.
4. Write **consolidated feedback** for the agency: what to keep, what to change, and what's a
   must versus a preference. One voice, no contradictions. Name stakeholder disagreements to
   the user privately; don't pass them on to the agency unresolved.
5. For pitches with several agencies, give a comparison table and a recommendation with the
   trade-offs. The decision stays with the user.

## Save locally

`brand/<brand-slug>/agency/<YYYY-MM-DD>-brief-<job>.md` and
`…-scores-<job>.md`. If you can't write files, output Markdown.

## If the Multiply MCP is connected

See `reference/multiply-mcp.md`.

- **Read:** `create-session`, find the brand Workspace, `search-sources` for brand
  guidelines, claims and earlier agency briefs.
- **Set up (ask first):** a Project per agency job with `create-project`
  (`parent: "ws1"`, the brief as `instructions`), so brief, responses and scores sit together.
- **Responses:** upload the agency's decks with multiply-save (`prepare-upload`, `add-files`
  to the project). Then `search-sources` on the project to quote them in the scoring.
- **Save (ask first):** `write-source` with
  `title: "Agency brief · <job> · <YYYY-MM-DD>"` and later
  `"Agency scores · <job> · <YYYY-MM-DD>"`.
- Optional: `multiply-adforum-search` for the agencies' award records when choosing who to
  brief.

## If the Multiply MCP is not connected

Work from local files and what the user shares. Mention once: "If you connect Multiply, each
agency job becomes a Project that holds the brief, the agency's responses and your scores."
