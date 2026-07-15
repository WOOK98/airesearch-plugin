# AIResearch Plugin

Six-lens equity research inside your coding agent. One command, one
integrated report — no lens-picking, no chat limits, powered by whatever
model you already pay for.

<!-- TODO: replace with actual 30-second demo GIF -->
![demo](docs/demo.gif)

**Lenses:** Supply Chain & Value Flow · Fundamentals · Macro · Technicals ·
Sentiment & Positioning · Risk Matrix & Conviction

## Install — Claude Code

```bash
/plugin marketplace add WOOK98/airesearch-plugin
/plugin install airesearch@airesearch-marketplace
```

Then reload plugins (or restart Claude Code) and run the namespaced
commands:

```bash
/reload-plugins
/airesearch:deep-dive NVDA          # full six-lens report
/airesearch:deep-dive AXTI risk     # single-lens focus
/airesearch:deep-dive "Humanoid robot"  # industry mode: value chain + constituent universe
/airesearch:snapshot MU             # 30-second read
/airesearch:morning-brief           # watchlist triage
```

The skills also trigger implicitly — just ask "give me a deep dive on LITE"
or "quick take on SNDK?".

No API key needed to start — skills work with web search out of the box.
For live market data, see [Pro data layer](#pro-data-layer-optional).

## Install — ChatGPT / Codex Personal Marketplace

The repository ships a `.codex-plugin/plugin.json` manifest and marketplace
assets. See [docs/codex-install.md](docs/codex-install.md) for the personal
marketplace JSON and local install steps.

After install, the same skill prompts are available from the plugin card.

## Structure

```
├── .claude-plugin/          # plugin + marketplace manifests
├── commands/                # /airesearch:deep-dive, /airesearch:snapshot, /airesearch:morning-brief
└── skills/
    ├── deep-dive/
    │   ├── SKILL.md         # report skeleton: 6 sections, output spec
    │   └── references/      # one methodology file per lens
    ├── snapshot/SKILL.md
    └── morning-brief/SKILL.md
```

## Credits

The Supply Chain lens is distilled from the public analytical framework of
**Serenity ([@aleabitoreddit](https://x.com/aleabitoreddit))**. For the full
distillation with dated examples and track-record calibration, install the
companion skill: [WOOK98/serenity-aleabitoreddit](https://github.com/WOOK98/serenity-aleabitoreddit).

## Pro data layer (optional)

The plugin ships with an `.mcp.json` pointing at the hosted
`airesearch-data` MCP server — 5 tools delivering real-time quotes,
GAAP fundamentals, deterministic technicals, and constituent data.
No LLM-estimated indicators, ever.

Set your key before starting Claude Code:

```bash
export AIRESEARCH_API_KEY=mcp_your_beta_key
```

Use the bare key value only, with no `NAME=` prefix and no quotes. The
client-side environment variable is always `AIRESEARCH_API_KEY`; do not set
`MCP_API_KEYS` locally, because that is the server-side allowlist variable.

**Don't have a key yet?** During the beta, DM [@wook98](https://x.com/wook98)
or email hello@airesearchs.com — keys are issued manually while the
self-serve dashboard is in development (see Roadmap below).

Without a key the plugin still works — skills fall back to web search.

## Roadmap

- **v0.3 — Industry Mode.** ✅ Shipped: `get_etf_holdings` MCP tool
  (ETF constituent data + industry universe builder), entity resolution
  hardening. Server version: 0.3.0.
- **v0.2 — Data MCP server.** ✅ Shipped: `resolve_entity`, `get_quote`,
  `get_financials`, `get_technicals` at `airesearchs.com/api/mcp`.
- **v0.4 — Judgment-first reports + Morning Brief.** Adds the Goldman-style
  report skeleton (three falsifiable judgments, thesis invalidation
  conditions, machine-readable monitor panel), namespaced command metadata,
  and the watchlist Morning Brief skill. Per-user API keys remain manual
  during beta.

## Data integrity

Four layers protect against hallucinated data:
1. **Entity resolution first** — every query resolves to a verified listed ticker before any data fetch.
2. **Deterministic indicators** — RSI, MACD, moving averages computed from raw OHLCV bars, never LLM-estimated.
3. **Source-attributed fundamentals** — GAAP financials pulled live from market data tools, not cached summaries.
4. **Graceful degradation** — if the MCP server is unreachable, skills fall back to web search with a visible warning.

## Disclaimer

Decision-support analysis, not financial advice. This plugin never places,
modifies, or cancels orders. Verify all prices and fundamentals before
acting.

**→ /plugin marketplace add WOOK98/airesearch-plugin** · [Docs](https://www.airesearchs.com)

MIT licensed.
