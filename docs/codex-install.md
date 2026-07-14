# Installing AIResearch in ChatGPT / Codex (Personal Marketplace)

The plugin ships a `.codex-plugin/` manifest alongside the Claude Code
manifest, so the same repository works in both ecosystems.

## Personal (local) install

1. Create the personal marketplace file `~/.agents/plugins/marketplace.json`:

```json
{
  "name": "wook-personal-plugins",
  "interface": { "displayName": "Wook Personal Plugins" },
  "plugins": [
    {
      "name": "airesearch",
      "source": { "source": "local", "path": "./airesearch" },
      "policy": {
        "installation": "AVAILABLE",
        "authentication": "ON_FIRST_USE"
      },
      "category": "Public Equity Investing"
    }
  ]
}
```

2. Copy the plugin into the marketplace root (exclude repo internals):

```bash
mkdir -p ~/.agents/plugins/airesearch
rsync -a --delete \
  --include='.codex-plugin/***' --include='skills/***' \
  --include='assets/***' --include='README.md' --include='LICENSE*' \
  --exclude='*' \
  <repo>/ ~/.agents/plugins/airesearch/
```

3. Restart the ChatGPT desktop app. The card appears under
   插件 → 个人 (Plugins → Personal).

## Data layer (optional)

Skills work without any key via web-search fallback. For the hosted MCP
data layer, make `AIRESEARCH_API_KEY` available in the environment the
desktop app inherits (see README for the variable format), then restart.

## Updating

After changing plugin files, re-run the rsync in step 2 and restart the
app to pick up the new files.
