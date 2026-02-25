# Pendo Analytics - Cursor Plugin

Bring Pendo analytics into Cursor with skills for account health, feature adoption, session replays, and feedback analysis.

## Getting started

1. **Start Cursor with the plugin:**
   ```bash
   claude --plugin-dir /path/to/cursor-pendo-plugin
   ```

2. **Authenticate the Pendo MCP server:**
   Run the `/mcp` command inside Claude Code and follow the authentication flow.

3. **Run a skill:**
   ```
   /account-health <account-name>
   /feature-adoption <feature-name>
   /feedback-analysis
   /session-replay
   ```

## Skills

| Skill | Description |
|:------|:------------|
| `account-health` | Prepare for a customer call by synthesizing engagement, sentiment, and feedback |
| `feature-adoption` | Analyze feature adoption rates, identify power users vs laggards, and track trends |
| `feedback-analysis` | Deep analysis of customer feedback - discover themes, extract insights, and identify risks |
| `session-replay` | Find and surface relevant session replays for debugging, UX research, and understanding user behavior |

## MCP Tools

| Tool | Purpose |
|:-----|:--------|
| `activityQuery` | Engagement metrics and activity data |
| `productEngagementScore` | PES calculations |
| `searchEntities` | Find accounts, pages, features |
| `accountQuery` | Account metadata |
| `accountMetadataSchema` | Account metadata schema |
| `visitorQuery` | Visitor metadata |
| `sessionReplayList` | Find session recordings |
| `generate_feedback_topics` | Cluster feedback into themes |
| `get_feedback_insights` | Extract key insights |
| `get_feedback_items` | Raw feedback data |
| `guideMetrics` | Guide performance metrics |
| `segmentList` | Available segments |
| `list_all_applications` | List Pendo applications |

## Validation

```bash
node scripts/validate-template.mjs
```

## Submission checklist

- Plugin has a valid `.cursor-plugin/plugin.json`
- Plugin name is lowercase and kebab-case
- `.cursor-plugin/marketplace.json` entry maps to real plugin folder
- All frontmatter metadata is present in skill files
- Logo is committed and referenced with a relative path
- `node scripts/validate-template.mjs` passes

## License

MIT
