# XAU/USD SMA Crossover Backtest

A systematic backtesting framework for a dual simple moving average crossover strategy on Gold Futures (GC=F), implemented in Python.

# Strategey Overview

The strategy uses two SMAs on 1-hour closing prices to generate long entries and exits:

Entry signal — bullish crossover: SMA(10) crosses above SMA(100)
Exit signal — bearish crossover: SMA(10) crosses below SMA(100)
Direction — long only
Instrument — Gold Futures (GC=F)
Timeframe — 1-hour candles
Data window — 60 days via Yahoo Finance

The core idea: when the short-term average crosses above the long-term average, momentum is turning bullish. The position is held until the reverse signal fires.

# Backtest Parameters
Parameter                  Value
Symbol                     GC=F (Gold Futures)
Timeframe                  1H
FastSMA                    10 periods
Slow SMA                   100 periods
Starting balance           $10,000
Volume per trade           1 contract
Stop loss / Take profit    None (exit on signal only)

# Implementation
The backtest is built around two classes:
Position — represents a single trade, tracking open/close prices, datetime, volume, and profit. P&L is calculated as (close_price - open_price) * volume for long trades.
Strategy — iterates over the full dataset bar by bar. On a bearish crossover, any open position is closed at the current close. On a bullish crossover, a new long position is opened. Returns a full trade log as a DataFrame with a cumulative PnL column.

# Visulisations
The notebook produces two charts using Plotly:

Price chart — 1H close price with SMA(10) and SMA(100) overlaid, vertical lines marking each entry signal, and green lines connecting open to close price for each profitable trade
PnL curve — cumulative profit/loss over the backtest period

# Requirements
yfinace
pandas
numpy
plotly

pip install yfinance pandas numpy plotly 

# Usage 
Open sma_crossover_backtest.ipynb in Jupyter Notebook or JupyterLab and run all cells. Data is pulled live from Yahoo Finance — no manual download needed.

# Limitations
This is a demonstration of my knowledge of python. Known limitations:
No transaction costs or slippage modelled
Long only — no short entries on bearish crossovers
Fixed volume with no position sizing logic
60-day window is short for robust strategy validation
No walk-forward testing or out-of-sample validation

# Author
Ryan James Forrester - BA Economics and Finance,
Leeds Beckett University
https://www.linkedin.com/in/ryan-forrester-708837303/

