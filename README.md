# AIResearch Plugin

Six-lens equity research inside your coding agent. One command, one
integrated report — no lens-picking, no chat limits, powered by whatever
model you already pay for.

**Lenses:** Supply Chain & Value Flow · Fundamentals · Macro · Technicals ·
Sentiment & Positioning · Risk Matrix & Conviction

## Install — Claude Code

```bash
/plugin marketplace add WOOK98/airesearch-plugin
/plugin install airesearch@airesearch-marketplace
```

Then:

```bash
/deep-dive NVDA          # full six-lens report
/deep-dive AXTI risk     # single-lens focus
/snapshot MU             # 30-second read
```

The skills also trigger implicitly — just ask "give me a deep dive on LITE"
or "quick take on SNDK?".

## Install — Codex

The `skills/` directories are Codex-compatible (SKILL.md format). Copy them
into your Codex skills location, e.g.:

```bash
git clone https://github.com/WOOK98/airesearch-plugin
cp -r airesearch-plugin/skills/* ~/.codex/skills/
```

Restart Codex, then invoke with `$deep-dive` / `$snapshot` or just ask
naturally. (Packaged Codex plugin distribution coming when self-serve
publishing opens.)

## Structure

```
├── .claude-plugin/          # plugin + marketplace manifests
├── commands/                # /deep-dive, /snapshot
└── skills/
    ├── deep-dive/
    │   ├── SKILL.md         # report skeleton: 6 sections, output spec
    │   └── references/      # one methodology file per lens
    └── snapshot/SKILL.md
```

## Credits

The Supply Chain lens is distilled from the public analytical framework of
**Serenity ([@aleabitoreddit](https://x.com/aleabitoreddit))**. For the full
distillation with dated examples and track-record calibration, install the
companion skill: [WOOK98/serenity-aleabitoreddit](https://github.com/WOOK98/serenity-aleabitoreddit).

## Pro data layer (optional)

The plugin ships with an `.mcp.json` pointing at the hosted
`airesearch-data` MCP server (real-time quotes, GAAP fundamentals, and
deterministically computed technicals — no LLM-estimated indicators,
ever). Set your key before starting Claude Code:

```bash
export AIRESEARCH_API_KEY=your_key   # get one at airesearchs.com
```

Without a key the plugin still works — skills fall back to web search.

## Roadmap

- **v0.2 — Data MCP server.** ✅ Shipped: `resolve_entity`, `get_quote`,
  `get_financials`, `get_technicals` at `airesearchs.com/api/mcp`.
- **v0.3 — Per-user API keys** issued from the billing dashboard;
  **report-to-social skill** bundled (X threads / blog HTML / hero SVG
  from any Deep Dive).

## Disclaimer

Decision-support analysis, not financial advice. This plugin never places,
modifies, or cancels orders. Verify all prices and fundamentals before
acting. MIT licensed.
