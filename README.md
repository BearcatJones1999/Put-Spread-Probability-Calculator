# Put Spread Probability & Tail-Risk Calculator

A notebook-based tool for estimating the probability that an underlying breaches a specified downside threshold over a configurable holding window — combining empirical frequency analysis with **GARCH(1,1) volatility forecasting**. Designed as a risk-gating sanity check for short-dated option strategies like put credit spreads.

## Motivation

Most retail probability calculators assume constant volatility and lognormal returns, which systematically underestimate tail risk during volatile regimes and overestimate it during calm ones. Equity returns exhibit **volatility clustering** — a feature directly captured by GARCH but ignored by Black-Scholes-style models.

This tool answers a practical question for option sellers:

> *Given current volatility conditions, how likely is it that my breakeven or short strike is breached over the next N trading days?*

It pairs that forward-looking estimate with a historical empirical baseline, letting you see whether the current regime is pricing in more (or less) tail risk than long-run history would suggest.

## Components

### 1. Empirical Breach Frequency
- Pulls daily price data via `yfinance`
- Resamples to configurable holding windows (1W, 2W, 4W, 1M, 3M)
- Computes end-to-end returns (simple or log) over each window
- Reports the historical frequency of returns falling below a user-defined threshold
- Surfaces distributional statistics and the most recent breach events

### 2. GARCH(1,1) Forward Forecast
- Fits GARCH(1,1) with **Student-t innovations** to daily log returns (handles fat tails)
- Forecasts cumulative variance over the target horizon
- Computes the probability of breaching the threshold under the fitted conditional distribution
- Reports a **tail-risk uplift** metric: the difference between GARCH-forecast breach probability and the empirical baseline, useful for flagging elevated-risk regimes before selling premium

### 3. Cross-Asset Correlation
- Downloads a user-specified basket of tickers
- Computes return correlations across the basket at daily, weekly, or monthly frequency
- Useful for identifying hedging candidates or diversification pairs for option positions

## Example Output

For AMZN with a −7.8% weekly threshold over 2010–present:
