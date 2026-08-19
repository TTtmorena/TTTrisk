# TTTrisk — Advanced API Reference

This document contains the official and recommended data sources used by **TTTrisk**.  
All endpoints are public or officially documented by Bankr. No authentication is required for the core fee endpoints.

---

## 1. Primary Endpoint — Token Fees (Most Important)

**GET** `https://api.bankr.bot/token-launches/{tokenAddress}/fees?days=30`

Legacy (still working but deprecated):  
`https://api.bankr.bot/public/doppler/token-fees/{tokenAddress}?days=30`

### Critical Fields for Risk Analysis

| Field                    | Description                                      | Usage in TTTrisk                          |
|--------------------------|--------------------------------------------------|-------------------------------------------|
| `lifetimeEarnedWeth`     | Total lifetime fees earned                       | Fee sustainability baseline               |
| `totals.claimableWeth`   | Currently claimable fees                         | Activity & liquidity proxy                |
| `dailyEarnings[]`        | Array of `{ date, weth }`                        | **Core for Fee Sustainability trend**     |
| `lifetimeBestDay`        | Best single day earnings                         | Peak performance reference                |
| `chain`                  | `"base"` or `"robinhood"`                        | Dual-chain awareness                      |
| `tokens[0].share`        | Creator fee share (usually ~57%)                 | Fee quality check                         |

### Example Response Structure
```json
{
  "address": "0x...",
  "chain": "base",
  "days": 30,
  "lifetimeEarnedWeth": "1.2345",
  "lifetimeDays": 42,
  "lifetimeBestDay": {
    "date": "2026-03-22",
    "weth": "0.0891"
  },
  "dailyEarnings": [
    { "date": "2026-08-10", "weth": "0.0123" },
    { "date": "2026-08-11", "weth": "0.0087" },
    { "date": "2026-08-12", "weth": "0.0156" }
  ],
  "totals": {
    "claimableWeth": "0.0456",
    "claimedWeth": "1.1889",
    "claimCount": 5
  }
}
```

**Rules for TTTrisk:**
- Always request `days=30` by default (allowed range: 1–90)
- Use `dailyEarnings` to calculate fee trend (rising / flat / declining / collapsing)
- Convert all WETH values to approximate USD using current ETH price
- Response is cached server-side for ~2 minutes

---

## 2. Creator / Portfolio Fees (for Portfolio Risk)

**GET** `https://api.bankr.bot/public/doppler/creator-fees/{walletAddress}?days=30`

Use this when the user asks for:
- “portfolio risk”
- “my risk”
- “TTTrisk portfolio”
- concentration analysis across all tokens

This endpoint returns fees for **all tokens** created by or benefiting the wallet.  
Perfect for calculating **Concentration Risk**.

---

## 3. Recent Launches

**GET** `https://api.bankr.bot/token-launches`

Returns the 50 most recent Bankr token launches.  
Useful for comparative risk context (optional advanced mode).

---

## 4. Agent Profiles

**GET** `https://api.bankr.bot/agent-profiles?sort=marketCap&limit=20`  
**GET** `https://api.bankr.bot/agent-profiles/{slug-or-address}`

Useful fields for risk enrichment:
- `marketCapUsd`
- `weeklyRevenueWeth`
- Token metadata

---

## 5. Market Data Sources (Price • Volume • Liquidity • Holders)

**Priority order** (use the first available):

1. **GeckoTerminal** / **DexScreener** (preferred)
2. **Birdeye**
3. **Zerion** or **Alchemy** (on-chain)
4. CoinGecko (fallback)

### Required Metrics for Risk Scoring

| Metric                      | Why Critical for TTTrisk                     |
|-----------------------------|----------------------------------------------|
| Current Price (USD)         | Base for volatility & drawdown               |
| 24h Price Change (%)        | Short-term volatility                        |
| 7d Price Change (%)         | Medium-term volatility                       |
| 24h Volume (USD)            | Activity confirmation                        |
| Liquidity (USD)             | **Most important** for Liquidity Health      |
| Market Cap (USD)            | Used with Liquidity for ratio                |
| Holders (if available)      | Optional concentration signal                |

### Key Derived Metric (Mandatory)
**Liquidity / Market Cap ratio**  
- ≥ 15% → Strong  
- 8% – 15% → Moderate  
- < 8% → Weak / High Risk

---

## 6. Best Practices for TTTrisk

- Cache all responses for 1–2 minutes within the same conversation
- Never invent or estimate missing numbers
- Always show both WETH and approximate USD
- Always detect and display the correct chain (`base` or `robinhood`)
- Prefer the newest Bankr endpoints over legacy ones
- If data is incomplete → lower Confidence level and clearly state “Limited data”
- Liquidity / Market Cap ratio is mandatory for every risk report
- `dailyEarnings` array is the primary source for Fee Sustainability scoring

---

**TTTrisk** uses these endpoints to deliver the most accurate, transparent, and actionable risk intelligence in the Bankr ecosystem.

**Protect capital. Optimize exposure. Stay resilient.**
```
