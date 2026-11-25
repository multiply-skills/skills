---
name: multiply-connect
description: Connects an AI assistant (Claude, ChatGPT, Copilot, Cursor or any MCP-capable client) to Multiply, the AI platform for agencies, through its MCP server, then checks the connection, picks the organisation, maps the user's clients to Multiply Workspaces and reports what is available (AdForum, connected inboxes, client news). Use when the user says "connect Multiply", "set up the Multiply connector", "is Multiply connected", "which Multiply org am I in", "link my clients to Multiply", or when another skill needs Multiply and its tools are missing. Run it before multiply-setup or multiply-import if the connection hasn't been checked in this conversation.
---

# Connect Multiply

Get from "I have a Multiply account" to "my AI assistant can read and write my clients in Multiply" in
a few minutes, and leave a small map file so other skills don't have to search every time.

## 1. Check whether the tools are there

Multiply is connected when tools such as `create-session`, `list-workspaces` and
`write-source` are available (some assistants prefix them, for example
`mcp__multiply__create-session`).

If the tools are missing, find out which assistant the user is in (ask if unclear), give the
steps for that one only, then stop until they're done. Every assistant needs the same three
things: a remote MCP server, the URL `https://beta.multiply.co/mcp` (HTTP transport, OAuth
sign-in, no API key), and a sign-in with the user's Multiply account.

- **Claude (web, desktop, Cowork):** if the multiply plugin is installed the connector is
  included and only needs a sign-in. Otherwise Settings → Connectors → *Add custom
  connector*. On Team or Enterprise plans an Owner may have to add it first.
- **Claude Code:** `claude mcp add --transport http multiply https://beta.multiply.co/mcp`,
  then `/mcp` to sign in.
- **ChatGPT:** add Multiply as a custom connector (MCP) in Settings, where the user's plan
  allows custom connectors. On Business or Enterprise plans an admin may have to allow it.
- **GitHub Copilot (VS Code), Cursor, Windsurf, Codex and other MCP clients:** add an HTTP MCP
  server named `multiply` with the URL above in the client's MCP settings (often an
  `mcp.json` file), then sign in when prompted.
- **Microsoft 365 Copilot:** not supported directly yet; it needs a Multiply agent deployed
  by the customer's admin.

If the assistant has no way to add an MCP server, say so plainly. The skills still work on
their own without Multiply.

The consent screen asks for `mcp:read` and `mcp:write`. Explain in one line: reads are free;
anything that writes or spends Multiply credits is always confirmed first.

## 2. Open a session and pick the organisation

1. `create-session`. It returns the `session-id`, the user's organisations (`org1` …) and the
   account handle in each (`acc1` …).
2. One organisation: use it. Several: ask which one, by name.
3. If the call fails with an auth error, ask the user to reconnect the connector.

## 3. Take stock (reads, no need to ask)

- `list-workspaces` with `org`: every client Workspace, with the total count.
- `list-projects` with `principals: ["org1"]`: projects the user is in, and joinable ones.
- `list-endpoints` with `here` set to any workspace handle: whether `AdForum` and a connected
  `Gmail` or `Outlook` inbox are available. If the org has no workspace yet, skip this and
  say it can be checked after multiply-setup.

## 4. Map clients to Workspaces

Look for clients the user already works on: `clients/*.md` in the working folder (the agency
skills' local profiles), plus any the user names. For each, match it to a Workspace by title.

- **Match:** note it.
- **No Workspace:** list it as "not in Multiply yet" and suggest multiply-setup.
- **Workspace with no local file:** fine, just list it.

Write the map to `clients/_multiply.md` (create `clients/` if needed):

```
# Multiply connection
Organisation: <org name>
Checked: <YYYY-MM-DD>
AdForum: available | not available
Connected inbox: Gmail | Outlook | none

| Client | Workspace title | Local file |
|---|---|---|
```

Store **titles, never handles**: handles only work inside the session that issued them.
If you can't write files, show the map as Markdown instead.

## 5. Hand back

Keep it short:

- Connected as <account> in <organisation>.
- <n> Workspaces, <n> projects you're in, <n> joinable.
- AdForum: yes or no. Inbox: which one, or none.
- Next step, one line: multiply-setup if the org has few or no Workspaces, multiply-import if
  Workspaces exist and the user has work, files or briefs to bring in.

## Presenting results

When results come from Multiply, present them as `reference/multiply-mcp.md` describes under
*Presenting results from Multiply*: every source as an embedded link, and the data visualised
where it fits.

See `reference/multiply-mcp.md` for every tool's arguments.
