# DS4002-Project2-Group5

Contains Project 2 Work for DS 4002 Group 5 Fall 2026

Members: Angelika Baloy, Samuel Bromberg, Inmar Chavarria

## Analyzing and Predicting Airline Delays at Washington Dulles International Airport
We are using data from The United States Department of Transportation. Specifically the Bureau of Transportation Statistics:

Bureau of Transportation Statistics, “Detailed Statistics Departures.” 
https://www.transtats.bts.gov/ontime/Departures.aspx

## Software and Platform
- Software: Python 3 (notebook: Arline_Project_Analysis.ipynb)
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

## Instruction for Reproducing Results

1. Access the data files by going to the data folder in this repository. Read the README.md file to get acquainted with the data. Download all raw data files.
2. Access the first script in the scripts folder: 01_Airline_Project_EDA&Cleaning.ipynb by opening the file in Google Colab or by downloading the file.
3. Run the first code chunk to import the necessary packages. Create a merged dataset for 2024 by running the following chunk. This should create a file combining all 2024 flight data from all three airlines (United, American, and Delta).
4. Save the combined 2024 dataset by running the next code chunk. This combined dataset is also accessible in the Data folder in this repo. Repeat this process for the 2025 data by running the next code chunk. The 2025 combined dataset is also stored with the combined 2024 dataset in this repo.
5. Exploratory Data Analysis
     a. Run the following code chunk and combine the combined 2024 and 2025 datasets. Convert Date column to the necessary format. Create variables: Delayed, Month, Quarter, and Day of Week. Set the colors and theme for the following plot.
     b. Run the following code chunk to create a visualization of Monthly Delay Rates by Airline (2024 vs 2025). Notice the variation by carrier. Yearly trends, overall, are still quite similar. 
     c. Run the next chunk to create a bar graph showing the Number of Flight Observations by Airline (2024 vs 2025). Notice that United flights are overrepresented in this dataset; there is not an even distribution of flights across carrier.
6. Analysis
     a. Access the second script in the scripts folder in this repository: 02_Airline_Project_Analysis_final.ipynb by opening the file in Google Colab or by downloading the file.
     b. Import the necessary packages for analysis.
     c. Run the next code chunk to read in the combined datasets created from the previous script.
     d. Clean the data to remove cancelled flights by running the following code chunk.
     e. Aggregate the data by running the next chunk. This prepares the data for modeling and organizes data into our desired variables: daily departure delay rates and daily average departure delay (in minutes).
     f. Set up forecast dates by running the first line in the next code chunk. Each day in 2025 will be predicted by our models.
     g. Check for stationarity by running the next chunk. The goal of this check is to calculate p-values below .05, indicating that the data is stationary.
     h. Run the next chunk. This code sets up the curve the model will make predictions off of.
     i. Address the non-stationarity by running the following code chunk. This should produce updated p-values that are statistically significant.
     j. Run the following chunk to create a function to create ARIMA and SARIMA models. Read comments explaining each part of the function.
     k. Run the following chunk to create a function to compare ARIMA, SARIMA, and 2024 Average MAE and RMSE.
     l. Run the next chunk to create a function to plot the results of our models.
     m. Create the first model and view its results by running the next chunk under Model 1. View the plot. Save the score and model output by running the following chunk.
     n. Create the second model and view its results by running the next chunk under Model 2. View the plot. Save the score and model output by running the following chunk.
     o. Reflect on the differences between the two main models, but also in the ARIMA/SARIMA. Note differences in error (MAE, RMSE).
     p. The next two chunks provide another opportunity for ARIMA/SARIMA comparison. Though these are outside of our research question and main analysis, this helps us better understand how ARIMA and SARIMA predictions differ. Particularly, SARIMA is much better at capturing fluctuations across the year.
     q. All output from this script is accessible in the output folder in this repo. 
