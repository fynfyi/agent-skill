# Budget Check — Monitor Budgets & Affordability

## Check Budget Status

**User:** "How's my budget looking?"

**Agent makes request:**

```bash
curl -s https://api.fyn.fyi/v1/agent/budget/status \
  -H "Authorization: Bearer $FYN_API_KEY"
```

**Response:**
```json
{
  "success": true,
  "data": {
    "budgets": [
      {
        "category": "Groceries",
        "budget": 400.00,
        "spent": 342.18,
        "remaining": 57.82,
        "percent_used": 85.5
      },
      {
        "category": "Dining",
        "budget": 200.00,
        "spent": 187.50,
        "remaining": 12.50,
        "percent_used": 93.8
      },
      {
        "category": "Entertainment",
        "budget": 100.00,
        "spent": 89.97,
        "remaining": 10.03,
        "percent_used": 90.0
      }
    ]
  }
}
```

**Agent responds:** "Your budgets are getting tight this month. Dining is at 93.8% ($12.50 left), Entertainment at 90% ($10.03 left), and Groceries at 85.5% ($57.82 left)."

---

## Categories Over Budget

**User:** "Am I over budget on anything?"

```bash
curl -s https://api.fyn.fyi/v1/agent/budget/over \
  -H "Authorization: Bearer $FYN_API_KEY"
```

**Response:**
```json
{
  "success": true,
  "data": {
    "over_budget": [
      {
        "category": "Shopping",
        "budget": 150.00,
        "spent": 217.23,
        "over_by": 67.23,
        "percent_used": 144.8
      }
    ]
  }
}
```

**Agent responds:** "You're over budget on Shopping by $67.23 (spent $217.23 against a $150 budget). All other categories are still within limits."

---

## Check Affordability (Pro)

**User:** "Can I afford a new PS5?"

```bash
curl -s https://api.fyn.fyi/v1/agent/affordability \
  -H "Authorization: Bearer $FYN_API_KEY" \
  -H "Content-Type: application/json" \
  -d '{"amount": 499.99, "description": "PS5"}'
```

**Response:**
```json
{
  "success": true,
  "data": {
    "affordable": true,
    "confidence": "medium",
    "analysis": {
      "checking_balance": 3247.82,
      "monthly_surplus": 412.50,
      "impact": "This purchase would use 15.4% of your checking balance. Based on your average monthly surplus of $412.50, you'd recover in about 5 weeks.",
      "recommendation": "Affordable, but it would tighten your budget. Consider waiting until after your next paycheck."
    }
  }
}
```

**Agent responds:** "You can technically afford the PS5 at $499.99 — your checking has $3,247.82 and you average a $412.50 monthly surplus. But it would use 15.4% of your balance. You'd recover in about 5 weeks."

---

## Subscriptions & Cash Flow

**User:** "How much am I spending on subscriptions?"

```bash
curl -s https://api.fyn.fyi/v1/agent/subscriptions/total \
  -H "Authorization: Bearer $FYN_API_KEY"
```

**Agent responds:** "Your detected subscriptions total $127.93/month across 8 services."

**User:** "What's my savings rate?"

```bash
curl -s https://api.fyn.fyi/v1/agent/cashflow/savings-rate \
  -H "Authorization: Bearer $FYN_API_KEY"
```

**Agent responds:** "Your savings rate is 18.3% — you're saving about $1,098 per month out of $6,000 in income."
