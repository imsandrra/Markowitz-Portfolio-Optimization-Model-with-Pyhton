# Markowitz Portfolio Optimization Model

A quantitative framework implementing Modern Portfolio Theory for optimal asset allocation across six major U.S. stocks representing diverse market sectors.

## Overview

This project applies mean-variance optimization (Markowitz Model) to construct efficient portfolios that maximize risk-adjusted returns. The analysis uses historical price data from January 2020 to August 2025 to derive optimal asset allocations based on individual risk preferences and return objectives.

## Portfolio Universe

The optimization framework includes six stocks across different sectors:

- **Technology**: AAPL (Apple), NVDA (NVIDIA)
- **Consumer Staples**: PG (Procter & Gamble)
- **Healthcare**: JNJ (Johnson & Johnson)
- **Financial Services**: GS (Goldman Sachs)
- **Energy**: XOM (ExxonMobil)

## Methodology

### Data Processing
- **Historical Period**: January 2020 - August 2025
- **Data Source**: Yahoo Finance (yfinance API)
- **Return Calculation**: Daily percentage changes, annualized assuming 252 trading days

### Optimization Framework
- **Model**: Mean-Variance Optimization (Markowitz)
- **Risk Measure**: Portfolio volatility (standard deviation of returns)
- **Performance Metric**: Sharpe ratio (return per unit of risk)
- **Constraints**: 
  - Weights sum to 1 (fully invested)
  - No short selling (0 ≤ weight ≤ 1)
- **Solver**: Sequential Least Squares Programming (SLSQP)

### Key Components

1. **Efficient Frontier Construction**: Generates 100 portfolios spanning the risk-return spectrum from minimum to maximum expected returns
2. **Minimum Variance Portfolio**: Identifies the lowest-risk allocation regardless of return
3. **Target Return Optimization**: Finds minimum-risk portfolios for specified return targets
4. **Target Volatility Optimization**: Finds maximum-return portfolios for specified risk levels

## Key Findings

### Minimum Variance Portfolio
- **AAPL**: 2.3%
- **NVDA**: 3.6%
- **PG**: 35.6%
- **JNJ**: 45.5%
- **GS**: 1.2%
- **XOM**: 11.8%

Portfolio Volatility: 17.5%
Portfolio Return: 12.3%

The optimizer heavily weights defensive assets (PG, GS) and reduces allocation to high-volatility growth stocks (AAPL, NVDA), reflecting the mathematical reality that diversification benefits are maximized by combining low-correlation assets.

### Optimal Risk-Return Profile
- **Optimal Sharpe Ratio**: ~1.42
- **Optimal Volatility Range**: 22.3% - 27.3% annualized
- **Expected Return Range**: ~25% - 35% annualized

The "sweet spot" occurs at moderate risk levels, where portfolios outperform both conservative and aggressive strategies on a risk-adjusted basis.

### Efficient Frontier Visualization
<img src="/image.png" alt="Efficient Frontier" width="700" height="500">

![Efficient Frontier](/image.png)
*Figure: The efficient frontier showing the risk-return trade-off. Color indicates Sharpe ratio, with optimal portfolios in the 22-27% volatility range.*

### Portfolio Insights

**Diversification Benefits**: 
- Low correlation between consumer staples (PG) and technology stocks maximizes diversification
- Sector diversification across healthcare (JNJ), energy (XOM), and financial services (GS) reduces concentration risk
- Technology stocks (AAPL, NVDA) exhibit correlation clustering, limiting diversification within the tech sector

**Risk-Return Relationship**:
- The efficient frontier is non-linear, showing diminishing returns at higher risk levels
- Higher expected returns require proportionally higher volatility acceptance

## Project Structure

```text
├── Data Collection & EDA
│   ├── Historical price download (yfinance)
│   └── Initial data inspection
│
├── Returns Analysis
│   ├── Daily returns calculation
│   ├── Annualized expected returns
│   └── Covariance/correlation matrix computation
│
├── Portfolio Optimization
│   ├── Performance functions (return, volatility)
│   ├── Minimum variance solution
│   └── Efficient frontier construction
│
└── Target Functions
    ├── Target return optimization
    └── Target volatility optimization
```

## Dependencies

```text
yfinance>=0.2.0
numpy>=1.20.0
pandas>=1.3.0
matplotlib>=3.4.0
scipy>=1.7.0
seaborn>=0.11.0
```

## Usage

The project provides two main optimization functions:

1. **`get_weights_for_target_return(target_return)`**: Returns optimal weights for achieving a specified annualized return
2. **`get_weights_for_target_volatility(target_volatility)`**: Returns optimal weights for achieving a specified annualized volatility

Example:
```python
# 75% target return
get_weights_for_target_return(0.75, expected_returns, cov_matrix, tickers)

# 27.3% target volatility  
get_weights_for_target_volatility(0.273, expected_returns, cov_matrix, tickers)
```

## Critical Success Factors

1. **Diversification across uncorrelated assets** remains the most reliable method for improving risk-adjusted performance
2. **Dynamic rebalancing** based on changing correlations and expected returns is essential for maintaining optimal allocations
3. **Risk tolerance assessment** must be realistic and account for behavioral biases during market stress

## Implementation Recommendations

- **Regular rebalancing**: Quarterly or semi-annually to maintain target allocations
- **Monitoring regime changes**: Track asset correlations and expected returns for significant shifts
- **Stress testing**: Validate portfolios against historical market downturns
- **Tax-efficient implementation**: Consider holding periods and account types for tax optimization

## Limitations & Disclaimers

⚠️ **Important**: This analysis is based on historical data and mathematical optimization. Past performance does not guarantee future results. Key limitations include:

- Assumes returns are normally distributed and stationary over time (often violated in practice)
- Does not account for transaction costs, taxes, or liquidity constraints
- Expected returns and covariances are estimated from historical data and may not reflect future conditions
- No consideration of investor-specific constraints (liquidity needs, time horizon, etc.)

Investors should consult with qualified financial advisors and consider their complete financial situation before making investment decisions.

*This project is for educational and research purposes only. Not financial advice.*
