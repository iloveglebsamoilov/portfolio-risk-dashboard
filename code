import yfinance as yf
import pandas as pd
import numpy as np
import matplotlib.pyplot as plt

tickers = ["AAPL", "MSFT", "NVDA", "SPY"]
start_date = "2020-01-01"
end_date = None
risk_free_rate = 0.02

print("downloading market data")

prices = yf.download(
    tickers,
    start=start_date,
    end=end_date,
    auto_adjust=True,
    progress=False
)["Close"]

print(prices.head())

returns = prices.pct_change().dropna()

print(returns.head())

cumulative_returns = (1 + returns).cumprod()

volatility = returns.std() * np.sqrt(252)

print("annualized volatility")
print(volatility)

annual_return = returns.mean() * 252

sharpe_ratio = (
    annual_return - risk_free_rate
) / volatility

print("sharpe ratio")
print(sharpe_ratio)

rolling_max = cumulative_returns.cummax()

drawdown = cumulative_returns / rolling_max - 1

max_drawdown = drawdown.min()

print("maximum drawdown")
print(max_drawdown)

var95 = returns.quantile(0.05)

print("historical var")
print(var95)

expected_shortfall = {}

for col in returns.columns:
    expected_shortfall[col] = returns[col][
        returns[col] <= var95[col]
    ].mean()

expected_shortfall = pd.Series(expected_shortfall)

print("expected shortfall")
print(expected_shortfall)

print("correlation matrix")
print(returns.corr())

plt.figure(figsize=(12, 6))
prices.plot(ax=plt.gca())
plt.title("historical prices")
plt.xlabel("date")
plt.ylabel("price")
plt.grid(True)
plt.show()

plt.figure(figsize=(12, 6))
cumulative_returns.plot(ax=plt.gca())
plt.title("cumulative returns")
plt.xlabel("date")
plt.ylabel("growth of $1")
plt.grid(True)
plt.show()

plt.figure(figsize=(12, 6))
drawdown.plot(ax=plt.gca())
plt.title("drawdown")
plt.xlabel("date")
plt.ylabel("drawdown")
plt.grid(True)
plt.show()

rolling_vol = returns.rolling(30).std() * np.sqrt(252)

plt.figure(figsize=(12, 6))
rolling_vol.plot(ax=plt.gca())
plt.title("30-day rolling volatility")
plt.xlabel("date")
plt.ylabel("annualized volatility")
plt.grid(True)
plt.show()

summary = pd.DataFrame({
    "annual return": annual_return,
    "annual volatility": volatility,
    "sharpe ratio": sharpe_ratio,
    "max drawdown": max_drawdown,
    "var (95%)": var95,
    "expected shortfall": expected_shortfall
})

print(summary.round(4))
