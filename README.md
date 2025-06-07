# Futures Statistical Arbitrage Strategy Development Report

## Data Processing and Cleaning

Our data preprocessing pipeline addressed significant data quality challenges:

- **Missing Symbol Filtering**: Removed approximately 30% of rows due to NaN symbol values, as imputation was not feasible for categorical identifiers
- **Price and Volume Imputation**: 
    - Implemented Brownian motion bridge methodology for large clusters of missing price and volume data
    - Applied forward-fill technique for smaller missing data gaps
- **Liquidity Filtering**: Constructed trading pairs exclusively from constituents with average liquidity exceeding 4x our target notional size

## Cointegration Analysis

Performed comprehensive cointegration testing across all eligible pairs:

- **Methodology**: Engle-Granger two-step procedure
    - Regressed near contract against far contract to estimate hedge ratios (Beta coefficients)
    - Validated spread stationarity using Augmented Dickey-Fuller (ADF) test
    - Confirmed mean-reverting properties via Hurst exponent analysis

## Market Regime Identification

Developed a sophisticated regime detection framework:

- **Feature Set**: Gaussian mixture model incorporating spread variance, trading volume, and term structure slope
- **Spread Construction**: Generated three distinct spread variants per pair:
    - Raw calendar spread
    - Log spread
    - Volatility-adjusted spread

## Primary Strategy: Volatility-Adjusted Calendar Spreads

Focused implementation on z-scored volatility-adjusted spreads with robust statistical measures:

- **Statistical Framework**: Utilized median and Median Absolute Deviation (MAD) instead of traditional mean/standard deviation
- **Rationale**: Enhanced robustness against regime changes and volatility clustering
- **Key Finding**: Market regime identification showed minimal impact on volatility-adjusted spread behavior

## Secondary Strategy: Butterfly Spreads

Implemented complementary statistical arbitrage approach:

- **Construction**: Level and slope-neutral spreads using three assets from identical underlying with monotonically increasing tenors
- **Signal Generation**: Z-scored butterfly spreads exhibited clear mean-reverting patterns suitable for systematic trading
- **Validation**: Visual inspection confirmed strong statistical arbitrage opportunities

## Strategy Performance

The signal-PnL analysis demonstrates strategy effectiveness across multiple underlying structures, providing empirical validation of our statistical arbitrage framework's profitability potential.

## Fee Impact Analysis and Strategy Viability

Post-transaction cost analysis revealed significant performance degradation across our trading strategies:

- **Calendar Spread Strategies**: Transaction costs systematically eroded alpha generation, with bid-ask spreads and exchange fees transforming ex-ante profitable statistical arbitrage opportunities into net-negative expected value propositions
- **Mean Reversion Deterioration**: The high-frequency nature of mean-reverting signals in calendar spreads resulted in excessive turnover, amplifying transaction cost impact and destroying risk-adjusted returns

## Butterfly Strategy Outperformance

In contrast, the butterfly spread implementation demonstrated superior risk-adjusted performance metrics post-fees:

- **Fee Resilience**: Lower signal frequency and larger expected moves per trade provided sufficient profit margins to absorb transaction costs
- **Risk-Adjusted Returns**: Multiple butterfly structures achieved annualized Sharpe ratios exceeding 1.5 while maintaining positive net returns after comprehensive fee deduction
- **Structural Advantage**: The three-leg construction's inherent stability and reduced sensitivity to regime shifts contributed to more predictable profit extraction

The empirical evidence strongly supports butterfly spread strategies as the primary statistical arbitrage vehicle for systematic implementation in futures markets.