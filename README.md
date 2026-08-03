# Trader Performance vs Bitcoin Market Sentiment

Analysis of the relationship between Hyperliquid trader performance and the Bitcoin Fear/Greed Index,
done as part of the Primetrade.ai data science hiring assignment.

## Objective
Explore how trader performance (PnL, win rate, position sizing, long/short bias) varies with market
sentiment, and translate the patterns into strategy takeaways.

## Repo Structure
```
.
├── README.md                              <- this file
├── notebook.ipynb                         <- full analysis (data cleaning, merge, EDA, charts, findings)
├── Report.md                              <- short written summary of methodology + key findings
├── sentiment_performance_overview.png      <- chart: avg PnL / win rate / trade size / trade count by sentiment
├── pnl_vs_sentiment_timeseries.png         <- chart: daily total PnL vs Fear/Greed value over time
├── fear_greed_index.csv                   <- Bitcoin Fear/Greed Index (Date, Classification)
└── .gitignore
```

## Note on the trade-level dataset
`historical_data.csv` (~47MB, 211k+ trade rows) is **not committed to this repo** to keep it lightweight —
GitHub isn't meant for large data files. Download it from the original source link below and place it in
the same folder as `notebook.ipynb` before running:

- Historical Data: https://drive.google.com/file/d/1IAfLZwu6rJzyWKgBToqwSmmVYU6VbjVs/view?usp=sharing
- Fear & Greed Index: https://drive.google.com/file/d/1PgQC0tO8XN-wqkNyghWc_-mnrYv_nhSf/view?usp=sharing
  (small file, already included in this repo as `fear_greed_index.csv`)

## How to Run
```bash
pip install pandas matplotlib jupyter
jupyter notebook notebook.ipynb
```
Run all cells top to bottom — the notebook expects `historical_data.csv` and `fear_greed_index.csv` to sit
in the same folder as `notebook.ipynb`.

## Summary of Findings
See [`Report.md`](./Report.md) for the full write-up. Headline results:

| Sentiment | Win Rate | Avg PnL/Trade |
|---|---|---|
| Extreme Fear | 37.1% | $34.54 |
| Fear | 42.1% | $54.29 |
| Neutral | 39.7% | $34.31 |
| Greed | 38.5% | $42.74 |
| Extreme Greed | 46.5% | $67.89 |

Win rate and average PnL both peak during Extreme Greed and are weakest during Extreme Fear. Traders in
this dataset size up the most during "Fear" specifically, and short-leaning trades do disproportionately
well in that regime. Full reasoning and additional charts (including a daily PnL-vs-sentiment time series)
are in the notebook.
