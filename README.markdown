# VaR and CVaR Calculation using Monte Carlo Simulations

This repository provides implementations and analyses of Value at Risk (VaR) and Conditional Value at Risk (CVaR) for a portfolio of stocks, specifically Apple (AAPL) and Google (GOOG), using Monte Carlo simulations and some statistical methods like GARCH to estimate volatility. It is designed for educational purposes, offering both theoretical insights and practical code to explore financial risk management techniques.

## Files in the Repository

1. **VaR.pdf**  
   A comprehensive document detailing the theoretical background of VaR calculation methods, including:
   - **Monte Carlo VaR**: Simulates portfolio returns to estimate potential losses.
   - **Parametric VaR**: Uses mean and covariance of returns, assuming a normal distribution.
   - **GARCH VaR**: Models time-varying volatility using the GARCH(1,1) model.
   - **EWMA VaR**: Applies an exponentially weighted moving average to prioritize recent data.
   - **Backtesting**: Techniques like the Kupiec Proportion of Failures (POF) Test to validate VaR models.  
   Note: The document focuses on VaR and does not cover CVaR explicitly.

2. **VaR_and_CVaR_Monte_Carlo_Simulation.ipynb**  
   A Jupyter notebook that implements Monte Carlo simulations to estimate VaR and CVaR for a portfolio of AAPL and GOOG stocks. Key features include:
   - Fetching historical data from January 1, 2022, using `yfinance` and OpenBB.
   - Simulating portfolio returns with 1000 simulations, incorporating historical volatility and correlations via Cholesky decomposition.
   - Calculating VaR (5th percentile of simulated portfolio values) and CVaR (average of values below VaR).
   - Visualizing simulated portfolio paths with VaR and CVaR thresholds.

3. **VaR.ipynb**  
   A Jupyter notebook comparing four VaR estimation methods (Monte Carlo, Parametric, EWMA, and GARCH) for the same portfolio, using data from January 1, 2014, to November 22, 2024. It includes:
   - Backtesting over a 252-day rolling window to assess model performance.
   - Statistical tests (Binomial and Kupiec) to evaluate VaR accuracy.
   - Volatility modeling and visualization using GARCH, EGARCH, and GJR-GARCH models compared to realized volatility.

Output Files: "Price Paths.png", "Historical Returns.csv" & "Kupiec Backtesting VAR.xlsx"

## Dependencies

To run the Jupyter notebooks, install the following Python libraries:

- `numpy`: For numerical computations.
- `pandas`: For data manipulation and analysis.
- `matplotlib`: For plotting and visualization.
- `yfinance`: For fetching historical stock data.
- `arch`: For GARCH modeling.
- `scipy`: For statistical functions.

Install them using pip:

```bash
pip install numpy pandas matplotlib yfinance arch scipy
```

Additionally, ensure you have Jupyter Notebook or JupyterLab installed to run the notebooks.

## How to Use

1. **Clone the Repository**:
   ```bash
   git clone https://github.com/uday-andotra/VaR-MC-GARCH.git
   cd VaR-MC-GARCH
   ```

2. **Set Up the Environment**:
   Install the required libraries as listed above.

3. **Run the Notebooks**:
   - Open Jupyter Notebook or JupyterLab.
   - Navigate to the repository folder and open `VaR_and_CVaR_Monte_Carlo_Simulation.ipynb` or `VaR.ipynb`.
   - Execute the cells sequentially to fetch data, run simulations, and view results.

4. **Review Theoretical Background**:
   Read `VaR.pdf` for a detailed understanding of VaR concepts and methods before running the notebooks.

## Key Findings

### Monte Carlo Simulation (`VaR_and_CVaR_Monte_Carlo_Simulation.ipynb`)
- **Data**: Historical stock data for AAPL and GOOG from January 1, 2022.
- **Methodology**: Uses Monte Carlo simulations (1000 iterations) with Cholesky decomposition to maintain historical correlations. VaR is calculated as the 5th percentile of simulated portfolio values, and CVaR as the average of values below this threshold.
- **Results**: Specific VaR and CVaR values are computed (e.g., VaR of approximately $59,283.67 for the final day at 5% confidence level). Historical volatility is incorporated to enhance realism.
- **Backtesting**: The Kupiec POF Test rejects the VaR model (p-value = 0.0), suggesting potential miscalibration, possibly due to assumptions like constant volatility.

### Comparison of VaR Methods (`VaR.ipynb`)
- **Data**: Historical data for AAPL and GOOG from January 1, 2014, to November 22, 2024.
- **VaR Estimates** (at 5% confidence level):
  | Method         | VaR Estimate  | Failure Rate (%) |
  |----------------|---------------|------------------|
  | Monte Carlo    | -0.023015     | 5.75%            |
  | Parametric     | -0.024840     | 6.11%            |
  | EWMA           | -0.019636     | 5.39%            |
  | GARCH          | -0.021841     | 5.27%            |
- **Backtesting**: Conducted over 2740 observations with a 252-day rolling window. Failure rates indicate how often actual losses exceeded VaR estimates.
- **Statistical Tests**:
  - **Binomial Test**: Parametric VaR has a low p-value (0.0109), suggesting it’s less accurate. GARCH (p=0.5393) and EWMA (p=0.3347) perform better.
  - **Kupiec Test**: Similar results, with Parametric VaR rejected (p=0.0099), while GARCH (p=0.5275) and EWMA (p=0.3598) are more reliable.
- **Volatility Modeling**: GARCH, EGARCH, and GJR-GARCH models closely track realized volatility, with GARCH providing prominent estimates.

### Conclusions
- **Monte Carlo Simulations**: Effective for modeling complex portfolios but may require enhancements like incorporating drift to improve accuracy.
- **Method Comparison**: GARCH and EWMA methods outperform Parametric VaR in backtesting, as their failure rates are closer to the expected 5% and have higher p-values in statistical tests.
- **Practical Use**: The repository is ideal for learning about risk management, offering both code and theory to understand VaR and CVaR calculations.

## Purpose and Applications

This repository serves as an educational tool for:
- Understanding VaR and CVaR concepts and their implementation in Python.
- Comparing different VaR estimation methods and their strengths/weaknesses.
- Learning backtesting and statistical validation techniques for risk models.
- Exploring volatility modeling with GARCH and related methods.

It is suitable for students, researchers, or finance professionals interested in risk management.

## Future Enhancements

- **Incorporate Drift**: Add drift to Monte Carlo simulations for more realistic price path modeling.
- **Portfolio Diversification**: Test diversified vs. undiversified portfolios to study risk reduction.
- **Advanced Volatility Models**: Further explore EGARCH and GJR-GARCH for improved volatility estimates.
- **Extended Data**: Use more recent or diverse datasets to validate findings across different market conditions.
