---
name: deep-dive
description: >
  Generate a full six-lens equity research report on any stock or ticker.
  Use this skill whenever the user asks for a deep dive, full analysis,
  research report, due diligence, "should I buy/sell/hold", a thesis review,
  or any substantive opinion on a listed company — even if they don't say
  "report". Covers six lenses in one pass: Supply Chain, Fundamentals, Macro,
  Technicals, Sentiment, and Risk Matrix. For quick one-screen reads, prefer
  the snapshot skill instead. Decision-support only — never places orders.
---

# Deep Dive — Six-Lens Equity Research Report

Produce ONE integrated report covering ALL SIX lenses below, in this order.
The user does not pick lenses — every Deep Dive includes all of them. Each
lens has a methodology file in `references/`; read the relevant file(s)
before writing that section.

| # | Section | Reference file | Target length |
|---|---------|----------------|---------------|
| 1 | Supply Chain & Value Flow | `references/supply-chain.md` | 300–500 words |
| 2 | Fundamentals | `references/fundamentals.md` | 250–400 words |
| 3 | Macro Context | `references/macro.md` | 150–300 words |
| 4 | Technicals | `references/technicals.md` | 150–250 words |
| 5 | Sentiment & Positioning | `references/sentiment.md` | 150–250 words |
| 6 | Risk Matrix & Conviction | `references/risk-matrix.md` | 250–400 words |

## Workflow

### Step 0 — Entity Resolution Gate (MANDATORY, blocks everything else)

Before ANY analysis, resolve the input to exactly ONE verified listed
entity. This gate exists because the single worst failure mode of
multi-lens research is each lens silently guessing a different company.

1. **Verify the ticker exists.** If the `airesearch-data` MCP server is
   connected, call its `resolve_entity` tool — it returns either one
   verified entity (with an entity-lock block) or candidates. Otherwise,
   web-search the input as a ticker symbol and confirm it resolves to a
   currently listed security. "Looks like a ticker" is not verification —
   confirm against a quote page or filing.
2. **If the input is NOT a valid ticker** (a material, industry, product,
   or brand name — e.g. "Liquid Silicone Rubber"), DO NOT coerce it into
   the nearest-looking symbol and DO NOT let any lens guess. Instead:
   - If plausible ticker candidates exist, STOP and ask the user which
     entity they mean, listing candidates with full names and exchanges.
   - If the input is an industry/material/theme, offer Industry Mode
     (below) instead of forcing the single-stock framework.
3. **Emit an Entity Block** and treat it as immutable for the rest of the
   report:

   ```
   ENTITY: <TICKER> — <full legal name> (<exchange>)
   SECTOR: <sector / industry>
   MKT CAP: <value, as-of date>
   ```

4. **Ambiguous symbols** (multiple listings, e.g. "SOI"): resolve to one
   and state the choice in the Entity Block; never analyze a blend.

### Steps 1–4

1. **Gather current data** for the Entity Block company only. Prefer the
   `airesearch-data` MCP tools when connected: `get_quote`,
   `get_financials` (GAAP fundamentals), `get_technicals` (real computed
   indicators). Use web search for news/filings/contracts, analyst
   coverage, and anything the tools don't cover — and as the full
   fallback when the MCP server is not connected. Never rely on training
   data for prices or recent quarters — theses decay.
2. **Run the six lenses.** Read each reference file, apply it, write the
   section. If subagents are available (Claude Code), you MAY fan out
   lenses 1–5 as parallel subagents — but every subagent prompt MUST begin
   with the verbatim Entity Block and the instruction "analyze ONLY this
   entity; do not re-resolve the ticker; if your lens lacks data for this
   entity, say so rather than substituting a similar company." Lens 6
   (Risk Matrix) must be written LAST by the main agent because it
   integrates the other five.
3. **Reconciliation check (before publishing).** Re-read all six sections
   and verify every company name and ticker mentioned as the subject
   matches the Entity Block. Any section referring to a different entity
   must be rewritten before the report is delivered — never publish and
   caveat.
4. **Write the verdict.** End with a Conviction Summary (see Output format).

## Industry Mode (fallback for non-ticker queries)

When the user confirms they want an industry/material/theme (e.g. "liquid
silicone rubber", "HBM", "grid transformers"), produce instead: (a) a value
chain map of the industry (Lens 1 methodology applied to the sector), (b) a
table of the key LISTED players per chain layer with tickers, exchanges,
and market caps, (c) which layers show bottleneck dynamics, and (d) an
offer to run a full Deep Dive on any named player. Do not output
per-company technicals or conviction tiers in Industry Mode.

## Optional focus argument

If the user asks for a single lens (e.g. "/deep-dive NVDA risk" or "just
the supply chain view"), produce only that section at 2–3x its target
length, plus the one-line disclaimer. Valid focus values: `supply-chain`,
`fundamentals`, `macro`, `technicals`, `sentiment`, `risk`.

## Output format

- Respond in the user's language; keep tickers, metric names, and section
  data labels in English.
- Structure: a 3–5 sentence executive summary up top, then the six
  sections with `##` headers, then **Conviction Summary**.
- Conviction Summary must contain: a tier (S/A/B/C/D/F), 2–3 bull points,
  2–3 bear points, what would upgrade/downgrade the tier, and position
  sizing guidance in qualitative terms (e.g. "binary microcap — small size
  or defined-risk options only").
- Every quantitative claim gets a date or period attached ("Q1 FY26",
  "as of 2026-07-03"). Distinguish facts from estimates from opinion.
- Close with one line: *Decision-support analysis, not financial advice.
  Verify prices and fundamentals before acting.*

## Hard rules

- Never fabricate financial figures. If a number can't be verified, say so.
- Fabricating price levels, indicator values (RSI, MACD), support/
  resistance, or entry/stop prices is a CRITICAL failure — worse than an
  empty section. Any section that cannot source real current data must
  say "insufficient data — section withheld" instead of estimating.
- Never analyze an entity that was not confirmed through the Entity
  Resolution Gate; never substitute a similarly-named company.
- GAAP first; if citing non-GAAP, name the excluded items.
- Never present the report as a trade instruction and never execute,
  place, or cancel orders under any circumstances.
