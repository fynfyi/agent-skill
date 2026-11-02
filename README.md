# FYN Finance Agent Skill

The official AI agent skill for [FYN](https://fyn.fyi) — personal finance with bank syncing, receipt AI, and spending intelligence.

## Cursor Marketplace

Read-only personal finance for Cursor. After you install FYN, the agent can ask about budgets, upcoming bills, receipt line items, net worth, and whether a purchase fits this month. The plugin connects to FYN's remote MCP server at `https://mcp.fyn.fyi` (streamable HTTP). Sign-in is OAuth 2.1 with PKCE, scope `fyn.read`. Cursor registers a public client on its own. The model never receives a bank password, and FYN does not move money or write to your accounts.

### Install

From the Marketplace:

1. Open **Customize** in the Cursor sidebar, or **Cursor Settings → Plugins**.
2. Search for **FYN**.
3. Click **Install**.
4. The first time a FYN tool runs, Cursor opens FYN sign-in. Approve read-only access.

A FYN account ([fyn.fyi](https://fyn.fyi)) is required. Budget, bill, and net-worth answers use the household's linked accounts. Receipt questions can be answered from scanned receipts.

To connect the same server without the Marketplace, add this to `~/.cursor/mcp.json` (all projects) or `.cursor/mcp.json` (one project):

```json
{
  "mcpServers": {
    "fyn": {
      "type": "http",
      "url": "https://mcp.fyn.fyi"
    }
  }
}
```

`http` is Cursor's streamable HTTP transport: JSON-RPC over HTTPS POST. There is no API key and no client secret to paste. Desktop and Cloud Agents keep separate FYN sign-ins; approve the Cloud row in Customize when you use Cloud Agents.

### Use

Ask in chat the way you would ask a finance app. Cursor calls FYN when the question needs your ledger. Every tool is read-only. Turn the server off in Customize to stop using it here, and revoke the app in FYN under Settings → Agent access to end access on FYN's side.

### Example prompts

- **Budgets:** "How are my budgets this month, and which categories are close to the limit?"
- **Bills:** "What bills are due in the next 10 days?"
- **Receipts:** "Find the receipt for my last Costco trip and list the items."
- **Net worth:** "What's my net worth trend over the past 6 months?"
- **Spend check:** "Can I afford a $1,200 laptop this month without going over budget?"

### Links

- Docs: https://fyn.fyi/docs/mcp
- Privacy: https://fyn.fyi/privacy
- Website: https://fyn.fyi
- Support: brian@fyn.fyi

The sections below are the ClawHub skill (`SKILL.md`, agent API, `FYN_API_KEY`). The Marketplace plugin is `.cursor-plugin/plugin.json` and `mcp.json`.

## What is this?

This is a [ClawHub](https://clawhub.com) skill package that lets any AI agent (OpenClaw, Clank, or any agent with HTTP tools) access your personal financial data through FYN.

Your agent can:
- Query bank transactions and spending patterns
- Check account balances and net worth
- Monitor budgets and subscriptions
- Get daily briefings, alerts, and financial health scores
- Ask natural language questions about your finances
- Search receipts with AI (Pro)
- Check affordability of purchases (Pro)

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
| `/insights/daily` | GET | Daily financial briefing |
| `/insights/alerts` | GET | Active anomalies & warnings |
| `/insights/opportunities` | GET | Money-saving suggestions |
| `/insights/weekly` | GET | Weekly financial recap |
| `/insights/health` | GET | Financial health score (0-100) |
| `/insights/ask` | POST | Natural language insight query |

### Pro Tier ($9.99/mo)

| Endpoint | Method | Description |
|----------|--------|-------------|
| `/receipts/search` | POST | Search receipt line items |
| `/receipts/rag` | POST | Chat with receipts (RAG) |
| `/affordability` | POST | Affordability check |

## Rate Limits

| Plan | Daily Calls | Receipt RAG Queries |
|------|------------|---------------------|
| Free | 50 | 10 |
| Pro | 2,000 | 500 |

## Examples

See the [examples/](./examples/) directory:

- [basic-query.md](./examples/basic-query.md) — Transactions, spending breakdown, balances
- [receipt-search.md](./examples/receipt-search.md) — Receipt AI search and RAG
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
- [MCP Documentation](https://fyn.fyi/docs/mcp)
- [Privacy](https://fyn.fyi/privacy)
- [SKILL.md](./SKILL.md) — Full skill definition

## License

MIT
