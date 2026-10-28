# DS4002-Project2-Group5

Contains Project 2 Work for DS 4002 Group 5 Fall 2026

Members: Angelika Baloy, Samuel Bromberg, Inmar Chavarria

## Analyzing and Predicting Airline Delays at Washington Dulles International Airport
We are using data from The United States Department of Transportation. Specifically the Bureau of Transportation Statistics:

Bureau of Transportation Statistics, “Detailed Statistics Departures.” 
https://www.transtats.bts.gov/ontime/Departures.aspx

## Software and Platform
- Software: Python 3 (notebooks: 01_Airline_Project_EDA&Cleaning.ipynb & 02_Airline_Project_Analysis_final.ipynb)
- Platform: Google Colab
- Python Version: 3.13.16

| Package | Version | Used for |
| -------- | ------ | --------| 
| pandas | 2.2.3          | Loading, cleaning, and roganizing the 2024 and 2025 airline datasets |
| matplotlib | 3.10.0      |  Plotting time series, trends, and forecasts  |
| seaborn |   0.13.2       |   Creating statistical visualizations         |
| statsmodels |   0.15.0       |   Fitting ARIMA models, conducting the ADF stationarity test, and forecasting airline delays  |

## Documentation

* Data
    * Combined Data
        * IAD_2024_Combined.csv
        * IAD_2025_Combined_csv
    * Raw Data     
       * IAD_2024_American.csv
       * IAD_2024_Delta.csv
       * IAD_2024_United.csv
       * IAD_2025_American.csv
       * IAD_2025_Delta.csv
       * IAD_2025_United.csv
    * README.md
    * explanatory_plots.jpeg
* Output
     * Conclusion.md
     * Monthly Delay Rates by Airline (2024 vs 2025).png
     * Number of Flight Observations by Airline (2024 vs 2025).png
     * adf_deseasonalized_tests.csv
     * avg_delay_accuracy.csv
     * avg_delay_forecast.png
     * avg_delay_monthly.png
     * avg_delay_rate_results.csv
     * delay_rate_accuracy.csv
     * delay_rate_forecast.png
     * delay_rate_results.csv
* Scripts
     * 01_Airline_Project_EDA&Cleaning.ipynb
     * 02_Airline_Project_Analysis_final.ipynb
* LICENSE
* README.md

## File locations

* `Data/Raw Data/` contains the source airline CSV files.
* `Data/Combined Data/` contains the combined datasets created by Script 01 and used as input by Script 02.
* `Output/` contains the generated results from Script 02, including ADF test results, accuracy tables, forecast tables, and plots.

## Instruction for Reproducing Results

1. Access the data files by going to the data folder in this repository. Read the README.md file to get acquainted with the data. Download all raw data files.
2. Access the first script in the scripts folder: 01_Airline_Project_EDA&Cleaning.ipynb by opening the file in Google Colab or by downloading the file.
3. Run the first code chunk to import the necessary packages. Create a merged dataset for 2024 by running the following chunk. This should create a file combining all 2024 flight data from all three airlines (United, American, and Delta).
4. Save the combined 2024 dataset by running the next code chunk. This combined dataset is also accessible in the Data folder in this repo. Repeat this process for the 2025 data by running the next code chunk. The 2025 combined dataset is also stored with the combined 2024 dataset in this repo.
5. Exploratory Data Analysis
   * Run the following code chunk and combine the combined 2024 and 2025 datasets. Convert Date column to the necessary format. Create variables: Delayed, Month, Quarter, and Day of Week. Set the colors and theme for the following plot.
   * Run the following code chunk to create a visualization of Monthly Delay Rates by Airline (2024 vs 2025). Notice the variation by carrier. Yearly trends, overall, are still quite similar. 
   * Run the next chunk to create a bar graph showing the Number of Flight Observations by Airline (2024 vs 2025). Notice that United flights are overrepresented in this dataset; there is not an even distribution of flights across carrier.
6. Analysis
   * Open `Scripts/02_Airline_Project_Analysis_final.ipynb` in Google Colab (or download it) and upload `IAD_2024_Combined.csv` and `IAD_2025_Combined.csv` to its working directory.
   * Run **code cell 1** (`# Packages required for analysis`).
   * Run **code cell 2** (`# Combined datasets`) to read in the combined datasets from the first script.
   * Run **code cell 3** (`# Cleaning applied to both years`) to remove cancelled flights.
     * Expected output: `Cancelled flights removed: 488` (2024) and `222` (2025).
   * Run **code cell 4** (`# Daily series`) to aggregate to daily average departure delay (minutes) and daily departure delay rate (% of flights delayed 15+ minutes).
     * Expected: 366 daily rows for 2024 and 365 for 2025; first row (2024-01-01) has avg_delay 8.977528 and delay_rate 14.606742.
   * Run **code cell 5** (`# Dates to forecast`) to set the forecast dates: every day in 2025.
   * Run **code cell 6** (`# checking for stationarity in both series`) for the first stationarity check. At this step the p-values are expected to be **above .05**, which means the series are non-stationary.
     * Expected output: average departure delay ADF statistic -2.835039, p = 0.053440; departure delay rate ADF statistic -2.777743, p = 0.061524.
   * Run **code cell 7** (`# Yearly seasonality: Fourier terms`) to build the yearly seasonal curve used by the models.
   * Run **code cell 8** (`# ADF test after removing yearly seasonality`) to address the non-stationarity. The p-values here are expected to be **below .05**.
     * Expected output: average departure delay ADF statistic -5.867932, p = 0.000000; departure delay rate ADF statistic -13.056633, p = 0.000000. This cell also saves `adf_deseasonalized_tests.csv`.
   * Run **code cell 9** (`# Model fitting and forecasting`) to define the ARIMA and SARIMA function. Read the comments explaining each part.
   * Run **code cell 10** (`# Accuracy against the actual 2025 values`) to define the function that compares ARIMA, SARIMA, and 2024 Average MAE and RMSE.
   * Run **code cell 11** (`# Plot predicted vs. actual`) to define the plotting function.
   * Model 1 (daily departure delay rate): run **code cell 12** (`# Model 1`) to fit the models, view the accuracy table, and view the plot, then run **code cell 13** (`# Save output`) to save `delay_rate_accuracy.csv` and `delay_rate_results.csv`.
     * Expected accuracy over 365 days of 2025 (the table prints twice; this is expected):

       | Model | MAE | RMSE |
       | --- | --- | --- |
       | 2024 Average | 7.91 | 10.84 |
       | ARIMA Prediction | 7.88 | 10.77 |
       | SARIMA Prediction | 7.02 | 10.19 |

     * `delay_rate_results.csv` should have 365 data rows (one per day of 2025) and the columns Date, ARIMA Prediction, SARIMA Prediction, Lower 95%, Upper 95%.
   * Model 2 (daily average departure delay, minutes): run **code cell 14** (`# Model 2`) and then **code cell 15** (`# Save output`) to save `avg_delay_accuracy.csv` and `avg_delay_rate_results.csv`.
     * Expected accuracy over 365 days of 2025:

       | Model | MAE | RMSE |
       | --- | --- | --- |
       | 2024 Average | 9.27 | 14.21 |
       | ARIMA Prediction | 9.27 | 14.21 |
       | SARIMA Prediction | 7.93 | 13.49 |

   * Reflect on the differences between the two main models, and between ARIMA and SARIMA. Note the differences in error (MAE, RMSE).
   * **Code cell 16** (`# Monthly view`) and **code cell 17** (`# Label rows by month name`) give another ARIMA/SARIMA comparison. These are outside our research question and main analysis, but they help show how ARIMA and SARIMA predictions differ. SARIMA is much better at capturing fluctuations across the year. Cell 17 saves `avg_delay_monthly.png`.
   * Small numeric differences from the values above are possible with different package versions, and a `ConvergenceWarning` from the SARIMA fit is expected.
   * All output from this script is accessible in the `Output/` folder in this repo.
