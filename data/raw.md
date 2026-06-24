## Raw Data: USD/LKR Historical Exchange Rates

This contains information on raw, unprocessed USD/LKR exchange rate data sourced from Investing.com, split across three CSV files due to the data provider's per-download row limit. 
1. The first file, `USD_to_LKR_Historical_Exchage_Rates_1975_01_02_to_1996_04_15.csv`, covers 2 January 1975 to 15 April 1996 (5,000 rows). 
2. The second file, `USD_to_LKR_Historical_Exchage_Rates_1996_04_16_to_2015_06_26.csv`, continues from 16 April 1996 to 26 June 2015 (5,000 rows).
3. The third file, `USD_to_LKR_Historical_Exchage_Rates_2015_06_29_to_2026_04_16.csv`, covers 29 June 2015 to 16 April 2026 (2,819 rows).
Together the three files span over 50 years of daily exchange rate history, totalling 12,819 rows before cleaning.

Each file contains seven columns: `Date`, `Price` (daily closing rate), `Open`, `High`, `Low`, `Vol.` (trading volume, largely empty across all three files), and `Change %` (daily percentage change). 
The dates are recorded in DD/MM/YYYY format and are stored in reverse chronological order (most recent date first). 
These files are combined, sorted chronologically, and cleaned in the data cleaning notebook before being used for analysis and modelling.


