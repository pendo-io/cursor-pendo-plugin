---
name: account-health
description: Prepare for a customer call by synthesizing engagement, sentiment, and feedback from Pendo analytics.
---

# Account Health Analysis

Synthesize engagement metrics, feature usage, feedback, and NPS data to prepare for customer conversations.

## Parameters

- **account_id**: The account identifier. Use the searchEntities tool to find accounts if the exact ID is unknown.
- **timeframe**: The time period for analysis (default: Last 90 days)

## Workflow

Execute the following tasks to build a comprehensive account health report:

### 1. Collect Engagement Metrics (Parallel)

Use the Pendo MCP tools to gather engagement data:

```
Tools: mcp__pendo-external__activityQuery, mcp__pendo-external__productEngagementScore
```

- Get the count of unique visitors for the account in the timeframe
- Get the count of unique visitors in the previous equivalent timeframe (for comparison)
- Identify the top 3 visitors by days active from this account
- Calculate PES (Product Engagement Score) if available

Example query approach:
> "What is the count of unique visitors for account id '{account_id}' in the last 90 days?"

### 2. Collect Feature Usage Data (Parallel)

Use Pendo MCP tools to analyze feature and page usage:

```
Tools: mcp__pendo-external__activityQuery, mcp__pendo-external__searchEntities
```

- Get top 3 pages by number of visitors from this account
- Get top 3 features by number of visitors from this account
- Identify any growth or decline trends

Example query approach:
> "What are the top 3 pages for account '{account_id}' in the last 90 days by visitor count?"

### 3. Collect Feedback Data (Parallel)

Use Pendo feedback tools to gather qualitative insights:

```
Tools: mcp__pendo-external__generate_feedback_topics, mcp__pendo-external__get_feedback_insights, mcp__pendo-external__get_feedback_items
```

- Group feedback from the account into topics
- Extract key insights and themes
- Note any alerts (Churn Risk, High Frustration, Blocker to Sale)

Example query approach:
> "Generate feedback topics for account id '{account_id}' in the last 90 days"

### 4. Collect NPS Scores (Parallel)

If NPS data is available, gather sentiment metrics:

```
Tools: mcp__pendo-external__activityQuery (with poll entity type)
```

- Get NPS score for the account in the timeframe
- Compare with previous period if available

## Output Format

Generate a structured account health report with:

### Account Health Summary: {account_name}

**Period**: {timeframe}

#### Engagement Overview
- **Unique Visitors**: {count} (vs {previous_count} previous period)
- **Top Active Users**:
  1. {visitor_1} - {days_active} days active
  2. {visitor_2} - {days_active} days active
  3. {visitor_3} - {days_active} days active
- **PES Score**: {score}/100

#### Feature & Page Usage
**Top Pages**:
1. {page_1} - {visitor_count} visitors
2. {page_2} - {visitor_count} visitors
3. {page_3} - {visitor_count} visitors

**Top Features**:
1. {feature_1} - {visitor_count} visitors
2. {feature_2} - {visitor_count} visitors
3. {feature_3} - {visitor_count} visitors

#### Customer Feedback Themes
{feedback_topics_summary}

#### Alerts & Risks
{any_flagged_items}

#### Recommendations for Customer Call
{synthesized_recommendations}

## Rules

- Always pass the account_id explicitly in queries
- Execute engagement, usage, feedback, and NPS collection in parallel when possible
- If account cannot be found, use searchEntities to help locate the account
- Keep user-facing responses minimal; let the report speak for itself
- Default timeframe is 90 days if not specified
