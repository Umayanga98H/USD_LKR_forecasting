## Processed Dataset: usd_lkr_gold_cleaned.csv

This file is the cleaned and merged output of the data cleaning notebook, combining the three raw USD/LKR exchange rate files and the gold price dataset into a single time-indexed table. The two sources were parsed to a consistent date format, sorted chronologically, deduplicated, and joined on matching dates using an inner join, retaining only dates present in both datasets. 

The resulting dataset contains 12,680 rows spanning 2 January 1975 to 16 April 2026, with eight columns: `lkr_close`, `lkr_open`, `lkr_high`, `lkr_low`, `gold_open`, `gold_high`, `gold_low`, and `gold_close`. There are no missing values in the final dataset. This file serves as the foundation for the exploratory data analysis and feature engineering stages of the project.

# USD/LKR Exchange Rate and Gold Price Overview (1975–2026)

![USD/LKR Exchange Rate and Gold Price 1975-2026](images/01_time_series_overview.png)

## Interpretation

### USD/LKR Closing Exchange Rate

From 1975 to 1977, the exchange rate remained almost completely flat at approximately 7–8 LKR per USD, reflecting the fixed/pegged exchange rate policy maintained by the Central Bank of Sri Lanka during this period. The 1977 liberalisation marks the point at which Sri Lanka shifted to a more market-determined exchange rate system, after which the series begins a gradual upward trend rather than remaining flat. From 1977 to approximately 2020, the depreciation of the LKR is steady and largely linear, rising from around 8 to roughly 180 LKR per USD over more than four decades — consistent with typical gradual currency depreciation in a developing economy. The 2022 crisis then produces a near-vertical spike to approximately 360 LKR per USD, by far the most extreme and abrupt movement across the entire 50-year history. Viewed against this longer timeframe, the 2022 crisis represents a genuine structural break rather than ordinary volatility, and should be treated as such during model development and evaluation.

### Gold Closing Price

The 1980 spike is clearly visible, where gold rose sharply toward $800/oz driven by the Iranian Revolution and the Soviet invasion of Afghanistan, before falling back through the 1980s and 1990s. Gold prices remained relatively low and stable (roughly $300–400/oz) throughout the 1990s. The Global Financial Crisis (GFC) of 2008 marks the beginning of a major bull run, with gold rising from approximately $700 to nearly $1,900/oz by 2011–2012, followed by a correction through the mid-2010s. The COVID-19 pandemic triggered a further surge, after which gold continued climbing aggressively into the 2020s, reaching over $5,000/oz by 2026 — roughly six times its 2008 pre-crisis level.

### Combined Interpretation

The period from 2022 onward is the only point in the 50-year history where both series exhibit extreme, simultaneous movement: the LKR collapsing sharply while gold continues its aggressive ascent. Viewed against the full historical record, this co-movement during a period of acute economic stress stands out as unusual relative to the long-run relationship between the two series, providing supporting evidence for the safe-haven hypothesis underpinning the inclusion of gold as a predictive feature in this project.
