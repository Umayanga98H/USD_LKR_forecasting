![Distribution Analysis_Prices and Log Returns](images/02a_distributions.png)
##### Interpretation
LKR price: extremely right-skewed — the 1975-1977 pegged-rate era produces a long flat run near zero, and the 2022 crisis adds an extreme tail.
Gold price: right-skewed across a much wider range now that 50 years of history are included, from the ~$300s in the 1970s-90s up to the >$5,000 levels reached by 2026.
Log returns: LKR returns are now extremely leptokurtic (skew ≈ 53, kurtosis ≈ 4,650) — this is a direct consequence of the 1975-1977 fixed exchange rate period, where daily returns were ~0 for long stretches, combined with the extreme 2022 depreciation tail. This is a much more extreme distribution than the 2000-2022 subset previously examined, and confirms the LKR series contains genuine regime changes that models must account for.
Gold returns: kurtosis ≈ 15.0, skew ≈ -0.29 — still fat-tailed but far closer to typical financial-asset behaviour than the LKR series.

![Daily Log Returns_Volatility Clustering](images/02b_log_returns.png)
##### Interpretation
The LKR panel now clearly shows a flat, near-zero-volatility stretch from 1975-1977 (fixed exchange rate), followed by low but non-zero daily movement after liberalisation, and then the extreme spike in 2022 that dwarfs all prior activity. The gold panel shows volatility clustering around all three major events (1980, 2008, 2020), confirming gold behaves as a continuously-traded asset throughout, in contrast to the LKR's policy-driven quiet periods. This justifies the use of GARCH to capture time-varying volatility, and confirms the 2022 LKR crisis should be treated as a structural break rather than ordinary volatility.

![Rolling Volatility(Annualised Standard Deviation of Log Returns](images/02c_rolling_volatility.png)
##### Interpretation
The 252-day LKR volatility line stays close to zero for almost the entire 1975-2020 period, then rises sharply from 2020 onward, peaking dramatically in 2022 — a structural regime shift not visible in the shorter 2000-2022 window previously examined. Gold maintains consistently higher baseline volatility throughout the full 50-year history, with visible peaks at 1980, 2008, and 2020.

![252-Day Rolling Correlation:USD/LKR Retuurns vs Gold Returns](images/02d_rolling_correlation.png)
##### Interpretation 
With the full 50-year history, the rolling correlation continues to oscillate between positive and negative — confirming the relationship between gold and LKR is NOT static across the entire historical record, not just the 2000-2022 window. A single full-sample correlation figure would be misleading; the relationship is regime-dependent and tends to shift around global stress events, consistent with the safe-haven theory.
