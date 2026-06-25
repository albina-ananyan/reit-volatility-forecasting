# REIT Return & Volatility Forecasting

Empirical analysis of REIT return predictability and financial volatility 
modeling, completed as part of MGTF 404 (Financial Econometrics) at UC San 
Diego's Rady School of Management.

## Overview

This project covers two empirical exercises in financial econometrics:

**Part 1 — Forecasting REIT Returns**  
Using monthly FTSE/NAREIT data (1972–2020), we examine whether REIT returns 
are predictable by their own lags (AR models) or by the dividend yield. We 
test for return persistence, apply Newey-West HAC standard error corrections 
for autocorrelated regressors, and generate out-of-sample forecasts for 
late 2017/early 2018. Subsample analysis covers 1972–1993 and 1994–2014.

**Part 2 — Volatility Forecasting**  
Using daily and monthly data for the S&P 500, Euro/USD exchange rate, and 
NYSE Oil & Gas index (2000–2014), we estimate ARCH and GARCH models to 
characterize volatility clustering and persistence. We compare model fit 
using likelihood ratio tests and benchmark model-implied volatility against 
realized volatility.

## Repository Structure

```
├── data/
│   ├── reit_data_2020.xls          # FTSE/NAREIT monthly REIT index data
│   └── vol_data_homework.xlsx      # S&P 500, Euro/USD, NYSE Oil & Gas daily prices
├── figures/
│    ├── garch11_daily_EuroUSD.png
│    ├── garch11_daily_OilGas.png
│    ├── garch11_daily_SP500.png
│    ├── garch11_monthly_EuroUSD.png
│    ├── garch11_monthly_OilGas.png
│    ├── garch11_monthly_SP500.png
│    └── realized_volatility.png
├── reit_volatility_forecasting.ipynb
└── README.md
```

## Key Methods

- AR(1), AR(2), AR(12) models on simple and log REIT returns
- Ljung-Box test and Wald test for return persistence
- Predictive regressions of returns on dividend yield (DY and smoothed DY)
- Newey-West HAC standard errors for persistent regressors
- Expanding-window out-of-sample forecasting
- ARCH(1), ARCH(3), ARCH(12) estimated via MLE
- GARCH(1,1) and GARCH(2,2) with likelihood ratio model comparison
- Realized volatility computed from daily squared returns

## Requirements

```bash
pip install pandas numpy scipy statsmodels matplotlib seaborn arch xlrd openpyxl
```

Developed with Python 3.13. All code is in a single Jupyter notebook.

## Data Sources

- **REIT data**: [FTSE/NAREIT](https://www.reit.com/data-research/reit-indexes/annual-index-values-returns)  
- **Volatility data**: Provided via course materials (UC San Diego MGTF 404)

## Results Summary

**REIT Return Predictability**  
Monthly REIT returns show minimal autocorrelation — AR(1) and AR(2) 
coefficients are small and statistically insignificant. The smoothed 
dividend yield (DY_s) provides slightly more predictive power than the 
raw yield, though R² remains below 0.3% in all specifications. Newey-West 
correction meaningfully widens standard errors for the raw DY regression 
(~38% increase) due to the near-unit-root persistence of dividend yields.

**Volatility Persistence**  
ARCH effects are strongly present in all three daily return series 
(LM test p ≈ 0.000). GARCH(1,1) substantially outperforms ARCH(1) across 
all assets. Volatility persistence (α + β) ranges from 0.989 to 0.998, 
implying shock half-lives of 61 days (S&P 500) to 281 days (Euro/USD). 
At monthly frequency, persistence weakens and GARCH(1,1) is generally 
sufficient over GARCH(2,2).
