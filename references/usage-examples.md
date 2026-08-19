# TTTrisk — Usage Examples

This document lists the most common triggers and expected behavior of **TTTrisk**.  
All responses must follow the standard 🛡️ TTTrisk Report format defined in SKILL.md.

---

## 1. Single Token Risk Assessment (Most Common)

```
TTTrisk for CLAWD
risk assessment for this token
how risky is this
TTTrisk $TICKER
is this token safe?
risk score for 0x...
full risk report
```

**Expected Output:**  
Full 🛡️ TTTrisk Report including:
- Overall Risk Score (0–100 + label)
- Liquidity Health (ratio + label)
- Volatility (24h / 7d)
- Fee Sustainability
- Approximate Drawdown
- Position Sizing Suggestion
- Key Risk Drivers
- Quick Actions (cross-skill)

---

## 2. Portfolio Risk Overview

```
portfolio risk
my risk
TTTrisk portfolio
my overall risk score
concentration risk
how risky is my portfolio
```

**Expected Output:**  
- Portfolio-level Overall Risk Score
- Concentration Risk percentage
- Ranking of tokens from highest to lowest risk
- Total claimable + lifetime fees
- Position sizing advice for the whole portfolio
- Suggested next actions

---

## 3. Liquidity Health Focus

```
liquidity health
liquidity risk
how is the liquidity
liquidity / market cap
is liquidity healthy?
```

**Expected Output:**  
Detailed Liquidity Health section with exact ratio + clear Strong / Moderate / Weak label, plus overall risk context.

---

## 4. Volatility & Drawdown

```
volatility check
how volatile is this
drawdown analysis
price risk
24h volatility
```

**Expected Output:**  
Emphasis on 24h & 7d volatility + approximate recent drawdown, with risk implications.

---

## 5. Position Sizing Requests

```
position size suggestion
how much should I allocate
recommended allocation
position sizing
max exposure
```

**Expected Output:**  
Clear recommended max allocation percentage based on current Overall Risk Score, with transparent reasoning + disclaimer.

---

## 6. Chain-Specific Risk

```
TTTrisk on Base
TTTrisk on Robinhood
risk on Base only
Robinhood risk assessment
```

**Expected Output:**  
Risk report filtered to the requested chain only.

---

## 7. Comparative Risk

```
compare risk CLAWD vs Surplus
which one is riskier
side by side risk
```

**Expected Output:**  
Side-by-side risk comparison table + clear declaration of which token currently has higher risk.

---

## 8. Natural Language / Flexible Triggers

```
is it safe to buy more?
should I reduce exposure?
protect my capital on this token
give me a full risk analysis
risk intelligence for my top token
```

**Expected Output:**  
Intelligent interpretation → full or focused TTTrisk Report.

---

## General Behavior Rules

- Always try to resolve token name → address automatically
- If wallet address is needed for portfolio risk and unknown → ask clearly once
- Always display the correct chain (Base / Robinhood)
- Always show both WETH and approximate USD for fees
- Always include Overall Risk Score + Position Sizing Suggestion
- Never invent data
- Lower Confidence level and state “Limited data” when information is incomplete
- End every response with 1–3 useful next actions
- Cross-recommend:
  - TTTracker → deeper analytics
  - TTTsignal → trading view
  - TTTalert → set monitoring
  - TTTfolio → full portfolio view
- Maintain professional, protective, and data-first tone
- Use 🛡️ emoji consistently

---

**TTTrisk** is designed to feel like a professional risk intelligence layer for every Bankr agent and creator.

**Protect capital. Optimize exposure. Stay resilient.**
```
