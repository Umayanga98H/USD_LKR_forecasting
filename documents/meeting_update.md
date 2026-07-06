1. Dataset updated and expanded
Switched from the Kaggle gold dataset (2000–2022) to the Stooq/Barchart source, giving a full overlap with the USD/LKR data from 1975 to 2026. The merged dataset now contains 12,679 observations — more than double the previous 5,700 rows.
2. Both price series are non-stationary — confirmed
ADF tests confirm both raw price series have a unit root (p ≈ 1.0 for gold, p = 0.97 for LKR). Log returns are stationary for both (p ≈ 0.00). All models will be trained on log returns, and ARIMA will use d=1 differencing.
3. The LKR distribution shows clear regime changes
LKR returns are extremely leptokurtic (skew ≈ 53, kurtosis ≈ 4,650) — driven by the 1975–1977 fixed exchange rate period and the 2022 crisis. This confirms the series contains genuine structural breaks that the models must account for.
4. Volatility clustering confirmed in both series
Both series exhibit clear volatility clustering — large moves cluster together. This directly justifies the inclusion of GARCH for time-varying volatility modelling in the hybrid architecture.
5. No significant linear relationship between gold and LKR returns
Spearman correlation on log returns is r = −0.014 (p = 0.11) — not significant. Granger causality is not significant at any lag from 1 to 5 across the full 50-year history.
6. Key finding — the relationship is crisis-dependent, not constant
The earlier marginal Granger significance at lags 3–5 (observed in the 2000–2022 subset) disappears when tested over the full history. This suggests gold's predictive relationship with LKR intensifies specifically during global stress events (1980, 2008, 2020, 2022) rather than being a stable everyday effect. The rolling correlation plot clearly shows this — the correlation oscillates between positive and negative and spikes during crises.
7. This strengthens the case for the hybrid model
A simple linear model would fail to capture this crisis-dependent, regime-switching relationship. The findings directly justify the LSTM/GRU/XGBoost architecture — these models can learn non-linear, time-varying patterns that a linear Granger test or ARIMA alone cannot detect.
