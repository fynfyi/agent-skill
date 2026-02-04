# Basic Query — Recent Transactions & Spending

## Get Recent Transactions

**User:** "Show me my last 5 transactions"

**Agent makes request:**

```bash
curl -s https://api.fyn.fyi/v1/agent/transactions/recent?limit=5 \
  -H "Authorization: Bearer $FYN_API_KEY"
```

**Response:**
```json
{
  "success": true,
  "data": {
    "transactions": [
      {
        "transaction_id": "txn_abc123",
        "date": "2026-02-03",
        "merchant": "Whole Foods",
        "amount": -87.43,
        "category": "Groceries"
      },
      {
        "transaction_id": "txn_def456",
        "date": "2026-02-02",
        "merchant": "Netflix",
        "amount": -15.99,
        "category": "Entertainment"
      }
    ]
  },
  "meta": {
    "plan": "free",
    "rateLimit": { "remaining": 49, "limit": 50, "resetAt": "2026-02-05T00:00:00.000Z" }
  }
}
```

**Agent responds:** "Here are your last 5 transactions. Your most recent was $87.43 at Whole Foods on Feb 3."

---

## Spending Breakdown

**User:** "Where did my money go this month?"

**Agent makes request:**

```bash
curl -s https://api.fyn.fyi/v1/agent/spending/breakdown \
  -H "Authorization: Bearer $FYN_API_KEY" \
  -H "Content-Type: application/json" \
  -d '{"group_by": "category", "start_date": "2026-02-01", "end_date": "2026-02-28", "limit": 5}'
```

**Response:**
```json
{
  "success": true,
  "data": {
    "breakdown": [
      { "category": "Groceries", "total": 342.18, "count": 8 },
      { "category": "Dining", "total": 187.50, "count": 12 },
      { "category": "Transportation", "total": 145.00, "count": 4 },
      { "category": "Entertainment", "total": 89.97, "count": 3 },
      { "category": "Shopping", "total": 67.23, "count": 2 }
    ],
    "period": { "start": "2026-02-01", "end": "2026-02-28" },
    "total": 831.88
  }
}
```

**Agent responds:** "This month you've spent $831.88 so far. Groceries lead at $342.18 (8 transactions), followed by Dining at $187.50."

---

## Check Account Balances

**User:** "What's my net worth?"

```bash
curl -s https://api.fyn.fyi/v1/agent/accounts/net-worth \
  -H "Authorization: Bearer $FYN_API_KEY"
```

**Agent responds:** "Your current net worth is $47,832.15 — $52,100 in assets minus $4,267.85 in liabilities."
