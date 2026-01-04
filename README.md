Two Fractals Trend Lines (Pine Script v5)

A multi-tool market structure overlay for TradingView that combines Bill Williams fractals, two-fractal trend lines, divergence arrows, bar-pattern markers, segments, Bollinger Bands, pivot points, trading sessions, MTF candle overlay, Fair Value Gaps, previous candle / last fractal S/R, volume spikes, an optional gradient volume profile, and a multi-timeframe trend info panel.

Intent: Use the signals in confluence (not as standalone entries). Most elements aim to visualize market structure, tension, and potential breakout / pullback zones.

Features
1) Market Structure Core

Bill Williams Fractals (5-bar default)

White triangles above/below bars.

Used as local S/R reference (last confirmed up/down fractal levels tracked).

Fractal Trend Lines (Two-Fractal Trendlines)

Connects the last two confirmed pivot highs (upper) and pivot lows (lower).

Optional special mode when Fractal Size: Bars Per Side = 0:

Uses an anchored linear regression slope from the newest pivot to “follow” the current trend more dynamically.

2) Divergences (Early Warnings)

Classic & hidden divergences between price and:

RSI

MACD fast line

MACD signal line (slow line)

Plotted as arrow up/down.

Controlled by a bar lookback window (“Bar Period”) and price source (high/low vs close).

3) Bar Pattern Markers

Last 12 Bar (L12): marks potential trend initiation zones

L below bar (long trigger) / above bar (short trigger)

NR7 (Narrow Range): n marker for tension / compression

Inside Bar: i

Outside Bar: o (colored by breakout direction)

Sandwich Bar: s

Fakey: F (inside-bar false breakout patterns)

4) Segments (Subtle Trend Change Detection)

Draws up to 3 “segment” lines for highs and lows, using a maximum bar distance (Max Segment Bars).

Useful as a subtle confirmation layer and for background filters.

Context & Confluence Tools
Bollinger Bands

Standard or exponential calculation toggle.

Optional “Touched BBs only” for cleaner charts.

Displays BB1 and BB3 envelopes with filled zones.

Pivot Points (Classic)

1H, 4H, Daily, Weekly, Monthly, 3M, 12M.

Uses optimized request.security() tuple fetches to stay within limits.

Drawn as lines to the right of the current price (offset varies by timeframe).

Trading Sessions

London / New York / Tokyo / Sydney

Styles:

Vertical Line

Box

Background

Includes an extra New York 19:30 vertical line when enabled and in “Vertical Line” style.

Session plotting is restricted to intraday charts ≤ 1H.

MTF Candle Overlay

Shows a higher timeframe candle “x-ray” overlay on the current chart.

Adjustable timeframe + opacity.

Fair Value Gaps (Price Imbalance)

Bullish / bearish FVG boxes.

Supports:

Current timeframe mode

MTF mode using time-based coordinates (xloc.bar_time) for reliable placement.

Additional Context

Previous Candle High/Low lines (selectable timeframe)

Last Fractal S/R (selectable timeframe)

High Volume Spikes marker v when volume exceeds x * SMA(volume, 20)

Gradient Volume Profile (Optional)

Draws a vertical gradient profile on the right side of the chart for the visible range.

Smart contrast mode clips extreme peaks so normal nodes remain visible.

Replay-aware scan depth protection.

Real-time Alert: “5th Fractal Candle”

An optional alert that triggers while the 5th candle is still forming (real-time), detecting “potential fractal forming” structures without relying on ta.pivothigh/low for the live bar.

How to use in TradingView

Enable: Real-time Alerts → “Alert on 5th Fractal Candle (Real-time)”

Create an alert for the indicator.

Choose: Condition = “Any function call”

Optional: enable once-per-bar to reduce spam (already handled via alert.freq_once_per_bar).

Background Color Filters (Quick Visual Backtest Layer)

You can route many internal signals into the background as a quick “state” visualization. Examples include:

Bill Williams fractal breaks

Anticipated fractals

Last 12 Bar triggers

Parabolic SAR state

DMI/ADX trend state

HMA slope state

MACD slow slope state / events

Trendline/fractal break combinations (OR/AND variants)

Segments combinations (OR/AND variants)

MA1/MA2 cross background

The background calculation is wrapped in an MTF function and executed via request.security() using the selected background timeframe.

Inputs Overview (Practical)
Core toggles

Bill Williams Fractals

Fractal Trend Lines

SR Lines (horizontal fractal S/R + ATH line)

Divergence arrows

Bar signals (L12, NR7, inside/outside/sandwich/fakey)

Segments

Bollinger Bands

Pivot Points

Trading Sessions

MTF Candle Overlay

FVG

Additional Context (PCH/PCL, last fractal S/R, volume spikes)

Gradient Volume Profile

Timeframe-heavy modules

SR lines fractal timeframe (manual or auto-adapted)

Background filter timeframe

Previous candle timeframe

Last fractal timeframe

FVG timeframe

MTF candle overlay timeframe

Pivot point base timeframes (fixed)

Recommended Usage Workflow (Typical)

Start with structure

Enable fractals, last fractal S/R, optionally SR lines.

Add breakout framing

Enable fractal trend lines and/or FVG.

Add tension + trigger hints

Enable NR7, L12, volume spikes.

Add trend context

Enable EMA cloud or MA1/MA2, plus optional MTF info panel.

Use background filter as confirmation

Pick one filter (e.g., “Fractals Trend Lines” or “MACD Slope/Fractal Break BG (OR)”) to avoid clutter.

Performance Notes

The script uses multiple request.security() calls and can draw many objects (lines/boxes).

If you hit performance issues:

Disable Gradient Volume Profile

Reduce visible complexity (segments, pivots, sessions, MTF overlay)

Keep scan depth (vp_maxScan) reasonable for your chart usage

Visual Legend (What you see on chart)

White triangles: Bill Williams fractals

Blue trend lines: fractal trend lines (upper/lower)

Arrows: divergence signals (green up / red down)

L: Last-12 bar trigger points

n: Narrow range bar (NR7-like compression)

i / o / s / F: inside / outside / sandwich / fakey patterns

Dashed gray lines: previous candle high/low, last fractal high/low

v (bottom): high volume spike

Boxes: FVG zones, MTF candle overlay, and (optional) sessions in “Box” style

Background tint: selected background filter state

Limitations & Disclaimers

This indicator is for visual decision support, not a complete trading system.

Divergences and anticipated fractals can be early and produce false positives; use confluence and context.

Trendline “special mode” (Bars Per Side = 0) is dynamic by design and may behave differently than classic “two-point” trendlines.

Changelog (Optional)

Add your version notes here (e.g., “Replay fix for Volume Profile scan depth”, “MTF FVG time-based placement”, etc.).

License / Attribution

Author: (add your name/handle if you want)

Pine Script v5

Intended for TradingView charts (overlay indicator)
