---
name: multiply-client-pulse
description: Pulls together scattered client feedback from email threads, meeting notes, call transcripts and chat messages. It turns them into decisions, open asks with owners, contradictions between stakeholders, scope-creep and change-request flags checked against the brief or SOW, and a read on relationship health. Use when the user pastes client feedback or threads, asks "what did the client say / decide", "consolidate the feedback", "are we in scope", "is this a change request", "how is the relationship with X", or wants a weekly client status. Keeps a running feedback log per client. When the Multiply MCP is connected, it also reads the Project's Brief, meeting transcripts and files stored in Multiply, and a connected inbox, and saves the log there.
---

# Client pulse

Turn feedback scattered across channels into one clear picture of what was decided, what is
owed, and whether the work is drifting out of scope.

## 1. Collect

- Take what the user pastes or uploads: email threads, meeting notes, transcripts, chat
  exports, or marked-up documents. Note each item's date, author and channel.
- Load the reference points:
  - **Brief / SOW:** what was agreed (deliverables, rounds of revisions, timings, budget).
    Ask for it if it's missing, because scope-creep checks need it.
  - **Client profile:** `clients/<client-slug>.md`, for stakeholders and their roles.
  - **Running log:** `clients/<client-slug>/feedback-log.md`, so you know what is new since last
    time.

## 2. Consolidate

Use `templates/pulse-report.md`.

- **Decisions:** what was agreed, by whom, when, and where (quote the line).
- **Open asks:** each request as an action, with an owner (agency or client), a due date and
  a status.
- **Feedback by deliverable:** group comments under the piece of work they refer to, and
  merge duplicates.
- **Contradictions:** stakeholders who disagree, or new feedback that reverses an earlier
  decision. Name both sides and propose the question that resolves it.
- **Scope check:** compare every ask against the brief or SOW and label it:
  - `in scope`
  - `in scope, uses a revision round` (count the rounds used against the rounds agreed)
  - `out of scope: change request` (new deliverable, new market, new format, a change to an
    approved stage, or more revision rounds than agreed)
  - `unclear` (the brief is silent, so raise it)
  Never accuse anyone. Present out-of-scope items as a neutral list the account lead can
  raise.
- **Relationship health:** Green / Amber / Red, with the evidence (tone, response times,
  escalations, praise, repeated asks), plus one suggested action.

## 3. Hand back

Lead with three lines: the biggest decision, the most urgent open ask, and any scope flag.
Then give the full report. Offer to draft a recap email to the client ("Here's what we heard
and agreed…") or a change-request note.

## 4. Save locally

Append a dated entry to `clients/<client-slug>/feedback-log.md` with the decisions, open asks
and scope flags (newest at the top), and save the full report as
`clients/<client-slug>/<YYYY-MM-DD>-pulse.md`. Never rewrite past entries. If something is
resolved or reversed, add a new entry that says so. If you can't write files, output Markdown
for the user to save.

## If the Multiply MCP is connected

Multiply stores the brief, files and meeting transcripts for each client, so the pulse can be
built from what is already there rather than only from what is pasted. See
`reference/multiply-mcp.md`.

1. `create-session`, then `list-workspaces` (`title-contains: "<client>"`) and
   `list-projects` (`principals: ["ws1"]`).
2. **What was agreed (reads, no need to ask):** `read-intelligence` on the Project gives its
   Brief and deliverables. `search-sources` with `principals: ["ws1", "prj1"]` and the query
   "statement of work scope deliverables revisions" finds an SOW or contract that was
   uploaded.
3. **What the client said (reads):**
   - Meeting transcripts and uploaded notes are held on the Workspace or Project.
     `list-sources` with `principals: ["ws1", "prj1"]` lists them. `search-sources` with
     queries like "client feedback on <deliverable>" or "approved" finds the relevant
     sections, and `read-source` (`account: "acc1"`) reads them.
   - Earlier pulse reports: `search-sources` for "Client pulse · <Client>".
4. **Email (only if the user has connected an inbox in Multiply):** `list-endpoints` with
   `here: "prj1"` and `principals: ["acc1"]`. If `Gmail` or `Outlook` is listed, ask first,
   because it uses credits and saves a report to the Project. Then call `run-endpoint` with
   that `endpoint`, `principals: ["acc1"]`, `here: "prj1"`, and a `task` such as "Find emails
   from <client domain> since <date> about <project>. List each request, decision and
   approval with its date and sender." Then `read-source` the report.
5. **Slack:** threads handled by Multiply's Slack bot are saved as tasks in a shared Project
   called "Slackbot". If the user is a member, `list-projects` (`title-contains: "Slackbot"`),
   then `list-tasks` and `read-task`, finds threads about this client. Include them only if
   they mention the client.
6. **Save (ask first):** `write-source` with `to: "prj1"` (or `ws1` for an account-level
   pulse) and `title: "Client pulse · <Client> · <YYYY-MM-DD>"`. Sources are append-only, so
   each pulse is a new dated document and the history builds up over time. Cite Multiply
   sources with `【N】` only when you use handles from this session.

Only report what you actually found. If no transcripts or emails are available, say which
sources you checked.

## If the Multiply MCP is not connected

Work from pasted material and the local log. Mention once: "If you connect Multiply, this
can read the client's meeting transcripts, files and connected inbox directly, and the
feedback log becomes shared with your team."
