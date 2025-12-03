# Mt. Everest Weather & Summit Attempt Analytics
An End-to-End Microsoft Fabric Project

## Overview

This project builds an end-to-end analytics system in Microsoft Fabric to predict the likelihood of successful summit attempts on Mt. Everest.
It integrates historic expedition data, high-altitude weather forecasts, data engineering pipelines, and machine learning models to deliver actionable insights.

This solution demonstrates:
- Time-series weather ingestion
- Data virtualization in OneLake
- Engineering pipelines using Dataflows & PySpark
- ML models for summit success prediction
- A rich Power BI dashboard for expedition intelligence

## Architecture

Weather APIs + Expedition Logs → OneLake → Dataflows / Notebooks → Lakehouse (Bronze/Silver/Gold) → Warehouse → ML Model → Power BI Dashboard

## Data Ingestion

### Weather Data
Sources such as Open-Meteo or NOAA provide:
- Wind speed
- Temperature
- Pressure
- Jet stream position
- Precipitation
- Historical summit window data
Frequency: hourly or daily.

### Expedition Data
Using the Himalayan Database (public dataset):
- Summit attempts
- Fatalities
- Expedition routes
- Experience level
- Oxygen use
- Dates & success outcomes

Raw JSON/CSV is stored in the Bronze Lakehouse.

## Data Processing & Engineering
Dataflows Gen2

Standardize expedition schema
Parse dates and flags
Clean route and season metadata
Notebooks (PySpark)
Merge weather + expedition outcomes
Feature engineering, including:
Oxygen usage
Route difficulty
Team size
Predicted vs. actual weather
Weather window availability
Wind chill index
Icefall danger proxy
Time-series alignment of weather to summit attempts

Processed tables are stored in the Silver and Gold Lakehouse layers.

## Machine Learning Modeling

Models trained to predict summit success likelihood:
- Gradient Boosting or Random Forest
- Time-series forecasting for optimal climbing days
- Logistic Regression for success/survival prediction

## Warehouse & Semantic Layer

Dimensional model includes:
`fact_summit_attempts`
`fact_weather_timeseries`
`dim_climber`
`dim_route`
`dim_weather_condition`

## Power BI Dashboard

Mt. Everest Expedition Intelligence Dashboard features:
- Weather vs. Success Rates
- Route Difficulty Comparison
- Year-over-Year Expedition Activity
- Predictive Summit Window Forecast
- Survival Analysis & Risk Factors
- Geospatial Map of:
  - - Base camps
  - - Standard routes
  - - Success & failure hotspots

Dashboard integrates ML model predictions for enhanced insights.

## Project Structure
/mteverest
│
├── data/
│   ├── expeditions/
│   ├── weather/
│   └── synthetic_samples/
│
├── notebooks/
│   ├── ingestion_weather.ipynb
│   ├── ingestion_expeditions.ipynb
│   ├── feature_engineering.ipynb
│   └── model_training.ipynb
│
├── pipelines/
│   ├── weather_ingestion_pipeline.json
│   └── expedition_ingestion_pipeline.json
│
├── powerbi/
│   └── everest_dashboard.pbix
│
└── README.md
