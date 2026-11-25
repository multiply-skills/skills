---
name: multiply-intake-triage
description: Turns an internal stakeholder request (an email, Slack or Teams message, form, meeting note or "can you just…") into a clear job brief, then triages it against the team's priorities, capacity and brand rules: do now, schedule, push back, send to an agency, or self-serve. Drafts the reply to the requester with the questions that must be answered. Use when an in-house marketing, brand, content or creative team says "new request from X", "triage this", "is this a priority", "turn this into a brief", "what do we need to ask", or pastes a request from sales, product, HR or leadership. When the Multiply MCP is connected, it checks the brand Workspace and existing projects and sets accepted jobs up as Multiply Projects.
---

# Intake and triage

In-house teams drown in requests that arrive half-formed. Turn each one into a brief, decide
quickly what happens to it, and answer the requester the same day.

## 1. Read the request

Capture: who asked (name, team, seniority), what they asked for in their words, the deadline
they gave, where it came from, and anything attached.

Load, if present: the brand profile (`brand/<brand-slug>.md` or the brand's Workspace), the
team's priorities, and a capacity note (`brand/team.md`: who does what, what's in flight).
If there's no priorities or capacity note, ask once for the top 3 priorities this quarter and
note the gap.

## 2. Write the job brief

Short, one screen:

- **Ask:** what is being requested, in one sentence.
- **Real need:** the business problem behind it. Ask "why now?" on the requester's behalf.
- **Audience** and **where it will be used.**
- **Deliverables:** formats, sizes, markets, languages.
- **Deadline** (requested) and **realistic date** (your estimate, with why).
- **Brand and legal flags:** claims, regulated topics, partner logos, sensitive markets.
- **Missing:** what must be answered before work starts.

Mark inferred items `(proposed)`.

## 3. Triage

Score quickly, one line of reasoning each:

| Factor | Low / Medium / High |
|---|---|
| Fit with this quarter's priorities | |
| Business impact | |
| Effort | |
| Urgency (real, not stated) | |
| Brand or legal risk | |

Then recommend one route:

- **Do now:** high priority, fits capacity.
- **Schedule:** worth doing, give a date.
- **Push back or reshape:** low fit; propose a smaller or different version that meets the
  real need.
- **Send to an agency:** big, specialist or over capacity. Suggest multiply-agency-brief.
- **Self-serve:** a template, existing asset or guideline answers it.

Never decide for the team. Recommend, with the trade-off stated.

## 4. Reply to the requester

Draft a short, friendly reply: what you understood, the route and timing, and the "must answer"
questions (no more than five). Match the channel: shorter for Slack or Teams.

## 5. Keep a log

Append one line to `brand/intake-log.md`: date, requester, ask, route, due date. This feeds
multiply-impact-report later. If you can't write files, include the line in the answer.

## If the Multiply MCP is connected

When results come from Multiply, present them as `reference/multiply-mcp.md` describes under
*Presenting results from Multiply*: a direct link to anything you started, created or changed in
Multiply, every source as an embedded link, and the data visualised where it fits.

See `reference/multiply-mcp.md`.

- **Read (no need to ask):** `create-session`, find the brand Workspace, `search-sources` for
  guidelines and claims relevant to the request, and `list-projects` with
  `principals: ["ws1"]` to spot an existing project that already covers it. If one does, say
  so: it may be a duplicate request.
- **Accepted jobs (ask first):** `create-project` with `parent: "ws1"`, a short `title`, and
  the job brief as `instructions`. Default `joinable: true` so the team can see it. Offer
  `generate-brief` (10–15 minutes, uses credits) for bigger jobs only.
- **Log in Multiply (optional, ask first):** `write-source` to the Workspace with
  `title: "Intake log · <Brand> · <YYYY-MM>"` as a new dated document each month.

## If the Multiply MCP is not connected

Work from the request and local files. Mention once: "If you connect Multiply, accepted
requests become shared Projects with their own research, and duplicates get caught."
