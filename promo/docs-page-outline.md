# Docs Page Outline — airesearchs.com/plugin

## Page structure

### Hero
- One-liner: "Six-lens equity research inside your coding agent."
- CTA button: "Install Plugin" → copy-paste install block below

### Install (copy-paste block)
```
/plugin marketplace add WOOK98/airesearch-plugin
/plugin install airesearch@airesearch-marketplace
```

No API key needed — skills work with web search out of the box.

### Quick start
- `/deep-dive NVDA` — full report
- `/snapshot MU` — quick take
- `/deep-dive "humanoid robot"` — industry mode

### MCP Tools Reference

#### `resolve_entity`
- Input: `{ query: string }` — ticker, company name, industry, material, or theme
- Output: verified ticker, company name, exchange, quote type, or candidates list
- Used internally by all other tools; exposed for custom workflows

#### `get_quote`
- Input: `{ ticker: string }`
- Output: real-time price, currency, exchange, entity lock metadata

#### `get_financials`
- Input: `{ ticker: string }`
- Output: GAAP financials from Yahoo Finance — revenue, margins, FCF, valuation multiples

#### `get_technicals`
- Input: `{ ticker: string, includeContext?: boolean }`
- Output: deterministic technical indicators from daily OHLCV — RSI, MACD, moving averages, ATR
- `includeContext: true` returns a prompt-ready TECHNICAL DATA LOCK string

#### `get_etf_holdings`
- Input: `{ query: string, includeContext?: boolean }`
- Dual mode:
  - ETF ticker → raw constituent holdings
  - Theme phrase → resolve ETF candidates, build merged industry universe
- `includeContext: true` returns a prompt-ready INDUSTRY CONTEXT block

### Pro data layer (optional)

The hosted MCP server delivers live market data — real-time quotes, GAAP
fundamentals, deterministic technicals, and ETF constituent data. No
LLM-estimated indicators, ever.

```bash
export AIRESEARCH_API_KEY=your_key
```

**During beta:** API keys are issued manually. DM [@wook98](https://x.com/wook98)
or email hello@airesearchs.com. Self-serve key generation is on the roadmap.

Without a key, skills fall back to web search (slower, less precise).

### Changelog

- **v0.3** — `get_etf_holdings` tool, Industry Mode, entity resolution hardening.
  Server version: 0.3.0.
- **v0.2** — Hosted MCP server with `resolve_entity`, `get_quote`,
  `get_financials`, `get_technicals`. Plugin initial release.
- **v0.1** — Skills-only: deep-dive and snapshot (no MCP server).

### Data integrity

Four layers protect against hallucinated data:
1. Entity resolution first — every query resolves to a verified listed ticker before any data fetch.
2. Deterministic indicators — RSI, MACD, moving averages computed from raw OHLCV bars, never LLM-estimated.
3. Source-attributed fundamentals — GAAP financials pulled live from Yahoo Finance, not cached summaries.
4. Graceful degradation — if the MCP server is unreachable, skills fall back to web search with a visible warning.

### Disclaimer
Research tool, not investment advice.

### SEO targets
- Title: "AIResearch Plugin — Stock Research for Claude Code"
- Meta description: "Six-lens equity research powered by live market data. Install in Claude Code, get structured reports with supply chain, fundamentals, technicals, and more."
- H1: "Stock Research Inside Your Coding Agent"
