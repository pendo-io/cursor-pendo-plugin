---
name: session-replay
description: Find and surface relevant session replays for debugging, UX research, and understanding user behavior.
---

# Session Replay Finder

Find relevant session replays to debug issues, conduct UX research, or understand how users interact with your product.

## Parameters

- **visitor_id**: Optional - find sessions for a specific visitor
- **page_name**: Optional - find sessions involving a specific page
- **timeframe**: The time period to search (default: Last 7 days, max: 31 days)
- **min_duration**: Minimum session duration in minutes (default: 2 minutes)
- **min_activity**: Minimum activity percentage (default: 5%)

## Workflow

Execute the following tasks to find relevant session replays:

### 1. Clarify Search Criteria (Sequential)

Determine what the user is looking for:

- Specific visitor sessions?
- Sessions on a particular page?
- Sessions with frustration signals (rage clicks, errors)?
- High-activity sessions for UX research?

If a page or feature name is provided, search for it first:

```
Tools: mcp__pendo-external__searchEntities
```

### 2. Find Session Replays (Sequential)

Use the session replay tool to find matching recordings:

```
Tools: mcp__pendo-external__sessionReplayList
```

Query parameters to use:
- **startDate/endDate**: Based on timeframe (max 31 days)
- **visitorId**: If searching for a specific visitor
- **pageId**: If searching for sessions on a specific page
- **minDuration**: Convert minutes to milliseconds (default: 120000ms = 2 min)
- **minActivityPercentage**: Filter out low-activity sessions (default: 5%)

Example query approach:
> "Find session replays from the last 7 days with at least 5% activity"

### 3. Enrich Results with Context (Parallel)

For the top results, gather additional context:

```
Tools: mcp__pendo-external__visitorQuery, mcp__pendo-external__accountQuery
```

- Get visitor metadata (name, email, account)
- Get account information
- Note frustration events from the replay metadata

### 4. Rank and Present Results

Prioritize sessions based on:
1. Frustration signals (rage clicks, dead clicks, u-turns, error clicks)
2. Activity percentage (higher = more engaged session)
3. Duration (longer sessions may have more context)
4. Recency

## Output Format

Present session replays in an actionable format:

### Session Replays Found

**Search Criteria**: {criteria_summary}
**Period**: {timeframe}
**Results**: {count} sessions found

#### Top Sessions

| # | Visitor | Account | Duration | Activity | Frustration Signals | Link |
|---|---------|---------|----------|----------|---------------------|------|
| 1 | {visitor} | {account} | {duration} | {activity}% | {signals} | [Watch]({url}) |
| 2 | {visitor} | {account} | {duration} | {activity}% | {signals} | [Watch]({url}) |
| ... | ... | ... | ... | ... | ... | ... |

#### Frustration Summary
- **Rage Clicks**: {total_rage_clicks} across {sessions_with_rage} sessions
- **Dead Clicks**: {total_dead_clicks} across {sessions_with_dead} sessions
- **Error Clicks**: {total_error_clicks} across {sessions_with_errors} sessions
- **U-Turns**: {total_uturns} across {sessions_with_uturns} sessions

#### Recommended Sessions to Review

1. **{session_1_reason}**: [Watch Session]({url})
   - Visitor: {visitor}, Duration: {duration}, {frustration_details}

2. **{session_2_reason}**: [Watch Session]({url})
   - Visitor: {visitor}, Duration: {duration}, {frustration_details}

## Rules

- Maximum date range is 31 days
- Default to last 7 days if no timeframe specified
- Always include the direct URL to watch each session
- Highlight sessions with frustration signals prominently
- Filter out very short or low-activity sessions by default
- If searching by page/feature name, resolve to ID first using searchEntities
- Present the most actionable sessions first (high frustration, high activity)
