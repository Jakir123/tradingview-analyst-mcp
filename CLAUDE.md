# Claude Analysis Instructions — DSE Stock Analysis

This project connects Claude to TradingView Desktop via MCP for DSE (Dhaka Stock Exchange) stock analysis.
See `README.md` for architecture and setup. See `uses_guide.md` for usage patterns and prompt examples.

## IMPORTANT: Always Follow These Rules

When analyzing any DSE stock, Claude MUST:

1. **Always check DSE market direction first** — never trade against the broad market trend
2. **Apply the correct strategy based on user's goal:**
   - Momentum trading → use Minervini SEPA (see `strategies/minervini_sepa.md`)
   - Swing trading → use Darvas Box + Weinstein Stage (see `strategies/darvas_box.md` + `strategies/weinstein_stage_analysis.md`)
   - Long-term investment → use Weinstein Stage Analysis (see `strategies/weinstein_stage_analysis.md`)
   - Any analysis → always check DSE-specific rules first (see `strategies/dse_rules.md`)
3. **Always give a structured output** with: Signal (BUY/SELL/WAIT), Entry, Stop Loss, Target, Risk/Reward ratio
4. **Never recommend a trade without a stop loss**
5. **Always state the strategy being applied** so the user knows which framework the analysis comes from

## Strategy Files (Read These for Analysis)

| File | Strategy | Best For |
|---|---|---|
| `strategies/weinstein_stage_analysis.md` | Stan Weinstein Stage Analysis | Overall trend identification, long-term |
| `strategies/minervini_sepa.md` | Mark Minervini SEPA + VCP | Momentum entries |
| `strategies/darvas_box.md` | Nicolas Darvas Box Theory | Swing trade breakouts |
| `strategies/livermore_trend.md` | Jesse Livermore Trend Rules | Trade management, discipline |
| `strategies/dse_rules.md` | DSE-Specific Adaptations | Always apply on top of any strategy |

## Default Analysis Template

When user asks "analyze this chart" without specifying a strategy, use this flow:

1. Read `strategies/dse_rules.md` — check if stock passes DSE filters
2. Read `strategies/weinstein_stage_analysis.md` — identify which stage the stock is in
3. If Stage 2: apply `strategies/minervini_sepa.md` for entry timing
4. If near a box breakout: apply `strategies/darvas_box.md`
5. Apply `strategies/livermore_trend.md` rules for trade management
6. Give final verdict: STRONG BUY / BUY / WAIT / AVOID

## MCP Tools Available

This project has TradingView MCP connected. Use these tools during analysis:
- `tv_health_check` — verify connection
- `chart_get_state` — get current symbol and indicators
- `data_get_ohlcv` — get price bars
- `data_get_study_values` — get live indicator values
- `quote_get` — get current price
- `chart_manage_indicator` — add/remove indicators
- `chart_set_symbol` — switch stocks
- `chart_set_timeframe` — change timeframe
- `alert_create` — set price alerts
- `capture_screenshot` — take chart screenshot
