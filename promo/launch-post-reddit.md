# Reddit Post — r/ClaudeAI

**Title:** I made a Claude Code plugin that does six-lens stock research with live data (and fixed the bug where it analyzed rubber as a ticker)

**Body:**

Been working on a plugin for Claude Code that generates structured equity research reports. Six lenses: supply chain, fundamentals, macro, technicals, sentiment, risk matrix. All data from a hosted MCP server — no LLM-guessed numbers.

The fun part was the entity resolution bug. Early version had no verification — type "Liquid Silicone Rubber" and it would confidently treat it as a stock ticker, make up financials, and present them as fact. Fixed it with four layers: entity resolution → entity lock → server-side validation → real-data-only fallback.

```
/airesearch:deep-dive NVDA
→ Supply Chain: top 5 suppliers, revenue concentration
→ Fundamentals: Yahoo Finance GAAP data
→ Technicals: deterministic RSI/MACD/MA/ATR from daily OHLCV
→ Sentiment: institutional ownership, short interest
→ Risk Matrix: concentration risk, regulatory exposure
```

Industry mode too — type a theme like "humanoid robot" and it builds an ETF constituent universe.

Install:
```
/plugin marketplace add WOOK98/airesearch-plugin
/plugin install airesearch@airesearch-marketplace
```

Works out of the box with web search. Live market data via MCP: DM for beta key during the early access period.

[github.com/WOOK98/airesearch-plugin](https://github.com/WOOK98/airesearch-plugin) · Research tool, not investment advice. Happy to answer questions.
