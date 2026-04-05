# Pine Script Collection

Trading indicators and strategies for TradingView by [@claygrace74](https://github.com/rubbermetal).

---

## Quad Rotation Indicators

Implementation of the **Day Trader Rock Star (DTRS) Quad Rotation Strategy** using 4 stochastic oscillators with progressively longer periods. Each stochastic gets its own pane so they can be stacked vertically on a chart.

| Indicator | Stochastic | Role | Glow Color |
|-----------|-----------|------|------------|
| Quad Rotation 9 3 | K=9, Smooth=3, D=3 | Fastest — turns first | Cyan |
| Quad Rotation 14 3 | K=14, Smooth=3, D=3 | Medium — confirms fast | Yellow |
| Quad Rotation 40 4 | K=40, Smooth=4, D=4 | Slow — trend confirmation | Red/Pink |
| Quad Rotation 60 10 | K=60, Smooth=10, D=10 | Slowest — major trend | Blue |

### Visual Elements

#### Lines

- **K line** (white, thin) — The K line of that pane's featured stochastic. It leads the D line. When K crosses D inside an extreme zone, a triangle signal fires.
- **D line** (colored glow + shadow) — The main signal line. Each pane has a unique glow color so you can tell them apart at a glance. The glow gets thicker on slower stochastics.
- **Convergence band** (white→gray) — Weighted average of all 4 D-lines, with the slowest (60/10) weighted heaviest. Bright white means all 4 stochastics agree. Fading to gray means they're diverging — weaker setup.

#### Zones

- **Green fill (0–20)** — Oversold zone. This is where buy setups form.
- **Red fill (80–100)** — Overbought zone. This is where sell setups form.

#### Signals

| Signal | Shape | Color | Meaning |
|--------|-------|-------|---------|
| **Quad Oversold** | Circle at 0 | Green | All 4 D-lines below 20 — in the buy zone |
| **Quad Overbought** | Circle at 100 | Red | All 4 D-lines above 80 — in the sell zone |
| **K/D Cross** | Triangle | Green (up) / Red (down) | K crossed D inside an extreme zone — turn confirmed |
| **TURN** | Label | Green (up) / Red (down) | First bar where the featured D-line changes direction in an extreme zone |
| **SEQ** | Diamond | Green / Red | Sequential rotation complete — all 4 stochastics turned in order (fast→slow) |
| **HG** (Holy Grail) | Flag | Gold | Quad alignment + RSI divergence confirming together — highest confidence signal |
| **CT** (Counter-Trend) | X-cross + orange background | Orange | 60/10 stuck in one extreme while 9/3 reached the opposite — trend is against you |

#### Histogram

The small green/red bars at the 50 midline show **RSI divergence** between fast RSI(5) and slow RSI(14). Green means bullish momentum is building (fast RSI leading slow RSI upward). Red means bearish momentum.

### How to Read a Buy Setup

All 4 panes show this sequence playing out:

1. All 4 D-lines drop below 20 into the green oversold zone — **green circles appear at 0**
2. If RSI divergence is also bullish, a **gold "HG" flag** appears (Holy Grail)
3. The **RSI histogram turns green** at the midline
4. The **9/3 pane shows "TURN" first** — the fastest stochastic starts curling up
5. A **green triangle** appears on the 9/3 pane — K crossed above D in the oversold zone
6. **14/3 shows "TURN"**, then 40/4, then 60/10 — each pane's D-line rises in sequence
7. A **green "SEQ" diamond** appears when the 60/10 (slowest) finally turns — full rotation confirmed
8. The **convergence band turns bright white** — all 4 D-lines are moving together
9. D-lines rise through 50 and head toward 80

### How to Read a Sell Setup

Mirror image of the buy:

1. All 4 D-lines climb above 80 into the red overbought zone — **red circles appear at 100**
2. Gold **"HG" flag** if RSI divergence is also bearish
3. **RSI histogram turns red**
4. **9/3 pane shows "TURN" first** — fastest starts curling down
5. **Red triangle** — K crossed below D in the overbought zone
6. **14/3, 40/4, 60/10 follow with "TURN"** in sequence
7. **Red "SEQ" diamond** when 60/10 finally turns down — full rotation confirmed
8. **Convergence band turns white** — agreement on the way down

### Signal Confidence Levels

Not every signal needs to fire for a valid trade. They are layers of confidence:

| Signal | What It Tells You | Confidence |
|--------|-------------------|------------|
| Green/Red circles | All 4 in the zone — you're in play | Baseline |
| TURN on 9/3 | Fastest is moving — earliest entry, most risk | Low |
| Triangle (K/D cross) | The turn is confirmed, not just a wiggle | Medium |
| TURN cascading across panes | Momentum building through slower stochastics | Medium-High |
| SEQ diamond | Full rotation confirmed — safest entry | High |
| HG flag | Everything aligns — quad + RSI divergence | Highest |

The tradeoff is timing vs. certainty. Entering on the first TURN gets a better price but carries more risk. Waiting for the SEQ diamond is safer but the move has already started.

### Counter-Trend Warning (Hard Rule)

The **orange X-cross with orange background flash** is the one signal that is a hard stop. It means the slowest stochastic (60/10) is stuck in one extreme while the fastest (9/3) has already reached the opposite extreme.

Example: 60/10 is still pinned below 20 (macro downtrend) but 9/3 already hit 80. The bounce was a counter-trend move, not a real reversal. Exit the trade.

---

## Crypto Scanner Climax

Multi-timeframe dashboard with overlay indicators. Displays across 4 configurable timeframes:

- Price metrics (Avg, High, Low)
- Volume metrics (Vol, AvgVol, Delta, RVWAP)
- Oscillators (RSI, Stoch K/D, CCI, MFI)
- **QR column** — Quad Rotation status per timeframe (how many of the 4 stochastics are oversold/overbought)
- Trend indicators (ADX, ROC, MOM, MACD, Hist, TarBaby, EMA crosses)
- Volatility (ATR, STDEV, Z-Score)
- Master Confluence signal (Strong Buy / Strong Sell / Neutral)

Optional overlays: Volume candles, Bollinger Bands, Keltner Channels, Ichimoku, Gator, Tar Baby bands, ALMA, EMA ribbon.

---

## Other Indicators

| File | Description |
|------|-------------|
| ADX and DI | Average Directional Index with DI+/DI- |
| Bears and Bulls | Bull/bear power oscillator |
| Center of Gravity | Ehlers center of gravity oscillator |
| Custom Reversal | Reversal pattern detection |
| Dynamic Support Line | Adaptive support level |
| EMA Cloud | EMA cloud overlay |
| EMA Crossover | EMA cross signals |
| Fear and Greed | Market sentiment oscillator |
| IntraDay Strategy | Intraday trading strategy |
| MACD | MACD with histogram |
| Momentum Swing Strategy | Momentum-based swing trades |
| RSI | Relative Strength Index |
| RSI Divergence | RSI divergence detection |
| Reversal Strategy | Reversal pattern strategy |
| Scalping Strategy | Short-term scalping signals |
| Stochastic RSI | Stochastic RSI oscillator |
| Support and Resistance | S/R level detection |
| Swing Trade Strategy | Swing trading strategy |
| Trade Worthy | Trade quality filter |
