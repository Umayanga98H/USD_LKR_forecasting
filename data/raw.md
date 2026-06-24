## Raw Data: USD/LKR Historical Exchange Rates

This contains information on raw, unprocessed USD/LKR exchange rate data sourced from [Investing.com](https://www.investing.com/currencies/usd-lkr-historical-data), split across three CSV files due to the data provider's per-download row limit. 
1. `USD to LKR Historical Exchage Rates 1975_01_02 to 1996_04_15.csv`, covers 2 January 1975 to 15 April 1996 (5,000 rows). 
2. `USD to LKR Historical Exchage Rates 1996_04_16 to 2015_06_26.csv`, continues from 16 April 1996 to 26 June 2015 (5,000 rows).
3. `USD to LKR Historical Exchage Rates 2015_06_29 to 2026_04_16.csv`, covers 29 June 2015 to 16 April 2026 (2,819 rows).
Together the three files span over 50 years of daily exchange rate history, totalling 12,819 rows before cleaning.

Each file contains seven columns: `Date`, `Price` (daily closing rate), `Open`, `High`, `Low`, `Vol.` (trading volume, largely empty across all three files), and `Change %` (daily percentage change). 
The dates are recorded in DD/MM/YYYY format and are stored in reverse chronological order (most recent date first). 
These files are combined, sorted chronologically, and cleaned in the data cleaning notebook before being used for analysis and modelling.

## Raw Data: Gold Price (XAUUSD)

This dataset contains historical daily gold spot prices in US Dollars per troy ounce, sourced from [Stooq](https://stooq.com/q/?s=xauusd) (`Gold Rates from 1793_03_01 to 2026_06_09.csv`), with commodity pricing data underlying the platform provided by Barchart, a recognised market data provider. The file spans an extensive historical range from 1 March 1793 to 9 June 2026, totalling 15,263 rows; however, observations prior to 1971 reflect the fixed gold standard era, where prices were set by government policy rather than determined by open market trading, and are therefore not representative of free-floating market prices. For the purposes of this project, only the subset of data overlapping with the USD/LKR exchange rate dataset and reflecting genuine market-determined pricing (from 2 January 1975 to 16 April 2026) is used.

Each row contains four columns: `Date`, `Open`, `High`, and `Close`, alongside `Low`, representing the daily price range. 
No missing values are present in the dataset. 
This raw file is filtered, cleaned, and merged with the USD/LKR dataset in the data cleaning notebook to form the final analytical dataset used for feature engineering and modelling.


