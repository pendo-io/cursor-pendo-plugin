---
name: feature-adoption
description: Analyze feature adoption rates, identify power users vs laggards, and track adoption trends.
---

# Feature Adoption Analysis

Analyze how features are being adopted across your user base, identify champions and laggards, and track adoption trends.

## Parameters

- **feature_name**: The feature to analyze. Use searchEntities to find the feature ID if the exact ID is unknown.
- **timeframe**: The time period for analysis (default: Last 30 days)
- **comparison_period**: Optional previous period for trend analysis

## Workflow

Execute the following tasks to build a comprehensive feature adoption report:

### 1. Identify the Feature (Sequential)

First, locate the feature in Pendo:

```
Tools: mcp__pendo-external__searchEntities
```

- Search for the feature by name
- Confirm the correct feature ID with the user if multiple matches
- Get feature metadata (name, description, tagged pages)

Example query approach:
> "Search for features matching '{feature_name}'"

### 2. Collect Adoption Metrics (Parallel)

Use Pendo MCP tools to gather adoption data:

```
Tools: mcp__pendo-external__activityQuery
```

- Get total unique visitors who used this feature in the timeframe
- Get total unique accounts with users of this feature
- Get total event count for the feature
- Calculate daily/weekly active users trend
- Get previous period metrics for comparison

Example query approach:
> "How many unique visitors used feature '{feature_id}' in the last 30 days?"

### 3. Identify User Segments (Parallel)

Analyze who is using the feature:

```
Tools: mcp__pendo-external__activityQuery, mcp__pendo-external__visitorQuery
```

- **Power Users**: Top 10 visitors by feature usage (event count)
- **Recent Adopters**: Visitors who first used the feature in the last 7 days
- **Account Distribution**: Top accounts by number of feature users

Example query approach:
> "Who are the top 10 visitors by event count for feature '{feature_id}'?"

### 4. Calculate Adoption Rate (Parallel)

Compare feature users to total active users:

```
Tools: mcp__pendo-external__activityQuery, mcp__pendo-external__segmentList
```

- Get total active visitors in the timeframe
- Calculate adoption rate: (feature users / total active users) * 100
- If segments available, calculate adoption by segment

### 5. Analyze Trends (Sequential)

Look at adoption over time:

```
Tools: mcp__pendo-external__activityQuery (with daily/weekly period)
```

- Get daily or weekly unique visitors for the feature
- Identify growth or decline patterns
- Note any significant spikes or drops

## Output Format

Generate a structured feature adoption report:

### Feature Adoption Report: {feature_name}

**Period**: {timeframe}

#### Adoption Overview
- **Total Users**: {unique_visitors} visitors across {unique_accounts} accounts
- **Adoption Rate**: {adoption_rate}% of active users
- **Total Events**: {event_count} interactions
- **Trend**: {trend_direction} ({percent_change}% vs previous period)

#### Power Users (Champions)
| Rank | Visitor | Account | Events | Days Active |
|------|---------|---------|--------|-------------|
| 1 | {visitor_1} | {account_1} | {events} | {days} |
| 2 | {visitor_2} | {account_2} | {events} | {days} |
| ... | ... | ... | ... | ... |

#### Top Accounts by Adoption
| Rank | Account | Users | Events |
|------|---------|-------|--------|
| 1 | {account_1} | {user_count} | {events} |
| 2 | {account_2} | {user_count} | {events} |
| ... | ... | ... | ... |

#### Adoption Trend
```
{weekly_or_daily_trend_visualization}
```

#### Insights & Recommendations
- {insight_1}
- {insight_2}
- {recommendations_for_improving_adoption}

## Rules

- Always search for the feature first if only a name is provided
- Execute metrics collection in parallel when possible
- Default timeframe is 30 days if not specified
- Calculate adoption rate relative to total active users, not all visitors
- Identify both champions (for case studies) and laggards (for outreach)
- Provide actionable recommendations based on the data
