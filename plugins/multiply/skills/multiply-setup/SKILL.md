---
name: multiply-setup
description: Sets up Multiply around the user's real clients in one guided run, so the first time they open it they see their own clients with relevant files, client news and project proposals instead of an empty app. Finds the user's clients (from what they say, local client files, or connected calendar, email and drive), creates one Workspace per client with a useful description, adds key client files, and runs client news. Use when the user says "set up Multiply", "get me started in Multiply", "add my clients to Multiply", "onboard me", or has just connected Multiply and has few or no Workspaces. Needs the Multiply MCP.
---

# Multiply setup

The aim is one moment: the user opens Multiply and it already knows their clients and has
found something relevant about each one this week.

Start small. Three to five active clients done well beat twenty empty Workspaces.

## 1. Check the connection

If Multiply tools aren't available or the org isn't chosen, run multiply-connect first.
Then `create-session` and `list-workspaces` to see what already exists. Never create a
duplicate: match on client name, including obvious variants ("Acme" vs "Acme Foods Ltd").

## 2. Find the clients

Use what is available, in this order, and stop as soon as you have a good list:

1. Clients the user names.
2. `clients/*.md` in the working folder, and `clients/_multiply.md` if it exists.
3. Other tools connected to the assistant, reads only: recent calendar meetings with external
   attendees, frequent external email domains, client folders in a drive.

Show a short list, client and why you think it's a client (for example "8 meetings in 30
days"), and ask the user to pick the 3–5 that matter most right now. Ask nothing else yet.

## 3. Draft each Workspace

For each chosen client, draft:

- **Title:** the client's name as the team says it (up to 70 characters).
- **Description** (up to 2,000 characters), which shapes client news and proposals, so make
  it specific:
  - what the client sells, to whom, in which markets
  - what the agency does for them (services, current mandates)
  - main competitors to watch
  - topics the team cares about (for example "sustainability claims in packaging")
  Use the local client profile if there is one, and a quick web check for the basics. Mark
  guesses so the user can correct them.
- **Files to add (optional):** up to a handful of the most useful client documents the user
  can point to, such as brand guidelines, the current brief or the last strategy deck. Quality
  over volume: each Workspace holds up to 20 uploaded files.

Show all drafts together and let the user edit them in one pass.

## 4. Create (ask first, once for the whole batch)

Explain: creating Workspaces is free; client news and file processing use Multiply credits
and take a few minutes. Then, per client:

1. `create-workspace` with `org`, `title`, `description`.
2. If there are files: upload them as multiply-import describes (`prepare-upload`, PUT,
   `add-files` with `to: "ws1"`). Adding files to a Workspace already re-runs its client
   news and brief proposals, so skip step 3 for that client.
3. Otherwise: `run-workspace` with `run: "client-news"`. Nothing runs on a new Workspace
   until its weekly schedule, so this is what makes it useful today. Use `wait: 0` and
   collect the operations, so all clients run in parallel. A run is refused while one of
   the same kind is already going (for example right after `add-files`): treat that as
   "already running", not an error, and don't retry.
4. `await` the operations, then `run-workspace` with `run: "brief-proposals"` for the same
   Workspaces, so the proposals draw on the fresh news. `await` those too.

## 5. Show what Multiply found

For each client, from `read-news` and `list-proposals`:

- the two or three most relevant news items, one line each on why they matter
- any project proposal worth a look

Then suggest one concrete next step per client, for example: start a proposal as a project,
or bring an active job, brief or the client profile in with multiply-import.

## 6. Leave a record

Update `clients/_multiply.md` (see multiply-connect) with the new Workspace titles. Tell the
user: client news and proposals now refresh weekly by themselves.

See `reference/multiply-mcp.md` for every tool's arguments.
