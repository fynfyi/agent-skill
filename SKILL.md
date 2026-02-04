---
name: fyn-finance
description: Query your personal finances — transactions, receipts, budgets, spending insights. Connects to FYN (fyn.fyi) for bank syncing + receipt AI.
metadata:
  openclaw:
    emoji: "\U0001F4B0"
    homepage: "https://fyn.fyi/agents"
    requires:
      env: ["FYN_API_KEY"]
---

# FYN Finance — Your Agent's Financial Brain

Query bank transactions, scan receipts with AI, check budgets, and get spending insights — all from your agent.

## Setup

1. Sign up at https://fyn.fyi (free tier available)
2. Connect your bank accounts
3. Go to Settings > Agent Access > Generate API Key
4. Set `FYN_API_KEY` in your agent's environment

## Available Commands

### Spending
- "How much did I spend on [category/merchant]?"
- "Show my spending breakdown by category"
- "Compare this month vs last month"
- "Where can I cut back?"

### Accounts
- "What's my checking balance?"
- "What's my net worth?"
- "Show all account balances"

### Budgets
- "How's my food budget?"
- "What am I over budget on?"

### Receipts (Pro)
- "What did I buy at [merchant]?"
- "Search my receipts for [item]"
- "Am I overpaying for groceries?"

### Intelligence (Pro)
- "Can I afford a $500 purchase?"
- "What are my subscriptions costing me?"
- "What's my savings rate?"

### Portfolio
- "Show my portfolio summary"
- "What are my holdings?"

## API Reference

Base URL: `https://api.fyn.fyi/v1/agent`

All requests require:
```
Authorization: Bearer <FYN_API_KEY>
```

Every response includes rate limit metadata:
```json
{
  "success": true,
  "data": { ... },
  "meta": {
    "plan": "free",
    "rateLimit": {
      "remaining": 47,
      "limit": 50,
      "resetAt": "2026-02-05T00:00:00.000Z"
    }
  }
}
```

### Transactions

#### GET /transactions/recent
Returns recent transactions.

Query params:
- `limit` (number, default 10, max 50)
- `merchant` (string, filter by merchant name)
- `category` (string, filter by category)
- `start_date` (ISO date, e.g. 2026-01-01)
- `end_date` (ISO date)

#### POST /transactions/sum
Get total spending for a period.

Body:
```json
{
  "start_date": "2026-01-01",
  "end_date": "2026-01-31",
  "merchant": "optional",
  "category": "optional"
}
```

### Spending

#### POST /spending/breakdown
Returns spending grouped by merchant or category.

Body:
```json
{
  "group_by": "merchant",
  "start_date": "2026-01-01",
  "end_date": "2026-01-31",
  "limit": 10
}
```

#### POST /spending/compare
Compare spending between two time periods.

Body:
```json
{
  "period1_start": "2025-12-01",
  "period1_end": "2025-12-31",
  "period2_start": "2026-01-01",
  "period2_end": "2026-01-31"
}
```

#### POST /spending/discretionary
Analyze discretionary vs. essential spending.

Body:
```json
{
  "start_date": "2026-01-01",
  "end_date": "2026-01-31"
}
```

### Accounts

#### GET /accounts/balances
Returns all account balances.

#### GET /accounts/balance
Returns a single account balance.

Query params:
- `account_id` (string, required)

#### GET /accounts/net-worth
Returns net worth (assets minus liabilities).

### Budgets

#### GET /budget/status
Returns budget status for all categories.

#### GET /budget/over
Returns categories that are over budget.

### Subscriptions

#### GET /subscriptions
Returns detected recurring subscriptions.

#### GET /subscriptions/total
Returns total monthly subscription cost.

### Cash Flow

#### GET /cashflow
Returns cash flow summary (income vs. expenses).

#### GET /cashflow/savings-rate
Returns savings rate percentage.

### Receipts (Pro)

#### POST /receipts/search
Search receipt line items.

Body:
```json
{
  "query": "coffee",
  "start_date": "2026-01-01",
  "end_date": "2026-01-31"
}
```

#### POST /receipts/rag
Chat with your receipts using RAG (retrieval-augmented generation).

Body:
```json
{
  "query": "What items did I buy at Costco last month?"
}
```

#### POST /receipts/insights
Get price insights for items you buy regularly.

Body:
```json
{
  "item": "milk",
  "merchant": "optional"
}
```

#### GET /receipts/deals
Find better deals based on your purchase history.

### Intelligence (Pro)

#### POST /affordability
Check if a purchase is affordable given your current finances.

Body:
```json
{
  "amount": 499.99,
  "description": "optional context"
}
```

### Portfolio

#### GET /portfolio
Returns portfolio summary (total value, allocation).

#### GET /holdings
Returns individual holdings with current values.

## Rate Limits

| Plan | Daily API Calls | Receipt RAG Queries |
|------|----------------|---------------------|
| Free | 50 | 10 |
| Pro ($9.99/mo) | 2,000 | 500 |

Rate limit headers are included in every response:
```
X-RateLimit-Limit: 50
X-RateLimit-Remaining: 47
X-RateLimit-Reset: 2026-02-05T00:00:00.000Z
```

When rate limited, you'll receive a 429 response:
```json
{
  "success": false,
  "error": {
    "message": "Daily API limit reached. Upgrade to Pro for higher limits.",
    "code": "RATE_LIMIT_EXCEEDED",
    "upgrade_url": "https://fyn.fyi/upgrade"
  }
}
```

## Error Codes

| Code | Status | Description |
|------|--------|-------------|
| `RATE_LIMIT_EXCEEDED` | 429 | Daily API call limit reached |
| `UNAUTHORIZED` | 401 | Missing or invalid API key |
| `FORBIDDEN` | 403 | Feature not available on current plan |
| `NOT_FOUND` | 404 | Resource not found |
| `INTERNAL_ERROR` | 500 | Server error |

## Privacy & Security

- API keys are hashed at rest (SHA-256) — FYN never stores your plaintext key
- All data is scoped to your account — agents can only access your finances
- Keys are instantly revocable from Settings > Agent Access
- All traffic over HTTPS
- No data is shared with third parties

[Full documentation at https://fyn.fyi/docs/agent-api]
