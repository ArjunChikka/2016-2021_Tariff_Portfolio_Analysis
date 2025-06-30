# Tariff Portfolio Analysis

## Project Overview
This repository contains a Jupyter notebook that analyzes the impact of the 2018–2019 U.S.–China tariff escalation on sector ETF portfolio optimization. We segment the period 2016–2021 into three regimes—Pre-Tariff, Tariff Escalation, and Post-Tariff Recovery—derive optimal portfolios for each via Sharpe-ratio maximization, and evaluate cross-regime performance.

## Repository Structure
```
tariff_portfolio_analysis/
├── README.md
├── requirements.txt
├── Portfolio_Writeup.ipynb
├── images/
│   ├── regime_weights.png
│   └── normalized_performance.png
└── LICENSE
```

## Setup & Usage
1. Clone the repository:
   ```bash
   git clone <repo-url>
   cd tariff_portfolio_analysis
   ```
2. (Optional) Create a virtual environment:
   ```bash
   python -m venv env
   source env/bin/activate  # on Windows: env\Scripts\activate
   ```
3. Install dependencies:
   ```bash
   pip install -r requirements.txt
   ```
4. Launch Jupyter:
   ```bash
   jupyter notebook Portfolio_Writeup.ipynb
   ```

## Results
- **Figure 3**: Optimal sector weights by regime.
- **Figure 4**: Normalized cross-regime performance metrics (Return, Volatility, Sharpe).

## License
This project is released under the MIT License.

## Acknowledgments
Built with Python, yfinance, Pandas, NumPy, SciPy, Seaborn, and Matplotlib.
