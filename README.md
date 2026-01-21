# Weekly Downside Breach Analysis (Mon Open → Fri Close)

This repository contains a small Python analysis that estimates how often a 1-week holding window experiences a downside move large enough to breach a chosen threshold (e.g., -1.5%). The motivation is to sanity-check the empirical frequency of breakeven violations for short-duration option structures such as put credit spreads, using a simple, transparent price-based proxy.

## What it measures

For each week in the sample:
- **Entry proxy:** Monday *open*
- **Exit proxy:** Friday *close*
- **Weekly return:** `FriClose / MonOpen - 1`

It then computes the frequency of weeks where:

- `weekly_return <= -1.5%` (configurable)

This can be interpreted as the empirical probability that the underlying ends the week at least 1.5% below the entry reference point—often used as a rough proxy for “breakeven is violated” for certain spread constructions.

## Why this approach

Option strategies are typically defined in terms of *moneyness* (e.g., “~1.5% OTM breakeven”), not fixed strikes across time. A strike-agnostic price proxy avoids the common backtesting pitfall of applying today’s strikes to historical price levels.

## Files

- `weekly_breach_analysis.py` (or notebook): main script that:
  - downloads price data via `yfinance`
  - builds Monday-open → Friday-close weekly periods
  - computes weekly return distribution
  - prints breach rates and recent breach weeks

## Requirements

- Python 3.9+
- `pandas`
- `numpy` (optional, depending on implementation)
- `yfinance`

Install dependencies:

```bash
pip install pandas yfinance numpy
