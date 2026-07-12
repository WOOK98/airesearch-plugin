# Hacker News — Show HN

**Title:** Show HN: I built a stock research plugin for Claude Code — and it once analyzed a rubber compound as a ticker

**Body:**

I've been building an equity research plugin for Claude Code that generates six-lens reports (supply chain, fundamentals, macro, technicals, sentiment, risk) using live market data through a hosted MCP server.

The interesting part isn't the plugin — it's the bug I had to fix along the way.

**The bug:** Early versions had no entity resolution. You'd type `/airesearch:deep-dive LITE` and the system would happily proceed — even when "LITE" could be Lumentum Holdings (a photonics company) or just the English word. Worse, if you typed something like "Liquid Silicone Rubber" (a material, not a company), it would *invent* a ticker, fabricate financial data, and present it with full confidence.

**The fix:** Four defense layers:
1. **Entity resolution** — every query goes through a verification step that resolves to exactly one listed ticker, or returns candidates/no-match
2. **Entity Lock** — once resolved, the ticker is locked and all downstream lenses use the same verified symbol
3. **Server-side validation** — the MCP data server rejects requests for unlisted tickers
4. **Real-data-only Technical lens** — if the market data fetch fails, the technical analysis is skipped entirely rather than filled with LLM estimates

The plugin now has 5 MCP tools (`resolve_entity`, `get_quote`, `get_financials`, `get_technicals`, `get_etf_holdings`) running at `airesearchs.com/api/mcp`. Every number in the reports comes from live data — Yahoo Finance for fundamentals, deterministic calculations for technicals.

**What it looks like:**

```
/airesearch:deep-dive NVDA
→ Supply Chain: top 5 suppliers mapped, revenue concentration analysis
→ Fundamentals: TTM revenue, margins, FCF, EV/EBITDA from Yahoo Finance
→ Macro: interest rate sensitivity, sector rotation positioning
→ Technicals: RSI, MACD, 20/50/200 MA, ATR (deterministic, not estimated)
→ Sentiment: institutional ownership, short interest signals
→ Risk Matrix: concentration risk, regulatory exposure, conviction score
```

Industry mode works too — type a theme instead of a ticker:
```
/airesearch:deep-dive "humanoid robot"
→ Resolves ETF candidates, pulls constituent holdings, builds value chain universe
```

**Install (Claude Code):**
```bash
/plugin marketplace add WOOK98/airesearch-plugin
/plugin install airesearch@airesearch-marketplace
```

No API key needed — works with web search out of the box. For live market data, DM me or email hello@airesearchs.com for a beta key.

**Tech stack:** Next.js monorepo, Hono API, Better Auth, hosted MCP server on Vercel. Plugin is two skills (deep-dive + snapshot) in SKILL.md format.

**Disclaimer:** This is a research tool, not investment advice. Always do your own due diligence.

Happy to answer questions about the entity resolution approach, MCP server architecture, or the six-lens methodology.
