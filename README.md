# CVD Momentum & Regime Filter Strategy

This project implements an algorithmic trading strategy focused on **Cumulative Volume Delta (CVD) Momentum** combined with a **Daily EMA Regime filter**. The strategy is backtested on 1-minute intraday data (QQQ and SPY) with intrabar stop-loss and take-profit logic.

## 📈 Strategy Logic

1.  **Regime Filter:** - Trades are only taken in the direction of the dominant trend.
    - Defined by the Daily Close relative to the Daily 50 EMA (or 100 EMA for SPY).
2.  **Momentum Trigger:** - Uses CVD (Cumulative Volume Delta) to gauge buying/selling pressure.
    - Enters when `CVD_Momentum` crosses its rolling mean.
3.  **Entry/Exit:**
    - **Long:** Price > VWAP + Bullish CVD + Bullish Regime.
    - **Short:** Price < VWAP + Bearish CVD + Bearish Regime.
    - **Risk Management:** Fixed Risk Per Trade (1%), Risk:Reward = 1:2.
    - **Execution:** Simulates intrabar execution (OHLC logic) to check if SL or TP was hit first within the 1-minute candle.

## 📊 Performance Results (3 Year Backtest)

### QQQ (Nasdaq 100)
The strategy significantly outperformed the Buy & Hold benchmark on QQQ.

| Metric | Strategy | Buy & Hold |
| :--- | :--- | :--- |
| **Total Return** | **141.59%** | 117.80% |
| **End Equity** | $24,159 | $21,779 |
| **Sharpe Ratio** | **1.34** | - |
| **Max Drawdown** | -7.79% | - |
| **Win Rate** | 38.29% | - |
| **Profit Factor** | 1.24 | - |

### SPY (S&P 500)
While profitable, the strategy underperformed the strong bullish run of the SPY benchmark during this period.

| Metric | Strategy | Buy & Hold |
| :--- | :--- | :--- |
| **Total Return** | 65.42% | **76.41%** |
| **Sharpe Ratio** | 0.71 | - |
| **Max Drawdown** | -8.72% | - |
| **Win Rate** | 37.61% | - |

