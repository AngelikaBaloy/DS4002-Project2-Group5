# Conclusion 

This study used IAD departure data across United Airlines, Delta Airlines, and American Airlines from 2024 to forecast 2025 daily flight delay rates.
EDA revealed that United airlines is overrepresented in this data, holding the vast majority of flights. EDA also revealed seasonal patterns in delays, 
with more frequent delay rates in the summer and holiday months. 

Before analyses were run, we checked the data for stationarity, and it was borderline non-stationary (p > .05). We differenced the data to accommodate this. 

## Model results:

We compared the performance of a plain ARIMA model with a seasonal SARIMA model that added weekly seasonality, yearly Fourier terms, and a log transform.
We also looked at average daily delay (in minutes) and built a similar pair of models to forecast that because we were interested in if a higher accuracy
could be achieved. 

Plain ARIMA performed no better than predicting the 2024 average every day: its 2025 forecast flattened to a constant, giving an MAE of 9.27 minutes for 
average departure delay (in minutes) and 7.88 percentage points for the share of flights delayed 15+ minutes. SARIMA was the most accurate model for both targets. 
It lowered MAE to 7.86 minutes, a 15% reduction, and to 7.24 percentage points, an 8% reduction, and its forecasts followed the seasonal pattern of low delays 
in fall and winter and peak delays in July and August. RMSE improved less than MAE (14.21 to 13.45 for average delay and 10.77 to 10.39 for delay rate), showing
that SARIMA predicts typical days better but still misses the most extreme days, likely caused by outages or extreme weather, which are not predictable from
past delays alone.

Our original research question was focused on forecasting daily departure delay rates, or the daily proportion of flights that had delays exceeding 15 minutes. 
Our goal MAE was 5, so we did not reach that goal. Supplementary analysis on daily average departure delay (in minutes) was even less accurate, with higher MAE. 
SARIMA consistently performed better than plain ARIMA and had higher prediction accuracy. 
