# Household-Energy-Consumption-Time-Series-Forecasting

##  Project Description
This project focuses on forecasting short-term household energy usage using historical time-based patterns. By cleaning and processing a high-frequency power dataset, we engineer cyclical time features and evaluate the predictive accuracy of three distinct time series methods: ARIMA, Prophet, and XGBoost.


##  Task Objective
The goal of this task is to build a reliable forecasting pipeline to predict future household electrical loads. Accurate short-term load forecasting helps utility providers optimize power distribution, manage grid demands efficiently, and reduce operational energy waste based on consumer habits.


##  Our Approach

To construct an optimized forecasting engine, we implemented a robust time-series data science workflow:

### 1. Data Cleaning & Parsing
* Loaded the raw historical power files (`household_power_consumption.txt`) explicitly handling structural irregularities and missing characters (`?`).
* Parsed and combined distinct string date and time logs into a unified, high-precision `Datetime` column.
* Converted raw objects into clean numeric floating points and handled missing rows safely.
* Resampled the minute-by-minute recordings into structural Daily (`D`) intervals by summing up global power loads for regularized trend learning.

### 2. Time-Based Feature Engineering
Since supervised regression frameworks cannot interpret chronological index sequences naturally, we manually extracted structural time vectors:
* Day of the Week (tracking weekend utility shifts vs. workdays)
* Month of the Year (tracking seasonal changes)
* Quarter Periods

### 3. Exploratory Data Analysis (EDA)
* Plotted the resampled historical daily data timeline to visually analyze overall consumption baselines, random spikes, and cyclical seasonal drops.

### 4. Predictive Modeling & Horizon Benchmarking
We split our time series data into a chronological training set, reserving the final **30 days** as a testing slice to evaluate short-term tracking precision across three distinct approaches:
1. **ARIMA (Classical Statistical Approach):** Configured to observe stationary autoregressive movements.
2. **Prophet (Additive Trend Model):** Deployed to capture strong overlapping weekly and annual cyclic seasonality lines.
3. **XGBoost (Supervised Machine Learning Regression):** Deployed to map non-linear variations using our engineered time-based calendar features.


##  Results and Actionable Findings

We evaluated the forecasting performance of each model by directly overlaying their 30-day predictions against actual historical consumption logs and calculating tracking errors (RMSE and MAE):

* **ARIMA Performance:** Offered a standard baseline trend profile, but its predictions tended to flatten out over longer test horizons, making it less effective at capturing volatile spikes.
* **Prophet Performance:** Demonstrated high accuracy in capturing regular human behavior cycles. It effectively matched structural weekday drops and weekend energy surges by leaning on its integrated seasonal components.
* **XGBoost Performance:** Handled sudden changes in variance effectively due to the engineered calendar components, though it requires precise lag features to maintain direction over extended timelines.
* **Core Takeaway:** For long-term infrastructure planning, combining Prophet’s stable cyclical forecasting with an ensemble machine learning model handles both steady seasonal habits and sudden consumption changes best.
