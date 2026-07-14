# Distribution Checklist

## Verified targets

| Target | Status | Action |
|---|---|---|
| Anthropic Official Plugin Directory | ✅ Exists | Submit via claude.ai/settings/plugins/submit (form-based review) |
| Cross AI Tools | ✅ crossaitools.com | Community directory with voting; auto-syncs from GitHub .claude-plugin/ manifest |
| GitHub awesome-claude-code | ✅ Exists | PR to add airesearch-plugin |

## Submission order

1. GitHub repo README — update with final README ✅
2. Community directories — auto-sync from GitHub (verify listing appears)
3. X 中文 thread — publish once listed in community directory
4. HN Show HN — 1-2 days after X thread
5. Reddit r/ClaudeAI — separate post, check sub rules first
6. English X post — same day as Reddit/HN
7. Anthropic directory — submit form (review cycle unpredictable, don't block on it)

## Pre-publish blockers

- [x] MCP API key auth — live, verified
- [x] {{VERIFY:}} placeholders replaced
- [x] Internal launch bundle removed from plugin distribution
- [x] Personal marketplace install path verified in repo metadata
- [ ] Clean environment install test
- [ ] Demo GIF recorded
- [ ] API key flow end-to-end test (manual beta distribution)

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
