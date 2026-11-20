---
name: multiply-stakeholder-pulse
description: Pulls together scattered internal feedback and approvals on a piece of work (from email, Slack or Teams threads, comments, meeting notes and transcripts) into decisions, open asks with owners, conflicting feedback between stakeholders, approval status per stakeholder, and changes that go beyond what was agreed. Use when an in-house team says "consolidate the feedback", "who has approved this", "legal and product want different things", "what did leadership decide", "where are we on sign-off", or pastes feedback from several people. Keeps a running log per job. With the Multiply MCP connected, it reads the project's brief, transcripts and files and saves the log there.
---

# Stakeholder pulse

In-house work stalls in approval rounds: too many reviewers, feedback that contradicts, and
"one small change" that resets the timeline. Make the state of play obvious in one page.

## 1. Collect

- What the user pastes or uploads: threads, comments, notes, transcripts. Note each item's
  date, author, role and channel.
- The job brief (from multiply-intake-triage or the project) for what was agreed: deliverables,
  rounds, dates.
- Approvers from the brand profile (`brand/<brand-slug>.md`) or the brief.
- The running log, `brand/<brand-slug>/<job>-feedback-log.md`, to know what's new.

## 2. Consolidate

- **Decisions:** what was decided, by whom, when (quote the line).
- **Approval tracker:**

| Stakeholder | Role | Needs to approve | Status | Date | Conditions |
|---|---|---|---|---|---|

  Status: approved, approved with changes, changes requested, not yet seen.
- **Open asks:** each as an action with owner and due date.
- **Feedback by deliverable,** duplicates merged.
- **Conflicts:** where stakeholders disagree, or new feedback reverses a decision. Name both
  sides, say whose call it is according to the approver list, and propose the question that
  settles it.
- **Beyond the brief:** asks that add deliverables, markets or rounds, or reopen an approved
  stage. Present neutrally with the likely impact on the date.
- **Risk to the date:** Green / Amber / Red with the reason.

## 3. Hand back

Lead with three lines: the decision that matters most, what's blocking sign-off, and any
conflict that needs escalating. Offer a recap message to the stakeholders ("Here's where we
landed…"), written so nobody feels overruled.

## 4. Save locally

Append a dated entry to the job's feedback log (newest first) and save the full pulse as
`brand/<brand-slug>/<YYYY-MM-DD>-pulse-<job>.md`. Never rewrite past entries.

## If the Multiply MCP is connected

See `reference/multiply-mcp.md`.

1. `create-session`, find the brand Workspace and the job's Project.
2. **Read (no need to ask):** `read-intelligence` for the Brief and deliverables;
   `list-sources` and `search-sources` with `principals: ["ws1", "prj1"]` for meeting
   transcripts, notes and earlier pulses ("Stakeholder pulse · <job>").
3. **Inbox (ask first, uses credits):** `list-endpoints` with `here: "prj1"` and
   `principals: ["acc1"]`. If `Gmail` or `Outlook` is listed, `run-endpoint` with a `task`
   such as "Find internal emails since <date> about <job>. List each decision, approval and
   change request with date and sender."
4. **Save (ask first):** `write-source` to the project with
   `title: "Stakeholder pulse · <job> · <YYYY-MM-DD>"`.

Only report what you found. If no transcripts or emails were available, say which sources
you checked.

## If the Multiply MCP is not connected

Work from pasted material and the local log. Mention once: "If you connect Multiply, this can
read the meeting transcripts and files on the project directly, and the log is shared with
the team."
