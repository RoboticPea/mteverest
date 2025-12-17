# Mt. Everest Weather & Summit Attempt Analytics

## Overview
This project builds an end-to-end analytics system in Microsoft Fabric to predict the likelihood of successful summit attempts on Mt. Everest.
It integrates historic expedition data, high-altitude weather forecasts, data engineering pipelines, and machine learning models.

This solution demonstrates:
- Time-series weather ingestion
- Data virtualization in OneLake
- Engineering pipelines using PySpark
- ML models for summit success prediction
- A Power BI report for expedition intelligence

## Architecture
Weather APIs + Expedition Logs → OneLake → Dataflows / Notebooks → Lakehouse (Bronze/Silver/Gold) → Warehouse → ML Model → Power BI Dashboard

## Data Ingestion

### Weather Data
Source: Open-Meteo 
- Wind speed and wind gusts
- Temperature
- Relative humidity
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
Notebooks (using PySpark) and Dataflow Gen 2

- Standardize table schema
- Create fact and dimension tables

Processed tables are stored in the Silver and Gold Layers.

## Machine Learning Modeling ****TO DO

Models trained to predict summit success likelihood:
- Gradient Boosting or Random Forest
- Time-series forecasting for optimal climbing days
- Logistic Regression for success/survival prediction

## Warehouse & Semantic Layer

The semantic model includes:

`fact_expeditions` - factual table with expedition information

`dim_climber` - dimension with all the information available about the climbers

`dim_route` - dimension with the up and down route for each expedition (created from Expeditions)

`dim_camps` - dimension with camp information for each expedition (created from Expeditions)

`dim_weather` - dimension for all the weather information available, including the description for the weather codes

`dim_date` - calendar dimension

## Power BI Dashboard

Mt. Everest Expedition Intelligence Dashboard features:
- Weather vs. Success Rates
- Route Difficulty Comparison
- Year-over-Year Expedition Activity
- Predictive Summit Window Forecast
- Survival Analysis & Risk Factors
- Map of:
  - Base camps
  - Success & failure hotspots

Dashboard integrates ML model predictions for enhanced insights. ****TO DO

## Project Structure
```
/mteverest
│
├── data/
│   ├── expedition_information.zip
│
├── notebooks&dataflow/
│   ├── 01 Data Ingestion.ipynb
│   ├── 02 Data Cleansing.ipynb
│   ├── 03 Data Transformation.pqt
│   ├── 04 ML Model Training.ipynb ***to do
│
├── powerbi/
│   └── everest_dashboard.pbix ***to do
│
└── README.md
```
