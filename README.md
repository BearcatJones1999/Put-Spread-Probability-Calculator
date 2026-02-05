Put Credit Spread Downside Risk Tool

This notebook evaluates downside risk for short-dated put credit spreads by combining historical breach frequencies with forward-looking, regime-adjusted risk using a GARCH(1,1) model with Student-t (fat-tailed) errors.

The goal is to determine whether a downside threshold represents true tail risk or routine market noise under current volatility conditions.

What it does

For a selected asset and holding window (e.g. 1W, 2W, 4W):

Computes historical downside breach rates for a user-defined return threshold

Reports distribution diagnostics (mean, volatility, downside percentiles, recent breaches)

Fits a GARCH(1,1) model to daily returns to estimate:

Forecast volatility over the next window

Conditional probability of breaching the threshold

Tail-risk uplift relative to historical averages

How to interpret the output

Empirical probability: long-run frequency of threshold breaches

GARCH probability: likelihood of breach under current volatility conditions

Positive uplift: elevated risk regime (unfavorable for selling premium)

Negative uplift: suppressed risk regime (favorable for selling premium)

As a rule of thumb, selling downside premium is most attractive when:

GARCH breach probability is low (approximately 5–8%)

GARCH probability is less than or equal to the historical probability

The threshold lies outside routine volatility

Intended use

Pre-trade risk filter for put credit spreads

Comparing downside risk across assets (indices vs single names)

Identifying volatility regimes where premium selling is structurally unsafe

This tool is risk-focused, not a pricing or PnL simulator, and assumes holding positions to expiration.

Key takeaway

Selling downside premium only works when you are being paid to insure against rare events, not normal market moves.
Selling downside premium only works when you are being paid to insure against rare events, not normal market moves.
