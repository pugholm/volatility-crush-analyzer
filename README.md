# Volatility Crush Analyzer

A small desktop tool (Tkinter) for pricing an at-the-money straddle with Black-Scholes and testing what happens to it if the stock price and implied volatility change, e.g. around earnings. Market data comes from Interactive Brokers.

## What it does
- Fetches the last daily close and 30-day implied volatility for a ticker from TWS
- Prices the call, put and straddle, with straddle Greeks (delta, gamma, vega, theta)
- Scenario analysis: enter a new spot price and new IV to see the new straddle price and the long/short P/L per share

## Setup
```
pip install numpy scipy ibapi==9.81.1.post1
python analyzer.py
```

Requires TWS or IB Gateway running and logged in, with "Enable ActiveX and Socket Clients" ticked. Default port is 7497 (TWS paper). Use 7496 for live.

## Usage
1. Connect, enter a ticker, click Fetch Data
2. Set spot, strike and days to expiry to the trade you actually have in mind
3. Click Price Straddle, then enter a new spot and IV and click Analyze Scenario

## Known limitations
- One flat IV for the whole straddle, so front-month vs back-month crush can't be modelled
- No time decay in the scenario (the crush is treated as instant)
- Fetched price is the regular-session close, not a live quote
- Fetched IV is IB's 30-day summary, not the IV of a specific expiry
- No bid/ask spread, commissions, skew or dividends
- P/L is per share (multiply by 100 per contract)

## Disclaimer
For learning and personal analysis only. Not financial advice.