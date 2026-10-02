# Gold & Silver Quantitative Analysis

A quantitative time-series analysis of Gold and Silver price behavior using
daily market data, rolling volatility, drawdowns, long-term trend analysis,
statistical price bands, and cross-asset relationships.

## Overview

This project analyzes more than a decade of daily Gold and Silver price data
to study:

- Return behavior
- Rolling volatility and volatility regimes
- Historical drawdowns
- Long-term price trends
- Statistical price bands
- Deviation from long-term trends
- Gold-Silver return correlation
- Gold/Silver price ratio
- Current quantitative positioning relative to historical bands

The analysis is designed to quantify price behavior using reproducible
statistical methods rather than relying on qualitative market narratives.

## Research Questions

The analysis focuses on the following questions:

1. How have Gold and Silver returns behaved over the analysis period?
2. How does realized volatility vary through time?
3. Which metal exhibits greater historical volatility?
4. When have unusually high-volatility regimes occurred?
5. How do current prices compare with their long-term trends?
6. How frequently do prices move outside their statistical bands?
7. How closely are Gold and Silver returns related?
8. How does the Gold/Silver ratio evolve over time?

## Data

Daily market data is retrieved using the `yfinance` Python library.

### Instruments

- Gold Futures: `GC=F`
- Silver Futures: `SI=F`
- USD/INR: `INR=X`

The analysis begins in January 2014 and uses the latest available observations
at the time the notebook is executed.

Gold and Silver prices are converted from USD terms to INR using the
USD/INR exchange rate.

> **Note:** The Yahoo Finance futures series are not equivalent to local
> physical-market or MCX quotations. INR-converted values are therefore
> treated as quoted futures-unit prices rather than local retail or exchange
> contract specifications.

## Methodology

### 1. Daily Returns

Daily percentage returns are calculated as:

$$
R_t = \frac{P_t}{P_{t-1}} - 1
$$

This provides a normalized measure of daily price movement.

### 2. Rolling Volatility

A 252-trading-day rolling standard deviation of daily returns is calculated
to measure how realized volatility changes over time. The volatility is
annualized using the square root of 252:

$$
\sigma_{\text{annualized}}
=
\sigma_{\text{252-day returns}}\sqrt{252}
$$

A 252-day window corresponds approximately to one trading year. This
rolling measure helps identify periods of relatively low, moderate, and
elevated volatility throughout the analysis period.

### 3. Volatility Regimes

Volatility observations are classified into three regimes using the empirical
33rd and 67th percentiles:

- Low volatility
- Medium volatility
- High volatility

The 90th percentile is additionally used to identify unusually elevated
volatility observations.

### 4. Drawdown Analysis

Historical drawdown is calculated relative to the previous running maximum:

$$
Drawdown_t =
\frac{P_t}{\max(P_1,\ldots,P_t)} - 1
$$

This measures the decline from a historical peak at each point in time.

### 5. Long-Term Trend

A 200-day moving average is used as the central trend measure:

$$
MA_t =
\frac{1}{200}
\sum_{i=0}^{199} P_{t-i}
$$

The 200-day window provides a long-term reference point for evaluating
price deviations.

### 6. Statistical Price Bands

Upper and lower price bands are constructed using the rolling 200-day
standard deviation of price:

$$
Upper_t = MA_t + 2\sigma_t
$$

$$
Lower_t = MA_t - 2\sigma_t
$$

These bands provide a descriptive statistical framework for measuring how
far prices have moved from their long-term trend.

The bands are not treated as trading signals or forecasts.

### 7. Trend Deviation

Deviation from the 200-day moving average is measured as:

$$
Deviation_t =
\frac{P_t - MA_t}{MA_t}\times100
$$

This allows Gold and Silver to be compared on a percentage basis.

### 8. Gold-Silver Relationship

The Pearson correlation between daily Gold and Silver returns is calculated
to examine their historical co-movement.

The Gold/Silver price ratio is also analyzed as:

$$
Gold/Silver\ Ratio =
\frac{Gold\ Price}{Silver\ Price}
$$

## Visualizations

The project generates the following figures:

- Gold and Silver price history
- Cumulative returns
- Rolling annualized volatility
- Volatility regimes
- Historical drawdowns
- Gold price with statistical bands
- Silver price with statistical bands
- Deviation from long-term trend
- Gold/Silver ratio

Figures are stored in:

```text
results/figures/
