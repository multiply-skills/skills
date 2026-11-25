---
name: multiply-research
description: Runs research in Multiply on any topic (a client, brand, category, market, audience, trend or competitor) and brings the result back into the conversation as a clear answer with every source linked and the data visualised in charts, tables or timelines. Uses Multiply's deep research for full reports and a quick web lookup for short questions, and saves the report to the right client Workspace or Project. Use when the user says "research X in Multiply", "run a Multiply research task", "deep dive on X", "what's happening in X market", "find data on X", "get me the numbers on X", or wants cited research grounded in a client's Multiply context. Needs the Multiply MCP.
---

# Multiply research

Ask Multiply to do the research, then bring it back so it reads well here: the answer
first, the evidence linked, and the numbers shown visually.

## 1. Frame the question

Pin down, inferring what you can and asking only what you can't:

- **The question:** what the user actually needs to know or decide.
- **Scope:** markets, time window (default: the last 2–3 years), audiences, competitors.
- **Client context:** which client or brand it's for, if any.
- **Depth:**
  - **Quick:** a short factual question. Use `run-endpoint` with `endpoint: "Web"` and
    `mode: "quick"` (a capped lookup: three searches, three pages).
  - **Report:** anything that needs an argued answer across many sources. Use
    `run-research` (5–15 minutes).
  - **Campaigns and awards:** use multiply-adforum-search instead.

## 2. Choose where it lands (reads, no need to ask)

1. `create-session`. If the user has more than one organisation, ask which one.
2. Pick `here`:
   - the client's Project, if there's an active job (`list-workspaces`, `list-projects`)
   - otherwise the client's Workspace
   - with no client, a private task: `create-task` with `parent: "acc1"` and a title such as
     `Research · <topic> · <YYYY-MM-DD>`
3. Add `principals` (the Workspace, the Project) when the research should read the client's
   own files, so it's grounded in what the team already knows.

## 3. Run (ask first: it uses Multiply credits)

Say in one line what will be researched, roughly how long it takes, and where the report will
be saved. Then:

- **Report:** `run-research` with `here`, `principals` if useful, and a `prompt` that stands
  alone, because the research agent sees nothing of this conversation. Include:
  - the question and why it matters (the decision it supports)
  - scope: markets, period, audiences, named competitors
  - what to return: key findings, **figures with their source, date and market**, trends over
    time, comparisons, and open questions
  - "Cite every figure with a link to its source."
  Use `wait: 170` (many assistants cut a tool call off after about 3 minutes). If an `op1`
  comes back, call `await` with `wait: 170` again until it's done, and tell the user once
  that it's still running.
- **Quick:** `run-endpoint` with `endpoint: "Web"`, `mode: "quick"`, `here` and a precise
  `task`.

Then `read-source` (`account: "acc1"`) on the report handle. For a long report, read it
through with `through` until you have all findings and figures.

## 4. Present it

Follow `reference/multiply-mcp.md` → *Presenting results from Multiply*. In this order:

1. **The answer** in two or three sentences.
2. **Key findings:** 4–7 bullets, each with its figure and an embedded source link.
3. **Visuals:** 1–3 that fit the data, built only from figures in the report, each with a
   one-line takeaway and its source underneath. If the report has no numbers, use a
   comparison table or timeline instead.
4. **So what:** 2–3 implications for the user's client or decision.
5. **Gaps:** what the research couldn't find or where sources disagree.
6. **Sources** list, and where the full report is saved in Multiply.

If the user asked a quick question or a specific format, give that and offer the visual in
one line instead.

Never add findings or figures that aren't in the Multiply report. If you know something
relevant that it missed, list it separately as "not in the Multiply report, verify".

## 5. Next steps to offer (one line)

A follow-up run on a gap, saving a short summary next to the report with multiply-import,
or turning the findings into a brief with multiply-brief-sharpener.

See `reference/multiply-mcp.md` for every tool's arguments.
