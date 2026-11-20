# The Agency Pack: AI assistant skills from Multiply

Twenty-one free skills in the open [Agent Skills](https://agentskills.io) format (`SKILL.md`), for
Claude, ChatGPT, GitHub Copilot, Cursor, Codex or any assistant that reads skills or custom
instructions. For agencies and the people who run client work (strategists, account leads, new-business
teams and creative directors), and for in-house marketing, brand and creative teams. They come from [Multiply](https://multiply.co).

Generic marketing skills cover copywriting, SEO and ads. This pack covers the work that sits
around the work: knowing the client, sharpening the brief, winning the pitch, knowing what's
been done, keeping feedback and scope under control, and writing up the results for awards.

**Every skill works on its own.** The skills share a simple client file
(`clients/<client>.md` in your working folder), so what one skill learns about a client, the
others can use.

**Connect Multiply and the client memory becomes your team's.** The same skills read from and
write to each client's Multiply **Workspace** and **Projects**. That covers the shared profile,
the Brief, meeting transcripts and files, and weekly client news. Organisations with AdForum
enabled also get AdForum's archive of campaigns and award records.

## The skills

| Skill | Use it to | On its own | With Multiply connected |
|---|---|---|---|
| [`multiply-client-context`](plugins/multiply-agency/skills/multiply-client-context/SKILL.md) | Build and maintain a living client profile: business, audiences, brand, competitors, history, stakeholders | Web research + `clients/<client>.md` | Finds or creates the client's Workspace and saves the profile there. Reads back client news, files and project intelligence |
| [`multiply-brief-sharpener`](plugins/multiply-agency/skills/multiply-brief-sharpener/SKILL.md) | Critique a client brief, rewrite it with a single-minded proposition, and draft questions for the client | Rubric, rewrite and questions | Grounds the brief in the client's Workspace and sets the job up as a Project. Multiply generates the Brief and intelligence and suggests next tasks |
| [`multiply-pitch-prep`](plugins/multiply-agency/skills/multiply-pitch-prep/SKILL.md) | Prepare a prospect dossier with opening provocations and matching credentials | Web research + your case studies | Runs Multiply's deep research, matches credentials from your agency's own files, adds AdForum campaigns from the category, and keeps watching the prospect |
| [`multiply-creative-precedents`](plugins/multiply-agency/skills/multiply-creative-precedents/SKILL.md) | Map a category's creative codes, standout work, award winners and white space before ideation | Web search with honest coverage caveats | Searches AdForum's campaign and awards archive (where enabled) and saves the map to the Project |
| [`multiply-idea-test`](plugins/multiply-agency/skills/multiply-idea-test/SKILL.md) | Test an idea or creative direction against recent category campaigns, similar brands and award winners: matches, category codes, award benchmark, risks and a Go / Strengthen / Rethink verdict | Web search with honest coverage caveats | Checks it against AdForum's campaign and awards archive (where enabled) and saves the test to the Project |
| [`multiply-client-pulse`](plugins/multiply-agency/skills/multiply-client-pulse/SKILL.md) | Consolidate client feedback, flag scope creep against the brief or SOW, and read relationship health | Pasted threads/notes + a running feedback log | Reads the Project's Brief, plus meeting transcripts and files in Multiply. Searches a connected Gmail or Outlook inbox and keeps the log shared |
| [`multiply-award-entry-writer`](plugins/multiply-agency/skills/multiply-award-entry-writer/SKILL.md) | Draft Cannes Lions, D&AD, One Show, Effie or Epica entries to each show's criteria and limits, and flag missing evidence | Your case material | Pulls the brief and results from the Project and benchmarks against past winners in AdForum |

## Multiply skills (need Multiply connected)

Six more skills for teams that use Multiply. They set it up around your real clients and
keep it useful.

| Skill | Use it to |
|---|---|
| [`multiply-connect`](plugins/multiply/skills/multiply-connect/SKILL.md) | Connect the MCP, pick the organisation, map your clients to Workspaces and see what's available (AdForum, inbox) |
| [`multiply-setup`](plugins/multiply/skills/multiply-setup/SKILL.md) | Create Workspaces for your 3–5 most important clients, with descriptions, key files and a first client news run |
| [`multiply-import-work`](plugins/multiply/skills/multiply-import-work/SKILL.md) | Bring active jobs from briefs, Asana, Monday, Linear, Notion or email into Multiply as Projects with the right intelligence areas |
| [`multiply-save`](plugins/multiply/skills/multiply-save/SKILL.md) | Save a chat output or upload files to the right Workspace, Project or task |
| [`multiply-adforum-search`](plugins/multiply/skills/multiply-adforum-search/SKILL.md) | Search AdForum's campaign and awards archive by brand, agency, category, market, year or show |
| [`multiply-tune-workspace`](plugins/multiply/skills/multiply-tune-workspace/SKILL.md) | Monthly health check: stale files, unopened news, waiting proposals, inactive projects, then fix what you approve |

Suggested order for a new user: multiply-connect, multiply-setup, multiply-import-work. Then
multiply-tune-workspace once a month.

## Install

The repo is a plugin marketplace with three plugins:

- **multiply**: the 6 Multiply skills plus the Multiply connector (needs a Multiply account).
- **multiply-agency**: the 7 agency skills. They work without Multiply and use it when the
  multiply plugin is installed.

- **multiply-in-house**: 9 skills for in-house marketing, brand and creative teams (see
  [its README](plugins/multiply-in-house/README.md)).

### Claude Code
```bash
/plugin marketplace add multiply-skills/skills
/plugin install multiply-agency@multiply-skills
/plugin install multiply-in-house@multiply-skills
/plugin install multiply@multiply-skills     # if you use Multiply
```
Then run `/mcp` and sign in to Multiply.

### Cowork (Claude desktop)
Install the `.plugin` file for each plugin (`dist/multiply.plugin`, `dist/multiply-agency.plugin`,
`dist/multiply-in-house.plugin`)
from a Cowork chat. On Team and Enterprise plans an org owner can add the plugins to the
organisation's catalogue so everyone can install them.

### Other assistants (ChatGPT, GitHub Copilot, Cursor, Codex and others)
The skills are plain Markdown with no Claude-specific features, and Multiply is a standard
remote MCP server.
- **Assistants that read `SKILL.md` skills** (for example GitHub Copilot in VS Code, Cursor,
  Codex): copy the skill folders from `plugins/*/skills/` into the assistant's skills folder.
- **Assistants without skills support** (for example a custom GPT or a ChatGPT project):
  paste the `SKILL.md` body into its instructions, and upload `reference/multiply-mcp.md` as a
  knowledge file.
- **Multiply:** add `https://beta.multiply.co/mcp` as a remote MCP server (HTTP, OAuth sign-in)
  wherever the assistant supports custom connectors.

### Claude (web)
Claude.ai takes one skill per zip: Settings → Capabilities → Skills, upload each skill
folder as a zip. Add the Multiply connector separately (see below). On claude.ai the skills
can't keep files between chats, so they hand you the client file as Markdown to paste back in.

## Connect Multiply (optional)

You need a Multiply account. You sign in with it through OAuth, so there is no API key to
manage. Claude then works as you, with access to what you can open in your Multiply
organisations.

**Server URL:** `https://beta.multiply.co/mcp`

**Claude (web or desktop):** go to Settings → Connectors → *Add custom connector*, paste the
server URL, and sign in with your Multiply account. See Anthropic's guide:
[custom connectors with remote MCP](https://support.claude.com/en/articles/11175166-get-started-with-custom-connectors-using-remote-mcp).

**Claude Code:**
```bash
claude mcp add --transport http multiply https://beta.multiply.co/mcp
```
Then run `/mcp` in Claude Code and sign in when prompted.

**What you allow** (Multiply's consent screen asks for):
- `mcp:read`: read your organisations, Workspaces, Projects, tasks and sources.
- `mcp:write`: make changes as you, such as creating Workspaces and Projects, editing
  Briefs and saving documents.

The skills read freely. They **always ask before writing** or before starting anything that
uses Multiply credits, such as deep research, AdForum searches or Brief generation. Everything
they save is a new dated document, so earlier versions are never overwritten.

Sign-ins are kept for about 30 days at a time and refresh automatically.

### AdForum
AdForum is an archive of advertising campaigns with award records from Cannes Lions, D&AD,
The One Show and others. The skills check whether your organisation has it and use it only if so. Otherwise they
fall back to the open web.
It is being enabled for all Multiply organisations.

## How the pack maps to Multiply

| In the pack | In Multiply |
|---|---|
| `clients/<client>.md` | The client's **Workspace** (profile saved as a dated document, plus the Workspace description) |
| A job, campaign or pitch | A **Project** with Instructions, a Brief, intelligence areas and suggested next tasks |
| Briefs, dossiers, precedent maps, idea tests, pulse reports, award entries | Dated documents saved to the Workspace or Project, searchable by your whole team |

Each skill folder includes `reference/multiply-mcp.md`, which lists the Multiply tools it uses.

## Privacy
Without Multiply, nothing leaves your conversation except what your assistant's own tools send
(for example, web searches). With Multiply, the skills only read and write what your Multiply
account can already access, and ask before every write.

---
*Draft v0.1 · MIT licence*
