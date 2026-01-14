# NYC-Subway-Demand-Forecasting-Resource-Optimization

**End-to-end time-series forecasting project using real NYC subway ridership data to optimize operational staffing decisions and quantify the cost of forecast errors.**

## Project Overview

Public transit systems face **over-staffing costs** during low demand and **service degradation** during peak hours.
This project builds a **demand forecasting pipeline** and translates forecast accuracy into **actionable staffing and cost insights**.

**Key question:**

> *How can hourly ridership forecasts reduce under- and over-staffing in major transit hubs?*

## What This Project Demonstrates

* Time-series forecasting with **real-world, non-Kaggle data**
* Feature engineering for **seasonality and temporal patterns**
* Baseline vs ML model comparison
* Business-aligned evaluation (staffing cost, not just MAE)
* End-to-end workflow: **data → model → dashboard**


## Data

**Source:** NYC MTA Open Data
**Granularity:** Hourly ridership
**Stations analyzed:**

* Grand Central–42 St
* Times Sq–42 St

**Time range:** Jan 2024 – Dec 2024

---

## Methodology

### 1. Data Preparation

* Parsed timestamps and station identifiers
* Converted cumulative turnstile counts to **hourly ridership**
* Filled missing hours using time-indexed reindexing
* Filtered anomalies (negative deltas)

---

### 2. Baseline Models

| Model          | Description                      |
| -------------- | -------------------------------- |
| Naive          | Last observed value              |
| Seasonal Naive | Same hour previous day (24h lag) |

**Result:** Seasonal Naive reduced MAE by ~40% vs naive.

---

### 3. Machine Learning Model

**Model:** Gradient Boosting Regressor
**Features:**

* Lag features (1, 2, 3, 24, 48, 168)
* Rolling statistics (mean & std)
* Hour of day, day of week
* Weekend indicator

**No hyperparameter tuning** (fair comparison).

---

### 4. Evaluation Metrics

* Mean Absolute Error (MAE)
* Forecast error trend
* Staffing error (demand → staff_required)
* Weekly staffing cost impact

---

## Results Summary

| Station       | Model             | MAE     |
| ------------- | ----------------- | ------- |
| Grand Central | Seasonal Naive    | **923** |
| Grand Central | Gradient Boosting | 1302    |
| Times Square  | Seasonal Naive    | **938** |
| Times Square  | Gradient Boosting | 1153    |

 **Insight:**
Simple seasonal baselines performed competitively, highlighting the importance of strong baselines in operational forecasting.


## Business Impact

Forecasts were translated into **staffing requirements** using demand-to-staff ratios.

* Reduced weekly staffing cost by **$30K–$70K** vs naive baselines
* Identified **peak staffing windows (8–10 AM, 4–7 PM)**
* Quantified cost of forecast error (over vs under staffing)


## Dashboard (Power BI)

Interactive planning dashboard includes:

* Actual vs forecast demand trends
* Peak-hour demand distribution
* Staffing requirements over time
* Forecast accuracy KPIs
* Station-level filtering

Dashboard file: `demand forecasting.pdf`

## Tech Stack

* **Python**: pandas, numpy, scikit-learn
* **Time Series**: lag features, rolling windows
* **Visualization**: Matplotlib, Power BI
* **Data Source**: NYC Open Data (MTA)


## Key Takeaways

* Strong baselines are critical before deploying ML
* Operational metrics (staffing cost) matter more than pure accuracy
* Forecasting systems must align with **decision-making workflows**
