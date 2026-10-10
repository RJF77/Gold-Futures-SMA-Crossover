# XAU/USD SMA Crossover Backtest

A systematic backtesting framework for a dual simple moving average crossover strategy on Gold Futures (GC=F), implemented in Python.

# Strategy Overview

The strategy uses two SMAs on 1-hour closing prices to generate long entries and exits:

Entry signal — bullish crossover: SMA(10) crosses above SMA(100)
Exit signal — bearish crossover: SMA(10) crosses below SMA(100)
Direction — long only
Instrument — Gold Futures (GC=F)
Timeframe — 1-hour candles
Data window — 60 days via Yahoo Finance

The core idea: when the short-term average crosses above the long-term average, momentum is turning bullish. The position is held until the reverse signal fires.

# Backtest Parameters
Parameter	Value
Symbol	GC=F (Gold Futures)
Timeframe	1H
Fast SMA	10 periods
Slow SMA	100 periods
Starting balance	$10,000
Volume per trade	1 contract
Stop loss / Take profit	None (exit on signal only)
# Implementation

The backtest is built around two classes:

Position — represents a single trade, tracking open/close prices, datetime, volume, and profit. P&L is calculated as (close_price - open_price) * volume for long trades.

Strategy — iterates over the full dataset bar by bar. On a bearish crossover, any open position is closed at the current close. On a bullish crossover, a new long position is opened. Returns a full trade log as a DataFrame with a cumulative PnL column.

# Visualisations

The notebook produces two charts using Plotly:

1. Price chart — 1H close price with SMA(10) and SMA(100) overlaid, vertical lines marking each entry signal, and green lines connecting open to close price for each profitable trade

<img width="482" height="330" alt="Screenshot 2026-10-10 at 23 56 47" src="https://github.com/user-attachments/assets/8d6dca81-fae2-419c-81ae-a89c28281f91" />

2. PnL curve — cumulative profit/loss over the backtest period

<img width="482" height="330" alt="Screenshot 2026-10-10 at 23 58 18" src="https://github.com/user-attachments/assets/88b95f65-f5bf-42ca-a425-1255fedbb858" />

# Requirements
yfinance
pandas
numpy
plotly
bash
pip install yfinance pandas numpy plotly
# Usage

Open gold_futures_sma_crossover.ipynb in Jupyter Notebook or JupyterLab and run all cells. Data is pulled live from Yahoo Finance — no manual download needed.

# Reflections

This project was built as a learning exercise in my first year of university to apply Python to real financial data and market concepts. It demonstrates:

Pulling and manipulating financial time series data with pandas and yfinance
Implementing signal logic using vectorised numpy operations
Building a simple object-oriented backtesting structure from scratch
Visualising price action, signals, and trade outcomes with Plotly

Known limitations: no transaction costs or slippage modelled, long-only logic, fixed volume with no position sizing, and a 60-day window that is short for robust validation. These are intentional trade-offs for a first project focused on understanding the mechanics of a systematic strategy rather than optimising performance.

# Author

Ryan James Forrester — BSc Economics and Finance, Leeds Beckett University
LinkedIn
