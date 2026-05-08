# 📈 Portfolio Optimisation using CAPM & Linear Regression

![Python](https://img.shields.io/badge/Python-3.8+-3776AB?style=for-the-badge&logo=python&logoColor=white)
![Jupyter](https://img.shields.io/badge/Jupyter-Notebook-F37626?style=for-the-badge&logo=jupyter&logoColor=white)
![NumPy](https://img.shields.io/badge/NumPy-013243?style=for-the-badge&logo=numpy&logoColor=white)
![pandas](https://img.shields.io/badge/pandas-150458?style=for-the-badge&logo=pandas&logoColor=white)
![Status](https://img.shields.io/badge/status-complete-brightgreen?style=for-the-badge)

> Applies the **Capital Asset Pricing Model (CAPM)** and **linear regression** to optimise a portfolio of 10 major US equities — minimising risk for a target return using quadratic programming and the Efficient Frontier.

---

## 🗂️ Project Structure

```
portfolio-optimisation/
│
├── portfolio_optimisation.ipynb   # Main Jupyter notebook
├── requirements.txt               # Python dependencies
└── README.md
```

---

## 📊 Assets Covered

| # | Ticker | Company | Sector |
|---|--------|---------|--------|
| 1 | AAPL | Apple Inc. | Technology |
| 2 | MSFT | Microsoft Corp. | Technology |
| 3 | GOOGL | Alphabet Inc. | Technology |
| 4 | AMZN | Amazon.com Inc. | Consumer Discretionary |
| 5 | TSLA | Tesla Inc. | Automotive / Energy |
| 6 | META | Meta Platforms | Communication |
| 7 | NFLX | Netflix Inc. | Communication |
| 8 | NVDA | NVIDIA Corp. | Semiconductors |
| 9 | JPM | JPMorgan Chase | Financials |
| 10 | V | Visa Inc. | Financials |

> 📅 Data sourced from **Yahoo Finance** — 5-year period: **Jan 2019 – Dec 2023**
> Benchmark: **S&P 500 (^GSPC)**

---

## ⚙️ Methodology

```
Raw Price Data → Daily Returns → CAPM Regression → Covariance Matrix → QP Optimisation → Efficient Frontier
```

| Step | Method | Tool |
|------|--------|------|
| 1. Data Collection | Download historical closing prices | `yfinance` |
| 2. Daily Returns | Percentage change on closing prices | `pandas.pct_change()` |
| 3. CAPM Regression | Estimate α (alpha) and β (beta) per asset | `scipy.stats.linregress` |
| 4. Expected Returns | CAPM formula: `μi = Rf + βi(E[Rm] − Rf)` | `numpy` |
| 5. Covariance Matrix | Systematic + idiosyncratic risk per asset pair | `numpy` |
| 6. Portfolio Optimisation | Minimise risk subject to constraints | `gurobipy` (Gurobi QP) |
| 7. Efficient Frontier | 10 evenly spaced target returns plotted | `matplotlib` |

### CAPM Formula

```
Ri − Rf = αi + βi(Rm − Rf) + εi
```

| Symbol | Meaning |
|--------|---------|
| `Ri` | Asset return |
| `Rf` | Risk-free rate (2% p.a. → daily: `/252`) |
| `Rm` | Market return (S&P 500) |
| `αi` | Excess return (intercept) |
| `βi` | Systematic risk (slope) |
| `εi` | Error term |

---

## 📈 Key Results

### CAPM Regression Summary

| Asset | Alpha | Beta | Expected Return | Idiosyncratic Risk |
|-------|------:|-----:|----------------:|-------------------:|
| AAPL  | 1.2156 | 0.000786 | 0.000080 | 0.000412 |
| MSFT  | 1.1821 | 0.000574 | 0.000080 | 0.000369 |
| GOOGL | 1.1354 | 0.000304 | 0.000080 | 0.000401 |
| AMZN  | 1.0658 | 0.000151 | 0.000079 | 0.000492 |
| TSLA  | 1.5033 | 0.001946 | 0.000080 | 0.001660 |
| META  | 1.2887 | 0.000395 | 0.000080 | 0.000755 |
| NFLX  | 1.0422 | 0.000291 | 0.000080 | 0.000846 |
| **NVDA**  | **1.7288** | **0.001684** | **0.000080** | **0.001063** |
| JPM   | 1.0986 | 0.000097 | 0.000079 | 0.000403 |
| V     | 1.0488 | 0.000091 | 0.000079 | 0.000312 |

> 🏆 **NVDA** has the highest alpha (1.73) — greatest excess returns
> ⚡ **TSLA** has the highest beta (0.00195) — most sensitive to market movements
> 🛡️ **V** and **JPM** have the lowest beta and idiosyncratic risk — most stable assets

---

### 🎯 Optimal Portfolio Weights

| Asset | Weight | Allocation |
|-------|-------:|-----------|
| AAPL  | 23.97% | ████████████ |
| NVDA  | 21.09% | ██████████ |
| MSFT  | 18.78% | █████████ |
| TSLA  | 15.70% | ███████ |
| GOOGL |  7.84% | ████ |
| META  |  5.85% | ███ |
| NFLX  |  3.51% | █ |
| AMZN  |  2.07% | █ |
| JPM   |  0.64% | ▌ |
| V     |  0.55% | ▌ |

> 📌 **Expected Portfolio Return:** `0.000080`
> 📌 **Portfolio Risk (Std Dev):** `0.011453`
> 📌 AAPL + NVDA combined make up ~**45%** of the portfolio

---

### 🔒 Optimisation Constraints

| Constraint | Rule |
|------------|------|
| Full capital allocation | `Σ weights = 1` |
| No short selling | `weight ≥ 0` for all assets |
| Target return | `Σ (weight × expected return) = target` |

---

## 📦 Requirements

| Library | Version | Purpose |
|---------|---------|---------|
| `pandas` | ≥1.5.0 | Data handling and returns |
| `numpy` | ≥1.23.0 | Matrix operations |
| `scipy` | ≥1.9.0 | Linear regression |
| `yfinance` | ≥0.2.0 | Stock data download |
| `matplotlib` | ≥3.6.0 | Efficient frontier plot |
| `statsmodels` | ≥0.13.0 | Statistical modelling |
| `scikit-learn` | ≥1.1.0 | Regression visualisation |
| `gurobipy` | ≥10.0.0 | Quadratic programming |
| `jupyter` | ≥1.0.0 | Notebook environment |

---

## 🚀 How to Run

```bash
# 1. Clone the repository
git clone https://github.com/your-username/portfolio-optimisation.git
cd portfolio-optimisation

# 2. Install dependencies
pip install -r requirements.txt

# 3. Launch the notebook
jupyter notebook portfolio_optimisation.ipynb
```

> ⚠️ **Note:** Gurobi requires a licence. A free academic licence is available at [gurobi.com](https://www.gurobi.com/academia/academic-program-and-licenses/).

---

## 📚 References

- Markowitz, H. (1952). Portfolio Selection. *Journal of Finance*
- Sharpe, W. F. (1964). Capital Asset Prices. *Journal of Finance*
- [Yahoo Finance](https://finance.yahoo.com) — historical price data
- [Gurobi Optimisation](https://www.gurobi.com) — quadratic programming solver
