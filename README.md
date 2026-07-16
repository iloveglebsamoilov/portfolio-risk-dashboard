# Portfolio Risk Analytics Dashboard

## Overview

This project analyzes the historical performance and risk characteristics of an equally weighted equity portfolio using Python and market data retrieved through `yfinance`.

The portfolio consists of Apple, Microsoft, NVIDIA, and SPDR S&P 500 ETF Trust. The analysis covers the period from January 2020 to the latest available trading date.

## Objectives

- Retrieve and clean historical market data
- Calculate individual asset and portfolio returns
- Measure portfolio volatility and downside risk
- Evaluate risk-adjusted performance
- Visualize portfolio growth, drawdowns, and changing volatility

## Portfolio

| Asset | Ticker | Weight |
|---|---:|---:|
| Apple | AAPL | 25% |
| Microsoft | MSFT | 25% |
| NVIDIA | NVDA | 25% |
| S&P 500 ETF | SPY | 25% |

The portfolio is assumed to be equally weighted and periodically rebalanced through the use of constant portfolio weights in the return calculation.

## Metrics

- Daily returns
- Cumulative returns
- Annualized return
- Annualized volatility
- 30-day rolling volatility
- Sharpe ratio
- Maximum drawdown
- Historical Value-at-Risk at the 95% confidence level
- Expected Shortfall at the 95% confidence level

## Methodology

Daily simple returns are calculated from adjusted closing prices.

Annualized return and volatility are estimated using 252 trading days per year.

The Sharpe ratio uses a 2% annual risk-free rate.

Historical Value-at-Risk is estimated from the fifth percentile of observed daily portfolio returns. Expected Shortfall is calculated as the average return on days when losses exceed the VaR threshold.

## Technologies

- Python
- pandas
- NumPy
- Matplotlib
- yfinance

## Installation

Clone the repository and install the required packages:

```bash
pip install -r requirements.txt
