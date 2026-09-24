# Pendo plugins for Cursor

Pendo analytics and Orchestrate journey building for Cursor via MCP-backed skills.

## Getting started

1. **Install or open the plugin** from this repo (see your Cursor plugin / marketplace flow for this marketplace).

2. **Authenticate the Pendo MCP server** and connect `pendo-external` (see [Connect to the Pendo MCP server](https://support.pendo.io/hc/en-us/articles/41102236924955-Connect-to-the-Pendo-MCP-server)).

3. **Run a skill** (exact invocation depends on your Cursor plugin UI).

## Plugins

| Plugin | Skills |
|:-------|:-------|
| `pendo-analytics` | `account-health`, `feature-adoption`, `feedback-analysis`, `session-replay` |
| `pendo-orchestrate` | `orchestrate-journeys` |

See `plugins/pendo-analytics/README.md` and `plugins/pendo-orchestrate/README.md` for details.

## Validation

```bash
node scripts/validate-template.mjs
```

## Submission checklist

- Each plugin has a valid `.cursor-plugin/plugin.json`
- Plugin names are lowercase kebab-case
- `.cursor-plugin/marketplace.json` entries map to real plugin folders
- All `SKILL.md` files include `name` and `description` frontmatter
- `node scripts/validate-template.mjs` passes

## License

MIT
