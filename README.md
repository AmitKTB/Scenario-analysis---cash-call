# Scenario-analysis---cash-call
Portfolio construciton based on cash call and its Back-test
# Portfolio Construction and Backtesting Workflow

This repository contains a series of Jupyter notebooks for constructing and backtesting a quantitative portfolio strategy. Below is an overview of each notebook and its role in the workflow:

---

## 1. **Base Portfolio Construction**
### File: `Base_Portfolio.ipynb`
- **Input File**: `Portfolio Changes Table 2018-21.csv`
  - Contains `BUY` and `SELL` signals for securities on a quarterly basis.
- **Objective**:
  - Process the input file to generate a list of securities to `BUY` or `HOLD` at the start of each quarter.
  - Securities marked as `SELL` are excluded from the portfolio for the respective quarter.
- **Output File**: `qtr_portfolio_18_21.csv`
  - Represents the base portfolio, listing securities to `BUY` or `HOLD` for each quarter.

---

## 2. **Data Compilation**
### File: `Data_Compilation.ipynb`
- **Input Files**:
  - `NSE_200_list.csv`: Contains:
    - Security Name
    - ISIN
    - Sector
    - Flag indicating whether data has been fetched from Bloomberg.
  - `Price_17_24.csv`: Historical price data for securities.
- **Objective**:
  - Calculate momentum for each security based on historical prices.
  - Save the processed momentum data for future use.
- **Output File**: `momentum_data.parquet`
  - Contains momentum values and other relevant data for all securities.

---

## 3. **Portfolio Construction**
### File: `Port_Const.ipynb`
- **Input Files**:
  - `momentum_data.parquet` (from Notebook 2)
  - `qtr_portfolio_18_21.csv` (from Notebook 1)
- **Objective**:
  - Add weekly evaluation dates to the base portfolio.
  - Enrich the portfolio with additional data (e.g., momentum decile) fetched from the `momentum_data.parquet` file.
  - Apply inclusion and exclusion rules to filter securities and construct the final portfolio.
    - Example Rule: Portfolio is evaluated based on 6-month momentum with the 4th decile as the threshold for inclusion.
  - Rules are detailed at the end of the notebook.
- **Output File**: `final_portfolio.csv`
  - Represents the final portfolio after applying all criteria.

---

## 4. **Backtesting**
### File: `backtest.ipynb`
- **Input Files**:
  - `Raw_data.xlsx`: Contains price data fetched from Bloomberg.
  - `final_portfolio.csv` (from Notebook 3)
- **Objective**:
  - Calculate daily returns for each security using price data.
  - Conduct backtesting based on the final portfolio and compute performance metrics.
  - Save results for further analysis.
- **Output File**: `backtest_results.csv`
  - Contains backtest results, including performance metrics and levels data.

---

