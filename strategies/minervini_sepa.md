# Mark Minervini — SEPA + VCP Strategy
**Best for:** Momentum trading entries, identifying stocks about to make big moves

## The Core Idea
Only buy the very strongest stocks at the very best entry points. Minervini's SEPA (Specific Entry Point Analysis) ensures you only enter when price, trend, and volume all align perfectly. His VCP (Volatility Contraction Pattern) gives you the precise entry point.

---

## SEPA Trend Template — The 7-Point Checklist

A stock must pass ALL 7 checks before considering an entry:

### Check 1: Price Above 200-Day MA
- Current price must be ABOVE the 200-day moving average
- This confirms the stock is in a long-term uptrend
- **Fail = SKIP the stock entirely**

### Check 2: 150-Day MA Above 200-Day MA
- The 150-day MA must be above the 200-day MA
- This confirms the medium-term trend is aligned with the long-term trend
- **Fail = SKIP**

### Check 3: 200-Day MA Trending Up
- The 200-day MA must have been rising for at least 1 month (4-5 weeks)
- A flat or declining 200-day MA means the stock is not in a true uptrend
- **Fail = SKIP**

### Check 4: 50-Day MA Above Both 150 and 200-Day MA
- The 50-day MA must be above the 150-day and 200-day MAs
- Short-term trend must be stronger than medium and long-term trends
- **Fail = SKIP**

### Check 5: Price at Least 25% Above 52-Week Low
- The stock must have already made a significant move from its lows
- This proves the stock has momentum — weak stocks don't do this
- **Formula:** (Current Price - 52W Low) / 52W Low × 100 ≥ 25%

### Check 6: Price Within 25% of 52-Week High
- The stock should be near its highs, not deep in a correction
- Ideally within 10-15% of the 52-week high
- **Formula:** (52W High - Current Price) / 52W High × 100 ≤ 25%

### Check 7: Relative Strength — Stock Outperforms the Market
- The stock must be going up more than the DSE broad index (DSEX)
- If DSEX is up 5% in 3 months but the stock is up 20%, it has strong RS
- **On TradingView:** Compare stock performance to DSEBD:DSEX

---

## VCP — Volatility Contraction Pattern (The Entry Setup)

After a stock passes the SEPA checklist, wait for the VCP before entering. This is the actual entry trigger.

### What VCP Looks Like
```
Price: ──▲───────╮         ╭───────▲ (breakout)
              ╰──╮   ╭──╯
                 ╰───╯
Volume: HIGH    MED   LOW   LOW    HIGH (on breakout)
```

- Stock makes a high, then pulls back (Contraction 1) — e.g., 15% pullback
- Bounces, then pulls back again, but LESS (Contraction 2) — e.g., 8% pullback
- Bounces, then pulls back even less (Contraction 3) — e.g., 4% pullback
- Volume DRIES UP during each contraction
- **Entry: Buy the breakout from the final tight contraction with HIGH volume**

### VCP Rules
- Each pullback must be smaller than the previous (contracting volatility)
- Volume must decrease on each pullback (drying up = smart money not selling)
- Volume must SURGE on the breakout (smart money buying)
- The tighter and longer the final base, the more powerful the breakout

---

## Entry Rules

- **Buy point:** Pivot high of the last contraction + 0.5-1% (just above resistance)
- **Position size:** Risk no more than 1-2% of portfolio on the stop loss
- **Add to position:** If stock moves 2-3% in your favor, add more (pyramiding)

---

## Stop Loss Rules

- **Initial stop:** Just below the lowest point of the VCP base (1-2% below)
- **Never move stop down** — only move it up as price rises
- **Hard rule:** If stock falls 7-8% from entry, EXIT. No exceptions.
- **Minervini's rule:** *"Cut every loss at a maximum of 10%. Most at 5-7%."*

---

## Target / Profit Taking

- **Minimum target:** 2:1 reward-to-risk (if stop is 8% below entry, target is 16% above)
- **Sell 1/3 at first target** — lock in profits
- **Trail stop on remaining 2/3** — let winners run
- **Sell all** if stock makes a climax run (huge gap up on enormous volume after a long advance)

---

## SEPA Score Card (Use This for Quick Screening)

| Check | Condition | Pass/Fail |
|---|---|---|
| 1 | Price > 200-day MA | ? |
| 2 | 150-day MA > 200-day MA | ? |
| 3 | 200-day MA rising for 1+ month | ? |
| 4 | 50-day MA > 150-day MA > 200-day MA | ? |
| 5 | Price 25%+ above 52-week low | ? |
| 6 | Price within 25% of 52-week high | ? |
| 7 | Stock outperforming DSEX index | ? |
| VCP | Volatility contracting, volume drying | ? |

**Score 7/7 + VCP = Strong momentum buy candidate**
**Score 5-6/7 = Watch list**
**Score < 5/7 = Skip**

---

## DSE Adaptation Notes

- Use 200-day MA, 150-day MA, 50-day MA on TradingView daily chart
- Compare stock to DSEBD:DSEX for relative strength
- DSE circuit breaker (10% daily limit) means gap-up breakouts can be limited — use limit orders at pivot
- Minimum volume for DSE momentum stocks: 100,000 shares/day average
- VCP works extremely well on DSE large-cap stocks (GP, SQUARE, RENATA, BRAC BANK)

---

## Key Minervini Quotes
- *"The stock market is not about buying cheap — it's about buying right."*
- *"Every big winner was once a little stock making new highs."*
- *"The best time to buy is when a stock is going up."*
