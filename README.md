# ✈️ Air Passengers Time Series Forecasting (ARIMA vs SARIMA)

## *Project Overview*

This repository contains an **end-to-end time series forecasting project** using the classic **AirPassengers dataset (1949–1960)**.

The objective is to demonstrate a **proper statistical workflow** for time series analysis, not just blind model fitting.

---

## *Dataset Description*

* **Source**: Kaggle – AirPassengers
* **Frequency**: Monthly
* **Target Variable**: `#Passengers`
* **Time Index**: `Month`

The data clearly shows:

* Strong upward **trend**
* Pronounced **12-month seasonality**
* Increasing **variance** over time

---

## *Workflow Overview*

### *1. Data Loading & Initial Visualization*

* Converted `Month` to datetime format
* Plotted raw passenger counts to inspect trend, seasonality, and variance

---

### *2. Variance Stabilization*

#### *Log Transformation*

* Applied log transform
* Rolling standard deviation became more stable

#### *Box-Cox Transformation*

* Applied Box-Cox transformation
* Optimal λ ≈ **0.148**
* Provided better variance stabilization than log

---

### *3. Stationarity Testing*

Stationarity was evaluated using **ADF and KPSS tests**.

#### *Before Differencing*

* **ADF**: Failed to reject non-stationarity
* **KPSS**: Rejected stationarity

Conclusion: **Series is non-stationary**.

---

### *4. Differencing*

* Applied first-order differencing
* Re-tested stationarity

#### *After Differencing*

* **ADF**: Stationary
* **KPSS**: Stationary

Conclusion: **Differenced series is stationary**.

---

### *5. ACF & PACF Analysis*

* ACF showed short-term autocorrelation
* PACF suggested AR components
* Used to guide ARIMA/SARIMA order selection

---

## *Modeling*

### *ARIMA Model*

* Configuration: **ARIMA(2,0,1)**
* Models short-term dependencies
* No explicit seasonal component

### *SARIMA Model*

* Configuration: **SARIMA(2,0,1)(1,0,1,12)**
* Explicitly models yearly seasonality
* Better suited for monthly passenger data

---

## *Inverse Transformations*

To return forecasts to the original scale:

1. Cumulative sum to undo differencing
2. Inverse Box-Cox transformation

---

## *Evaluation*

**Metric**: Root Mean Squared Error (RMSE)

* **ARIMA RMSE**: 73.50
* **SARIMA RMSE**: 32.66

Result: **SARIMA significantly outperforms ARIMA**.

---

## *Results Visualization*

* Compared **Actual vs ARIMA vs SARIMA** forecasts
* SARIMA captures seasonal patterns accurately
* ARIMA underfits periodic structure

---

## *Tech Stack*

* Python
* NumPy
* Pandas
* Matplotlib
* SciPy
* Statsmodels
* Scikit-learn

---

## *Key Takeaways*

* Always combine **ADF + KPSS** for stationarity decisions
* Variance stabilization is essential
* Seasonal data requires seasonal models
* SARIMA is superior when periodicity exists

---

## *Future Work*

* STL decomposition
* SARIMAX with exogenous variables
* ETS / Prophet / LSTM comparison
* Rolling-origin cross-validation

---

## *How to Run*

1. Clone the repository
2. Install dependencies
3. Run the notebook sequentially
 
