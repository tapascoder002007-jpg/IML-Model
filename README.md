# Short-Horizon Air Quality Forecasting

## Project Overview

**Short-Horizon Air Quality Forecasting: A Comparative Study of Regression Ensembles with Meteorological and LLM-Derived Features** is a machine learning project focused on forecasting **PM2.5 concentrations for the next 1–24 hours** using historical air-quality and meteorological data.

The project combines publicly available **Indian AQI data** with hourly **ERA5 weather data** to develop a supervised time-series forecasting system. It uses pollutant history, lag features, rolling statistics, weather variables, and cyclical time features to predict future PM2.5 levels and classify the resulting predictions into standard AQI categories.

The main objective is to compare different machine learning models and determine which approaches provide reliable short-term air-quality forecasts, particularly during seasonal changes and extreme pollution events.

---

## Objectives

- Forecast **PM2.5 concentrations 1–24 hours ahead**.
- Incorporate meteorological variables into air-quality prediction.
- Compare traditional regression models with ensemble learning methods.
- Classify predicted pollution levels into AQI categories.
- Analyze model performance across different:
  - Locations
  - Seasons
  - Weather conditions
  - Extreme pollution events
- Investigate whether **LLM-derived text embeddings** from air-quality advisories can improve predictions.

---

## Dataset

The project uses publicly available datasets:

1. **India Air Quality Index Dataset (2023–2025)**
   - Contains 235,000+ AQI records across Indian cities.
   - Used as the primary air-quality dataset.

2. **ERA5 Hourly Weather Data**
   - Provides historical meteorological variables.
   - Used to incorporate weather conditions into the forecasting pipeline.

3. **CPCB Air-Quality Data**
   - 15-minute air-quality data may be used as an optional reference dataset.

The AQI and meteorological datasets are mapped using **station coordinates and timestamps**.

---

## Features

The forecasting pipeline uses several types of features:

- Historical pollutant values
- Lag features
- Rolling statistics
- Meteorological variables
- Hour-of-day information
- Seasonal information
- Cyclical time encodings
- Location/station information

These features are used to predict future PM2.5 concentrations.

---

## Machine Learning Models

### Baseline Models

- Persistence baseline
- Linear Regression
- Majority-class baseline for AQI classification

### Core Models

- Ridge Regression
- Lasso Regression
- Random Forest
- XGBoost

### Stretch Goal

- 1D-CNN-LSTM

### Auxiliary Experiment

An optional branch investigates whether **LLM-derived embeddings from publicly issued air-quality advisory text** can provide additional predictive information when combined with the numerical features.

---

## Evaluation Metrics

### Regression

The regression models are evaluated using:

- RMSE
- MAE
- MSE

Performance is evaluated separately for different forecast horizons.

### AQI Classification

For AQI-bucket classification, the following metrics are used:

- Macro Precision
- Macro Recall
- Macro F1-Score

Additional analysis is performed across:

- Seasons
- Locations
- Weather conditions
- Extreme pollution events

---

## Experimental Methodology

The project follows a strictly chronological train-validation-test split to prevent **look-ahead data leakage**.

The general workflow is:

```text
Air Quality Data ─────┐
                      ├──> Data Preprocessing
ERA5 Weather Data ────┘
                              │
                              ▼
                       Feature Engineering
                              │
                              ▼
                    Lag & Rolling Features
                              │
                              ▼
                     Train / Validation
                              │
                              ▼
                    Machine Learning Models
                              │
                              ▼
                     PM2.5 Forecasting
                              │
                 ┌────────────┴────────────┐
                 ▼                         ▼
          Regression Task            AQI Classification
                 │                         │
                 ▼                         ▼
          RMSE / MAE / MSE          Precision / Recall / F1
