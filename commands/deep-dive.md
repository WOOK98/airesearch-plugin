---
name: deep-dive
description: Full six-lens equity research report on a ticker, or industry/theme value-chain analysis
argument-hint: TICKER|THEME [focus: supply-chain|fundamentals|macro|technicals|sentiment|risk]
---

Run the `deep-dive` skill on: $ARGUMENTS

This command is registered through the plugin namespace as
`/airesearch:deep-dive`.

If the input is a valid ticker, produce the full six-lens report. If a
second argument is present, treat it as the optional focus lens per the
skill's "Optional focus argument" section.

If the input is NOT a valid ticker (industry, material, theme — e.g.
"Humanoid robot", "HBM", "liquid silicone rubber"), use Industry Mode:
resolve via MCP `resolve_entity` + `get_etf_holdings` for real constituent
data, then produce the value-chain analysis per the skill's Industry Mode
section.
