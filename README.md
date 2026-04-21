# Non-Linear Pairs Trading: A Multivariate Copula Approach

## Objective
This project develops a pairs trading strategy based on nonlinear dependence modeling using copulas. The goal is to identify asset pairs with strong dependence structures and exploit deviations from their joint behavior.

## Data
- Source: Yahoo Finance (via yfinance)
- Period: 2020–2026
- Assets: Equities grouped by sector (Semiconductors, Financials, Big Tech, Healthcare)
- Frequency: Daily closing prices
- Transformation: Log returns

## Methodology

### 1. Pair Selection
- Dependence measured using **Kendall’s tau**
- For each sector, the pair with the highest dependence is selected

### 2. Marginal Modeling
- Returns are fitted with a **Student-t distribution**
- Probability Integral Transform (PIT) applied to obtain uniform marginals

### 3. Copula Estimation
For each selected pair, multiple copula families are fitted:
- Gaussian
- Clayton (lower tail dependence)
- Gumbel (upper tail dependence)
- Frank (symmetric dependence)

Model selection is performed using **Akaike Information Criterion (AIC)**.

### 4. Dependence Validation
- Comparison between real data and simulated samples from fitted copulas
- Visual inspection via scatter plots

### 5. Trading Strategy
Trading signals are based on **conditional probabilities** derived from the copula:

- Long X / Short Y when:
  - P(U|V) is in the lower tail
- Short X / Long Y when:
  - P(V|U) is in the lower tail

Positions are forward-filled to maintain exposure.

### 6. Backtesting
- Strategy applied on historical data
- Spread defined as difference in log returns
- Transaction costs included (fixed cost per trade)

## Performance Metrics
- Total cumulative return (net of costs)
- Annualized Sharpe ratio
- Number of trades
- Maximum drawdown

## Tools & Libraries
- Python
- NumPy, Pandas
- SciPy
- yfinance
- pyvinecopulib
- statsmodels
- seaborn, matplotlib

## Results
The strategy identifies sector-specific pairs and adapts the copula family accordingly. Performance varies across sectors, highlighting the importance of dependence structure in trading strategies.

Detailed results and visualizations are available in the Jupyter Notebook.

## Notes
This project is intended for research and educational purposes. It does not constitute financial advice.
