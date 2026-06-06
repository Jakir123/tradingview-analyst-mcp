# Stock Analysis with Claude AI + TradingView MCP

A local AI stock analysis system that connects **Claude Code** directly to **TradingView Desktop** via the Model Context Protocol (MCP). Ask Claude in plain English to analyze any chart on any exchange — read live indicators, apply strategy frameworks, set alerts, and get structured trade setups — all without leaving your editor.

Works with any market TradingView supports: stocks, forex, crypto, futures, indices — on any exchange worldwide.

> This project is configured for **DSE (Dhaka Stock Exchange)** as its primary use case, with DSE-specific strategy rules and filters in the `strategies/` folder. The core system is fully exchange-agnostic — point it at any TradingView chart and it works.

---

## What This Does

- **Reads your live TradingView chart** — OHLCV bars, indicator values, current price, chart state
- **Controls TradingView** — switch symbols, change timeframes, add/remove indicators, draw levels
- **Applies classic trading strategies** — Weinstein Stage Analysis, Minervini SEPA, Darvas Box, Livermore rules
- **Delivers structured trade setups** — Signal, Entry, Stop Loss, Target, Risk/Reward ratio
- **Sets alerts** — price alerts directly in TradingView via Claude
- **Writes Pine Script** — Claude can write, compile, and debug custom indicators for you
- **Scans multiple symbols** — batch analysis across a watchlist in one request

All data stays on your machine. The MCP server is a local bridge only — nothing is sent to external servers.

---

## Architecture

```
You (natural language prompt)
         ↕
    Claude Code  (AI brain — reads CLAUDE.md for strategy rules)
         ↕  MCP Protocol (stdio)
  tradingview-mcp/src/server.js  ←── local Node.js process
         ↕  Chrome DevTools Protocol (localhost:9222)
  TradingView Desktop App        ←── running on your machine
         ↕
    Live Chart Data (any exchange, any symbol)
```

### How a Request Flows

1. You type — e.g., *"Analyze this chart with Weinstein Stage Analysis"*
2. Claude reads `CLAUDE.md` (auto-loaded) to apply the configured strategy rules
3. Claude calls MCP tools — `chart_get_state`, `data_get_ohlcv`, `data_get_study_values`, etc.
4. The MCP server (`tradingview-mcp/src/server.js`) receives each tool call
5. Server talks to TradingView via Chrome DevTools Protocol on `localhost:9222`
6. TradingView returns live data — bars, indicator values, quote — for whatever symbol is on screen
7. Claude analyses the data, applies the strategy frameworks, and responds with a structured report

---

## Prerequisites

| Requirement | Details |
|---|---|
| OS | macOS recommended (Windows/Linux also supported — see platform notes below) |
| TradingView Desktop | Download from [tradingview.com/desktop](https://www.tradingview.com/desktop/) |
| Node.js | v18+ — check with `node --version` |
| Claude Code | VS Code extension or CLI — [install guide](https://docs.anthropic.com/claude-code) |
| TradingView plan | Any plan with access to your target exchange's data |

> **Exchange data:** TradingView supports NYSE, NASDAQ, LSE, BSE, DSE, SGX, crypto exchanges, forex, and more. You need a TradingView plan that includes data for your exchange. This project uses `DSEBD:` prefix symbols for DSE, but any TradingView symbol format works.

---

## Setup

### Step 1 — Install MCP Server Dependencies

```bash
cd tradingview-mcp
npm install
```

### Step 2 — Verify `.mcp.json` Path

The `.mcp.json` at the project root tells Claude Code where to find the MCP server:

```json
{
  "mcpServers": {
    "tradingview": {
      "command": "node",
      "args": ["/absolute/path/to/claude-tv-mcp/tradingview-mcp/src/server.js"]
    }
  }
}
```

If you moved this project folder, update the path in `.mcp.json` to match your new location. Use an absolute path — relative paths are not reliable here.

### Step 3 — Launch TradingView with Debug Port

TradingView must be running with Chrome DevTools Protocol enabled. It cannot be launched normally from the Dock or Start Menu for this to work.

**Mac (use the provided script):**
```bash
bash tradingview-mcp/scripts/launch_tv_debug_mac.sh
```

Or manually:
```bash
/Applications/TradingView.app/Contents/MacOS/TradingView --remote-debugging-port=9222
```

**Windows:**
```bash
%LOCALAPPDATA%\TradingView\TradingView.exe --remote-debugging-port=9222
```

**Linux:**
```bash
tradingview --remote-debugging-port=9222
```

Alternatively, after connecting Claude, use the `tv_launch` MCP tool — it auto-detects your platform and launches TradingView with the right flags.

### Step 4 — Open Project in Claude Code

```bash
cd /path/to/claude-tv-mcp
code .
```

Claude Code's VS Code extension auto-detects `.mcp.json` and connects the MCP server on startup.

### Step 5 — Verify Connection

Ask Claude:

> *"Run tv_health_check and tell me if TradingView is connected."*

Expected response:
```json
{
  "success": true,
  "cdp_connected": true,
  "chart_symbol": "...",
  "api_available": true
}
```

If `cdp_connected` is false, TradingView is not running with the debug port — re-run the launch script.

### Step 6 — Start Analyzing

Open any stock on TradingView, then ask Claude:

> *"Analyze this chart. Add RSI(14), MACD, and EMA(20,50) if not there. Give me momentum signals, key levels, and a trade setup with entry, stop, and target."*

Claude reads whatever symbol is currently on your TradingView chart — no need to specify the exchange or symbol in your prompt.

---

## Project Structure

```
claude-tv-mcp/
├── .mcp.json                        ← MCP server config (Claude reads on startup)
├── CLAUDE.md                        ← AI instructions: strategy rules, analysis flow, tools list
├── README.md                        ← This file
├── uses_guide.md                    ← Full usage guide: every prompt, workflow, and tip
│
├── strategies/                      ← Strategy knowledge base (Claude reads during analysis)
│   ├── weinstein_stage_analysis.md  ← Stan Weinstein Stage 1–4 framework
│   ├── minervini_sepa.md            ← Mark Minervini SEPA + VCP momentum system
│   ├── darvas_box.md                ← Nicolas Darvas Box Theory for swing trades
│   ├── livermore_trend.md           ← Jesse Livermore trade management rules
│   └── dse_rules.md                 ← Exchange-specific rules (configured for DSE — adapt for other markets)
│
└── tradingview-mcp/                 ← MCP server (subproject)
    ├── src/
    │   ├── server.js                ← MCP server entry point (the bridge)
    │   ├── core/                    ← Business logic (chart, data, pine, alerts, etc.)
    │   └── tools/                   ← MCP tool definitions (78 tools)
    ├── scripts/
    │   ├── launch_tv_debug_mac.sh   ← Launch TradingView with debug port (Mac)
    │   ├── launch_tv_debug.bat      ← Launch script (Windows)
    │   └── launch_tv_debug_linux.sh ← Launch script (Linux)
    ├── package.json
    └── SETUP_GUIDE.md               ← Detailed MCP server setup reference
```

### Adapting for a Different Exchange

The four core strategy files (`weinstein_stage_analysis.md`, `minervini_sepa.md`, `darvas_box.md`, `livermore_trend.md`) are universal — they work on any market.

The exchange-specific file is `strategies/dse_rules.md`. It contains:
- Minimum volume/price filters specific to DSE
- DSE circuit breaker rules (10% daily limit)
- DSE sector rotation order
- DSE market hours and settlement

To use this project for a different exchange, replace `dse_rules.md` with your own exchange-specific rules and update `CLAUDE.md` to reference the new file.

---

## Available MCP Tools (78 total)

### Core Analysis
| Tool | What It Does |
|---|---|
| `tv_health_check` | Verify TradingView connection |
| `chart_get_state` | Get symbol, timeframe, all indicator names and IDs |
| `quote_get` | Real-time price, OHLC, volume for any symbol |
| `data_get_ohlcv` | Historical price bars (up to 500 bars) |
| `data_get_study_values` | Live values from all visible indicators (RSI, MACD, BBands, etc.) |

### Chart Control
| Tool | What It Does |
|---|---|
| `chart_set_symbol` | Switch to any symbol on any exchange |
| `chart_set_timeframe` | Change resolution (1, 5, 15, 60, D, W, M) |
| `chart_manage_indicator` | Add or remove studies |
| `indicator_set_inputs` | Change indicator parameters (length, source, etc.) |
| `draw_shape` | Draw horizontal lines, trend lines, rectangles, text |

### Custom Indicator Data
| Tool | What It Does |
|---|---|
| `data_get_pine_lines` | Price levels drawn by custom Pine indicators |
| `data_get_pine_labels` | Text annotations from custom indicators |
| `data_get_pine_tables` | Table data from custom indicators |
| `data_get_pine_boxes` | Price zones/ranges from custom indicators |

### Pine Script
| Tool | What It Does |
|---|---|
| `pine_set_source` | Inject Pine Script code into the editor |
| `pine_smart_compile` | Compile and check for errors automatically |
| `pine_get_errors` | Read compilation errors |
| `pine_save` | Save script to TradingView cloud |

### Alerts & Utilities
| Tool | What It Does |
|---|---|
| `alert_create` | Set a price alert in TradingView |
| `alert_list` | View active alerts |
| `alert_delete` | Remove alerts |
| `capture_screenshot` | Take chart screenshot (full, chart, or strategy tester) |
| `batch_run` | Run an action across multiple symbols at once |
| `replay_start` / `replay_step` | Enter bar replay mode for backtesting practice |
| `tv_launch` | Auto-detect and launch TradingView with debug port |

---

## Strategy Frameworks

All strategy files are in `strategies/`. Claude reads them automatically during analysis.

| Framework | File | Works On |
|---|---|---|
| Stan Weinstein Stage Analysis | `weinstein_stage_analysis.md` | Any market — identifies Stage 1–4 trend cycle |
| Mark Minervini SEPA + VCP | `minervini_sepa.md` | Any market — momentum entry with 7-point checklist |
| Nicolas Darvas Box Theory | `darvas_box.md` | Any market — swing trade breakout setups |
| Jesse Livermore Rules | `livermore_trend.md` | Any market — trade management and position sizing |
| Exchange-Specific Rules | `dse_rules.md` | DSE-specific (adapt this file for other exchanges) |

### Default Analysis Flow

When you say "analyze this chart", Claude follows this sequence:

1. Read exchange rules — check if stock passes filters (volume, price, liquidity)
2. Read `weinstein_stage_analysis.md` — which stage is the stock in?
3. If Stage 2 → apply `minervini_sepa.md` for momentum entry timing
4. If near a box boundary → apply `darvas_box.md` for breakout entry
5. Apply `livermore_trend.md` for trade management and sizing rules
6. Output: **STRONG BUY / BUY / WAIT / AVOID** with full trade setup

---

## Output Format

Every analysis delivers this structured report:

```
STOCK:         [Symbol — Exchange]
STAGE:         [1 / 2 / 3 / 4] (Weinstein)
SEPA SCORE:    [X/7] (Minervini)
BOX SETUP:     [Yes / No] (Darvas)
MARKET CHECK:  [Pass / Fail] (exchange filters)
───────────────────────────────────────
SIGNAL:        [STRONG BUY / BUY / WAIT / AVOID]
ENTRY:         [price or range]
STOP LOSS:     [price] ([X]% below entry)
TARGET 1:      [price] ([X]% above entry)
TARGET 2:      [price] ([X]% above entry)
RISK/REWARD:   [1:X]
CONFIDENCE:    [High / Medium / Low]
───────────────────────────────────────
REASON:        [2–3 sentences explaining the setup]
RISK:          [Key risk to watch]
```

---

## Troubleshooting

| Problem | Solution |
|---|---|
| `cdp_connected: false` | TradingView not running with debug port — re-run the launch script |
| `ECONNREFUSED` | TradingView isn't running, or another app is using port 9222 |
| MCP server not loading | Check `.mcp.json` has the correct absolute path, reload VS Code window |
| Indicator values not showing | Make sure the indicator is visible on chart (not hidden in a pane) |
| EMA not adding via Claude | Add EMA manually in TradingView — the MCP `chart_manage_indicator` is unreliable for EMAs |
| Tools return stale data | TradingView still loading — wait a few seconds and retry |
| Pine Script tools fail | Open the Pine Editor panel in TradingView first |
| Connection drops after idle | Re-run the launch script; TradingView may have closed the debug port |

---

## Related Files

- [uses_guide.md](uses_guide.md) — Full usage guide: every prompt pattern, workflow, and tip
- [CLAUDE.md](CLAUDE.md) — Claude's operating instructions (auto-loaded on session start, do not rename)
- [tradingview-mcp/SETUP_GUIDE.md](tradingview-mcp/SETUP_GUIDE.md) — Detailed MCP server setup reference
- [tradingview-mcp/README.md](tradingview-mcp/README.md) — Full MCP tool reference (78 tools, 30 CLI commands)
