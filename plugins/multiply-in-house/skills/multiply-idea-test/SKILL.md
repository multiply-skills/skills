---
name: multiply-idea-test
description: Stress-tests a creative idea, campaign concept or creative direction against what is already out there before it is presented or produced. It compares the idea with recent campaigns in the same category, work by similar brands and competitors, and award winners (Cannes Lions, D&AD, The One Show, Effies) that used the same mechanic in any category. It returns, per idea, close and partial matches, how it sits against the category's codes, an award benchmark, risks, a Go / Strengthen / Rethink verdict and concrete moves to make it more distinct. Use when the user says "test this idea", "validate this creative direction", "has this been done?", "is this original?", "is this too close to anything?", "how does this compare to award winners?", "pressure-test our routes", or shares concepts, scripts, manifestos or route decks for a sanity check. Works for agency teams and in-house brand teams. Standalone it uses web search with honest coverage caveats. When the Multiply MCP is connected and AdForum is enabled, it searches AdForum's campaign and awards archive and saves the test to the Project.
---

# Idea test

Find out what an idea is up against before the client, the boss or the jury does. The output is
a stress test that makes the idea stronger, not a verdict on taste.

## Non-negotiables

- **Never invent a campaign, agency, award or year.** Every match names the brand, campaign,
  year, agency (if known), market and a source. If you can't verify it, leave it out or label it
  "unverified".
- **Absence of evidence isn't proof the idea is new.** Always say which sources were searched and
  what they are likely to miss.
- **Judge the mechanic, not the surface.** Two ideas with different visuals can be the same idea;
  two ideas with the same visual can be different.
- **Be useful, not harsh.** Every weakness comes with a move that fixes it. "Similar to X" doesn't
  kill an idea by itself: say how famous X is in this audience's market, how recent, and how close.
- Treat ideas as confidential. Search for the mechanic and the category, never paste the full
  concept into a public search.

## 1. Frame (ask only what you can't infer)

- **The ideas:** one or several routes. Accept anything: a line, a script, a manifesto, a mood
  board description, a deck.
- **Brand, category and competitors.** Read the profile if there is one: `clients/<client-slug>.md`
  for agencies, `brand/<brand-slug>.md` for in-house teams, or the Multiply Workspace.
- **Markets and audience**, and the **objective** (awareness, launch, behaviour change, fame,
  awards).
- **Time window:** recent work = the last 3 years; award benchmark = the last 5 years, unless the
  user says otherwise.

Ask at most two questions. If the brand or category is missing and can't be inferred, ask for it:
the test is meaningless without it.

## 2. Break each idea down

For every idea, write three short lines before searching:

- **Core mechanic:** what the idea *does*, in plain words, without execution details
  (for example "the product is hidden in famous artworks and people hunt for it").
- **Territory:** the insight, tension or claim it stands on (for example "freedom from routine").
- **Execution codes:** the tone, visual world, format and channels it relies on.

Show these to the user in the output so they can correct a misreading.

## 3. Build the comparison set

Search through three lenses. Run many narrow searches rather than one broad one.

| Lens | What you are looking for | Default window |
|---|---|---|
| **A. Category now** | Recent campaigns in the same category and markets: what is running, the dominant codes, the clutter the idea has to cut through | Last 3 years |
| **B. Similar brands** | Direct competitors, plus brands with a similar positioning or audience in adjacent categories | Last 3 years |
| **C. Award benchmark** | Award winners in the category, and winners in *any* category that used the same mechanic or territory | Last 5 years |

Standalone sources: award-show winner archives, Effie case studies, trade press (Ad Age, Campaign,
The Drum, Adweek, LBBOnline, Contagious), agency case pages, brand channels and ad libraries (Meta
Ad Library, Google Ads Transparency). Open each page before citing it.

## 4. Assess each idea

| Test | Question | Rating |
|---|---|---|
| **Originality** | Has this mechanic been done, in this category or elsewhere? | Clear / Echoes / Done before |
| **Category codes** | Does it follow the category's conventions or break them? | Breaks / Bends / Follows |
| **Brand fit (swap test)** | Could a competitor run it unchanged by swapping the logo? | Owned / Partly owned / Swappable |
| **Award benchmark** | Compared with winners using similar mechanics: is the insight as sharp, the craft as ambitious, the scale or results story as strong? | Above / On par / Below the bar |
| **Risks** | Too close to a famous campaign, cultural or regulatory flags for the markets, timing (a competitor ran something similar recently) | Listed, or "none found" |

Then give a **verdict**:

- **Go:** distinct, owned and at or above the bar. Note what to protect in production.
- **Strengthen:** the core is good but it echoes existing work or falls below the bar. Give the
  specific changes.
- **Rethink:** done before by a famous campaign in the audience's market, or fully swappable.
  Say what is worth keeping.

Always finish each idea with **3 moves to make it more distinct**, grounded in what the
comparison set showed (for example "every winner in this space had a real product demonstration;
this route has none").

When there are several routes, end with a short **ranking** and a one-line reason for each.

## 5. Write it up

Use `templates/idea-test.md`. Lead with the verdicts, then the evidence.

Save locally to `clients/<client-slug>/<YYYY-MM-DD>-idea-test-<topic>.md` (agency) or
`brand/<brand-slug>/<YYYY-MM-DD>-idea-test-<topic>.md` (in-house), or output Markdown if you can't
write files.

## If the Multiply MCP is connected

When results come from Multiply, present them as `reference/multiply-mcp.md` describes under
*Presenting results from Multiply*: every source as an embedded link, and the data visualised
where it fits.

See `reference/multiply-mcp.md` for every tool's arguments.

1. `create-session`, then find the client or brand: `list-workspaces` (`title-contains`) and
   `list-projects` (`principals: ["ws1"]`). If there is no matching Project, use the Workspace, or
   a private task (`create-task` with `parent: "acc1"`) for a quick test.
2. **Read what is already known (no need to ask):**
   - `read-intelligence` on the Project. Use its Brief and the `competitors`, `category` and
     `campaign-history` areas where present.
   - `read-news` on the Workspace with `category: "competitor"` for what competitors launched
     recently.
   - `search-sources` with `principals: ["ws1", "prj1"]` for earlier precedent maps or idea tests,
     so you don't repeat a search that was already done.
3. **AdForum:** call `list-endpoints` with `here: "prj1"` (or the handle you chose).
   - If `AdForum` is listed, tell the user what you will search and that it uses Multiply credits
     and takes a few minutes, and ask first. Then call `run-endpoint` with `endpoint: "AdForum"`,
     `here`, `wait: 300`, and a self-contained `task` (the driver sees nothing of this
     conversation). Keep it to **two runs at most**:
     - **Run 1, lenses A and B:** "Campaigns from 2023 to 2026 in the [category] category in
       [markets], including [brand] and [competitors]. For each, give the brand, title, year,
       agency, country, media, a one-line description of the idea, and any awards with their
       level."
     - **Run 2, lens C:** "Award-winning campaigns from 2021 to 2026, in any category, whose core
       idea is one of the following: [mechanic 1]; [mechanic 2]. Also include award winners in the
       [category] category. For each, give the brand, title, year, agency, country, media, the
       core mechanic in one line, and awards with their level."
     Describe mechanics in neutral words, never paste the full confidential concept. Add `context`
     (a two-line brief summary) and `focus` (for example "closeness of the core mechanic, and award
     level").
   - `await` an `op1` if one is returned, then `read-source` (`account: "acc1"`) each report
     handle. Merge with any web findings, and credit AdForum's trend write-ups to AdForum.
   - If `AdForum` isn't listed, say so once and continue with web search.
4. **Save (ask first):** `write-source` with `to: "prj1"` (or the Workspace) and
   `title: "Idea test · [topic] · [YYYY-MM-DD]"`. Sources are append-only, so each re-test is a new
   dated document. Cite the AdForum reports with `【N】` using their source handles from this
   session; use plain links for everything else.

## If the Multiply MCP is not connected

Use web search and add a "Coverage" line: web search finds famous and recent work well, but misses
older, non-English and less publicised work, and its award data is patchy. Without web access,
work only from what you reliably know, mark every match "verify before use", and keep the list
short. Mention once: "If you connect Multiply with AdForum enabled, this can check the idea against
a licensed archive of campaigns and award records instead of the open web."

## Related skills

- **multiply-creative-precedents** (agency plugin): a full map of a category's codes, standout work
  and white space, best *before* ideation. This skill is for testing ideas *after* they exist.
- **multiply-adforum-search** (multiply plugin): a direct AdForum lookup by brand, agency, show or
  year.
