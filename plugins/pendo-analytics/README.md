# Pendo Analytics plugin

Pendo analytics for Cursor and Claude Code: account health, feature adoption, session replays, and feedback analysis.

## Claude Code Quickstart

1. **Clone the repo:**
   ```bash
   git clone https://github.com/pendo-io/cursor-MCP-plugin.git
   ```

2. **Start Claude Code with the plugin:**
   ```bash
   claude --plugin-dir /path/to/cursor-MCP-plugin/cursor-pendo-plugin
   ```

3. **Authenticate the Pendo MCP server:**
   Run the `/mcp` command inside Claude Code and follow the authentication flow.

4. **Run a skill:**
   ```
   /account-health pendo-internal
   /feature-adoption <feature-name>
   /feedback-analysis
   /session-replay
   ```

## Components

### Skills

| Skill | Description |
|:------|:------------|
| `account-health` | Prepare for a customer call by synthesizing engagement, sentiment, and feedback from Pendo analytics |
| `feature-adoption` | Analyze feature adoption rates, identify power users vs laggards, and track adoption trends |
| `feedback-analysis` | Deep analysis of customer feedback - discover themes, extract insights, and identify risks |
| `session-replay` | Find and surface relevant session replays for debugging, UX research, and understanding user behavior |

### MCP Tools

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

## License

MIT
