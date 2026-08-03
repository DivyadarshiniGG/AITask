# Trader Performance vs Market Sentiment — Summary Report

## Objective
Explore whether Bitcoin market sentiment (Fear/Greed Index) relates to trader performance on Hyperliquid,
and identify patterns that could inform a sentiment-aware trading strategy.

## Data & Method
- **Trader data:** 211,224 individual trade records (May 2023 – May 2025) with fields including account,
  coin, size (USD), side/direction, and closed PnL.
- **Sentiment data:** Daily Fear & Greed Index classification (Extreme Fear, Fear, Neutral, Greed, Extreme Greed).
- Each trade was matched to the market sentiment on its trade date (only 6 of 211,224 rows had no match and
  were dropped). Performance metrics (average/median PnL, win rate, average trade size, volume) were then
  computed per sentiment bucket.

## Key Findings

| Sentiment | Trades | Win Rate | Avg PnL/Trade | Avg Trade Size |
|---|---|---|---|---|
| Extreme Fear | 21,400 | 37.1% | $34.54 | $5,350 |
| Fear | 61,837 | 42.1% | $54.29 | $7,816 |
| Neutral | 37,686 | 39.7% | $34.31 | $4,783 |
| Greed | 50,303 | 38.5% | $42.74 | $5,737 |
| Extreme Greed | 39,992 | 46.5% | $67.89 | $3,112 |

1. **Win rate and average PnL both peak in Extreme Greed** (46.5% win rate, $67.89 avg PnL) and are weakest
   in Extreme Fear (37.1%, $34.54). Trending, euphoric markets appear more forgiving for the average trade
   in this sample.
2. **"Fear" (not Extreme Fear) sees the largest trade sizes and highest total volume** — traders seem to treat
   moderate fear as an opportunity to size up, rather than a reason to de-risk.
3. **Short-leaning trades perform disproportionately well during Fear**, consistent with down-moves that tend
   to accompany fear readings.
4. **Individual traders are not uniformly better in one regime.** Among accounts active across 3+ sentiment
   regimes, most performed better on average during Greed-type days than Fear-type days — suggesting the
   dataset's traders skew toward momentum/trend-following rather than contrarian styles.

## Time-Series View
Plotting daily total PnL against the raw Fear/Greed index value (0-100) over time shows that the largest
PnL swings — both gains and losses — cluster around periods of sharp sentiment movement rather than calm,
stable-sentiment stretches. This suggests performance *dispersion* (risk), not just average performance,
rises with sentiment volatility — itself a useful signal for position sizing.

## Strategy Implications
- Consider **scaling position size with sentiment strength** — larger in Extreme Greed, smaller in Extreme Fear —
  given the win-rate and PnL gap.
- A **short-bias overlay specifically filtered on "Fear" (not Extreme Fear)** may be worth backtesting further.
- **Extreme Fear periods show the weakest win rate**; a simple risk rule reducing exposure there could reduce
  drawdowns.
- These are correlational patterns from a single historical window and a small set of ~32 unique accounts
  concentrated in a few coins (HYPE, BTC, ETH) — results should be validated out-of-sample before being used
  to size real capital.

## Files
- `notebook.ipynb` — full reproducible notebook (data loading, cleaning, merge, analysis, charts)
- `sentiment_performance_overview.png` — summary chart (avg PnL, win rate, avg size, trade count by sentiment)
- `pnl_vs_sentiment_timeseries.png` — daily total PnL overlaid with Fear/Greed index value over time
