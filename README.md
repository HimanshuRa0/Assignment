# Bitcoin Trader Performance vs Market Sentiment

Analyzes the relationship between Hyperliquid trader performance and the Bitcoin Fear & Greed Index across 211,224 trades from Dec 2024 – May 2025.

---

## Files

| File | Description |
|------|-------------|
| `trader_sentiment_analysis.py` | Main analysis script |
| `fear_greed_index.csv` | Daily Bitcoin Fear & Greed Index (date, value, classification) |
| `historical_data.csv` | Hyperliquid trader data (account, coin, PnL, direction, size, timestamp, etc.) |
| `trader_sentiment_dashboard.png` | Output dashboard (auto-generated on run) |

---

## Requirements

Python 3.8+ and the following libraries:

```bash
pip install pandas numpy matplotlib seaborn
```

---

## Usage

1. Place both CSV files in the same folder as the script.
2. Run:

```bash
python trader_sentiment_analysis.py
```

3. Two outputs are produced:
   - A **summary table** printed to the terminal
   - A **dashboard image** saved as `trader_sentiment_dashboard.png`

---

## What It Analyzes

| Analysis | Description |
|----------|-------------|
| Total PnL by sentiment | Which sentiment regime generated the most profit |
| Win rate by sentiment | % of closed trades that were profitable per regime |
| Avg trade size | Whether traders size up or down in Fear vs Greed |
| Short trade profitability | Avg closed PnL per short trade across sentiments |
| Monthly stacked PnL | How sentiment composition shifted month-to-month |
| FG correlation | Pearson correlation between daily FG index value and total PnL |
| Top coins by sentiment | Best-performing assets in Fear vs Extreme Greed |

---

## Key Findings

- **Fear = best performance** — highest win rate (88.6%) and total PnL ($3.36M)
- **Greed = most risk** — lowest win rate (76.1%), only liquidation event occurred here
- **Contrarian sizing** — traders placed largest positions ($7,816 avg) during Fear
- **Short edge in Fear** — avg short PnL was $207 in Fear vs $29 in Extreme Greed
- **Weak negative correlation (−0.08)** between FG index value and daily PnL — higher fear index values are very slightly associated with better returns

---

## Dataset Columns Reference

### `fear_greed_index.csv`
| Column | Description |
|--------|-------------|
| `date` | Date (YYYY-MM-DD) |
| `value` | Numeric index value (0–100) |
| `classification` | Extreme Fear / Fear / Neutral / Greed / Extreme Greed |

### `historical_data.csv`
| Column | Description |
|--------|-------------|
| `Account` | Trader wallet address |
| `Coin` | Asset traded (BTC, ETH, SOL, etc.) |
| `Direction` | Open Long / Close Long / Open Short / Close Short / Liquidated |
| `Size USD` | Trade size in USD |
| `Closed PnL` | Realized profit or loss on close |
| `Timestamp IST` | Trade timestamp (DD-MM-YYYY HH:MM, IST) |

---

## Customization

- **Change date range** — filter `df` by date after `load_data()` before calling `compute_metrics()`
- **Filter by account** — add `df = df[df["Account"] == "0x..."]` after loading
- **Filter by coin** — add `df = df[df["Coin"] == "BTC"]` after loading
- **Save chart at higher DPI** — change `dpi=150` to `dpi=300` in `plt.savefig()`

