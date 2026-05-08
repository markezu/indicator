# ICT + SMC + SNR PRO Indicator

A powerful TradingView Pine Script (v5) indicator that combines **Inner Circle Trader (ICT)**, **Smart Money Concepts (SMC)**, and **Support & Resistance (SNR)** logic to deliver **BUY/SELL signals** with **Stop Loss**, **Take Profit (1, 2, 3)**, and **detailed entry reasoning** — engineered specifically for **Gold (XAU/USD)** and **BTC/USD** trading.

> File: [`ICT_SMC_SNR_Indicator.pine`](./ICT_SMC_SNR_Indicator.pine)

---

## Features

### ICT (Inner Circle Trader) Concepts
- **Order Blocks (OB)** — Auto-detected bullish/bearish institutional zones
- **Fair Value Gaps (FVG / Imbalances)** — Auto-drawn, auto-removed when filled
- **Liquidity Sweeps (Stop Hunts)** — Detects buy-side / sell-side liquidity grabs
- **Killzones** — London, New York, Asia session highlighting (UTC times)

### SMC (Smart Money Concepts)
- **BOS (Break of Structure)** — Continuation signals
- **CHoCH (Change of Character)** — Trend reversal signals
- **Equal Highs / Equal Lows (EQH/EQL)** — Liquidity pools
- **Premium / Discount / Equilibrium** — Institutional buy/sell zones (50% Fib model)
- Internal + Swing structure detection

### SNR (Support & Resistance)
- **Pivot-based dynamic S/R** with touch counter (strength)
- **Multi-Timeframe (HTF) levels** — Daily/Weekly highs and lows
- Automatic merging of nearby levels (within 0.5×ATR)

### Signal Engine
- **7-point confluence scoring system** (Structure, OB, FVG, Liquidity, Premium/Discount, Killzone, HTF Trend)
- 3 modes: **Aggressive (≥2)**, **Confluence (≥3)**, **Conservative (≥4)**
- HTF EMA200 trend filter
- Cooldown between signals to avoid noise
- Minimum R:R filter

### Risk Management
- **Stop Loss** modes:
  - `ATR + Structure` (recommended) — uses the further of the two
  - `Pure ATR`
  - `Pure Structure` (last swing)
- **Take Profit 1 / 2 / 3** at configurable R-multiples (default 1R / 2R / 3R)
- Asset-aware ATR multipliers (Gold vs BTC have different volatility profiles)

### On-Chart Information
- Entry price, SL, TP1, TP2, TP3 lines drawn for each signal
- **Detailed entry reason label** listing every confluence that fired
- **Live info panel** (top-right) showing trend, zone, killzone, scores, signal status
- TradingView **alert conditions** for every event (BUY / SELL / BOS / CHoCH / Sweeps)

---

## Installation (TradingView)

1. Open [TradingView](https://www.tradingview.com).
2. Open any chart (e.g., **OANDA:XAUUSD** or **BINANCE:BTCUSDT**).
3. Click **Pine Editor** at the bottom of the screen.
4. Delete any existing code and **paste** the contents of `ICT_SMC_SNR_Indicator.pine`.
5. Click **Save** → name it `ICT+SMC+SNR PRO`.
6. Click **Add to chart**.
7. The indicator overlays on price with auto-detected asset profile.

---

## Recommended Settings

### Gold (XAU/USD)
| Setting              | Recommended |
|----------------------|-------------|
| Timeframe            | M15 / H1 / H4 |
| Asset Profile        | XAUUSD (Gold) |
| Swing Pivot Length   | 10 |
| ATR Length           | 14 |
| ATR Multiplier (SL)  | 1.5 – 1.8 |
| Signal Mode          | Confluence (3+) |
| Min R:R              | 1.5 |
| Trend TF             | 60 (1H) when scalping M15 |

### BTC/USD
| Setting              | Recommended |
|----------------------|-------------|
| Timeframe            | M15 / H1 / H4 |
| Asset Profile        | BTCUSD |
| Swing Pivot Length   | 10–15 |
| ATR Length           | 14 |
| ATR Multiplier (SL)  | 2.0 – 2.5 (BTC is more volatile) |
| Signal Mode          | Confluence (3+) |
| Min R:R              | 1.8 |
| Trend TF             | 240 (4H) when trading H1 |

---

## How Signals Are Generated

A **BUY signal** fires when at least N of the following 7 confluences align (N depends on mode):

1. **Bullish market structure** (BOS up or CHoCH up)
2. **Price tapped a Bullish Order Block**
3. **Price filled a Bullish FVG**
4. **Sell-side liquidity swept** (price wicked below a swing low and closed back inside)
5. **Price is in the Discount zone** (below 50% of the recent range)
6. **Active killzone** (London / NY / Asia)
7. **HTF trend is bullish** (price above HTF EMA200)

A **SELL signal** is the mirror opposite.

The signal is **only printed** when:
- Score ≥ required threshold
- Score is greater than the opposite-side score
- HTF trend allows it (if filter enabled)
- Computed R:R to TP2 ≥ user minimum
- Cooldown bars have passed since last signal

---

## How SL / TP Are Calculated

- **Risk (R)** = `|Entry − SL|`
- **SL (ATR + Structure)** = the **further** of:
  - Last swing low (for buys) / swing high (for sells), with 0.2×ATR buffer
  - `Entry ± ATR × Multiplier`
- **TP1** = Entry ± R × `tp1RR` (default 1.0R)
- **TP2** = Entry ± R × `tp2RR` (default 2.0R)
- **TP3** = Entry ± R × `tp3RR` (default 3.0R)

> **Recommended trade management**: Take 50% off at TP1, move SL to break-even, take 30% at TP2, let the runner go to TP3.

---

## Reading the Info Panel

The top-right table updates every bar:

| Row             | Meaning |
|-----------------|---------|
| Trend (HTF)     | Higher-timeframe EMA200 bias |
| Structure       | Current market structure (BOS-based) |
| Zone            | Premium / Discount / Equilibrium |
| Killzone        | Active session (if any) |
| In Bull/Bear OB | ✅ if price is sitting inside an order block |
| In Bull/Bear FVG| ✅ if price is sitting inside a fair value gap |
| ATR             | Current Average True Range |
| Buy / Sell Score| Live confluence score (0–7) |
| Signal          | 🟢 BUY NOW / 🔴 SELL NOW / ⏳ Wait |
| Mode            | Active confluence mode + threshold |

---

## Setting Up Alerts (TradingView)

1. Right-click the chart → **Add Alert**.
2. Condition: `ICT+SMC+SNR PRO` → choose:
   - `ICT BUY Signal`
   - `ICT SELL Signal`
   - `BOS Up / Down`
   - `CHoCH Up / Down`
   - `Liq Sweep High / Low`
3. Set **frequency** to **Once per bar close** (recommended for clean signals).
4. Configure webhook / notification as desired.

---

## Important Disclaimers

- **No indicator is 100% accurate.** This is a decision-support tool, **not** a guaranteed system.
- **Always backtest** on your specific symbol/timeframe before going live.
- **Risk no more than 1–2% of capital per trade.**
- Crypto and Gold can have **gap risk** — use **guaranteed stops** with your broker when possible.
- Killzone times are in **UTC** — adjust if your chart uses exchange time.
- The indicator is for educational and research purposes. Use at your own risk.

---

## File Structure

```
webapp/
├── ICT_SMC_SNR_Indicator.pine   # Main Pine Script v5 indicator
└── README.md                    # This file
```

---

## License

MIT — free to use, modify, and share. Credit appreciated but not required.
