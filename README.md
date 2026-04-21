# 📈 Institutional-Grade Algorithmic Trading System

## Overview
This project is a fully automated, multi-threaded algorithmic trading system built in Python.The system integrates a Machine Learning classification engine with institutional price action concepts, dynamic risk management, and live fundamental news filtering.

> **Note:** The source code for this algorithmic trading system is proprietary and hosted in a private repository. This repository serves as a technical architectural overview.

## 🛠 Tech Stack
* **Language:** Python 3.x
* **Trading API:** MetaTrader 5 (MT5) Python Integration
* **Machine Learning:** Scikit-Learn (`RandomForestClassifier`)
* **Data Processing:** Pandas, NumPy
* **Alerting/Monitoring:** Telegram Bot API
* **Other:** Multi-threading, dotenv (Secrets Management)

## 🧠 Core System Architecture

### 1. Machine Learning Engine
* **Model:** Random Forest Classifier trained on historical M5 candlestick data.
* **Feature Engineering:** Computes 17+ custom features including momentum slopes, volatility ratios, and multi-timeframe EMA differentials.
* **Probability Scoring:** The model outputs directional confidence scores, which are mathematically combined with technical indicators to form a final execution threshold.

### 2. Institutional Order Flow & Price Action
The system detects complex market structures autonomously, avoiding the lag of traditional indicators:
* **Liquidity Sweeps & Market Structure Shifts:** Identifies buy-side and sell-side liquidity grabs to trade alongside smart money.
* **Volume Profile & Value Area (VAH/VAL):** Calculates Point of Control (POC) dynamically, executing fading strategies in ranges and breakout strategies during momentum.
* **VWAP Alignment:** Hunts for textbook institutional VWAP pullbacks and wick rejections.
* **Classic & Advanced Patterns:** Autonomously charts Double Tops/Bottoms, Head & Shoulders, and 1-2-3 Reversals while scanning for candlestick formations (e.g., Engulfing, Hammers).

### 3. Advanced Risk Management (The "Split-Brain" Engine)
* **Dynamic Sizing:** Replaces static lot sizes with institutional percentage-based risk models, dynamically adjusting position size based on account equity and current ATR.
* **Twin-Ticket Execution:** Splits successful signals into two tickets: a "Paycheck" ticket for immediate profit realization and a "Runner" ticket with a wide trailing leash to capture macro trends.
* **Volatility-Adjusted Stops:** Stop Loss and Take Profit levels automatically expand or contract based on real-time Average True Range (ATR) expansion limits.
* **Capital Preservation Logic:** * Features a hard daily drawdown limit (5%).
  * Time-based staleness exits (auto-closing trades that stagnate).
  * 40-minute automatic profit-locking algorithms.

### 4. Fundamental Integration
* **Live News Blackouts:** Parses local MT5 economic calendars to pause the execution engine 15 minutes before and after high-impact USD data releases (CPI, NFP, GDP).
* **Macro Bias:** Adjusts algorithmic confidence scores positively or negatively based on the directional surprise of live economic data.

### 5. Multi-Threaded Execution & Monitoring
* **Asynchronous Trailing:** Trailing stops and break-even logic are handled on a separate thread to ensure zero API latency during volatile tick movements.
* **Live Telemetry:** Integrates directly with Telegram to push instant execution receipts, spread warnings, and daily P&L session summaries directly to a mobile device.

## 🚀 Performance Validation
The strategy was validated through rigorous out-of-sample forward testing, emphasizing absolute risk containment over aggressive yield. Key performance indicators heavily monitored include the Sharpe Ratio, Maximum Drawdown, and Profit Factor metrics.
