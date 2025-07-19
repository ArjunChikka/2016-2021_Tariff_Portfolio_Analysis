[![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/ArjunChikka/2016-2021_Tariff_Portfolio_Analysis/blob/main/Tariffs_Writeup_Extensive.ipynb)

# Tariff Portfolio Analysis

## Executive Summary
This case study investigates the sensitivity and robustness of U.S. equity portfolios to the 2018–2019 U.S.–China tariff escalation. We divide 2016–2021 into three regimes—Pre-Tariff (2016–2017), Tariff Escalation (2018–2019), and Post-Tariff Recovery (2020–2021)—and optimize a 35-stock portfolio via annualized Sharpe-ratio maximization under full-investment, no-shorting constraints. Each regime’s optimal weights are then backtested across all periods to evaluate out-of-sample resilience. We find that portfolios trained in high-volatility regimes deliver superior cross-regime stability, while those trained in tranquil regimes suffer drawdowns when conditions shift. Our results underscore the value of regime-aware portfolio design for risk mitigation under structural policy shocks.

## Data Acquisition
- **Source:** Daily close prices for 35 large-cap U.S. equities (across Technology, Consumer, Healthcare, Industrials, Energy sectors).
- **Period:** January 1, 2016 – December 31, 2021.
- **Tool:** `yfinance` API to download data and compute daily returns (`pct_change()`).

## Regime Segmentation
- **Pre-Tariff (2016–2017):** Steady growth, low trade tensions.
- **Tariff Escalation (2018–2019):** Rapid volatility spikes amid U.S.–China tariff announcements.
- **Post-Tariff Recovery (2020–2021):** COVID shocks, market stabilization, and recovery.
- Returns are partitioned by date ranges to isolate policy-driven regime effects.

## Portfolio Optimization
We solve for each regime:
<p align="center">
  <img
    src="https://latex.codecogs.com/png.latex?
      \max_{w\ge0,\;\mathbf{1}^\top w=1}
      \frac{w^\top\mu - r_f}{\sqrt{w^\top\Sigma\,w}}
    "
    alt="Sharpe-ratio optimization"
  />
</p>
where $\mu$ and $\Sigma$ are the annualized mean and covariance of regime returns, and $r_f=2\%$. Optimization uses SciPy’s `minimize` on the negative Sharpe ratio.

## Backtesting Framework
1. **Portfolios:** Weights from each regime’s in-sample optimization.  
2. **Test:** Apply each weight vector to all three regimes (in-sample + two out-of-sample).  
3. **Metrics:**  
   - Cumulative growth (growth-of-\$1)  
   - Daily returns sampled on five evenly spaced dates  
   - Total return, annualized return, and annualized volatility tabulated in 3×3 matrices.

## Performance Comparison Across Tariff Regimes
- **Total Return (3×3):** End-of-period wealth for each train/test pairing.  
- **Annual Return & Volatility (3×3):** Mean and standard deviation of daily returns, scaled to 252 trading days.  
- **Normalized Performance Grid:** Bar charts rescaling return, volatility, and Sharpe to [0,1] in each test regime.  
- **Sharpe Ratio Heatmap:** 3×3 matrix highlighting in-sample (diagonal) and out-of-sample (off-diagonal) Sharpe values.

## Conclusion & Visual Insights
### 1. Sharpe-Ratio Heatmap: Consistency vs. Over-Fit
- Diagonal (in-sample) peaks confirm home-court advantage.  
- Only the Tariff-trained portfolio sustains Sharpe >1.0 across all regimes.

### 2. Normalized Performance Grid: Trade-Off Profiles
- **Pre-Tariff test:** Pre-trained leads return and Sharpe, but low volatility buffer.  
- **During-Tariff test:** Tariff-trained dominates on all metrics under stress.  
- **Post-Tariff test:** Post-trained yields highest return at cost of higher volatility.

### 3. Cumulative-Returns Curves: Growth & Drawdowns
- **Pre-Tariff strategy** excels early but underperforms in escalation.  
- **Tariff-Escalation strategy** delivers smooth, steady growth across regimes.  
- **Post-Tariff strategy** surges in recovery but lags during stress.

### 4. Key Takeaways & Recommendations
- **Stress-Period Calibration:** Builds a “volatility buffer,” enhancing resilience.  
- **Calm-Period Training:** May over-fit and suffer when shock arrives.  
- **Regime Segmentation:** Essential for robust, adaptive portfolio design under policy shocks.

## Repository Structure
```text
2016-2021_Tariff_Portfolio_Analysis/
├── Tariffs_Writeup_Extensive.ipynb
├── requirements.txt
├── README.md
└── LICENSE
```

## Setup & Usage
1. **Clone**  
```bash
git clone https://github.com/ArjunChikka/2016-2021_Tariff_Portfolio_Analysis.git
cd 2016-2021_Tariff_Portfolio_Analysis
   ```
2. **Env & Install**
  ```bash
  python -m venv env
  source env/bin/activate      # or `env\Scripts\activate` on Windows
  pip install -r requirements.txt
  ```
3. Launch Notebook
  ```bash
  jupyter notebook notebooks/Tariffs_Writeup_Extensive.ipynb
  ```


