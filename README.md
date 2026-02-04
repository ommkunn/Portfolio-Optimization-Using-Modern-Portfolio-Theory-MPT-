# Portfolio Optimization Using Modern Portfolio Theory (MPT)

This repository contains a learning-focused implementation of portfolio optimization using Modern Portfolio Theory (MPT) in Python. The objective is to construct an optimal portfolio allocation by maximizing the Sharpe Ratio based on historical market data.

This project was created as part of a personal learning exercise. While online resources such as YouTube tutorials were referenced for guidance, all code structure, comments, and explanations were written independently to ensure conceptual clarity and understanding.

---

## Project Overview

The script performs the following operations:

- Downloads historical financial data using the `yfinance` library  
- Uses adjusted close prices to account for dividends and stock splits  
- Calculates logarithmic returns for additive and stable return modeling  
- Constructs an annualized covariance matrix to estimate portfolio risk  
- Optimizes asset weights by maximizing the Sharpe Ratio  
- Visualizes the optimal portfolio allocation using a bar chart  

---

## Assets Used

The portfolio includes diversified exchange-traded funds (ETFs):

| Ticker | Description |
|-------|-------------|
| SPY | S&P 500 ETF (US Equity) |
| QQQ | NASDAQ 100 ETF (Technology-focused Equity) |
| VTI | Total US Stock Market ETF |
| BND | US Total Bond Market ETF |
| GLD | Gold ETF |

---

## Key Concepts Applied

- Modern Portfolio Theory (MPT)  
- Logarithmic Returns  
- Expected Portfolio Return  
- Portfolio Volatility (Standard Deviation)  
- Covariance and Correlation  
- Sharpe Ratio  
- Constrained Optimization using SLSQP  

---

## Libraries Used

```python
yfinance
pandas
numpy
scipy
matplotlib
datetime
```

---


## Install Dependencies using:
pip install yfinance pandas numpy scipy matplotlib

---

## Methodology

This project follows a structured approach to implement portfolio optimization using Modern Portfolio Theory. Each step is designed to build clarity around how returns, risk, and optimal asset allocation are calculated.

---

### Data Collection

Historical price data is retrieved using the `yfinance` library. For each asset, adjusted close prices are used whenever available. Adjusted prices account for dividends and stock splits, ensuring that return calculations are not distorted by corporate actions. If adjusted close data is unavailable, closing prices are used as a fallback.

---

### Return Calculation

Logarithmic returns are calculated using consecutive adjusted close prices. Log returns are preferred because they are time-additive and provide better mathematical properties for portfolio-level calculations.

Missing values created by price shifts are removed to ensure clean return series.

---

### Risk Estimation

Portfolio risk is modeled using the covariance matrix of asset log returns. The covariance matrix captures both individual asset volatility and the relationship between assets. To make the risk estimates comparable on an annual basis, the covariance matrix is annualized using a factor of 252 trading days.

---

### Expected Portfolio Return

Expected portfolio return is computed as the weighted average of the mean historical log returns of individual assets. The resulting value is annualized under the assumption that historical return patterns persist into the future.

This approach reflects a key assumption of Modern Portfolio Theory: historical returns are a proxy for future expectations.

---

### Portfolio Volatility

Portfolio volatility is calculated as the square root of the weighted variance derived from the covariance matrix. This represents the overall risk of the portfolio and accounts for diversification effects among assets.

---

### Sharpe Ratio Optimization

The Sharpe Ratio is used as the optimization objective. It measures risk-adjusted return by comparing excess portfolio return over the risk-free rate relative to portfolio volatility.

Because the optimization function used (`scipy.optimize.minimize`) performs minimization, the negative Sharpe Ratio is defined and minimized to achieve maximization of the original metric.

---

### Optimization Technique

The Sequential Least Squares Quadratic Programming (SLSQP) algorithm is used to solve the constrained optimization problem. This method is well-suited for nonlinear optimization problems with both equality and inequality constraints.

---

### Constraints and Bounds

Several constraints are applied to ensure realistic portfolio construction:

- The sum of all asset weights must equal one
- No short-selling is allowed
- Individual asset weights are bounded between zero and forty percent

These constraints promote diversification and prevent excessive concentration in a single asset.

---

### Visualization

The optimized asset weights are visualized using a bar chart. This provides an intuitive representation of portfolio allocation and helps interpret the results of the optimization process.

![chart Review](https://github.com/ommkunn/Portfolio-Optimization-Using-Modern-Portfolio-Theory-MPT-/blob/main/Optimal%20Portfolio%20Weights%20Bar%20chart.png)

---

## Risk-Free Rate

The risk-free rate represents the theoretical return of an investment with zero risk. In portfolio optimization, it serves as a benchmark for evaluating whether the additional risk taken by a portfolio is adequately compensated by higher returns.

In this project, the risk-free rate is used exclusively in the calculation of the Sharpe Ratio, where it is subtracted from the expected portfolio return to measure excess return per unit of risk.

---

### Role in Sharpe Ratio

The Sharpe Ratio is defined as:

Sharpe Ratio = (Expected Portfolio Return − Risk-Free Rate) / Portfolio Volatility


By incorporating the risk-free rate:
- Portfolio returns are evaluated relative to a minimum acceptable return
- Risk-adjusted performance becomes more meaningful
- Portfolios with higher volatility must generate proportionally higher returns to remain attractive

---

### Implementation in This Project

The code includes an optional implementation to retrieve the risk-free rate using the Federal Reserve Economic Data (FRED) API, typically via short-term U.S. Treasury yields such as the 3-month Treasury Bill.

To keep the project accessible and focused on core learning objectives, the FRED API section is commented out by default. Users can enable it by providing their own API key and uncommenting the relevant section of the code.

If the FRED API is not used, the risk-free rate can be manually defined as a constant value.

---

### Why the Risk-Free Rate Is Optional

For educational purposes, portfolio optimization concepts can be understood without dynamically sourcing the risk-free rate. Keeping this component optional allows learners to focus on return, risk, and optimization mechanics before introducing macroeconomic inputs.

---

## Assumptions

- Historical returns are representative of future performance
- Markets are liquid with no transaction costs
- Assets can be rebalanced without restrictions
- Risk is adequately captured by return variance

---

## Limitations

- Results are sensitive to the historical time period selected
- Covariance estimates may change over time
- The model does not account for transaction costs or taxes
- Risk-free rate assumptions can significantly impact results

---

## Purpose of the Project

The primary purpose of this project is educational. It is designed to help learners understand how portfolio optimization works in practice by combining financial theory with Python-based implementation.

Specifically, the project aims to:

- Translate Modern Portfolio Theory concepts into executable code
- Demonstrate how risk and return interact at the portfolio level
- Illustrate the impact of diversification through covariance
- Introduce constrained optimization techniques used in quantitative finance
- Encourage interpretability through detailed comments and visualization

This project prioritizes clarity and learning over production-level financial modeling and should be viewed as a foundational exploration rather than an investment tool.

## Reproducibility

The methodology is fully reproducible. By adjusting the asset list, time horizon, or constraints, the same framework can be extended to test alternative portfolio configurations.
