# Distribution Checklist

## Verified targets

| Target | Status | Action |
|---|---|---|
| Anthropic community marketplace (claude-plugins-community) | 📨 Submitted 2026-07-18 | Form done via platform.claude.com/plugins/submit. NOTE: the form feeds the community marketplace (@claude-community), NOT claude-plugins-official — the official directory is editorially curated with no application process. Launch copy must say "community plugin marketplace", never "official directory". |
| Cross AI Tools | ✅ crossaitools.com | Community directory with voting; auto-syncs from GitHub .claude-plugin/ manifest |
| GitHub awesome-claude-code | ✅ Exists | PR to add airesearch-plugin |
| Codex/ChatGPT public plugin directory | ⛔ Blocked | OpenAI developer identity verification rejected (2026-07-16, region-restricted). Do NOT retry blindly — attempts are limited. Fallback below. |
| Codex personal marketplace | ✅ Works today | Users add a one-file `marketplace.json` — full guide in `docs/codex-install.md`. Include this path in launch posts as the ChatGPT/Codex install option. |

## Submission order

1. GitHub repo README — update with final README ✅
2. Community directories — auto-sync from GitHub (verify listing appears)
3. X 中文 thread — publish once listed in community directory
4. HN Show HN — 1-2 days after X thread
5. Reddit r/ClaudeAI — separate post, check sub rules first
6. English X post — same day as Reddit/HN
7. Anthropic community marketplace — ✅ submitted 2026-07-18 (review cycle unpredictable, don't block on it)

## Pre-publish blockers

- [x] MCP API key auth — live, verified
- [x] {{VERIFY:}} placeholders replaced
- [x] Internal launch bundle removed from plugin distribution
- [x] Personal marketplace install path verified in repo metadata
- [ ] Clean environment install test
- [ ] Demo GIF recorded
- [ ] API key flow end-to-end test (manual beta distribution)

## Codex distribution (fallback path — decided 2026-07-16)

The OpenAI public directory requires verified developer identity; individual
verification was rejected (region). Decision: distribute via the personal
marketplace path and keep the submission bundle warm.

- **Active path:** `docs/codex-install.md` — personal `marketplace.json` +
  rsync install. Reference it from launch posts wherever ChatGPT/Codex users
  are addressed.
- **Kept warm:** `promo/codex-submission/` stays submission-ready. If a
  verification channel opens later (supported-region ID or registered
  business entity), submit without rework.
- Do not present the plugin as "available in the ChatGPT plugin directory"
  in any launch copy — it is not, and overclaiming distribution is the same
  failure class as overclaiming results.

## Discover submission

Claude Code's default Discover tab is backed by the official
`claude-plugins-official` marketplace. Third-party plugins are not added by
committing to this repository; they require Anthropic's plugin directory
submission form and review.

[WOOK] Submit after the public package is clean:

1. Open <https://github.com/anthropics/claude-plugins-official>.
2. In the README, use the "plugin directory submission form" link under
   **Contributing -> External Plugins**.
3. Submit `WOOK98/airesearch-plugin` with plugin name `airesearch`, version
   `0.4.1` or newer, category `research`, and the install command:
   `/plugin marketplace add WOOK98/airesearch-plugin`.
4. After approval, verify `/plugin > Discover` can find AIResearch and
   `/plugin install airesearch@claude-plugins-official` works.
