# ICT + SMC + SNR PRO Indicator (v3.0)

A powerful TradingView Pine Script (v5) indicator combining **every major institutional trading concept** — Inner Circle Trader (ICT), Smart Money Concepts (SMC), Support & Resistance (SNR), and 4 high-probability premium entry models — to deliver **BUY/SELL signals** with **Stop Loss**, **Take Profit (1, 2, 3)**, and **detailed entry reasoning** — engineered specifically for **Gold (XAU/USD)** and **BTC/USD** trading.

> File: [`ICT_SMC_SNR_Indicator.pine`](./ICT_SMC_SNR_Indicator.pine)

## What's New in v3.0
- **MSS (Market Structure Shift)** — sharper than CHoCH, requires displacement candle
- **Breaker Blocks** — failed OBs that flip role into high-probability retest zones
- **Mitigation Block entries** — institutional rebalancing on fresh OB retests
- **AMD Entry Model** — Wyckoff-style Accumulation → Manipulation → Distribution
- **HTF Sweep + LTF MSS Sniper** — H4 sweep + M5 MSS + FVG retrace (★★ premium)
- **Trendline Liquidity** — false breakouts of diagonal pivot trendlines
- **CRT (Candle Range Theory)** — 2-candle / 3-candle sweep reversal models
- **Displacement detection** — strong impulsive candles confirming institutional intent
- Confluence scoring upgraded from 9 → **15 points**
- Info panel expanded to **22 rows** showing every detection live

---

## Features

### ICT (Inner Circle Trader) Concepts
- **Order Blocks (OB)** — Auto-detected bullish/bearish institutional zones
- **Fair Value Gaps (FVG / Imbalances)** — Auto-drawn, auto-removed when filled
- **Inversion FVG (IFVG) / CISD** — Failed FVGs that flip role (support↔resistance)
- **Breaker Blocks** — Failed OBs that flip role (high-prob retest zones)
- **Mitigation Blocks** — Fresh OB retests for institutional rebalancing entries
- **Liquidity Sweeps (BSL / SSL)** — Detects buy-side / sell-side stop hunts
- **HTF Sweep Detection** — Multi-timeframe liquidity grabs (H4 / Daily)
- **Trendline Liquidity** — False breakouts of diagonal pivot trendlines
- **Displacement Detection** — Strong impulsive candles confirming intent
- **Killzones** — London, New York, Asia session highlighting (UTC times)

### SMC (Smart Money Concepts)
- **BOS / CHoCH / MSS** — Full structure detection with displacement confirmation
- **AMD Entry Model** — Accumulation → Manipulation → Distribution phases
- **Premium / Discount / Equilibrium** — Institutional buy/sell zones (50% Fib model)
- **Equal Highs / Equal Lows (EQH/EQL)** — Liquidity pool detection
- **CRT (Candle Range Theory)** — 2-candle and 3-candle sweep models
- Internal + Swing structure detection

### SNR (Support & Resistance)
- **Pivot-based dynamic S/R** with touch counter (strength)
- **Multi-Timeframe (HTF) levels** — Daily/Weekly highs and lows
- Automatic merging of nearby levels (within 0.5×ATR)

### Signal Engine
- **15-point confluence scoring system** (Structure, MSS, OB, Breaker, Mitigation, FVG, Liquidity, HTF Sweep, Trendline Liquidity, CRT, AMD, Displacement, Premium/Discount, Killzone, HTF Trend, IFVG)
- 3 modes: **Aggressive (≥3)**, **Confluence (≥5)**, **Conservative (≥7)**
- **4 dedicated Premium Model overrides** — LS+CISD+FVG, HTF Sweep Sniper, AMD, Breakout+OB — fire high-probability entries even at lower confluence
- HTF EMA200 trend filter
- Cooldown between signals to avoid noise
- Minimum R:R filter

### Premium Entry Models — 4 high-probability complete setups

#### 1. LS + CISD + FVG (Inversion Entry Model)
1. **HTF bias** confirmed
2. **Liquidity Grab** — price sweeps a previous BSL or SSL
3. **Find Inversion** — a failed FVG flips role (CISD)
4. **Wait for Retracement** back into the inversion zone
5. **Entry & SL** — entry at the IFVG, SL just beyond invalidation
6. **Target** — most recent high/low

#### 2. ★★ HTF Sweep + LTF MSS Sniper (highest probability)
1. **HTF sweep** (e.g., H4 high or low taken on the configured HTF)
2. **LTF MSS / CHoCH** confirms reversal on current timeframe
3. **FVG / OB / IFVG entry** as price retraces
4. **HTF bias aligned**
5. **Target the swept HTF extreme**

#### 3. AMD Model (Accumulation → Manipulation → Distribution)
1. **Accumulation** — tight range detected (low volatility)
2. **Manipulation** — false breakout in one direction (sweep)
3. **Distribution** — displacement candle in opposite direction
4. **Entry** on the distribution leg with HTF alignment

#### 4. Breakout + Order Block Formation
1. Sweep liquidity at highs/lows
2. Strong displacement breaks structure
3. Fresh OB forms at the origin of the displacement
4. Entry on mitigation (retest) of that OB

All 4 models fire dedicated signals on the chart and can be alerted independently.

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
| Timeframe            | M5 / M15 / H1 / H4 |
| Asset Profile        | XAUUSD (Gold) |
| Swing Pivot Length   | 10 |
| ATR Length           | 14 |
| ATR Multiplier (SL)  | 1.5 – 1.8 |
| Signal Mode          | Confluence (≥5) |
| Min R:R              | 1.5 |
| Trend TF             | 60 (1H) when trading M15 |
| HTF Sweep TF         | 240 (4H) for M5/M15 sniper setups |
| Require Displacement | ON (filters weak MSS) |
| Premium Models       | All 4 enabled for maximum coverage |

### BTC/USD
| Setting              | Recommended |
|----------------------|-------------|
| Timeframe            | M15 / H1 / H4 |
| Asset Profile        | BTCUSD |
| Swing Pivot Length   | 10–15 |
| ATR Length           | 14 |
| ATR Multiplier (SL)  | 2.0 – 2.5 (BTC is more volatile) |
| Signal Mode          | Confluence (≥5) |
| Min R:R              | 1.8 |
| Trend TF             | 240 (4H) when trading H1 |
| HTF Sweep TF         | D (Daily) for H1/H4 sniper setups |
| Require Displacement | ON |
| Premium Models       | All 4 enabled |

---

## How Signals Are Generated

A **BUY signal** fires when the bullish confluence score reaches the selected threshold (Aggressive ≥3, Confluence ≥5, Conservative ≥7). The **15-point** scoring system:

| # | Confluence | Pts |
|---|------------|-----|
| 1 | Bullish market structure (BOS up / CHoCH up) | 1 |
| 2 | **MSS up** (structure shift with displacement) | 2 |
| 3 | Price tapped a Bullish **Order Block** | 1 |
| 4 | Price tapped a Bullish **Breaker Block** (flipped OB) | 2 |
| 5 | **Mitigation Block** retest (fresh OB) | 1 |
| 6 | Price filled a Bullish **FVG** | 1 |
| 7 | **SSL liquidity sweep** (stop hunt below recent low) | 1 |
| 8 | **HTF Sweep** (H4/D liquidity grab on higher timeframe) | 2 |
| 9 | **Trendline Liquidity** sweep (diagonal false breakout) | 1 |
| 10 | **CRT bullish** (2-candle/3-candle sweep reversal) | 1 |
| 11 | **AMD Distribution leg** up (accumulation → manipulation → expansion) | 2 |
| 12 | **Displacement candle** up | 1 |
| 13 | Price is in the **Discount zone** (below 50%) | 1 |
| 14 | Active **killzone** (London / NY / Asia) | 1 |
| 15 | **HTF trend** is bullish (price above HTF EMA200) | 1 |
| 16 | **Bullish IFVG / CISD tap** | 2 |

A **SELL signal** is the mirror opposite.

**Premium Model overrides:** If any of the 4 premium models fires a complete pattern (LS+CISD+FVG, HTF Sweep + LTF MSS Sniper, AMD, or Breakout + OB Formation), a dedicated signal is printed regardless of total score — these are the **highest probability** entries.

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
- **SL when in IFVG zone** — anchored to the **far edge of the inversion zone** with a small ATR buffer (matches the rule: *"stop loss just beyond the invalidation point"*)
- **TP1** = Entry ± R × `tp1RR` (default 1.0R)
- **TP2** = Entry ± R × `tp2RR` (default 2.0R)
- **TP3** = Entry ± R × `tp3RR` (default 3.0R)

> **Recommended trade management**: Take 50% off at TP1, move SL to break-even, take 30% at TP2, let the runner go to TP3.

---

## Reading the Info Panel

The top-right **22-row info panel** updates every bar:

| Section | Rows |
|---------|------|
| **Bias** | Trend (HTF), Structure, MSS, Zone, Killzone |
| **Zones** | In Bull/Bear OB, In Bull/Bear FVG, In Bull/Bear Breaker, IFVG Tap |
| **Liquidity** | BSL/SSL Sweep, HTF Sweep, Trendline Liquidity, CRT |
| **AMD** | Phase (Accumulation / Manipulation / Distribution) |
| **Displacement** | Up / Down detection |
| **Engine** | ATR, Buy Score, Sell Score (0–15), Signal status, Active Mode |

A signal cell shows 🟢 **BUY NOW**, 🔴 **SELL NOW**, ★ **PREMIUM MODEL FIRED**, or ⏳ **Wait**.

---

## Setting Up Alerts (TradingView)

1. Right-click the chart → **Add Alert**.
2. Condition: `ICT+SMC+SNR PRO` → choose one of the **26 alert conditions**:

**Core signals**
- `ICT BUY Signal` / `ICT SELL Signal`

**Premium models (highest probability)**
- `LS+CISD+FVG BUY` / `LS+CISD+FVG SELL`
- `HTF Sweep Sniper BUY` / `HTF Sweep Sniper SELL`
- `AMD BUY` / `AMD SELL`
- `Breakout+OB BUY` / `Breakout+OB SELL`

**Structure**
- `BOS Up` / `BOS Down`
- `CHoCH Up` / `CHoCH Down`
- `MSS Up` / `MSS Down`

**Liquidity**
- `BSL Sweep` / `SSL Sweep`
- `HTF BSL Sweep` / `HTF SSL Sweep`
- `Trendline Liquidity Sweep`
- `CRT Bullish` / `CRT Bearish`

**Zones**
- `Bull IFVG Tap` / `Bear IFVG Tap`
- `Bull Breaker Tap` / `Bear Breaker Tap`

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
