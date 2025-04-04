# Time Series Analysis and Forecasting of Heart Rate Data

This project implements a comprehensive time series analysis and forecasting pipeline using physiological data (heart rate, respiration rate, etc.). The code is organized into several key sections that guide the process from data loading to forecasting and saving final predictions. Below is a high-level summary of the workflow:

---

## 1. Environment Setup

- **Library Installation:**  
  The necessary packages for time series analysis are installed, including `pmdarima`, `pykalman`, `ruptures`, and `statsmodels`.

- **Imports and Configuration:**  
  The code imports libraries for data manipulation (Pandas, NumPy), visualization (Matplotlib, Seaborn), time series modeling (Statsmodels, ARIMA, SARIMAX, Exponential Smoothing), change point detection (ruptures), Fourier analysis, and state-space filtering (PyKalman). Warnings are suppressed to keep the output clean.

---

## 2. Data Loading and Preprocessing

- **Data Import:**  
  The dataset is read from a Google Drive URL. The timestamp column is converted to a datetime format and set as the index, which is essential for time series operations.

- **Correlation Analysis:**  
  A correlation matrix is computed and visualized using a heatmap. This helps identify which features are most strongly related to the target variable (heart rate).

- **Outlier Detection:**  
  Box plots are used to visualize outliers in both heart rate and respiration rate. Outliers are detected using the Interquartile Range (IQR) method and replaced with the mode value to reduce their impact on the analysis.

- **Missing Value Check:**  
  The code verifies the dataset for missing values, noting that some fields (like SpO2 and pulse) might be excluded due to low correlation with the target.

---

## 3. Exploratory Data Analysis (EDA)

- **Time Series Plotting:**  
  The heart rate data is plotted over time to visualize trends and potential anomalies.

- **Distribution Analysis:**  
  Histograms with kernel density estimates (KDE) are generated to inspect the distribution of heart rate values, highlighting patterns such as bimodality or skewness.

- **Rolling Statistics:**  
  A moving average (e.g., 10-minute window) is computed and plotted alongside the original data to reveal underlying trends and smooth out short-term fluctuations.

- **Time Series Decomposition:**  
  The series is decomposed into trend, seasonal, and residual components using seasonal decomposition. This helps in understanding the inherent patterns within the data.

- **Autocorrelation Analysis:**  
  Autocorrelation (ACF) and partial autocorrelation (PACF) plots are produced to identify significant lags, which are useful for parameter selection in ARIMA modeling.

- **Change Point Detection:**  
  Using the `ruptures` library, the code identifies potential change points where the statistical properties of the series shift, indicating structural changes.

- **Fourier Transform Analysis:**  
  FFT is applied to extract the dominant frequency components in the heart rate data, which can signal cyclic behaviors or seasonality.

---

## 4. Stationarity Testing

- **Stationarity Check:**  
  The code tests whether the heart rate series is stationary using tests such as KPSS. Non-stationarity is detected, which informs the need for transformations (e.g., differencing or log transformation).

---

## 5. Feature Engineering and Data Transformation

- **Log Transformation:**  
  A logarithmic transformation is applied to reduce variance and potentially stabilize the data.  
- **Deseasonalisation and Differencing:**  
  The series undergoes seasonal differencing to remove periodic effects, and first-order differencing is applied to remove trends. Subsequent stationarity tests confirm that the transformed series is now stationary and suitable for forecasting.

---

## 6. Model Training and Forecasting

- **ARIMA Modeling:**  
  An ARIMA model is specified and fitted to the heart rate data. Predictions are made over a specific time window, and error metrics (MSE, MAE, RMSE) are computed.
  
- **SARIMA Modeling:**  
  A seasonal ARIMA (SARIMA) model is fitted to capture both the trend and seasonality. The model is used for in-sample prediction as well as out-of-sample forecasting.

- **SARIMAX Modeling:**  
  An extension of SARIMA, SARIMAX includes exogenous variables (e.g., respiration rate) to improve prediction accuracy. Forecasts are generated and compared with actual values.

- **Forecast Comparison:**  
  The forecasts from ARIMA, SARIMA, and SARIMAX are plotted together with the observed heart rate data to visually compare performance.

---

## 7. Saving Final Predictions

- **Output Generation:**  
  The final SARIMA forecast is formatted into a DataFrame, its index is reset for clarity, and the results are saved to a CSV file (`sarima_forecast_index_prediction.csv`). This file can be used for reporting or further analysis.

---

## Conclusion

This pipeline demonstrates a robust approach to time series analysis on physiological data, covering everything from data cleaning and exploratory analysis to advanced forecasting models and error metric computation. By applying transformations to ensure stationarity and leveraging multiple modeling techniques (ARIMA, SARIMA, SARIMAX), the project provides a detailed framework for accurate heart rate forecasting.


