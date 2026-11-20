# Multiply in-house pack

Nine free AI assistant skills (open `SKILL.md` format: Claude, ChatGPT, Copilot, Cursor, Codex)
for in-house marketing, brand and creative teams, from
[Multiply](https://multiply.co). Their client is the business, so the work is intake, brand
governance, managing agencies and proving value.

Every skill works on its own with a simple local brand file (`brand/<brand>.md`). Install
the **multiply** plugin and connect Multiply, and the same skills read from and write to each
brand's Multiply **Workspace** and **Projects**, shared with the whole team.

| Skill | Use it to |
|---|---|
| [`multiply-brand-context`](skills/multiply-brand-context/SKILL.md) | Keep one living brand profile per brand, business unit or market: tone, rules, approved claims, approvers |
| [`multiply-intake-triage`](skills/multiply-intake-triage/SKILL.md) | Turn a stakeholder request into a brief, triage it (do now, schedule, push back, agency, self-serve) and reply |
| [`multiply-brand-guardian`](skills/multiply-brand-guardian/SKILL.md) | Review work against the brand and claims, with a verdict, fixes and a corrected version |
| [`multiply-agency-brief`](skills/multiply-agency-brief/SKILL.md) | Brief external agencies, then score their responses and write consolidated feedback |
| [`multiply-stakeholder-pulse`](skills/multiply-stakeholder-pulse/SKILL.md) | Consolidate internal feedback, track approvals and settle conflicting asks |
| [`multiply-competitor-watch`](skills/multiply-competitor-watch/SKILL.md) | A running digest of competitor and category comms, with a "so what" for the brand |
| [`multiply-idea-test`](skills/multiply-idea-test/SKILL.md) | Test a creative idea or agency route against recent category work, similar brands and award winners, with a verdict and moves to make it distinct |
| [`multiply-campaign-adapter`](skills/multiply-campaign-adapter/SKILL.md) | Adapt a master campaign across markets, languages and channels without drifting off-brand |
| [`multiply-impact-report`](skills/multiply-impact-report/SKILL.md) | Report to leadership on what the team delivered, achieved and saved versus agency spend |

**Also useful for in-house teams:** `multiply-creative-precedents` and
`multiply-award-entry-writer` from the multiply-agency plugin, and the whole **multiply**
plugin (connect, setup, import to Multiply, AdForum search). In Multiply,
set up one Workspace per brand, business unit or market rather than per client.

## How the pack maps to Multiply

| In the pack | In Multiply |
|---|---|
| `brand/<brand>.md` | The brand's **Workspace** (profile as a dated document, plus the Workspace description, which steers its weekly news on your market and competitors) |
| An accepted request, campaign or agency job | A **Project** with Instructions, a Brief, intelligence areas and suggested next tasks |
| Reviews, pulses, digests, adaptation packs, impact reports | Dated documents on the Workspace or Project, searchable by the team |

Each skill includes `reference/multiply-mcp.md` with the Multiply tools it uses. The skills
read freely and **always ask before writing** or before anything that uses Multiply credits.

---
*Draft v0.1 · MIT licence*
