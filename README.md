# Quantitative Trading Framework & Intraday Momentum Strategy
### *High-Fidelity Backtesting with Friction Modeling & Microstructure Proxies*

## 📌 Project Overview
This project is a professional-grade backtesting engine designed to bridge the gap between theoretical alpha and live execution. Unlike standard vectorized backtesters, this framework utilizes an **event-driven simulation** on high-resolution 1-minute data. 

The system is specifically engineered to account for **market friction**, **liquidity constraints**, and **intrabar price pathing**, ensuring that results remain valid in a live institutional environment.

## 🚀 Key Features
* **Execution Realism:** Signals are generated on the close of bar $T$ and executed at the open of bar $T+1$, strictly eliminating **Look-Ahead Bias**.
* **Friction Modeling:** Implements a realistic **$0.01 per share slippage** model on every entry and exit, simulating the bid-ask spread and regulatory fees.
* **Microstructure Proxy:** Utilizes a **Cumulative Volume Delta (CVD)** proxy to identify volume exhaustion and institutional order flow bias.
* **Intrabar Exit Engine:** A custom-coded simulation that analyzes the price path (O-L-H-C) within a single minute to accurately trigger Stop-Loss and Take-Profit orders.
* **Risk-First Analytics:** Prioritizes **Max Drawdown** and **Sharpe Ratio** over raw ROI to evaluate the strategy's viability for leveraged scaling.

## 📊 Backtesting Results (Post-Friction)
*Results generated over a 3-year period (2021–2024) including a $0.01/share slippage tax on 1,000+ trades.*

| Metric | QQQ (Nasdaq 100) | SPY (S&P 500) |
| :--- | :--- | :--- |
| **Total Return** | **127.33%** | 59.96% |
| **Benchmark (Buy & Hold)** | 117.80% | **76.41%** |
| **Sharpe Ratio (Rf=5%)** | **1.23** | 0.64 |
| **Max Drawdown** | **-7.96%** | -8.96% |
| **Profit Factor** | 1.22 | 1.19 |
| **Total Trades** | 1,230 | 819 |

### **Key Performance Insight:**
While raw returns in the SPY test lagged the benchmark, the strategy’s **Alpha** is found in its risk management. In both indices, the strategy maintained a **Max Drawdown of <9%**, effectively preserving capital during the significant market corrections of 2022 where the benchmarks suffered 20-30% losses.

## 🛠 Strategy Architecture
1. **Trend Regime:** Daily 50-EMA (QQQ) and 100-EMA (SPY) filter to ensure alignment with major market structure.
2. **Volume Analysis:** CVD Momentum oscillator used to detect intra-day buyer/seller exhaustion.
3. **Execution Logic:** * **Entry:** Market order at $T+1$ Open following a $T$ Close signal.
    * **Risk:** 1% Equity-at-Risk per trade.
    * **Target:** Mathematical 2.0 Profit Factor (Reward-to-Risk).
4. **Stress Test:** Every trade is penalized with a fixed $0.01/share cost to ensure the edge is "thick" enough to survive the spread.

## 📂 Technical Stack
* **Language:** Python 3.x
* **Data Ingestion:** Alpaca Markets API
* **Processing:** Pandas (Time-series manipulation), NumPy (Vectorized indicator math)
* **Visualization:** Matplotlib (Equity curve & Drawdown profiling)

## ⚖️ Assumptions & Limitations
* **Liquidity:** Assumes fills are available at the Open price for highly liquid ETFs (QQQ/SPY).
* **CVD Proxy:** Uses candle-based volume delta; true tick-level CVD requires Level 2 data.
* **Pathing:** Intrabar exits assume a standard O-L-H-C path for bullish candles and O-H-L-C for bearish candles to remain conservative.

---
*Developed by Samith Suranjana*
