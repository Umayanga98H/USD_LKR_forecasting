# A Multi-Stage Hybrid Ensemble Architecture for USD/LKR Exchange Rate Forecasting
 
**MSc Data Science | University of the West of England, Bristol**
**Student:** Hirushani Umayanga 
**Supervisor:** Dr. Alireza Bolhari 
 

 
## Project Overview
 
This project develops and evaluates a multi-stage hybrid ensemble forecasting model for the USD/LKR exchange rate, combining statistical models (ARIMA, ARIMAX, GARCH), deep learning architectures (LSTM, GRU), and gradient boosted trees (XGBoost). Gold spot price is incorporated as a novel exogenous predictive feature, motivated by its well-documented safe-haven relationship with emerging market currencies during periods of financial stress.
 
The model is trained on 50 years of daily USD/LKR OHLC data (1975-2026) and evaluated on the 2022 Sri Lanka economic crisis period, the most extreme structural break in the dataset's history. A formal ablation study quantifies gold's marginal predictive contribution. An interactive five-page Power BI dashboard translates findings into stakeholder-accessible visualisations.
 
## Research Question
 
Can a multi-stage hybrid ensemble model incorporating technical indicators and gold price as an exogenous macroeconomic signal achieve superior USD/LKR forecasting accuracy compared to individual baseline models, and does gold price contribute meaningfully to that accuracy?
 
## Key Results (Test Set 2022–2026)
 
| Model | Type | RMSE | MAE |
|---|---|---|---|
| ARIMA | Individual | 0.007943 | 0.002872 |
| GARCH(1,1) | Individual | 0.007943 | 0.002872 |
| XGBoost | Individual | 0.007960 | 0.002923 |
| ARIMAX | Individual | 0.008019 | 0.003293 |
| **Best 3 Ensemble (ARIMA+ARIMAX+XGB)** | **Ensemble** | **0.008056** | **0.002978** |
| Hybrid Ensemble (weighted) | Ensemble | 0.008395 | 0.003742 |
| Equal weight ensemble | Ensemble | 0.010627 | 0.007134 |
| LSTM | Individual | 0.014709 | 0.008308 |
| GRU | Individual | 0.038416 | 0.032279 |
 
**Ablation Study:** With gold RMSE = 0.008060 | Without gold RMSE = 0.008050
Despite negligible linear difference, 13 of the top 20 XGBoost features are gold-derived — with `gold_bb_width` ranking #1 overall, confirming gold's non-linear predictive contribution.
 
## Repository Structure
 
```
USD_LKR_forecasting/
├── code/
│   ├── Cleaning_Merging.ipynb       # Data cleaning, merging, validity tests
│   ├── EDA.ipynb                    # Exploratory data analysis
│   ├── Feature_engineering.ipynb    # 48 features across 7 categories
│   ├── Model.ipynb                  # ARIMA, ARIMAX, GARCH, LSTM, GRU, XGBoost
│   └── Hybrid_ensemble.ipynb        # Ensemble construction and ablation study
├── data/
│   ├── raw/                         # Original CSV files from Investing.com and Stooq
│   └── processed/
│       ├── usd_lkr_gold_cleaned.csv     # Merged cleaned dataset (12,680 rows × 8 cols)
│       └── usd_lkr_gold_features.csv    # Feature-engineered dataset (12,646 rows × 48 cols)
├── dashboard/
│   ├── README.md                    # Dashboard page descriptions
│   ├── USD_LKR_Forecasting_Dashboard.pbix
│   ├── 01_predictions.csv
│   ├── 02_historical_prices.csv
│   ├── 03_technical_indicators.csv
│   ├── 04_model_results.csv
│   └── 05_ablation_study.csv
├── images/                          # All output plots and charts
└── README.md
```
 

 
## Data Sources
 
| Dataset | Source | Period | Rows |
|---|---|---|---|
| USD/LKR Exchange Rate (OHLC) | [Investing.com](https://uk.investing.com/currencies/usd-lkr-historical-data) | 1975–2026 | 12,819 |
| Gold Spot Price XAUUSD (OHLC) | [Stooq/Barchart](https://stooq.com/q/?s=xauusd) | 1793–2026 | 15,263 |
| **Merged Dataset** | Inner join on Date | **1975–2026** | **12,680** |
 

 
## Feature Engineering
 
48 features engineered across 7 categories from the merged dataset:
 
| Category | Features | Count |
|---|---|---|
| Log returns | lkr_returns, gold_returns | 2 |
| LKR technical indicators | SMA-10/30, EMA-10/30, RSI-14, MACD, Bollinger Bands, ATR-14 | 12 |
| Gold technical indicators | SMA-10/30, RSI-14, MACD, BB width, ATR-14 | 7 |
| Lagged gold features | gold_returns_lag1–5, gold_close_lag1–5 | 10 |
| Rolling volatility | lkr_vol_10/30, gold_vol_10/30 | 4 |
| Calendar features | day_of_week, month, quarter | 3 |
| Raw OHLC (retained) | lkr and gold OHLC columns | 8 |
| Target variables | target_lkr_returns, target_lkr_close | 2 |
| **Total** | | **48** |
 

 
## Train / Validation / Test Split
 
| Split | Period | Rows | Proportion | Key Events |
|---|---|---|---|---|
| Training | 1975–2018 | 10,797 | 85.2% | 1977 liberalisation, 2008 GFC |
| Validation | 2019–2021 | 775 | 6.1% | COVID-19 pandemic |
| Test | 2022–2026 | 1,107 | 8.7% | 2022 Sri Lanka crisis |
 

 
## Model Architecture
 
### Statistical Stage
- **ARIMA(1,1,5)** - univariate baseline, order selected by auto_arima (AIC)
- **ARIMAX(1,1,5)** - gold log returns + lagged gold at lags 3 and 5 as exogenous variables
- **GARCH(1,1)** - fitted on ARIMA residuals; produces confidence intervals
### Deep Learning Stage
- **LSTM / GRU** - 64+32 units, dropout 0.2, Dense(16, ReLU), RMSprop (lr=0.001), 30-day lookback, early stopping patience=10
### Gradient Boosting Stage
- **XGBoost** - 500 trees, max_depth=4, learning_rate=0.05, early stopping=50 rounds
### Hybrid Ensemble
- Inverse-RMSE weighted average of all five models
- Best configuration: ARIMA + ARIMAX + XGBoost (equal weight)

 
## Google Drive
 
All model outputs, saved models, and Power BI data files are available on Google Drive:
 
**[Access Google Drive Project Folder](https://drive.google.com/drive/folders/1e7FaOphmI8WkzkywyxhbbaFPHcPQbe1V?usp=sharing)**
 
Contents:
- `data/processed/` - cleaned and feature-engineered datasets
- `models/` - saved LSTM (`lstm_model.h5`) and GRU (`gru_model.h5`) models
- `outputs/` - all prediction CSVs, model results, and chart images
- `powerbi/` - dashboard CSV files

 
## Tools and Technologies
 
| Tool | Purpose |
|---|---|
| Python 3 / Google Colab | Development environment with free GPU access |
| pandas / NumPy | Data processing and feature engineering |
| ta | Technical indicator computation (OHLC-based) |
| pmdarima | ARIMA/ARIMAX with auto order selection |
| arch | GARCH volatility modelling |
| TensorFlow / Keras | LSTM and GRU implementation |
| XGBoost | Gradient boosted trees |
| scikit-learn | MinMaxScaler and preprocessing |
| Power BI Desktop | Interactive dashboard |
| GitHub | Version control |
 

 
## Data Validity Testing
 
After merging the two datasets, 7 date-based test cases and 9 structural integrity checks were run to confirm the merged file is correct. All 16 tests passed - values match exactly across raw source files and the merged dataset for all test dates spanning 1975 to 2026. Test code is at the end of `code/Cleaning_Merging.ipynb`.
 

 
## How to Run
 
1. Clone the repository:
```bash
git clone https://github.com/Umayanga98H/USD_LKR_forecasting.git
```
 
2. Open notebooks in order in Google Colab:
```
1. Cleaning_Merging.ipynb
2. EDA.ipynb
3. Feature_engineering.ipynb
4. Model.ipynb
5. Hybrid_ensemble.ipynb
```
 
3. Mount Google Drive when prompted and update the file paths to your Drive location.
4. To view the dashboard: download `dashboard/USD_LKR_Forecasting_Dashboard.pbix` and open with [Power BI Desktop](https://powerbi.microsoft.com/desktop) (free, no sign-in required for local viewing).
