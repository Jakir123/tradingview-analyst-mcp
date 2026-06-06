# DSE-Specific Rules & Adaptations
**Always apply these rules on top of any strategy. DSE has unique characteristics.**

---

## DSE Market Characteristics

| Feature | Detail | Impact on Strategy |
|---|---|---|
| Circuit breaker | 10% daily price limit (up or down) | Breakouts can be slow — don't chase gaps |
| Market hours | Sun–Thu, 10:00 AM – 2:30 PM (Bangladesh time) | Plan trades before market opens |
| Settlement | T+2 | Cash is tied up for 2 days after selling |
| Retail dominated | 70%+ retail investors | More emotional swings, clearer patterns |
| Low institutional | Less sophisticated money | Trends persist longer, reversals can be sharp |
| Sector sensitivity | Telecom, Pharma, Bank, Textile dominant | Follow sector rotation |
| Political sensitivity | Government policy affects market sentiment | Watch macro/political news |

---

## Minimum Requirements (Filter Before Analysis)

Reject any stock that does NOT meet these minimums:

| Filter | Minimum | Why |
|---|---|---|
| Average daily volume | 80,000 shares/day | Below this = illiquid, hard to exit |
| Price | Above 20 BDT | Penny stocks are high manipulation risk |
| Market cap | Preference for large/mid cap | More reliable patterns |
| Listed age | At least 2 years on DSE | Enough data for analysis |

---

## DSE Market Direction Rules (Check DSEX First)

Before analyzing any stock, always check DSEBD:DSEX (DSE broad index):

| DSEX Condition | Your Action |
|---|---|
| DSEX above 20-week MA and rising | Full confidence in long/swing setups |
| DSEX near 20-week MA (flat) | Selective — only best setups |
| DSEX below 20-week MA | Reduce position sizes by 50% |
| DSEX in clear downtrend | Only trade with 25% normal size or stay in cash |

**How to check:** Ask Claude — *"Switch to DSEBD:DSEX weekly chart and tell me the trend direction."*

---

## DSE Sector Rotation Priority

When market is bullish, sectors move in this general order on DSE:

1. **Banking & NBFI** — first to move in a bull cycle (liquidity providers)
2. **Telecom** (GP, Robi) — large cap leaders, move steadily
3. **Pharma** (SQURPHARMA, RENATA, BEXIMCO PHARMA) — defensive, steady growers
4. **IT/Tech** — higher beta, move more aggressively
5. **Textile/Garments** — export driven, sensitive to USD/BDT and global demand
6. **Cement/Construction** — infrastructure cycle dependent
7. **Insurance** — laggards, move last and weakest

**Rule:** Focus on stocks in the LEADING sectors for that market cycle.

---

## DSE-Specific Entry Rules

### Do Use Limit Orders (Not Market Orders)
- DSE has wide bid-ask spreads on many stocks
- Market orders can get filled at bad prices
- Always use limit orders within 0.5% of the current price

### Circuit Breaker Strategy
- If a stock is near the 10% upper circuit, do NOT chase it
- Wait for it to settle into a box the next day or two
- Buy the pullback, not the circuit run

### Volume Confirmation for DSE
- Standard: 1.5x average volume on breakout day
- For DSE large caps (GP, SQUARE, RENATA): 1.3x is sufficient (already liquid)
- For DSE mid caps: require 2x average volume — more manipulation risk

---

## DSE Red Flags (Avoid These)

| Red Flag | Why to Avoid |
|---|---|
| Stock up 9-10% (near upper circuit) for 3+ days in a row | Possible pump — smart money distributing to retailers |
| Sudden 3-5x volume spike with no news | Manipulation signal |
| Price rises while DSEX falls | Suspicious divergence — check for news |
| Stock below 20 BDT | Penny stock zone — avoid |
| No analyst coverage | Less transparent — higher risk |
| Frequent regulatory actions on company | Governance risk |

---

## DSE Position Sizing Rules

Use these position sizes based on setup quality:

| Setup Quality | Max Position Size (% of portfolio) |
|---|---|
| A+ setup (all signals align, DSEX bullish) | 15-20% |
| A setup (most signals align) | 10-15% |
| B setup (partial confirmation) | 5-10% |
| Experimental / testing | 2-5% |
| Speculative / small cap | Max 3% |

**Never put more than 20% in a single stock — no exceptions on DSE.**

---

## Stop Loss Rules for DSE

| Strategy | Stop Loss |
|---|---|
| Momentum (Minervini) | 7-8% below entry |
| Swing trade (Darvas) | Below the box bottom |
| Stage 2 entry (Weinstein) | Below the 30-week MA |
| Any trade | Never more than 10% loss — MUST EXIT |

---

## DSE Watchlist — Reliable Stocks for Pattern Analysis

These stocks tend to have clean, reliable technical patterns on DSE:

| Stock | Category | Why Reliable |
|---|---|---|
| GP (Grameenphone) | Large cap Telecom | Highest liquidity, clean patterns |
| SQURPHARMA | Large cap Pharma | Strong fundamentals, trendy |
| RENATA | Large cap Pharma | Premium stock, institutional interest |
| BRACBANK | Large cap Bank | High volume, good patterns |
| DUTCHBANGLA | Large cap Bank | Very liquid |
| MARICO | Large cap FMCG | Steady, low volatility |

---

## Reporting Format — How Claude Should Report DSE Analysis

Every analysis must include:

```
STOCK: [Symbol]
STAGE: [1/2/3/4] (Weinstein)
SEPA SCORE: [X/7] (Minervini)
BOX SETUP: [Yes/No] (Darvas)
DSE FILTERS: [Pass/Fail]
---
SIGNAL: [STRONG BUY / BUY / WATCH / AVOID]
ENTRY: [price range]
STOP LOSS: [price] ([X]% below entry)
TARGET 1: [price] ([X]% above entry)
TARGET 2: [price] ([X]% above entry)
RISK/REWARD: [1:X]
CONFIDENCE: [High/Medium/Low]
---
REASON: [2-3 sentences explaining the setup]
RISK: [Key risk to watch]
```
