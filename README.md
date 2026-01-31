# Two Fractals Trend Lines (Pine Script v5)

A multi-tool market structure overlay for TradingView that combines **Bill Williams fractals**, **two-fractal trend lines**, **divergence arrows**, **bar-pattern markers**, **segments**, **Bollinger Bands**, **pivot points**, **trading sessions**, **MTF candle overlay**, **Fair Value Gaps**, **Key Levels (PDH/PDL/PDC + Weekly/Monthly Open)**, **VWAP + Bands + Z-Score**, **RVOL (Relative Volume)**, **Opening Range / Initial Balance (OR/IB)**, an optional **Squeeze Box**, and a compact **CONF/REG + MTF trend info panel**.

> **Intent:** Use the signals in **confluence** (not as standalone entries). Most elements aim to visualize **market structure**, **tension**, and **potential breakout / pullback zones**, while helping to avoid **low-participation moves** and **late (stretched) entries**.

---

## Features

### 1) Market Structure Core
- **Bill Williams Fractals (5-bar default)**
  - White triangles above/below bars.
  - Used as local S/R reference (last confirmed up/down fractal levels tracked).
- **Fractal Trend Lines (Two-Fractal Trendlines)**
  - Connects the last two confirmed pivot highs (upper) and pivot lows (lower).
  - Optional **special mode** when `Fractal Size: Bars Per Side = 0`:
    - Uses an **anchored linear regression slope** from the newest pivot to “follow” the current trend more dynamically.

### 2) Divergences (Early Warnings)
- **Classic & hidden divergences** between price and:
  - RSI
  - MACD fast line
  - MACD signal line (slow line)
- Plotted as **arrow up/down**.
- Controlled by a bar lookback window (“Bar Period”) and price source (high/low vs close).

### 3) Bar Pattern Markers
- **Last 12 Bar (L12)**: marks potential trend initiation zones  
  - `L` below bar (long trigger) / above bar (short trigger)
- **NR7 (Narrow Range)**: `n` marker for tension / compression
- **Inside Bar**: `i`
- **Outside Bar**: `o` (colored by breakout direction)
- **Sandwich Bar**: `s`
- **Fakey**: `F` (inside-bar false breakout patterns)

### 4) Segments (Subtle Trend Change Detection)
- Draws up to **3 “segment” lines** for highs and lows, using a maximum bar distance (`Max Segment Bars`).
- Useful as a subtle confirmation layer and for background filters *(if you use them externally)*.

---

## Context & Confluence Tools

### Context Lenses (Focused Presets)
A **Context Lens** applies focused defaults to reduce clutter and align the toolset with a specific market read.  
- **Custom**: manual control (no automatic switching)
- **Market Map**: sessions + key levels + volume profile + pivots
- **Opening Auction**: OR/IB + RVOL + 1st session candle + MTF candles
- **Value Reversion**: VWAP + bands/z + divergences + volume profile
- **Compression -> Expansion**: squeeze box + RVOL + trendlines + last fractal
- **Trend Continuation**: EMA cloud + FVG1 + weekly VWAP + MTF candles
- **Range Rotation**: volume profile + VWAP line + last fractal + PDC

> **Note:** Lenses are intentionally minimal so they don’t constantly override your personal layout. Custom remains fully manual.

### Key Levels (Origin-Anchored)
- **PDH / PDL / PDC** (Previous Day High/Low/Close)
- **Weekly Open / Monthly Open**
- Levels are designed as **clean reference lines** (origin-anchored when available) and extend right for consistent context.

### VWAP (Fair Value) + Bands + Z-Score
- **Session VWAP (daily reset)** and/or **Weekly VWAP**
- **VWAP Bands** (K1/K2/K3) for stretch zones
- **VWAP Z-Score** (distance to VWAP in σ units) for “don’t chase” and MR framing

### RVOL (Relative Volume)
- RVOL = `volume / SMA(volume, N)` to measure **participation**
- Optional marker points (recommended: show only **high/extreme** participation to reduce noise)
- Works well as a confirmation layer for ORB, squeeze releases, breakouts, and reclaims

### Opening Range / Initial Balance (OR/IB)
- **OR**: first X minutes
- **IB**: first ~60 minutes (common in futures)
- “Lock after window” for stable break/fail logic

### Squeeze Box (Optional)
- Builds a range box during squeeze regime and tracks release/break events.
- Best used with RVOL confirmation to reduce false breaks.

### Bollinger Bands
- Standard or exponential calculation toggle.
- Optional “Touched BBs only” for cleaner charts.
- Displays BB envelopes with filled zones (depending on configuration).

### Pivot Points (Classic)
- 1H, 4H, Daily, Weekly, Monthly, 3M, 12M.
- Calculated from the **previous period’s OHLC** (standard method).
- Designed to update **on period changes** and remain stable during chart navigation.

### Trading Sessions
- London / New York / Tokyo / Sydney
- Styles:
  - **Vertical Line**
  - **Box**
  - **Background**
- Includes an extra **New York 19:30** vertical line when enabled and in “Vertical Line” style.
- Session plotting is restricted to **intraday charts ≤ 1H**.

### MTF Candle Overlay
- Shows a higher timeframe candle “x-ray” overlay on the current chart.
- Adjustable timeframe + opacity.

### Fair Value Gaps (Price Imbalance)
- Bullish / bearish FVG boxes.
- Supports:
  - Current timeframe mode
  - **MTF mode** using time-based coordinates (`xloc.bar_time`) for reliable placement.

### Additional Context
- **Last Fractal S/R** (selectable timeframe)
- **High Volume Spikes** marker `v` when volume exceeds `x * SMA(volume, 20)`
- *(If enabled in your build)* optional **Gradient Volume Profile** for the visible range

---

## Panel Legend (Compact Pro Readout)
The panel is intended to be readable at a glance (numbers + classification):

- **RVOL**: `VOL 0.14x L`  
  - `L/M/H/E` = low / moderate / high / extreme participation
- **VWAP Z**: `VWP -4.1σ E`  
  - `N/S/T/E` = normal / stretched / TP zone / extreme
- **CONF / REG**: regime + confluence bias/quality context (not a standalone entry)

---

## Real-time Alert: “5th Fractal Candle”
An optional alert that triggers **while the 5th candle is still forming** (real-time), detecting “potential fractal forming” structures without relying on `ta.pivothigh/low` for the live bar.

**How to use in TradingView**
1. Enable: **Real-time Alerts → “Alert on 5th Fractal Candle (Real-time)”**
2. Create an alert for the indicator.
3. Choose: **Condition = “Any function call”**
4. Optional: enable once-per-bar to reduce spam (already handled via `alert.freq_once_per_bar`).

---

## Inputs Overview (Practical)

### Core toggles
- **Strategy Lense** / **Custom**
- **Bill Williams Fractals**
- **Fractal Trend Lines**
- **SR Lines** (horizontal fractal S/R + ATH line)
- **Divergence arrows**
- **Bar signals** (L12, NR7, inside/outside/sandwich/fakey)
- **Segments**
- **Bollinger Bands**
- **Key Levels** (PDH/PDL/PDC + Weekly/Monthly Open)
- **VWAP** (Anchor, Bands K1/K2/K3, Z-Score)
- **RVOL**
- **OR/IB**
- **Pivot Points**
- **Trading Sessions**
- **MTF Candle Overlay**
- **FVG**
- **Additional Context** (last fractal S/R, volume spikes, squeeze box, optional volume profile)

### Timeframe-heavy modules
- SR lines fractal timeframe (manual or auto-adapted)
- Last fractal timeframe
- FVG timeframe
- MTF candle overlay timeframe
- Pivot point base timeframes (fixed)
- VWAP anchor selection (session vs weekly)

---

## Recommended Usage Workflow (Typical)

1. **Start with a regime scan**
   - Use **Market Map** to see sessions, key levels, pivots, and volume profile in context.
2. **Pick a focused lens**
   - Switch to **Opening Auction**, **Value Reversion**, **Compression -> Expansion**, **Trend Continuation**, or **Range Rotation** based on the regime.
3. **Refine execution**
   - Toggle any extra tools manually in **Custom** if you want full control beyond the presets.

---

## Performance Notes
- The script uses multiple `request.security()` calls and can draw many objects (lines/boxes).
- If you hit performance issues:
  - Disable optional heavy visuals (e.g., volume profile, extra overlays)
  - Reduce visible complexity (segments, pivots, sessions, MTF overlay)
  - Keep scan depth (if applicable) reasonable for your chart usage

---

## Visual Legend (What you see on chart)
- **White triangles**: Bill Williams fractals
- **Blue trend lines**: fractal trend lines (upper/lower)
- **Arrows**: divergence signals (green up / red down)
- **L / n / i / o / s / F**: bar pattern markers
- **Key level lines**: PDH/PDL/PDC + Weekly/Monthly Open (style may differ)
- **VWAP line + bands**: fair value + stretch zones (K1/K2/K3)
- **VOL markers**: RVOL participation points (optional)
- **Boxes**: FVG zones, MTF candle overlay, sessions (Box style), squeeze box (if enabled)
- **Panel**: compact context readout (CONF/REG, VWAP Z, RVOL, ATR/ADR%)

---

## Limitations & Disclaimers
- This indicator is for **visual decision support**, not a complete trading system.
- Divergences and anticipated fractals can be **early** and produce false positives; use confluence and context.
- Trendline “special mode” (`Bars Per Side = 0`) is dynamic by design and may behave differently than classic “two-point” trendlines.

---

## Changelog (Optional)
- Add your version notes here (e.g., “Strategy Lense presets”, “Key Levels origin-anchored”, “VWAP bands + Z panel codes”, “Pivot stability pass”, “CONF VWAP quality gate”, etc.).

---

## License / Attribution
- Author: *(add your name/handle if you want)*
- Pine Script v5
- Intended for TradingView charts (overlay indicator)
