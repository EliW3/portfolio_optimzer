# Modern Portfolio Theory (MPT) Efficient Frontier Optimizer

A quantitative finance tool that applies **Markowitz Modern Portfolio Theory (MPT)** to identify optimal asset allocations. By running thousands of Monte Carlo asset-weight combinations, the script computes annualized log returns, asset covariances, and risk-adjusted metrics to plot the **Efficient Frontier** and isolate optimal investment allocations based on user-selected criteria.

## Core Features

*   **Efficient Frontier Simulation:** Evaluates thousands of randomized asset allocations to construct an empirical risk-vs-reward Efficient Frontier.
*   **Dirichlet Weight Normalization:** Utilizes a **Dirichlet distribution** (`np.random.dirichlet`) to guarantee all generated portfolio weight vectors naturally sum to exactly `1.0` (100%), removing iterative filtering overhead.
*   **Multi-Metric Optimization Targets:** Allows immediate optimization targeting for three foundational quantitative frameworks: Maximum Sharpe Ratio, Minimum Volatility, or Maximum Expected Return.
*   **Capital Market Line (CML) Overlay:** Automatically derives and plots the risk-free rate vector tangency path directly through the maximum Sharpe ratio node when optimizing for risk-adjusted returns.
*   **Advanced Visual Scatter Mapping:** Generates a custom `matplotlib` scatter map color-coded by Sharpe ratio tiering, explicitly marking your target "Optimal Portfolio" with a distinctive red anchor point.

## Getting Started

### Prerequisites

Ensure you have the required analytical, modeling, and graphing libraries installed:

```bash
pip install numpy pandas yfinance matplotlib
```

### Usage Example

```python
from datetime import datetime
# Import or paste the function here

# Optimize a 3-stock portfolio targeting the lowest possible volatility
portfolio_optimizer(
    stocks=["AAPL", "GOOGL", "MSFT"],
    risk_free_rate=0.04,
    metric_to_optimize="min_volatility",
    portfolios_simulated=20000
)
```

## Function Arguments & Parameters

| Parameter | Type | Default | Description |
| :--- | :--- | :--- | :--- |
| `stocks` | `list` | `["AAPL", "GOOGL", "MSFT"]` | Array of yFinance asset ticker symbols to include in the optimizer universe. |
| `risk_free_rate` | `float` | `0.04` | The annualized benchmark risk-free percentage rate (expressed as a decimal, e.g., `0.04` = 4%). |
| `start` | `str` | `'2010-01-01'` | The historical boundary start date (`YYYY-MM-DD`) used to calculate variance and drift. |
| `end` | `str` | *Dynamic (Today)* | The historical boundary end date. Defaults to the current active calendar date. |
| `metric_to_optimize` | `str` | `'sharpe_ratio'` | The target framework to isolate. Options: `'sharpe_ratio'`, `'min_volatility'`, `'max_return'`. |
| `portfolios_simulated` | `int` | `10000` | The total number of randomized asset allocation combinations to evaluate. |

## Terminal Outputs & Visuals Explained

When executed, the script processes your financial data matrix and logs the precise weight allocation for each stock asset matching your desired configuration target:

*   **Optimal Portfolio Weights:** Prints a clean terminal breakdown of the individual asset percentages required to replicate the target portfolio (e.g., `AAPL: 42.15%`).
*   **Efficient Frontier Scatter Plot:** Displays a multi-colored scatter landscape mapping portfolio risk (Volatility) on the X-axis against portfolio reward (Expected Return) on the Y-axis. 
*   **Color-Mapped Sharpe Ratio:** Variations in the scatter dots change color density based on their underlying Sharpe quality value, providing an intuitive view of risk-efficiency tiers.
*   **Red Target Marker (X):** Explicitly anchors on top of the unique configuration row that maximized or minimized your designated `metric_to_optimize`.
