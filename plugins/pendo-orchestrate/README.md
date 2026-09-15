# Pendo Orchestrate plugin

Create, configure, and edit draft Orchestrate email journeys via Pendo MCP — multi-email journeys and conditional split flows. Activation stays in the Orchestrate UI.

## Skill

| Skill | Description |
|:------|:------------|
| `orchestrate-journeys` | Lifecycle skill for draft Orchestrate journeys: intake, create, configure audience/schedule/goal, write email HTML, and hand off for activation in the Orchestrate UI (dispatch by user intent; content craft per message type) |

## MCP

Connect `pendo-external` via the plugin `mcp.json` (see [Connect to the Pendo MCP server](https://support.pendo.io/hc/en-us/articles/41102236924955-Connect-to-the-Pendo-MCP-server)). The skill calls Orchestrate lifecycle tools through the Pendo connector (`Pendo:` prefix in the tool list); start with `Pendo:listAllApplications` when `subId` / `appId` are unknown.

## License

MIT
