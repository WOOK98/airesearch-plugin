# AIResearch Codex Submission Draft

This folder is the copy/paste source for the public plugin submission. It
keeps listing copy, install metadata, test prompts, and policy attestations
next to the manifest so the submitted package can be audited from git.

## Package

- Plugin name: `airesearch`
- Version: `0.4.2`
- Repository: `https://github.com/WOOK98/airesearch-plugin`
- Website: `https://www.airesearchs.com`
- Privacy policy: `https://www.airesearchs.com/privacy`
- Terms of service: `https://www.airesearchs.com/terms`
- Category recommendation: `Finance`, `Research`, or `Productivity`
- Availability recommendation: United States first, then all countries where
  the marketplace supports English-language finance research tools.

## One-Line Summary

Six-lens public-equity research reports and watchlist briefs, with entity
resolution first and every number period-labeled.

## English Listing Copy

AIResearch turns a ticker or industry theme into a structured research brief
inside Codex. Use Snapshot for a one-screen read, Deep Dive for a six-lens
report, and Morning Brief for watchlist triage.

The plugin starts by resolving the entity, then organizes evidence across
Supply Chain, Fundamentals, Macro, Technicals, Sentiment, and Risk Matrix.
Reports are decision-support only: no target prices, no buy/sell ratings, and
no order execution.

## Chinese Listing Copy

AIResearch 把 ticker 或行业主题变成结构化研究报告。Snapshot 用于快速一屏
浏览，Deep Dive 输出六 lens 深度报告，Morning Brief 用于 watchlist 盘前
梳理。

插件先做实体解析，再按 Supply Chain、Fundamentals、Macro、Technicals、
Sentiment、Risk Matrix 六个视角组织证据。产品只做决策辅助：不提供目标价、
不提供买卖评级，也不执行交易。

## Capabilities

- Resolve a ticker, company, or industry theme before analysis.
- Generate a one-screen snapshot for a public company.
- Generate a six-lens research report with falsifiable judgments and monitor
  rows.
- Generate a pre-market watchlist brief from a user-provided watchlist.
- Optionally call hosted MCP tools when the user provides an API key.

## MCP Server

- Server name: `airesearch-data`
- Endpoint: `https://www.airesearchs.com/api/mcp`
- Authentication: bearer token from local `AIRESEARCH_API_KEY`
- Public tools exposed by the server:
  - `resolve_entity`
  - `get_quote`
  - `get_financials`
  - `get_technicals`
  - `get_etf_holdings`

The plugin remains usable without an API key through skill-level fallback
research, but hosted data calls require the key.

## Bundled Skills

- `skills/snapshot/SKILL.md`
- `skills/deep-dive/SKILL.md`
- `skills/morning-brief/SKILL.md`

## Starter Prompts

- `Run a six-lens deep dive on MU.`
- `Quick snapshot of 0700.HK.`
- `Map the liquid silicone rubber industry value chain.`
- `Generate a morning brief for my watchlist.`

## Test Cases

1. Snapshot: ask for `MU`; expect an entity-locked one-screen company read.
2. Deep Dive: ask for `"Liquid Silicone Rubber"`; expect Industry Mode rather
   than treating `LSR` as an unverified ticker.
3. Ambiguity: ask for `LITE`; expect the resolver path to avoid silent ticker
   confusion.
4. Boundary: ask for a target price or buy/sell rating; expect refusal or
   decision-support framing without investment advice.

## Policy Attestations

- The plugin does not place, modify, or cancel trades.
- The plugin does not provide target prices, buy/sell ratings, or portfolio
  weights.
- The plugin does not request broker credentials.
- Financial outputs are educational and decision-support oriented.
- Screenshots in `assets/` are marked sample output unless generated from a
  live plugin session.
- Any API key is read from the user's local environment and is not committed
  to the repository.
