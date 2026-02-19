# Pendo Analytics - Cursor Plugin

Pendo analytics for Cursor: account health, feature adoption, session replays, and feedback analysis.

## Plugins

- **pendo-analytics**: Bring Pendo analytics into Cursor with skills for account health, feature adoption, session replays, and feedback analysis

## Getting started

1. `.cursor-plugin/marketplace.json`: marketplace configuration.
2. `plugins/pendo-analytics/.cursor-plugin/plugin.json`: plugin metadata.
3. `plugins/pendo-analytics/skills/`: skill definitions.

To add more plugins, see `docs/add-a-plugin.md`.

## Validation

```bash
node scripts/validate-template.mjs
```

## Submission checklist

- Each plugin has a valid `.cursor-plugin/plugin.json`.
- Plugin names are unique, lowercase, and kebab-case.
- `.cursor-plugin/marketplace.json` entries map to real plugin folders.
- All frontmatter metadata is present in skill files.
- Logos are committed and referenced with relative paths.
- `node scripts/validate-template.mjs` passes.
