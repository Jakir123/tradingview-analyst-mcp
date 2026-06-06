# User's Guide — DSE Stock Analysis with Claude AI

How to get the most out of this system: every prompt pattern, workflow, strategy, and tip for analyzing DSE stocks using Claude + TradingView.

---

## Before You Start — Every Session

### Startup Checklist

- [ ] Launch TradingView with debug port (do NOT open from Dock):
  ```bash
  bash tradingview-mcp/scripts/launch_tv_debug_mac.sh
  ```
- [ ] Open this project in Claude Code (VS Code)
- [ ] Open your target stock on TradingView
- [ ] Verify connection — ask Claude:
  > *"Run tv_health_check"*
- [ ] You're ready

### First-Time Setup

If you've never used this before, see [README.md](README.md) for full installation steps.

---

## Core Analysis Prompts

These are the most powerful prompts to use. Copy and adapt them.

### Full Stock Analysis (Most Useful)

```
Analyze this chart. Add RSI(14), MACD, and EMA(20,50) if not there.
Then give me momentum signals, key levels, and a trade setup with
entry, stop, and target.
```

Claude will: check DSE filters → identify Weinstein Stage → score SEPA → find Darvas boxes → read live MACD/RSI → deliver the full report.

### Quick Momentum Check

```
Is there a momentum setup on this chart right now?
Check RSI, MACD histogram, and whether price is above EMA50.
Only flag as BUY if at least 2 of 3 confirm.
```

### Swing Trade Setup

```
On the daily chart, identify the Darvas Box structure.
Find the box top, box bottom, and volume pattern.
Is this near a valid breakout entry? Give entry, stop below the box, and target.
```

### Long-Term Investment Check

```
Switch to weekly chart. Apply Weinstein Stage Analysis.
What stage is this stock in? Is the 30-week MA rising?
Should I consider this for long-term holding?
```

### Multi-Stock Scan

```
Scan these stocks one by one: DSSL, MONNOFABR, FEKDIL.
For each: check momentum (RSI, MACD), identify the stage, and give a
BUY / WAIT / AVOID verdict with a one-line reason. Rank them at the end.
```

### Market Direction Check (Do This First)

```
Switch to DSEBD:DSEX weekly chart.
Is the index above or below its 20-week MA?
Is it rising or declining? What does this mean for my long setups?
```

### Compare Two Stocks

```
Compare [STOCK A] and [STOCK B] side by side.
Analyze both: stage, SEPA score, MACD, key levels, and trade setup.
Which one has the better risk/reward and cleaner setup right now?
```

---

## Strategy-Specific Workflows

### Weinstein Stage Analysis

Use this to identify the broad trend before any entry.

**Step 1 — Check the Stage:**
```
Switch to daily chart for [SYMBOL].
Apply Weinstein Stage Analysis. What stage is this stock in?
Look at: price vs 30-week MA, volume pattern, price structure (higher highs/lows).
```

**Step 2 — If Stage 2, time the entry:**
```
The stock is in Stage 2. Where is the optimal pullback entry?
Find the 30-week MA level and the most recent higher low.
Is price currently above the 30-week MA?
```

**Step 3 — Stage 3/4 — exit or avoid:**
```
Is this stock showing Stage 3 topping signs?
Check: volume on down days vs up days, MA flattening, price choppiness near highs.
Should I exit or reduce position?
```

**Stage Reference:**

| Stage | Action |
|---|---|
| Stage 1 (Basing) | Watch. Set alert at resistance. |
| Stage 2 (Uptrend) | BUY on breakout or pullback to 30W MA. |
| Stage 3 (Topping) | Take 50% profits. Trail stop. |
| Stage 4 (Downtrend) | Do not touch. |

---

### Minervini SEPA + VCP

Use this for momentum entries on strong stocks.

**Full SEPA Check:**
```
Run the Minervini SEPA checklist on this stock.
Check all 7 conditions: price vs 200MA, 150MA vs 200MA, 200MA trend direction,
50MA stack, 25% above 52W low, within 25% of 52W high, and RS vs DSEX.
Give me a score out of 7.
```

**VCP Pattern:**
```
Look at the last 60 bars. Is there a Volatility Contraction Pattern (VCP)?
Find: each pullback smaller than the previous, volume drying up on contractions,
and the pivot point (last tight area before breakout).
Where is the exact entry pivot?
```

**Quick SEPA Score:**
```
Does this stock pass the Minervini SEPA template?
Give me a quick score (X/7) and flag any checks that fail.
```

**SEPA Score Guide:**

| Score | Action |
|---|---|
| 7/7 + VCP | Strong momentum buy candidate |
| 5-6/7 | Watchlist — wait for VCP or stage confirmation |
| Below 5/7 | Skip |

---

### Darvas Box Theory

Use this for swing trade breakout entries.

**Find the Box:**
```
Look at the last 60 bars. Identify any Darvas Box formation —
a tight range where price consolidated for at least 5 days.
Find the box top, box bottom, and tell me if we are near a breakout.
Volume should be declining inside the box.
```

**Breakout Entry:**
```
Is this stock breaking out of a Darvas Box right now?
Check: did price close above the box top? Was volume at least 1.5x average?
Give me: entry (just above box top), stop (below box bottom), target (box height x2).
```

**Multi-Box Stack:**
```
How many Darvas Boxes has this stock built?
Map out each box (top, bottom, breakout date) and identify where we are in the sequence.
Is there room for another leg up?
```

**Box Rules Reminder:**

| Rule | Requirement |
|---|---|
| Box width | Max 15-20% range (tighter = better) |
| Duration | Minimum 1 week inside the box |
| Volume in box | Must be declining or quiet |
| Breakout volume | Must be 1.5x+ average |
| Entry | Buy just above box top on a close above it |
| Stop | Just below box bottom |

---

### Livermore Trade Management

Use these prompts after you're in a trade.

**Before Entering:**
```
I'm about to buy [SYMBOL] at [PRICE]. Run the Livermore pre-trade checklist:
Is DSEX in an uptrend? Is the stock in Stage 2? Is there a clear pivotal point?
Is my stop loss defined? Is my risk less than 2% of portfolio?
```

**While in a Trade:**
```
I bought [SYMBOL] at [PRICE]. Current price is [CURRENT].
Apply Livermore rules: Should I hold, add (pyramid), or exit?
Is the stock still above its key MA? Any distribution signals?
```

**Position Sizing:**
```
My total portfolio is [AMOUNT]. I want to trade [SYMBOL].
My stop is at [STOP PRICE] and entry at [ENTRY PRICE].
Apply Livermore position sizing — how much should I buy for the first tranche?
```

---

## DSE-Specific Workflows

### Check the Broad Market First (Always)

Before any trade, run this:

```
Switch to DSEBD:DSEX weekly chart.
Is the DSEX above or below its 20-week MA? Is it rising or flat or declining?
Based on DSE market direction rules, how should I size my positions today?
```

**DSE Market Direction Rules:**

| DSEX Condition | Your Action |
|---|---|
| Above 20W MA, rising | Full size — aggressive entries |
| Near 20W MA, flat | Selective — only best setups |
| Below 20W MA | Half size — reduce all positions |
| Clear downtrend | 25% size or stay in cash |

### DSE Sector Rotation Check

```
What sector is [SYMBOL] in?
In the current DSE market cycle, which sectors are leading and which are lagging?
Is this stock's sector in favor right now?
```

**DSE Sector Rotation Order (Bull Cycle):**
1. Banking & NBFI (first to move)
2. Telecom (steady leaders)
3. Pharma (defensive, reliable)
4. IT/Tech (aggressive movers)
5. Textile/Garments (export-driven)
6. Cement/Construction
7. Insurance (last, weakest)

### DSE Filter Check

```
Does [SYMBOL] pass the DSE minimum filters?
Check: average daily volume above 80,000 shares, price above 20 BDT,
and look for any red flags (pump patterns, regulatory issues, erratic volume).
```

### DSE Circuit Breaker Strategy

```
[SYMBOL] is near its upper circuit today (up ~9-10%).
Apply DSE circuit breaker rules — should I chase this or wait?
If wait, what level should I set an alert for the pullback entry?
```

---

## Alert Workflows

### Set Entry Alert

After analysis, immediately lock in your levels:

```
Set a TradingView alert at [BREAKOUT PRICE] for [SYMBOL].
Condition: price crossing above this level.
I want to know the moment it breaks out.
```

### Set Stop Loss Alert

```
Set an alert for [SYMBOL] at [STOP PRICE].
Condition: price crossing below this level.
This is my stop loss — alert me immediately if it's hit.
```

### Multiple Alerts at Once

```
Set three alerts for [SYMBOL]:
1. Alert at [ENTRY PRICE] — this is my buy trigger (crossing above)
2. Alert at [TARGET 1] — first profit-taking level (crossing above)
3. Alert at [STOP PRICE] — stop loss (crossing below)
```

### Review Active Alerts

```
List all my active TradingView alerts.
Which stocks am I watching and at what levels?
```

---

## Screenshot & Documentation Workflows

### Save Analysis

```
Take a screenshot of the current chart.
Save it so I can review this setup later.
```

### Before/After Comparison

```
Take a screenshot of [SYMBOL] daily chart now.
I want to document this setup before the potential breakout.
```

### Strategy Tester Results

```
Take a screenshot of the strategy tester results.
What are the key performance metrics showing?
```

---

## Pine Script Assistance

### Write a Custom Indicator

```
Write a Pine Script indicator that:
- Shows EMA(20) and EMA(50) on the price chart
- Colors the background green when EMA20 > EMA50 and price is above both
- Colors it red when price is below EMA50
- Shows a "BUY" label when MACD histogram turns positive above EMA20
Add it to my chart.
```

### Write a DSE Strategy

```
Write a Pine Script strategy using these rules:
- Buy signal: price breaks above a 20-day high with volume 1.5x average
- Stop loss: 7% below entry
- Target: 15% above entry
- Only trade when price is above EMA50
Compile it and show me the backtest results.
```

### Debug Pine Script

```
My Pine Script has errors. Read the current code, fix the errors,
and recompile. Show me what you changed and why.
```

---

## Daily & Weekly Routines

### Morning Routine (15 min)

1. **Check market direction:**
   > *"Switch to DSEBD:DSEX weekly and tell me the trend direction and 20W MA position."*

2. **Quick watchlist scan:**
   > *"Scan these stocks one by one and give each a momentum score 1-10: [your watchlist]. Rank them."*

3. **Focus on the top 2:**
   > *"Do a full analysis on [TOP STOCK] — add indicators if needed, give the complete trade setup."*

4. **Set alerts:**
   > *"Set alerts at the entry and stop loss levels for [SYMBOL]."*

### Deep Dive on a Stock (30 min)

```
I want a full deep dive on [SYMBOL].

Step 1: Check DSEX direction — is the market supporting long trades?
Step 2: Apply Weinstein Stage Analysis — what stage is it in?
Step 3: Run the full Minervini SEPA checklist — give me the score.
Step 4: Look for Darvas Box structure — is there a valid box forming or broken?
Step 5: Read RSI and MACD values — confirm momentum direction.
Step 6: Give me the final trade setup: entry, stop, two targets, risk/reward.
Step 7: Set a TradingView alert at my entry level.
```

### Weekly Review (Sunday)

```
Switch to weekly chart for [SYMBOL].
How has the stock performed this week?
Is the Weinstein Stage still intact?
Any change in volume pattern or MA direction?
What should I watch for next week?
```

### End of Day Review

```
Take a screenshot of [SYMBOL] chart.
Summarize today's price action: where did price open, where did it close,
how was volume, and what does this mean for tomorrow?
What level should I watch?
```

---

## Timeframe Guide

| Goal | Timeframe | What to Ask |
|---|---|---|
| Momentum / Scalp | 15min or 1H | *"Switch to 1H and check RSI and MACD momentum"* |
| Swing Trade | Daily (1D) | *"Daily chart — Darvas Box setup and entry"* |
| Stage Analysis | Weekly (1W) | *"Weekly chart — Weinstein stage and 30W MA"* |
| Long-Term | Weekly + Monthly | *"Switch to weekly, tell me the multi-year trend"* |
| Confirmation | Check 2 timeframes | *"Analyze on daily and weekly both — do they agree?"* |

---

## Multi-Stock Comparison

### Two-Stock Head-to-Head

```
Compare [STOCK A] vs [STOCK B]:
- Weinstein Stage for both
- SEPA score for both
- Darvas Box structure for both
- MACD and RSI for both
- Which has better R:R and cleaner setup?
- Which would you trade first and why?
```

### Full Sector Scan

```
Scan the DSE textile sector: DSSL, MONNOFABR, FEKDIL, [add others].
For each stock:
1. Current price and DSE filter status
2. Weinstein Stage
3. Momentum signal (RSI + MACD)
4. Trade setup (BUY / WAIT / AVOID)
Rank them from best to worst setup quality.
```

### Batch Screenshot

```
Take screenshots of these stocks one by one: [SYMBOL1], [SYMBOL2], [SYMBOL3].
Save each for my records.
```

---

## Replay Mode — Practice & Backtesting

### Enter Replay Mode

```
Enter bar replay mode starting from [DATE e.g., 2024-01-15].
I want to practice reading this setup as if I were trading it live.
Step me forward one bar at a time.
```

### Step-by-Step Practice

```
Step forward one bar.
What does the chart show now? Should I enter, hold, or exit based on the setup?
```

### Trade in Replay

```
In replay mode, execute a buy at the current bar's close.
Set my stop loss at [PRICE].
Step forward and tell me how the trade is developing.
```

---

## Pro Tips for Best Results

### 1. Always Check DSEX First
The single most important habit. A stock in Stage 2 in a bear market still loses. Check `DSEBD:DSEX` weekly before any trade.

### 2. Use Limit Orders on DSE
Wide bid-ask spreads on many DSE stocks. Always ask Claude to identify a specific limit price, not just "buy at market."

### 3. Don't Chase Circuits
If a stock is near the 10% upper circuit (DSE limit), never chase it. Ask Claude for the ideal pullback entry level instead.

### 4. Volume Confirms Everything
Always check volume on the breakout bar. Ask: *"Was volume at least 1.5x the 10-day average on the breakout?"* No volume = false breakout.

### 5. Combine Two Timeframes
Before any swing trade, confirm the weekly and daily agree:
> *"On weekly: is this Stage 2? On daily: is there a Darvas breakout? Both must confirm."*

### 6. Set Alerts Immediately After Analysis
Memory fades. After every analysis, set the alert in TradingView via Claude before you close the conversation.

### 7. Never Move Your Stop Down
If the stop is hit, exit. Ask Claude for a re-entry setup at a lower level instead of averaging down.

### 8. Keep the Sector Rotation Map in Mind
DSE sector rotation is predictable. If banking is leading, pharma is next. Ask Claude which sector is currently in the lead before picking stocks.

### 9. Best SEPA Score Threshold for DSE
Score 6+/7 = Trade. Score 4-5/7 = Watchlist. Below 4/7 = Skip. Don't bend this rule.

### 10. Position Sizing Reminder
- A+ setup (all signals align, DSEX bullish): 15-20% of portfolio
- A setup: 10-15%
- B setup (partial): 5-10%
- Price <20 BDT: cap at 5-8% regardless of setup quality
- Never exceed 20% in a single DSE stock

---

## Known Limitations & Workarounds

| Limitation | Workaround |
|---|---|
| TradingView must run with debug port | Always launch via `scripts/launch_tv_debug_mac.sh`, never from Dock |
| EMA add via Claude sometimes fails | Add EMA manually in TradingView — Claude will compute values from OHLCV |
| RSI values may not appear in study data | RSI lives in a sub-pane — Claude estimates from OHLCV data |
| Only reads visible indicators | Unhide indicators in TradingView if values aren't showing |
| One chart at a time | Ask Claude to switch symbols for multi-stock scans |
| Connection drops after long idle | Re-run the launch script and ask Claude to reconnect |
| Free TradingView limits indicators | Upgrade plan for more simultaneous indicators |

---

## Quick Reference — Best Prompt for Each Goal

| Goal | Prompt to Use |
|---|---|
| Full analysis | *"Analyze this chart. Add RSI(14), MACD, EMA(20,50). Momentum signals, key levels, trade setup."* |
| Market check | *"Switch to DSEBD:DSEX weekly. Is the market above its 20W MA? Uptrend or downtrend?"* |
| Stage check | *"What Weinstein Stage is this stock in? Is the 30W MA rising?"* |
| Momentum | *"Check RSI and MACD. Is momentum bullish? Is histogram expanding?"* |
| Swing setup | *"Find the Darvas Box. Is there a valid breakout setup? Entry, stop, target."* |
| Multi-stock | *"Scan DSSL, MONNOFABR, FEKDIL — stage, momentum, verdict for each. Rank them."* |
| Alert | *"Set a TradingView alert at [PRICE] for [SYMBOL], crossing above."* |
| Pine Script | *"Write a Pine Script for [RULE]. Add it to the chart and compile."* |
| Replay | *"Start replay from [DATE]. Step me through bar by bar."* |
| Screenshot | *"Take a screenshot of the current chart."* |
| Stop loss | *"Set a stop loss alert at [PRICE] for [SYMBOL], crossing below."* |
