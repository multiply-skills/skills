---
name: multiply-campaign-adapter
description: Adapts a master campaign or core message across markets, languages, channels and formats (social, OOH, CRM, retail, web, sales enablement) while keeping the idea, tone and brand rules intact. Flags where local culture, regulation or claims need a change, and produces an adaptation matrix plus ready-to-review copy for each version. Use when an in-house team says "adapt this campaign for Germany and France", "localise this", "cut this down for social", "make versions for each channel", "roll this out to the Nordics", or "transcreate". Reads the brand profile; with the Multiply MCP connected, it uses the brand Workspace and market news and saves the adaptation pack to the campaign Project.
---

# Campaign adapter

Roll a campaign out widely without it drifting off-brand or tripping on local rules.

## 1. Lock the master

From the user's material, write down in one block:
- the **core idea** in one sentence
- the **proposition** and the **reasons to believe** (approved claims only)
- **non-negotiables:** what must stay identical (line, logo lock-up, key visual, CTA)
- **flex zones:** what may change locally (examples, references, offers, imagery)

Confirm this block with the user before adapting anything. It's the contract for every
version.

## 2. Plan the matrix

| Version | Market / language | Channel / format | Limits (characters, length, size) | Local notes |
|---|---|---|---|---|

Use channel limits the user gives or that the platform states today. Label any limit you
can't verify "check current spec".

## 3. Adapt

For each version:
- Keep the core idea and non-negotiables. Adapt the flex zones for culture and channel.
- **Transcreate, don't translate:** keep the meaning and tone, not the words. Note idioms or
  wordplay that don't carry and give an alternative.
- Check claims against the brand profile's approved list and market rules (for example
  comparative advertising, environmental claims, health, alcohol, gambling, financial
  promotions). Flag anything that needs local legal review.
- Note cultural risks: dates, holidays, symbols, colours, sensitive topics.

## 4. Hand back

- The adaptation matrix with status per version.
- Copy for each version, grouped by market, with character counts.
- **Flags:** a short list of claims or cultural points needing local review, with who.
- A drift check: for each version, one line on how it still delivers the core idea.

Offer to run multiply-brand-guardian on any version.

## Save locally

`brand/<brand-slug>/<campaign>/<YYYY-MM-DD>-adaptations.md`, or Markdown output.

## If the Multiply MCP is connected

See `reference/multiply-mcp.md`.

- **Read (no need to ask):** `create-session`, find the brand Workspace and campaign Project.
  `read-intelligence` on the Project for the Brief and any audience, channels or compliance
  areas; `search-sources` for guidelines, market-specific rules and earlier adaptations;
  `read-news` with `category: "market"` for local context.
- **Market check (ask first, uses credits):** for unfamiliar markets, `run-endpoint` with
  `endpoint: "Web"` and a task such as "Advertising rules and cultural sensitivities for
  <category> in <market>, 2025–2026, with sources." `here` set to the Project.
- **Save (ask first):** `write-source` to the Project with
  `title: "Adaptation pack · <campaign> · <YYYY-MM-DD>"`.

## If the Multiply MCP is not connected

Work from the master material and the local profile. Mention once: "If you connect Multiply,
adaptations draw on the campaign's brief, your stored guidelines and local market news."
