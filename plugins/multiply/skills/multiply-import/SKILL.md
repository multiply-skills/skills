---
name: multiply-import
description: Moves what the user is working on into Multiply, in the right place, so the team can find and build on it. Takes content from the conversation (a draft, summary, analysis, meeting notes, a brief), files the user has (PDF, Word, PowerPoint, Excel, images), links, or a job from another tool, and adds it to the right client Workspace, Project or task, creating the Project first if the work doesn't have one yet. Use when the user says "add this to Multiply", "save this to Multiply", "import this", "put this in the X workspace", "add this to the project", "upload these files to Multiply", "add this brief as a project", "bring this job into Multiply", "move this from Asana/Monday/Notion into Multiply", or finishes a piece of client work that others will need. Needs the Multiply MCP.
---

# Import to Multiply

Get work out of a private chat, a desktop folder or another tool and into the right place in
Multiply, under a name the team will recognise. Keep it quick: one confirmation, then done.

## 1. Work out what is coming in

| What | How it goes in |
|---|---|
| **Content from this conversation** (a draft, summary, analysis, notes, a brief) | A document, with `write-source`. Doesn't count against file limits |
| **A file the user has** (PDF, deck, spreadsheet, image) | Uploaded as the original file, with `prepare-upload` and `add-files`, so Multiply reads the real thing, not a retyped copy |
| **A public or presigned https link to a file** | `add-files` with `urls` |
| **A job from another tool** (Asana, Monday, Linear, Notion, a drive, an email brief) | Read it with the tools connected to the assistant, then bring its brief and files in as below. The source tool stays as it is |

If it's unclear what "this" is, confirm in one line: "Add the brief rewrite above as a document?"
If the user points at several things, handle them together in one go.

## 2. Find the right place (reads, no need to ask)

1. If Multiply tools aren't available, run multiply-connect first. Then `create-session`. If the
   user has more than one organisation, ask which.
2. Find the client or brand from the conversation, the file names or `clients/_multiply.md` if it
   exists: `list-workspaces` with `title-contains`.
3. Look at its Projects: `list-projects` with `principals: ["ws1"]`.
4. Pick the level:
   - **Workspace:** about the client or brand in general (profile, brand guidelines, account notes,
     research that serves every job).
   - **Project:** about one job, campaign or pitch. This is the default for anything tied to
     specific work. Only Projects the user is a member of can be written to; a joinable one must
     be joined in Multiply first.
   - **Task:** only if the user names one.
5. **No Project for this work yet?** Offer to create one as part of the import (see step 3). Match
   by title first and never create a duplicate.
6. **No Workspace for the client?** Offer to create it with a one-line description, or suggest
   multiply-setup if several clients are missing.

## 3. Prepare

- **Title:** `[Type] · [Topic] · [YYYY-MM-DD]`, for example
  `Meeting notes · Q1 planning · 2026-11-20`. Up to 200 characters. Uploaded files keep their own
  file names.
- **Content:** clean Markdown. Keep the user's wording. Remove chat chatter ("Sure, here's…").
- **Citations:** `【N】` only for source handles returned in this session. Any other marker makes
  the whole write fail. Use plain links otherwise.
- **Versions:** sources can't be edited or deleted through the MCP. A new version is a new dated
  document whose first line reads "Supersedes [earlier title]".
- **New Project (only when needed):** a short title (up to 70 characters, the way the team names
  the job) and brief `instructions` in Markdown: the goal, deliverables, audience, timing and where
  it came from (for example "From Asana: Spring launch, imported 2026-11-20"). Mark anything
  inferred `(proposed)`. Use `joinable: true` for client work unless the user says otherwise, so the
  team can find it.

## 4. Confirm once, then import

Say in one or two lines what goes where, for example: "Adding 'Brief review · Spring launch ·
2026-11-20' and the client's brief PDF to the Spring launch project in the Acme workspace. OK?"
If a new Project is part of it, say so in the same line. Then:

**New Project:** `create-project` with `parent: "ws1"`, `title`, `instructions`, `joinable`.

**Documents:** `write-source` with `to`, `title`, `markdown`.

**Files:**
1. `prepare-upload` with `org` and each file's `name`, `mime` and `size` (up to 20 per call; PDF,
   Word, Excel, PowerPoint, text, Markdown, CSV, HTML, PNG, JPEG).
2. PUT each file's bytes to its `url` with exactly the headers returned, for example
   `curl -X PUT --upload-file [file] -H "[header]" "[url]"`. URLs expire after 15 minutes.
3. `add-files` with `to` and the `uploads` handles (or `urls` for links). `await` if an
   operation comes back.

If you can't run commands here (for example a chat assistant without code execution), say so and
offer two options: add the content as a document instead, or drag the file into Multiply's Files
panel.

Mention these when they apply:
- A Workspace or Project holds up to 20 uploaded files. Check with `list-sources` if it's close.
- Adding files to a **Workspace** re-runs its client news and brief proposals, and adding files to
  a **Project** updates its intelligence. Both use Multiply credits.

## 5. Hand back

One or two lines: what was added, its title, and where (Workspace › Project), with anything that
couldn't be read and why. If a new Project was created, add one optional next step: "Want
Multiply to write the Brief for it? That takes 10–15 minutes and uses credits." Only run
`generate-brief` if the user says yes.

## Presenting results

When results come from Multiply, present them as `reference/multiply-mcp.md` describes under
*Presenting results from Multiply*: every source as an embedded link, and the data visualised
where it fits.

See `reference/multiply-mcp.md` for every tool's arguments.
