---
name: multiply-brand-context
description: Builds and maintains the in-house team's living brand profile for its own company, one per brand, business unit or market: positioning, audiences, tone of voice, visual and verbal rules, claims that are approved or banned, products, priorities, stakeholders and approvers. Built from brand guidelines, strategy decks, intranet pages, briefs and web research. Use when an in-house marketing, brand or creative team says "set up our brand profile", "what are our brand rules", "remember this about our brand", "update the tone of voice", or pastes brand material to keep. The other in-house skills (intake-triage, brand-guardian, agency-brief, campaign-adapter, idea-test) read this profile. Saves to a local brand/X.md file, or to the brand's Multiply Workspace when the Multiply MCP is connected.
---

# Brand context

One current, trusted source of truth for the brand, so every request, agency brief and review
starts from the same rules.

## Where the profile lives

- **Standalone:** `brand/<brand-slug>.md` in the working folder, one per brand, sub-brand,
  business unit or market. Longer documents go in `brand/<brand-slug>/`.
- **With Multiply connected:** the brand's **Workspace** (see below).

Check for an existing profile first. Never create a second one for the same brand.

## 1. Gather

- Read what the user provides: brand guidelines, brand book, strategy decks, messaging
  frameworks, legal claim lists, intranet pages.
- With web access, check how the brand presents itself today: site, social, current campaigns,
  recent press.
- Ask **at most three** questions, only ones that change the profile, for example who signs
  off brand work, which markets are in scope, or what this year's priorities are.

## 2. Write or update

Sections, in this order:

1. **Brand in one paragraph:** what it is, for whom, why it wins.
2. **Positioning and proposition.**
3. **Audiences:** each as a person with a need, not demographics only.
4. **Tone of voice:** 3–5 traits, each with a do and a don't example.
5. **Verbal rules:** naming, spelling, words to use and avoid, taglines and how to use them.
6. **Visual rules:** logo, colour, type, imagery, in short. Link to the full guidelines.
7. **Claims:** approved claims with their proof and owner; banned or restricted claims.
8. **Products and portfolio** that marketing covers.
9. **Priorities this year.**
10. **Stakeholders and approvers:** by role, who must say yes to what.
11. **Open questions.**
12. **Change log.**

Rules:
- Tag every non-obvious fact with its source and date: `(brand book v3, 2026-03)`,
  `(legal claims list, 2026-09)`, `(assumption)`.
- Mark each rule **approved** (signed off) or **proposed** (inferred or suggested). The other
  skills only enforce approved rules as rules, and treat proposed ones as guidance.
- Never silently drop a fact. Move outdated ones to the change log as "superseded".
- When sources conflict, keep both, flag it, and add it to open questions.

## 3. Hand back

Show the profile or what changed, then three lines: what you assumed, what's missing, who
should approve what.

## If the Multiply MCP is connected

See `reference/multiply-mcp.md`.

1. `create-session`, then `list-workspaces` with `title-contains: "<brand>"`.
2. No Workspace: ask before `create-workspace` with the brand name and a description that
   says what the brand sells, to whom, in which markets, its main competitors and the topics
   the team tracks. The description steers the Workspace's weekly client news, which for an
   in-house team is news about its own brand, market and competitors.
3. Read (no need to ask): `search-sources` with `principals: ["ws1"]` for guidelines and
   claims, `read-news`, and `read-intelligence` on active projects.
4. Save (ask first): `write-source` with `to: "ws1"` and
   `title: "Brand profile · <Brand> · <YYYY-MM-DD>"`. Sources are append-only, so each update
   is a new dated document whose first line reads "Supersedes …". Upload the real brand
   guidelines file with multiply-save so the original is always there.
5. If the summary changed, `update-workspace` with the new description.

## If the Multiply MCP is not connected

Use the local file. If you can't write files, output one Markdown block to save. Mention once:
"If you connect Multiply, this profile becomes the brand's shared Workspace for the whole
team, and its weekly news keeps an eye on your market and competitors."
