---
name: snapshot
description: >
  Generate a fast one-screen stock snapshot: what the company is, where it
  sits in its supply chain, key GAAP numbers, top bull/bear points, and a
  conviction tier. Use whenever the user wants a quick take, a "TLDR",
  "quick look", "worth a look?", or mentions a ticker casually without
  asking for a full report. For thorough analysis, hand off to the
  deep-dive skill instead. Decision-support only — never places orders.
---

# Snapshot — One-Screen Stock Read

A Snapshot is NOT a mini Deep Dive with six headers. It is a single compact
read, under ~350 words, that a user can absorb in 30 seconds.

## Workflow

1. **Entity gate first.** Verify the input resolves to exactly one
   currently listed security (confirm via web search against a quote page
   or filing — same rule as deep-dive's Entity Resolution Gate). If the
   input is not a valid ticker (a material, industry, or brand name), do
   NOT guess a similar-looking company: ask which entity the user means,
   or offer deep-dive's Industry Mode for industry/theme queries.
2. Web-search current price, market cap, latest reported quarter (GAAP),
   and any major news from the past 30 days. Never use training-data
   prices; any number you can't verify gets omitted, not estimated.
3. Write the snapshot in the user's language (tickers and metric labels in
   English).

## Format

- **One-liner:** what the company actually sells and to whom.
- **Chain position:** one sentence — where it sits in its value chain and
  whether a bottleneck dynamic applies (upstream chokepoint / commodity
  layer / downstream integrator).
- **Numbers that matter:** 4–6 datapoints max, period-labeled — market cap,
  revenue growth, GAAP gross/op margin, cash/dilution flag if notable.
- **Bull vs. bear:** 2 points each, one line per point.
- **Tier + next catalyst:** S/A/B/C/D/F tier (same rubric as deep-dive's
  risk-matrix reference), the next dated catalyst, and when a full Deep
  Dive would be warranted ("run /airesearch:deep-dive TICKER for the full six-lens
  report").
- Close with: *Decision-support analysis, not financial advice.*

## Hard rules

Same as deep-dive: no fabricated figures, GAAP first, never an order
instruction, never execute trades.
