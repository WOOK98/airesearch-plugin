# AIResearch Plugin

Six-lens equity research inside Claude Code. One prompt, one structured report — powered by live market data, not LLM-guessed numbers.

<!-- TODO: replace with actual 30-second demo GIF -->
![demo](docs/demo.gif)

## Install

```bash
/plugin marketplace add WOOK98/airesearch-plugin
/plugin install airesearch@airesearch-marketplace
```

No API key needed to start — skills work with web search out of the box.
For live market data via the hosted MCP server, see [Pro data layer](#pro-data-layer-optional).

## What you get

```bash
/airesearch:deep-dive NVDA                    # full six-lens report
/airesearch:deep-dive AXTI risk               # single-lens focus
/airesearch:deep-dive "Humanoid robot"        # industry mode: value chain + ETF universe
/airesearch:snapshot MU                       # 30-second quick take
```

Or just ask naturally: *"give me a deep dive on LITE"* / *"quick take on SNDK?"*

### Example output (abbreviated)

**`/airesearch:deep-dive NVDA`** produces a structured report covering:

| Lens | What it does |
|---|---|
| Supply Chain & Value Flow | Maps upstream suppliers, downstream customers, revenue concentration |
| Fundamentals | GAAP financials from Yahoo Finance — revenue, margins, FCF, valuation multiples |
| Macro | Interest rate sensitivity, sector rotation positioning, macro headwinds |
| Technicals | Deterministic indicators from daily OHLCV — RSI, MACD, moving averages, ATR |
| Sentiment & Positioning | Institutional ownership shifts, short interest, options flow signals |
| Risk Matrix | Concentration risk, regulatory exposure, balance sheet red flags, conviction score |

Every number comes from live data via the hosted MCP server — no hallucinated financials.

## Pro data layer (optional)

The plugin connects to a hosted MCP data server at `airesearchs.com/api/mcp`
with 5 tools — real-time quotes, GAAP fundamentals, deterministic technicals,
and ETF constituent data. No LLM-estimated indicators, ever.

```bash
export AIRESEARCH_API_KEY=your_key
```

**Don't have a key yet?** During the beta, DM [@wook98](https://x.com/wook98)
or email hello@airesearchs.com — keys are issued manually while the
self-serve dashboard is in development.

Without a key, skills fall back to web search (slower, less precise).

## Data integrity

Four layers protect against hallucinated data:
1. **Entity resolution first** — every query resolves to a verified listed ticker before any data fetch.
2. **Deterministic indicators** — RSI, MACD, moving averages computed from raw OHLCV bars, never LLM-estimated.
3. **Source-attributed fundamentals** — GAAP financials pulled live from Yahoo Finance, not cached summaries.
4. **Graceful degradation** — if the MCP server is unreachable, skills fall back to web search with a visible warning.

## Disclaimer

This is a research tool, not investment advice. Always do your own due diligence before making investment decisions. The plugin provides structured data and analysis frameworks — investment decisions are your responsibility.

## Credits

The Supply Chain lens is distilled from the public analytical framework of **Serenity ([@aleabitoreddit](https://x.com/aleabitoreddit))**.

---

**→ Install:** `/plugin marketplace add WOOK98/airesearch-plugin`
**→ Docs & API keys:** [airesearchs.com](https://www.airesearchs.com)

*Research tool, not investment advice.*
