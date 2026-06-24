## Processed Dataset: usd_lkr_gold_cleaned.csv

This file is the cleaned and merged output of the data cleaning notebook, combining the three raw USD/LKR exchange rate files and the gold price dataset into a single time-indexed table. The two sources were parsed to a consistent date format, sorted chronologically, deduplicated, and joined on matching dates using an inner join, retaining only dates present in both datasets. 

The resulting dataset contains 12,680 rows spanning 2 January 1975 to 16 April 2026, with eight columns: `lkr_close`, `lkr_open`, `lkr_high`, `lkr_low`, `gold_open`, `gold_high`, `gold_low`, and `gold_close`. There are no missing values in the final dataset. This file serves as the foundation for the exploratory data analysis and feature engineering stages of the project.
