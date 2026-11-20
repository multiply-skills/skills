---
name: multiply-save
description: Saves work from the current conversation into Multiply so the whole team can find and build on it, as a document on a client's Workspace, a Project or a task. Handles content the assistant wrote (summaries, drafts, analyses, meeting notes, briefs) and real files (PDF, Word, PowerPoint, Excel, images). Use when the user says "save this to Multiply", "put this in the X workspace", "add this to the project", "upload these files to Multiply", "store this for the team", or finishes a piece of client work that others will need. Needs the Multiply MCP.
---

# Save to Multiply

Get finished work out of a private chat and into the client's shared memory, in the right
place, under a name the team will recognise.

## 1. Work out what is being saved

- **Content the assistant wrote or can write** (a summary, draft, analysis, notes, a brief):
  saved as a document with `write-source`. Doesn't count against file limits.
- **A file the user has** (PDF, deck, spreadsheet, image): uploaded with `prepare-upload`
  and `add-files`, so Multiply reads the original rather than a retyped copy.
- **A file at a public or presigned https URL:** `add-files` with `urls`.

If it's unclear what "this" is, confirm in one line: "Save the brief rewrite above as a
document?"

## 2. Find the destination (reads)

1. `create-session`. If the user has more than one org, ask which.
2. Use the client named in the conversation, or `clients/_multiply.md` if it exists, to
   find the Workspace (`list-workspaces` with `title-contains`).
3. Decide the level:
   - **Workspace:** about the client in general (profile, brand guidelines, account notes).
   - **Project:** about one job (`list-projects` with `principals: ["ws1"]`). Only projects
     the user is a member of can be written to; a joinable one must be joined in Multiply
     first.
   - **Task:** only if the user names one.
4. If no Workspace or Project fits, offer to create one (ask first) or suggest multiply-setup.

## 3. Prepare

- **Title:** `<Type> · <Topic> · <YYYY-MM-DD>`, for example
  `Meeting notes · Q1 planning · 2026-11-20`. Up to 200 characters.
- **Content:** clean Markdown. Keep the user's wording. Remove chat chatter ("Sure, here's…").
- **Citations:** `【N】` only for source handles returned in this session. Any other marker
  makes the whole write fail. Use plain links otherwise.
- **Versions:** sources can't be edited or deleted through the MCP. A new version is a new
  dated document whose first line reads "Supersedes <earlier title>".

## 4. Confirm, then save

Say in one line what goes where: "Saving 'Brief review · Spring launch · 2026-11-20' to the
Spring launch project in the Acme workspace. OK?" Then:

**Documents:** `write-source` with `to`, `title`, `markdown`.

**Files:**
1. `prepare-upload` with `org` and each file's `name`, `mime` and `size` (up to 20 per call;
   PDF, Word, Excel, PowerPoint, text, Markdown, CSV, HTML, PNG, JPEG).
2. PUT each file's bytes to its `url` with exactly the headers returned, for example
   `curl -X PUT --upload-file <file> -H "<header>" "<url>"`. URLs expire after 15 minutes.
3. `add-files` with `to` and the `uploads` handles. `await` if an operation comes back.

If you can't run commands here (for example a chat assistant without code execution), say so and
offer two options: save the content as a document instead, or drag the file into Multiply's
Files panel.

Watch-outs to mention when they apply:
- A Workspace or Project holds up to 20 uploaded files. Check with `list-sources` if close.
- Adding files to a **Workspace** re-runs its client news and brief proposals; adding to a
  **Project** updates its intelligence. Both use credits.

## 5. Hand back

One or two lines: what was saved, its title, and where (Workspace › Project). If a file
couldn't be read, name it and why.

See `reference/multiply-mcp.md` for every tool's arguments.
