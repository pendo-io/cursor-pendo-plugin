---
name: feedback-analysis
description: Deep analysis of customer feedback - discover themes, extract insights, and identify risks.
---

# Feedback Deep Dive

Analyze customer feedback to discover themes, extract actionable insights, and identify at-risk customers.

## Parameters

- **search_term**: Optional - search for feedback about a specific topic
- **account_id**: Optional - filter to feedback from a specific account
- **feedback_type**: Optional - filter by type (Product Enhancement Request, Product Issues, Pain Point, Positive Product Feedback, Competitor Weakness, Competitor Strength)
- **alerts**: Optional - filter by alert flags (Churn Risk, High Frustration, Blocker to Sale)
- **account_type**: Optional - filter by account type (Customer, Prospect, Churned)
- **timeframe**: The time period to analyze (default: Last 90 days)

## Workflow

Execute the following tasks to analyze customer feedback:

### 1. Determine Analysis Scope (Sequential)

Clarify what the user wants to analyze:
- All feedback or filtered by topic/keyword?
- Specific account or all accounts?
- Specific feedback types or alerts?
- What timeframe?

If searching for feedback about a topic, use similarity search:
> Use similaritySearchTerms for conceptual/semantic matches
> Use exactMatchSearchTerms only for exact phrase matches

### 2. Generate Feedback Topics (Sequential)

Cluster feedback into AI-generated themes:

```
Tools: mcp__pendo-external__generate_feedback_topics
```

This returns topic clusters with:
- Topic name and description
- Count of feedback items in each topic

Example query approach:
> "Generate feedback topics for the last 90 days"

### 3. Extract Key Insights (Parallel)

Get distilled, actionable insights from the feedback:

```
Tools: mcp__pendo-external__get_feedback_insights
```

Each insight includes:
- Summary of the insight
- Explanation of why it matters
- Supporting quote from actual feedback

### 4. Get Raw Feedback Items (Parallel)

Retrieve the actual feedback for deeper analysis:

```
Tools: mcp__pendo-external__get_feedback_items
```

Returns up to 30 feedback items with:
- Title and description
- Account and visitor info
- Feedback type and alerts

### 5. Identify Risk Signals (Parallel)

Look specifically for high-risk feedback:

```
Tools: mcp__pendo-external__get_feedback_items (with alerts filter)
```

Filter for:
- Churn Risk alerts
- High Frustration alerts
- Blocker to Sale alerts

## Output Format

Present a comprehensive feedback analysis:

### Feedback Analysis Report

**Scope**: {filter_summary}
**Period**: {timeframe}
**Total Feedback Analyzed**: {count}

#### Top Themes

| # | Theme | Description | Count |
|---|-------|-------------|-------|
| 1 | {topic_1} | {description} | {count} |
| 2 | {topic_2} | {description} | {count} |
| 3 | {topic_3} | {description} | {count} |
| ... | ... | ... | ... |

#### Key Insights

**Insight 1: {summary}**
> "{supporting_quote}"
- {explanation}

**Insight 2: {summary}**
> "{supporting_quote}"
- {explanation}

**Insight 3: {summary}**
> "{supporting_quote}"
- {explanation}

#### Risk Alerts

**Churn Risk** ({count} items)
| Account | Feedback | Date |
|---------|----------|------|
| {account} | {summary} | {date} |

**High Frustration** ({count} items)
| Account | Feedback | Date |
|---------|----------|------|
| {account} | {summary} | {date} |

**Blocker to Sale** ({count} items)
| Account | Feedback | Date |
|---------|----------|------|
| {account} | {summary} | {date} |

#### Feedback by Type

- **Product Enhancement Requests**: {count}
- **Product Issues**: {count}
- **Pain Points**: {count}
- **Positive Feedback**: {count}
- **Competitor Mentions**: {count}

#### Recommendations

Based on this feedback analysis:
1. {recommendation_1}
2. {recommendation_2}
3. {recommendation_3}

## Rules

- Always run generate_feedback_topics first to get the high-level view
- Use similaritySearchTerms for topic searches (semantic matching)
- Use exactMatchSearchTerms only when user wants exact phrase matches
- Highlight Churn Risk and High Frustration alerts prominently
- Include direct quotes to support insights
- Limit raw feedback display to most relevant items
- Provide actionable recommendations based on the analysis
- If searching for a specific topic with no results, suggest broadening the search
