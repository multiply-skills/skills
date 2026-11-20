---
name: multiply-import-work
description: Brings the user's active client jobs into Multiply as Projects, each in the right client Workspace, with clear Instructions, the brief and key files, and the intelligence areas that fit the job, so Multiply's research and suggested next tasks are about real work. Reads jobs from what the user pastes or uploads, local client files, or connected tools such as Asana, Monday, Linear, Notion, a drive or email briefs. Use when the user says "import my work", "bring my projects into Multiply", "set up my active jobs", "add this brief as a project", "move my campaigns from Asana/Monday into Multiply", or has Workspaces but few Projects. Needs the Multiply MCP. Creates Projects, not to-do lists.
---

# Import my work

A Multiply Project is only as useful as what it knows. Bring in the jobs people are actually
working on, with enough context that the Brief, intelligence and Drafts are worth reading.

## 1. Check the connection

If Multiply tools aren't available, run multiply-connect first. Then `create-session`,
`list-workspaces` and `list-projects` with `principals: ["org1"]`, so you know what exists.

## 2. Find the active jobs (reads)

Use what's available, in this order:

1. Briefs or job lists the user pastes or uploads.
2. `clients/<client>/` files from the agency skills (briefs, dossiers).
3. Other tools connected to the assistant: open projects or epics in Asana, Monday, Linear or Notion;
   brief documents in a drive; recent briefing emails from client domains.

A job is worth importing if it has a client, an outcome and is live (not done, not just an
idea). Skip internal admin and individual to-dos: Multiply Projects are for client work.

Show a short table and let the user pick:

| Job | Client | Source | Due | Brief found? | Already in Multiply? |

Match "already in Multiply" by title within the client's Workspace. Never create a duplicate;
offer to update the existing Project's Instructions instead.

## 3. Draft each Project

- **Workspace:** the client's. If it doesn't exist, offer to create it (or run multiply-setup).
- **Title:** short and recognisable, up to 70 characters, the way the team names the job.
- **Instructions** (Markdown, up to 20,000 characters). Multiply writes the Brief and
  intelligence from these plus the files, so be concrete:
  - **Goal:** the business and communication objective.
  - **Deliverables:** what is being made, formats, markets.
  - **Audience.**
  - **Timing:** key dates and the deadline.
  - **Stakeholders:** client approvers and the agency team, by role.
  - **Constraints:** budget, mandatories, legal, brand rules.
  - **Source:** where this came from (for example "Asana: Spring launch, imported 2026-11-20").
  Mark anything inferred `(proposed)`.
- **Files:** the brief and up to a few key documents (up to 20 per Project).
- **Intelligence areas:** pick 3–6 from Multiply's catalogue that fit this job:
  audience, brand, category, culture, competitors, media-landscape, channels,
  product-and-offer, commercial-context, campaign-history, measurement, stakeholders,
  compliance, sustainability-and-impact, partnerships-and-talent.
  For example a PR launch might take media-landscape, stakeholders and competitors; a
  regulated product launch adds compliance. Give one line on why each.
- **Visible to the team?** `joinable: true` lets everyone in the org find it. Default to
  that for client work unless the user says otherwise.

Show all drafts together for one round of edits.

## 4. Create (ask first, once for the batch)

Explain: creating Projects is free; generating the Brief and researching areas uses
Multiply credits and takes about 10–15 minutes per project. Then, per job:

1. `create-project` with `parent: "ws1"`, `title`, `instructions`, `joinable`.
2. Files: upload as multiply-save describes (`prepare-upload`, PUT, `add-files` with
   `to: "prj1"`).
3. Brief and areas, one of:
   - **Default:** `generate-brief` with `wait: 0`. Multiply writes the Brief, chooses areas
     and suggests Drafts. After it settles, if an area you picked is missing, add it with
     `update-areas`.
   - **User wants control:** `update-areas` with `add` set to your picks, and skip the
     generated Brief for now.
   Run all projects in parallel and `await` the operations.

## 5. Hand back

Per project, from `read-intelligence`:
- one line on what the Brief says the job is (flag where it differs from the source)
- the areas it researched
- the top one or two Drafts (suggested next tasks)

Then list anything not imported and why. Don't change the source tool: Asana, Monday and
the rest stay as they were.

See `reference/multiply-mcp.md` for every tool's arguments.
