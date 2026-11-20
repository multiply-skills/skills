# Multiply MCP: quick reference

Use this file only when the Multiply MCP server is connected. You can tell because tools
such as `create-session`, `list-workspaces` and `write-source` are available. Some assistants
add a prefix to the tool names, for example `mcp__multiply__create-session`.
This file uses the bare names.

## How Multiply is organised

Organisation → **Workspace** (normally one per client or prospect) → **Project** (a job,
campaign or pitch) → Task. Files and notes on a Workspace give context to every Project
inside it. Each Project has **Instructions**, a **Brief**, **intelligence areas** (chosen per
brief from a catalogue of 15, see `update-areas`) and suggested next
tasks, called Drafts. Each Workspace has a weekly **client news** run and weekly **brief
proposals**.

## Session and handles

1. Call `create-session` first. It takes no arguments and returns a `session-id`, the
   account's organisations (`org1` …) and the account's handle in each one (`acc1` …).
2. Pass `session-id` to every other tool.
3. Short handles name everything: `org1`, `acc1`, `ws1`, `prj1`, `t1`, a source number such
   as `18`, or a section such as `18.2.1`. A handle only works in the session that issued it,
   so look handles up again in every new session.
4. If a call is still running when its `wait` ends (default 60 s, maximum 600 s), it returns
   an operation handle such as `op1`. Pass that to `await` with `operation` and `wait`.
5. If the user belongs to more than one organisation, ask which one to use.

## Tools

| Tool | Key arguments | Gives you |
|---|---|---|
| `create-session` | none | session-id, orgs, account handles |
| `list-workspaces` | `org`, `title-contains?` | workspaces (`ws1` …) |
| `create-workspace` | `org`, `title` (≤70), `description?` (≤2,000) | new workspace handle |
| `update-workspace` | `workspace`, `title?`, `description?` | nothing |
| `read-news` | `workspace`, `category?` (`market`/`trends`/`competitor`), `limit?` | client-news digest and items |
| `list-proposals` / `read-proposal` | `workspace` (+ `proposal` id) | weekly project proposals based on client news |
| `update-proposal` | `workspace`, `proposal`, `status` (`new`/`saved`/`archived`) | nothing |
| `start-proposal` | `workspace`, `proposal`, `instructions?`, `sections?`, `accept?`, `wait?` | starts a proposal as a project and builds its intelligence (10–15 minutes, uses credits) |
| `run-workspace` | `workspace`, `run` (`client-news`/`brief-proposals`), `wait?` | runs a Workspace's news or proposals now. A new Workspace runs nothing until its weekly schedule. Uses credits |
| `list-projects` | `principals` ([`org1`] or [`ws1`]), `title-contains?` | projects, each marked member or joinable |
| `create-project` | `parent` (org or ws), `title` (≤70), `instructions?` (Markdown, ≤20,000), `joinable?` | new project handle |
| `update-project` | `project`, `instructions?`, `title?`, `parent?` | nothing |
| `read-intelligence` | `project` | Brief (summary, sections `sec-…`, deliverables `del-…`), intelligence areas, Drafts |
| `generate-brief` | `project`, `wait?` | builds the Brief and intelligence from Instructions and files. The first run takes 10–15 minutes and uses Multiply credits. Running it again replaces any manual edits to the Brief |
| `update-brief` | `project`, `summary?`, `sections?` [{`section`, `title?`, `text?`}], `add-deliverables?`, `remove-deliverables?` | edits an existing Brief. It cannot add or remove sections |
| `update-areas` | `project`, `add?` (catalogue ids), `remove?`, `wait?` | adds or removes intelligence areas. Catalogue: audience, brand, category, culture, competitors, media-landscape, channels, product-and-offer, commercial-context, campaign-history, measurement, stakeholders, compliance, sustainability-and-impact, partnerships-and-talent. Adding uses credits; removing deletes findings and needs the user's confirmation |
| `dismiss-draft` | `project`, `draft` (`dft-…`) | removes a suggested next task |
| `list-sources` | `principals`, `status?`, `limit?`, `cursor?` | files, documents, reports and meeting transcripts held by those handles |
| `search-sources` | `principals`, `query`, `limit?` | matches by meaning, with section handles |
| `prepare-upload` | `org`, `files` [{`name`, `mime`, `size`}] (≤20) | upload slots (`up1` …) with a URL to PUT each file's bytes to, valid 15 minutes |
| `add-files` | `to` (ws, prj or task), `uploads?`, `urls?`, `sources?`, `wait?` | adds files. Up to 20 uploaded files per Workspace or Project. On a Workspace it re-runs client news and proposals; on a Project it updates intelligence |
| `read-source` | `account` (`acc1`), `handle`, `through?`, `max-tokens?` | a source as Markdown |
| `write-source` | `to` (ws, prj or task), `title` (≤200), `markdown` (≤100,000) | saves a Markdown document as a source and returns its handle |
| `create-task` | `parent` (prj or `acc1` for a private task), `title?` | an empty task handle, useful as `here` for a one-off run |
| `list-tasks` / `read-task` | `principals` / `task` | tasks and their conversations |
| `list-endpoints` | `here`, `principals?` | what `run-endpoint` can run on, such as `Web`, `AdForum`, or a connected `Gmail` or `Outlook` inbox |
| `run-endpoint` | `endpoint`, `task`, `here`, `principals?`, `focus?`, `context?`, `mode?` | a cited report saved at `here` |
| `run-research` | `prompt`, `here`, `principals?`, `agent?` | an in-depth cited research report, taking 5–15 minutes |
| `await` | `operation`, `wait?` | the result of a long call |

## Rules

- **`write-source` is append-only.** Nothing in the MCP edits or deletes a source, and
  writing the same title and text a second time does nothing. Always write a new **dated**
  document, for example `Client profile · Acme · 2026-11-20`. When it replaces an earlier
  one, say so in the first line: "Supersedes …".
- **Citation brackets.** In `write-source`, `【18】` cites source 18 and must name a real
  source handle from this session. If it names one that doesn't exist, nothing is written. Use
  plain links everywhere else.
- **Each handle only covers its own sources.** A workspace handle does not search its
  projects' sources, so pass both, for example `principals: ["ws1", "prj1"]`.
- **Reads are fine to run without asking.** Ask before anything that creates something,
  edits a Brief, or uses credits (`generate-brief`, `run-research`, `run-endpoint`,
  `run-workspace`, `start-proposal`, `update-areas`). Tell the user where the output will be saved.
- **No edits or deletes for files, projects or Workspaces.** The MCP can't delete sources or
  archive projects and Workspaces. Send the user to Multiply for those.
- **Project tools need membership.** A project marked "joinable" has to be joined in
  Multiply before you can use it.
- **AdForum** is AdForum's archive of advertising campaigns and award records. It is an
  endpoint that you call with `run-endpoint`, not a tool of its own, and Multiply enables
  it per organisation. Use it only if `list-endpoints` lists `AdForum`. Always call it
  "AdForum".
- **Email** is not stored as sources. If the user has connected Gmail or Outlook in Multiply,
  `list-endpoints` with `principals: ["acc1"]` shows it, and `run-endpoint` searches it live
  and saves a report.
