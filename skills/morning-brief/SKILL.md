---
name: morning-brief
description: >
  Generate a two-minute pre-market watchlist brief from a local watchlist.
  Use whenever the user asks for a morning brief, pre-market brief,
  overnight brief, "what happened overnight", "what changed while I slept",
  "盘前简报", "隔夜发生了什么", or asks to run this as a scheduled/daily
  task. Designed for unattended Claude Code runs: never asks follow-up
  questions mid-run.
---

# Morning Brief — Two-Minute Watchlist Triage

Morning Brief turns a saved watchlist into a ranked attention map. It is
not a Deep Dive and not a trading plan. Its only opinion is priority:
which names deserve attention first because something changed overnight.

Target read time: two minutes.

## Workflow

### Step 0 — Find the watchlist file

Before researching anything, find the user's watchlist. Use this fallback
order:

1. **Explicit path** from the user, `--watchlist <path>`, or the
   `AIRESEARCH_WATCHLIST` environment variable.
2. **Project-local files**, in this order:
   - `./watchlist.md`
   - `./watchlist.json`
   - `./.airesearch/watchlist.md`
   - `./.airesearch/watchlist.json`
3. **Home fallback files**, in this order:
   - `~/.airesearch/watchlist.md`
   - `~/.airesearch/watchlist.json`
   - `~/Documents/airesearch-watchlist.md`
   - `~/Documents/airesearch-watchlist.json`

If no watchlist is found, stop and output the accepted format. Do not
invent a sample portfolio.

Accepted Markdown:

```md
# Watchlist
- <TICKER>
- <TICKER.HK>
- <TICKER.SS>
- <TICKER.KS>
```

Accepted JSON:

```json
{
  "watchlist": ["<TICKER>", "<TICKER.HK>", "<TICKER.SS>", "<TICKER.KS>"]
}
```

### Step 1 — Parse and normalize tickers

Extract tickers only. Ignore notes, section headings, comments, and empty
lines. Preserve exchange suffixes. Deduplicate after uppercasing.

Cross-market suffix map:

| Suffix | Market |
|--------|--------|
| `.HK` | Hong Kong |
| `.SS` | Shanghai |
| `.SZ` | Shenzhen |
| `.KS` | Korea |

Do not strip these suffixes. If a ticker lacks a suffix, treat it as a US
symbol unless entity resolution says otherwise.

### Step 2 — Entity gate every ticker

Every ticker must pass entity resolution before any news or market summary.

1. If the `airesearch-data` MCP server is connected, call
   `resolve_entity` for each ticker.
2. If MCP is unavailable, verify each ticker through a current quote page
   or exchange/filing source.
3. If a ticker is invalid, ambiguous, delisted, or maps to multiple
   candidates, do not ask a follow-up question. Put it in **Skipped** with
   the reason and continue.

For unattended scheduled runs, never stop the whole brief because one
ticker fails.

### Step 3 — Gather overnight signals

For each resolved entity, gather only current, verifiable signals:

- Price move in the most recent regular or pre-market session when
  available.
- Company news, filings, guidance, earnings, offerings, buybacks, recalls,
  regulatory actions, lawsuits, analyst actions, or major contracts.
- Sector or macro news that directly affects the entity.
- Upcoming dated catalyst in the next 10 trading days.
- Optional MCP data: quote, financials, technicals. Never estimate missing
  indicators.

Use web search for news and source links. If no fresh signal is found,
say "No material overnight signal found" rather than padding.

### Step 4 — Rank by attention needed

Sort output by "needs attention first", not by ticker order. Ranking
drivers:

1. Material company event with near-term price or thesis impact.
2. Earnings/guidance/filing/regulatory update.
3. Large price move or technical break confirmed by real data.
4. Sector shock affecting multiple watchlist names.
5. Upcoming catalyst in the next 10 trading days.
6. No material change.

Ambiguous or skipped tickers always go in the Skipped footnote, not the
main ranked list.

## Output format

Use the user's language. Keep tickers, exchanges, and metric labels in
English.

```md
# Morning Brief — <date>

## What needs attention first

1. **<TICKER> — <company>** (<market>)
   - **Why now:** <one sentence>
   - **Signal:** <verified overnight/current signal with source/date>
   - **Watch today:** <one concrete catalyst/data point to monitor>

2. ...

## Quiet names

- **<TICKER> — <company>:** No material overnight signal found.

## Skipped

- **<input>:** <invalid / ambiguous / delisted / unresolved reason>.

## Sources

- <source title> — <date>
```

If the watchlist is long, include only the top 8 attention names, then
summarize the rest under **Quiet names**.

## Hard rules

- Never ask follow-up questions during a scheduled or unattended run.
  Ambiguity belongs in **Skipped**, not in a blocking question.
- This skill's only opinion is attention ranking. Do not write "buy the
  dip", "take profit", "trim", "add", "entry", "stop", "target", or any
  similar trade instruction. In Chinese output, do not write "低吸",
  "止盈", "加仓", "减仓", "买点", "卖点", "止损", or similar phrasing.
- Never fabricate prices, financial figures, technical indicators, news,
  or catalysts. If data is unavailable, say so.
- Do not publish per-stock conviction tiers. Use Deep Dive for that.
- Do not analyze an unresolved entity. A failed entity gate means Skipped.
- Decision-support only, not financial advice. This skill never places,
  modifies, or cancels orders.
