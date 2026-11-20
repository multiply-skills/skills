---
name: multiply-impact-report
description: Writes a monthly, quarterly or yearly report for leadership on what the in-house marketing, brand or creative team delivered and what it achieved: volume and mix of work, results against goals, speed, work brought in-house versus agency spend, stakeholder satisfaction, and the case for priorities or resources next period. Use when the user says "impact report", "quarterly review for leadership", "what did we deliver this quarter", "show the value of the in-house team", "agency savings", or "prepare our team update for the CMO". Works from logs and data the user provides; with the Multiply MCP connected, it reads the period's projects, tasks and saved reports.
---

# Impact report

Leadership funds what it can see. Show what the team shipped, what it changed for the
business, and what it needs next, with numbers that hold up.

## 1. Frame

Confirm: the period, the audience (CMO, leadership team, finance), the format (one-page
memo, short deck outline, or both), and the goals the team was set for the period.

## 2. Gather the evidence

- **Work delivered:** `brand/intake-log.md` (from multiply-intake-triage), project lists,
  trackers the user exports.
- **Results:** campaign and channel results, brand tracking, sales or lead data the user
  provides. Each number with its source, period and baseline.
- **Cost and savings:** agency fees for work now done in-house. Use the user's rate card or
  past invoices; if there are none, ask for a typical day rate or project fee and label the
  estimate as one.
- **Speed:** time from request to delivery, where dates exist.
- **Stakeholders:** quotes or survey scores, if available.

Build an evidence table: claim · number · source · period · confidence. Flag anything
missing as a question, ranked by how much it would strengthen the report.

## 3. Write

One page first, then detail:

1. **Headline:** the one sentence leadership should remember.
2. **Delivered:** volume and mix (campaigns, assets, requests), with two or three highlights.
3. **Results against goals:** each goal, the result, and whether it was met.
4. **Value:** agency spend avoided or reduced, with the method shown in one line.
5. **Speed and service:** turnaround, stakeholder feedback.
6. **What got in the way:** capacity, late requests, approval delays, with evidence.
7. **Asks for next period:** priorities, people, budget or tools, each tied to evidence above.

Rules: no number without a source; no savings figure without its method; plain language; no
superlatives without proof. Separate what was measured from what is estimated.

## 4. Save locally

`brand/impact/<YYYY>-<period>-impact-report.md`, or Markdown output. Offer a short deck
outline (5–7 slides, one message each) if they present it.

## If the Multiply MCP is connected

See `reference/multiply-mcp.md`.

- **Read (no need to ask):** `create-session`; `list-workspaces`; `list-projects` with
  `principals: ["org1"]`; `list-tasks` with project handles for activity in the period
  (created and modified dates). `search-sources` for "results", "post-campaign report",
  "Intake log", "Stakeholder pulse" and earlier impact reports. Count only what you find,
  and say what Multiply covers and what it doesn't.
- **Save (ask first):** `write-source` to the main brand Workspace with
  `title: "Impact report · <period> · <YYYY-MM-DD>"`.

## If the Multiply MCP is not connected

Work from the user's logs and data. Mention once: "If you connect Multiply, the report can
count projects and activity for the period straight from your workspaces."
