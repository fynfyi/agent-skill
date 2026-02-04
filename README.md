# FYN Finance Agent Skill

The official AI agent skill for [FYN](https://fyn.fyi) — personal finance with bank syncing, receipt AI, and spending intelligence.

## What is this?

This is a [ClawHub](https://clawhub.com) skill package that lets any AI agent (OpenClaw, Clank, or any agent with HTTP tools) access your personal financial data through FYN.

Your agent can:
- Query bank transactions and spending patterns
- Check account balances and net worth
- Monitor budgets and subscriptions
- Search receipts with AI (Pro)
- Check affordability of purchases (Pro)
- Get price insights and find better deals (Pro)

## Install

```bash
clawhub install fyn-finance
```

Or manually: copy `SKILL.md` into your agent's skill directory.

## Quick Start

1. **Sign up** at [fyn.fyi](https://fyn.fyi) (free)
2. **Connect** your bank accounts via Plaid
3. **Generate** an API key at Settings > Agent Access
4. **Set** `FYN_API_KEY` in your agent's environment

```bash
export FYN_API_KEY=fyn_ak_your_key_here
```

5. **Ask** your agent about your finances:

> "How much did I spend on groceries this month?"
> "What's my net worth?"
> "Am I over budget on anything?"

## API Endpoints

All endpoints use `https://api.fyn.fyi/v1/agent` as the base URL.

### Free Tier

| Endpoint | Method | Description |
|----------|--------|-------------|
| `/transactions/recent` | GET | Recent transactions |
| `/transactions/sum` | POST | Total spending for a period |
| `/spending/breakdown` | POST | Spending by category/merchant |
| `/spending/compare` | POST | Compare two time periods |
| `/spending/discretionary` | POST | Discretionary vs. essential |
| `/accounts/balances` | GET | All account balances |
| `/accounts/balance` | GET | Single account balance |
| `/accounts/net-worth` | GET | Net worth |
| `/budget/status` | GET | Budget status |
| `/budget/over` | GET | Over-budget categories |
| `/subscriptions` | GET | Detected subscriptions |
| `/subscriptions/total` | GET | Total subscription cost |
| `/cashflow` | GET | Cash flow summary |
| `/cashflow/savings-rate` | GET | Savings rate |
| `/portfolio` | GET | Portfolio summary |
| `/holdings` | GET | Individual holdings |

### Pro Tier ($9.99/mo)

| Endpoint | Method | Description |
|----------|--------|-------------|
| `/receipts/search` | POST | Search receipt line items |
| `/receipts/rag` | POST | Chat with receipts (RAG) |
| `/receipts/insights` | POST | Price insights |
| `/receipts/deals` | GET | Find better deals |
| `/affordability` | POST | Affordability check |

## Rate Limits

| Plan | Daily Calls | Receipt RAG Queries |
|------|------------|---------------------|
| Free | 50 | 10 |
| Pro | 2,000 | 500 |

## Examples

See the [examples/](./examples/) directory:

- [basic-query.md](./examples/basic-query.md) — Transactions, spending breakdown, balances
- [receipt-search.md](./examples/receipt-search.md) — Receipt AI search, RAG, price insights
- [budget-check.md](./examples/budget-check.md) — Budgets, affordability, subscriptions

## Authentication

All requests require an API key:

```
Authorization: Bearer fyn_ak_your_key_here
```

Generate keys at [fyn.fyi/settings/agent-access](https://fyn.fyi/settings/agent-access).

## Links

- [FYN Homepage](https://fyn.fyi)
- [Agent Landing Page](https://fyn.fyi/agents)
- [API Documentation](https://fyn.fyi/docs/agent-api)
- [SKILL.md](./SKILL.md) — Full skill definition

## License

MIT
