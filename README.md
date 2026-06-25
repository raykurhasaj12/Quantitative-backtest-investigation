# Quantitative-backtest-investigation
Quantitative backtest testing whether retail trading strategies (ORB and previous-day liquidity) hold statistical edge on NASDAQ-100. Monte Carlo validation, out-of-sample testing, compounding position sizing.

# Do Retail Trading Strategies Hold Statistical Edge?
### A Quantitative Backtesting Investigation into ORB and Liquidity Sweep Concepts on NASDAQ-100

**Author:** Ray Kurhasaj | BSc Mathematics, University of Liverpool  
**Language:** Python 3.13 | **Environment:** Jupyter Notebook  

---

## Overview

This project tests whether two commonly taught retail trading strategies — the 15-minute Opening Range Breakout (ORB) and previous-day liquidity sweep concepts — hold genuine statistical edge on the NASDAQ-100 index. Rather than accepting retail trading claims at face value, this project applies rigorous quantitative methods to determine whether these strategies are backed by statistical evidence or whether profitable results can be explained by chance alone.

The project was motivated by personal trading experience, including passing a Topstep funded account evaluation (achieved by approximately 5% of participants), and the subsequent question of whether that result reflected genuine edge or favourable variance.

---

## Key Findings

| Strategy | Result |
|---|---|
| ORB (15-min, 4 variations) | ❌ Rejected — underperformed buy-and-hold across all configurations |
| Previous Day High/Low Reversal | ❌ Rejected — unprofitable across all 12 SL/RR configurations |
| Previous Day High/Low Continuation | ✅ Strong evidence of edge — p < 0.001 |

**Headline result (SL=10, RR=3:1, 2020–2024):**
- Win rate: **40.94%** vs. 25% breakeven at 3:1 RR
- Total return: **364.69%** on £10,000 starting capital
- Return / Max Drawdown ratio: **17.61x**
- Beat **100% of 1,000 random-entry Monte Carlo simulations** (p < 0.001)
- Survived out-of-sample test on **2016–2020 data** (unseen period)

**Core insight:** Retail traders correctly identify previous-day highs and lows as price levels containing exploitable information — but teach the *wrong direction*. The data supports **continuation**, not reversal, at these levels.

---

## Methodology

### Data
- Source: NASDAQ-100 1-minute OHLCV data (Kaggle, 2016–2025)
- In-sample window: 2020–2024 (~1,260 trading days)
- Out-of-sample window: 2016–2020 (untouched during strategy development)
- Timezone: New York (ET), non-trading days removed

### Position Sizing
- Liquidity setups: 1% of current account equity per trade (compounding)
- ORB setups: 1% of entry price (fixed, for direct comparison)

### Statistical Validation
- **Monte Carlo random-entry test:** 1,000 simulations using identical exit mechanics but randomised entry timing — real strategy beat all 1,000 (p < 0.001)
- **Trade-order permutation test:** 1,000 reshufflings of real trade sequence — Return/DD ratio ranked at 89.5th percentile (above average but not suspiciously lucky)
- **Out-of-sample test:** Strategy applied unchanged to 2016–2020 data, confirmed profitable with recalibrated parameters
- **Sharpe ratio analysis:** Per-trade and annualised versions computed and critically examined

---

## Repository Contents

| File | Description |
|---|---|
| `backtest_strategy.ipynb` | Full backtesting notebook — all cells executed with outputs visible |
| `Do retail Trading strategies hold statistical edge Final.pdf` | Complete written research report (methodology, results, limitations, conclusion) |

---

## Data Setup

Data is not included in this repository due to file size. To reproduce results:

1. Download the NASDAQ-100 1-minute dataset from Kaggle
2. Place the following CSV files in the same directory as the notebook:
   - `1m_data.csv`
   - `1d_data.csv`
   - `5m_data.csv`
   - `15m_data.csv`
   - `1h_data.csv`
3. Run all cells in order (Kernel → Restart and Run All)

---

## Dependencies
