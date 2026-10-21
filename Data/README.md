# Data Establishment & Metadata

## Data Summary

This project uses historical flight departure data for United Airlines, American Airlines, and Delta Air Lines at Washington Dulles International Airport (IAD). The data covers 2024 and 2025 and is organized into six CSV files: one for each airline in each year.

The main outcome for the analysis is the daily percentage of flights delayed by 15 minutes or more. We will calculate this measure from the flight-level departure delay data and use it to explore delay patterns and forecast daily delay rates.

## Provenance

The flight data comes from the [Bureau of Transportation Statistics (BTS) Detailed Statistics Departures database](https://www.transtats.bts.gov/ontime/Departures.aspx), which provides historical departure data by origin airport and airline. To obtain the data used in this project, select all flight statistics, all months, and all days; select IAD as the origin airport; and download records for United, American, and Delta for 2024 and 2025.

The original data is organized by year and airline, with flights listed chronologically. It includes flight-identification fields, such as carrier code, flight number, and tail number, as well as departure information, flight times, delay durations, and reported delay causes. The six CSV files are stored in this project’s GitHub repository.

During preparation, we will skip the seven-row report header in each CSV, standardize column names, and check the date range, airline, row count, missing values, and duplicate flights. We will document rows excluded for missing or unusable dates or departure-delay values.

## License and Attribution

The data is collected and published by the U.S. Department of Transportation’s Bureau of Transportation Statistics. We use it for educational purposes and credit BTS as the source. The data and its underlying ownership remain with BTS and the U.S. Department of Transportation.

## Ethical Considerations

The dataset contains flight information, including flight numbers and tail numbers, but this project will analyze flights in aggregate. We will not use these fields to identify or track individual flights. The analysis focuses on airline-level and daily delay patterns.

## Data Dictionary

| Feature | Type | Meaning | Uncertainty |
| --- | --- | --- | --- |
| Carrier Code | Categorical / string | Identifies the airline operating the flight. | Codes may be missing or incorrect. |
| Date | Date | Scheduled departure date. | Dates may be missing or incorrectly recorded. |
| Destination Airport | Categorical / string | Three-letter code for the flight’s destination. | Airport codes may be missing or incorrect. |
| Scheduled Departure Time | Time / integer | Planned departure time. | Schedule changes may not be reflected. |
| Actual Departure Time | Time / integer | Recorded departure time. | May be missing for canceled flights or incorrectly recorded. |
| Scheduled Elapsed Time (Minutes) | Numeric / integer | Planned flight duration. | May differ from actual flight duration. |
| Actual Elapsed Time (Minutes) | Numeric / integer | Recorded flight duration. | May be missing for canceled or diverted flights. |
| Departure Delay (Minutes) | Numeric / integer | Difference between actual and scheduled departure times. | May be missing or contain recording errors. |
| Wheels-Off Time | Time / integer | Recorded time the aircraft took off. | May be missing or incorrectly recorded. |
| Delay Carrier (Minutes) | Numeric / integer | Delay attributed to airline operations or maintenance. | Delay causes may be difficult to classify and can overlap. |
| Delay Weather (Minutes) | Numeric / integer | Delay attributed to weather. | Weather-related delays may overlap with other causes. |
| Delay National Aviation System (Minutes) | Numeric / integer | Delay attributed to air traffic control or airport congestion. | Causes may overlap with weather or other delays. |
| Delay Security (Minutes) | Numeric / integer | Delay attributed to security-related issues. | May be missing or difficult to distinguish from other causes. |
| Delay Late Aircraft Arrival (Minutes) | Numeric / integer | Delay attributed to the aircraft arriving late from a previous flight. | May overlap with other delay causes. |
| Delayed Flight | Binary / integer | Derived indicator equal to 1 when departure delay is at least 15 minutes, and 0 otherwise. | Calculated from usable departure-delay values. |
| Daily Flight Count | Numeric / integer | Number of flights with usable departure-delay values on a given date. | Days with unusually few flights may produce less stable rates. |
| Daily Delayed Flight Count | Numeric / integer | Number of flights delayed by at least 15 minutes on a given date. | Depends on the completeness of departure-delay records. |
| Daily Delay Rate | Numeric / percentage | Daily delayed flight count divided by daily flight count. | Days with no usable delay values are treated as missing, not as zero-delay days. |

## Explanatory Plots

[![Description of the image](Data/explanatory_plots.jpeg)](Data/explanatory_plots.jpeg)

## Data Preparation and Analysis

We will combine the six airline-year datasets after standardizing their column names and checking for missing values and duplicate flights. A flight will count as delayed when its departure delay is 15 minutes or more.

For each date, we will calculate the delay rate as:

`daily delayed flight count / daily flight count`

The overall daily rate will be calculated from the combined flight counts, so each flight receives equal weight. We will also retain airline-specific rates for comparisons. Flights without a usable date or departure-delay value will be excluded from the rate calculation, and the number of excluded rows will be documented. Cancellations will be reported separately if they can be identified in the data.

The analysis will check date coverage and daily flight counts, then compare delay rates across airlines, quarters, and days of the week. We will use 2024 data to select and train the forecasting model and 2025 data to evaluate it. ARIMA and, if appropriate, SARIMA models will be compared using time-ordered validation within 2024. The selected model will be compared with a simple baseline, such as the 2024 average delay rate. Final performance will be reported as mean absolute error (MAE) in percentage points, with a target of 5 percentage points or less.

## References

[1] Bureau of Transportation Statistics, “Detailed Statistics Departures.” [https://www.transtats.bts.gov/ontime/Departures.aspx](https://www.transtats.bts.gov/ontime/Departures.aspx). Accessed October 8, 2026.

[2] J. Noble, “What are ARIMA Models?,” IBM. [https://www.ibm.com/think/topics/arima-model](https://www.ibm.com/think/topics/arima-model). Accessed October 12, 2026.
