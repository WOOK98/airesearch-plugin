# Docs Page Outline — airesearchs.com/plugin

## Page structure

### Hero
- One-liner: "Six-lens equity research inside your coding agent."
- CTA button: "Get API Key" → /auth/register

### Install (copy-paste block)
```
/plugin marketplace add WOOK98/airesearch-plugin
/plugin install airesearch@airesearch-marketplace
export AIRESEARCH_API_KEY=your_key
```

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

### Authentication
- Bearer token in `Authorization` header
- Get a key: register at airesearchs.com → dashboard → generate key
- Rate limit: 60 requests/minute per key
- Without a key: skills fall back to web search (slower, less precise)

### Pricing
- Free: 10 reports/day, all 5 MCP tools
- Pro: unlimited reports, priority data access

### Changelog
- v0.3 — `get_etf_holdings` tool, industry mode, entity resolution hardening
- v0.2 — Hosted MCP server with `resolve_entity`, `get_quote`, `get_financials`, `get_technicals`
- v0.1 — Initial plugin with deep-dive and snapshot skills

### Disclaimer
Research tool, not investment advice.

### SEO targets
- Title: "AIResearch Plugin — Stock Research for Claude Code"
- Meta description: "Six-lens equity research powered by live market data. Install in Claude Code, get structured reports with supply chain, fundamentals, technicals, and more."
- H1: "Stock Research Inside Your Coding Agent"
