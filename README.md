# Mt. Everest Weather & Summit Attempt Analytics

## Overview
This project builds an end-to-end analytics system in Microsoft Fabric to predict the likelihood of successful summit attempts on Mt. Everest.
It integrates historic expedition data, high-altitude weather forecasts, data engineering pipelines, and machine learning models.

This solution demonstrates:
- Time-series weather ingestion
- Data virtualization in OneLake
- Engineering pipelines using Dataflows & PySpark
- ML models for summit success prediction
- A Power BI report for expedition intelligence

## Architecture
Weather APIs + Expedition Logs → OneLake → Dataflows / Notebooks → Lakehouse (Bronze/Silver/Gold) → Warehouse → ML Model → Power BI Dashboard

## Data Ingestion

### Weather Data
Source: Open-Meteo 
- Wind speed and wind gusts
- Temperature
- Weather code
- Precipitation and snowfall
- Sunrise and sunset

### Expedition Data
Using the Himalayan Database (public dataset):
- Summit attempts and dates
- Fatalities
- Expedition routes and members
- Oxygen use
- Dates & success outcomes

All this data is stored in the Bronze Layer in its most raw format.

## Data Processing & Engineering
Dataflows Gen2

- Standardize expedition schema
- Parse dates and flags
- Clean route and season metadata
- Merge weather + expedition outcomes

Processed tables are stored in the Silver and Gold Layers.

## Machine Learning Modeling

Models trained to predict summit success likelihood:
- Gradient Boosting or Random Forest
- Time-series forecasting for optimal climbing days
- Logistic Regression for success/survival prediction

## Warehouse & Semantic Layer

The semantic model includes:

`fact_expeditions` - factual table with all the data from the expeditions

`dim_climber` - dimension with all the information available about the climbers

`dim_route` - dimension created with the route information on the Expeditions table

`dim_weather`

`dim_weather_codes` - dimension just for the weather codes, retrieved on the OpenMeteo website

`dim_calendar` - calendar dimension

## Power BI Dashboard

Mt. Everest Expedition Intelligence Dashboard features:
- Weather vs. Success Rates
- Route Difficulty Comparison
- Year-over-Year Expedition Activity
- Predictive Summit Window Forecast
- Survival Analysis & Risk Factors
- Geospatial Map of:
  - Base camps
  - Standard routes
  - Success & failure hotspots

Dashboard integrates ML model predictions for enhanced insights.

## Project Structure
```
/mteverest
│
├── data/
│   ├── expedition_information.zip
│
├── notebooks/
│   ├── 01 Data Ingestion.ipynb
│   ├── 02 Data Cleansing.ipynb
│   ├── 03 Data Transformation - GOLD LAYER.ipynb ***to do
│   ├── 04 model training.ipynb ***to do
│
├── pipelines/
│   ├── weather_ingestion_pipeline.json ***to do
│   └── expedition_ingestion_pipeline.json ***to do
│
├── powerbi/
│   └── everest_dashboard.pbix ***to do
│
└── README.md
```
