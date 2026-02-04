# Receipt Search — AI-Powered Receipt Intelligence (Pro)

Receipt features use AI to parse, index, and search your uploaded receipts. These endpoints require a Pro plan.

## Search Receipt Items

**User:** "How much have I been spending on coffee?"

**Agent makes request:**

```bash
curl -s https://api.fyn.fyi/v1/agent/receipts/search \
  -H "Authorization: Bearer $FYN_API_KEY" \
  -H "Content-Type: application/json" \
  -d '{"query": "coffee", "start_date": "2026-01-01", "end_date": "2026-02-28"}'
```

**Response:**
```json
{
  "success": true,
  "data": {
    "items": [
      {
        "item_name": "Oat Milk Latte",
        "price": 5.75,
        "merchant": "Blue Bottle Coffee",
        "date": "2026-02-02",
        "receipt_id": "rct_abc123"
      },
      {
        "item_name": "Drip Coffee x2",
        "price": 7.50,
        "merchant": "Starbucks",
        "date": "2026-01-28",
        "receipt_id": "rct_def456"
      },
      {
        "item_name": "Cold Brew 12oz",
        "price": 4.99,
        "merchant": "Trader Joe's",
        "date": "2026-01-15",
        "receipt_id": "rct_ghi789"
      }
    ],
    "total": 18.24,
    "count": 3
  }
}
```

**Agent responds:** "You've spent $18.24 on coffee items across 3 receipts since January. Blue Bottle was the priciest at $5.75 for an oat milk latte."

---

## Chat with Receipts (RAG)

**User:** "What did I buy at Costco last time?"

```bash
curl -s https://api.fyn.fyi/v1/agent/receipts/rag \
  -H "Authorization: Bearer $FYN_API_KEY" \
  -H "Content-Type: application/json" \
  -d '{"query": "What did I buy at Costco last time?"}'
```

**Response:**
```json
{
  "success": true,
  "data": {
    "answer": "Your last Costco trip on Jan 27 totaled $187.43. You bought: Kirkland Organic Eggs ($6.99), Rotisserie Chicken ($4.99), Kirkland Paper Towels 12-pack ($18.99), Organic Blueberries 2lb ($8.49), and 8 other items.",
    "sources": [
      { "receipt_id": "rct_xyz", "merchant": "Costco", "date": "2026-01-27", "total": 187.43 }
    ]
  }
}
```

---

## Price Insights

**User:** "Am I overpaying for eggs?"

```bash
curl -s https://api.fyn.fyi/v1/agent/receipts/insights \
  -H "Authorization: Bearer $FYN_API_KEY" \
  -H "Content-Type: application/json" \
  -d '{"item": "eggs"}'
```

**Agent responds:** "Based on your receipts, you pay an average of $5.89 for eggs. Costco is your cheapest option at $4.99. Whole Foods is the most expensive at $7.49."

---

## Find Better Deals

**User:** "Where can I save money on groceries?"

```bash
curl -s https://api.fyn.fyi/v1/agent/receipts/deals \
  -H "Authorization: Bearer $FYN_API_KEY"
```

**Agent responds:** "Based on your purchase history, switching these items to cheaper stores could save you $23/month: milk (Trader Joe's vs Whole Foods saves $2.50/gallon), bread (Costco vs local bakery saves $3/loaf)."
