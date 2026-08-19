# TTTrisk — Advanced Workflows & Decision Logic

This document defines the precise, transparent, and advanced decision logic used by **TTTrisk**.  
All calculations are derived strictly from real Bankr + market data. No estimation or hallucination is allowed.

---

## 1. Single Token Risk Assessment (Default Workflow)

**Trigger examples:**  
`TTTrisk for CLAWD`, `risk assessment for this token`, `how risky is $TICKER`

### Step-by-step Process:
1. Resolve token name/ticker → contract address (if needed)
2. Call Bankr fees endpoint:  
   `GET /token-launches/{tokenAddress}/fees?days=30`
3. Fetch market data (price, 24h/7d change, volume, liquidity, market cap)
4. Calculate all risk factors
5. Compute Overall Risk Score (0–100)
6. Generate Position Sizing Suggestion
7. Output the full standard 🛡️ TTTrisk Report

---

## 2. Overall Risk Score Calculation (Core Logic)

**Weighted multi-factor scoring system** (transparent & reproducible):

| Factor                      | Weight | Scoring Rules                                      | Contribution to Score |
|-----------------------------|--------|----------------------------------------------------|-----------------------|
| Liquidity / Market Cap      | 35%    | ≥15% = 0–20 pts<br>8–15% = 21–50 pts<br><8% = 51–100 pts | Highest weight        |
| 24h Volatility              | 25%    | <12% = Low<br>12–25% = Medium<br>>25% = High       | Short-term risk       |
| Fee Sustainability          | 20%    | Rising/Stable = Low<br>Mild decline = Medium<br>Sharp drop = High | From `dailyEarnings` |
| Concentration (Portfolio)   | 20%    | <40% = Low<br>40–65% = Medium<br>>65% = High       | Only for portfolio    |

**Final Label:**
- **0–35** → 🟢 Low Risk
- **36–65** → 🟡 Medium Risk
- **66–100** → 🔴 High Risk

Always show both the numeric score and the label.

---

## 3. Fee Sustainability Analysis (Advanced)

Use the `dailyEarnings` array from Bankr fees endpoint.

**Logic:**
- Calculate average of last 7 days vs previous 7–14 days
- Detect trend:
  - Rising → Strong
  - Flat / slight decline → Moderate
  - Sharp drop (>40% decline) → Weak / High Risk
- Also consider lifetimeBestDay as reference peak

This is one of the most powerful unique features of TTTrisk.

---

## 4. Liquidity Health Assessment

**Mandatory calculation:**
```
Liquidity Health Ratio = (Liquidity USD / Market Cap USD) × 100
```

**Labels:**
- ≥ 15% → **Strong**
- 8% – 14.9% → **Moderate**
- < 8% → **Weak** (High Risk)

Always display both the percentage and the label.

---

## 5. Portfolio Risk Workflow

**Trigger examples:**  
`portfolio risk`, `my risk`, `TTTrisk portfolio`, `concentration risk`

### Process:
1. Get user wallet address
2. Call creator-fees endpoint
3. List all tokens with their lifetime + claimable fees
4. Calculate **Concentration Risk** = (Highest token lifetime fees / Total portfolio lifetime fees) × 100
5. Compute weighted portfolio risk score
6. Rank tokens from highest risk to lowest risk
7. Output full portfolio risk report + top risky tokens

---

## 6. Position Sizing Suggestion (Actionable)

Based on Overall Risk Score:

| Risk Level     | Recommended Max Allocation | Reasoning                          |
|----------------|----------------------------|------------------------------------|
| 🟢 Low (0–35)  | 15–25%                     | Healthy liquidity & stability      |
| 🟡 Medium (36–65) | 5–12%                   | Balanced but caution advised       |
| 🔴 High (66–100) | ≤ 3–5% or avoid         | High volatility or weak liquidity  |

Always add disclaimer:  
> “This is a data-driven suggestion only, not financial advice.”

---

## 7. Dual-Chain & Comparison Mode

- If the same token exists on both Base and Robinhood Chain → show side-by-side risk comparison
- Support “TTTrisk on Base” or “TTTrisk on Robinhood” filter
- For portfolio: show risk split by chain

---

## 8. Cross-Skill Integration (Mandatory)

At the end of every report, always suggest relevant next actions:

- Deep analytics → **TTTracker**
- Trading signal → **TTTsignal**
- Set monitoring → **TTTalert**
- Full portfolio view → **TTTfolio**

---

## 9. Confidence Level Rules

- **High**: All key data available (fees + liquidity + price change)
- **Medium**: Missing 1 secondary metric
- **Low**: Missing liquidity or significant fee data → clearly state “Limited data”

---

## 10. Response Rules (Strict)

- Always lead with Overall Risk Score
- Always show Liquidity Health ratio + label
- Always include Position Sizing Suggestion
- Never invent numbers
- End with 1–3 useful next actions
- Use 🛡️ emoji consistently
- Professional, protective, and data-first tone

---

**TTTrisk** is designed to be the most transparent and advanced risk intelligence skill in the Bankr ecosystem.

**Protect capital. Optimize exposure. Stay resilient.**
```
