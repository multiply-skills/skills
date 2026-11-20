---
name: multiply-tune-workspace
description: Health check for the user's Multiply Workspaces and Projects. Finds stale, superseded, duplicate or failed files (and gives a clean-up checklist, since the MCP can't delete files), client news nobody has opened, project proposals left waiting, inactive projects, outdated descriptions and Instructions, and intelligence areas that failed or don't fit the job, then fixes what it's allowed to (with approval) and lists what to do in Multiply. Use when the user says "tune my workspace", "clean up Multiply", "is my workspace up to date", "what's stale in Multiply", "review my clients in Multiply", or as a monthly check. Needs the Multiply MCP.
---

# Tune my workspace

Context that goes stale makes the AI work on the wrong things. Keep each client's Workspace
current, lean and acted on.

## 1. Scope

`create-session`, then `list-workspaces`. Ask whether to check one client, a few, or all.
For more than 10, do the ones with the most projects first and offer the rest after.

## 2. Collect (reads only, no need to ask)

Per Workspace:

- **Description:** `list-workspaces` shows it. Missing, very short, or out of line with what
  the news and projects are about?
- **Files:** `list-sources` with `principals: ["ws1"]` and `status: ["indexed", "failed"]`
  (and each active project's handle). For each file, decide:
  - **Failed:** couldn't be read, so the AI never sees it.
  - **Superseded:** a newer version exists (later year, "v2" vs "v1", "final" vs "draft").
  - **Possibly stale:** time-bound content that has likely passed (last year's plan, an old
    campaign brief, a finished job's files sitting on the Workspace). Mark these as a question
    for the user, not a fact.
  - **Duplicate:** the same document added twice.
  Count uploaded files against the 20-file limit per Workspace or Project.
- **Client news:** `read-news`. Date of the latest item, and how many are still marked new
  (nobody has opened them).
- **Proposals:** `list-proposals`. How many are new or saved, and how old.
- **Projects:** `list-projects` with `principals: ["ws1"]`. For projects the user is a member
  of, `list-tasks` with the project handle gives the last activity.
  - No task modified in 30 days: inactive.
  - `read-intelligence` on active ones: Brief or areas marked failed, open knowledge gaps,
    areas that don't fit the job, Drafts nobody acted on.

## 3. Report

One block per Workspace, worst first:

**<Client>** · Green / Amber / Red
- What's off, with numbers: "2 superseded files, 3 failed files, 14 unopened news items, 6 proposals older than
  4 weeks, 2 projects inactive since September".
- **Fixes I can make** (numbered, so the user can say "do 1, 3 and 4").
- **Do in Multiply** (things the MCP can't do).

Lead the whole report with two lines: the healthiest and the most neglected client.

## 4. Fix (only what the user approves)

What can be done from here:

- **Description:** `update-workspace` with a sharper description (show before and after).
- **Proposals:** `update-proposal` to `archived` or `saved`. Or, if one fits a live need,
  start it with `start-proposal` (uses credits, takes 10–15 minutes: say so).
- **Refresh news:** `run-workspace` with `client-news` where the latest item is old. It uses
  credits, so say so when asking. It is refused while a run is already going: report that
  one as "already running" and move on rather than retrying.
- **Project Instructions:** `update-project` where the job has changed. This refreshes Drafts.
- **Intelligence areas:** `update-areas` to add a missing area (uses credits). Removing an
  area deletes its findings for good, so Multiply asks the user to confirm.
- **Drafts:** `dismiss-draft` for suggestions that are no longer relevant.
- **Missing context:** add a current document with multiply-save.
- **Mark what's current (optional, ask first):** the MCP can't remove a stale file, so the
  AI keeps reading it until someone deletes it. As a stopgap, `write-source` a short note
  to the Workspace titled `Current sources · <Client> · <YYYY-MM-DD>` that lists which files
  are current and which are superseded or out of date, citing each with `【N】`. It doesn't
  count against the file limit. Say plainly that this is a pointer, not a clean-up.

## Stale files: the user removes them in Multiply

No MCP tool can delete, replace or edit a source (`write-source` only adds). So this skill
flags stale files but never claims to have cleaned them up. Give the user a checklist they
can work through in the Workspace's Files panel:

| File | Where (Workspace › Project) | Why | Action |
|---|---|---|---|
| Brand guidelines 2024.pdf | Acme | Superseded by Brand guidelines 2026.pdf | Delete |
| Spring launch brief.docx | Acme › Spring launch | Job finished in June? | Confirm, then delete |

Order it so the files that most mislead the AI come first: superseded brand, tone of voice
and strategy documents, then old briefs, then duplicates and failed files.

If a later version of the MCP adds a tool to delete or archive sources (check the tool list
at the start), use it for the rows the user approves instead of the checklist, one
confirmation for the batch.

Also under **Do in Multiply**: archive projects or Workspaces, change project members.

## 5. Close

Summarise what changed, what's left for the user, and suggest running this again in a
month. Update `clients/_multiply.md` with the date checked, if the file exists.

See `reference/multiply-mcp.md` for every tool's arguments.
