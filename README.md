# TB Outbreak Prediction Project

A machine learning project to track tuberculosis cases and predict potential outbreak zones using location-based analysis.

## Overview

This project focuses on data acquisition from WHO GHO API to gather TB incidence and mortality data for 2018-2023, preparing it for machine learning analysis to identify high-risk outbreak zones.

## Project Structure

```
datascienceproject/
├── notebooks/
│   └── 01_data_acquisition.ipynb    # Main data acquisition notebook
├── data/
│   ├── database/
│   │   └── tb_data.db               # SQLite database (gitignored)
│   └── raw/
│       └── *.csv                     # Raw CSV exports (gitignored)
├── requirements.txt                  # Python dependencies
└── README.md
```

## Setup

1. Install dependencies:
```bash
pip install -r requirements.txt
```

2. Open the notebook:
```bash
jupyter notebook notebooks/01_data_acquisition.ipynb
```

## Data Sources

- **WHO GHO API**: TB incidence and mortality data
  - Endpoint: `https://ghoapi.azureedge.net/api`
  - Indicators: TB_e_inc_tbhiv_num, TB_e_mort_exc_tbhiv_num

## Notebook

The `01_data_acquisition.ipynb` notebook is self-contained and includes:
- Configuration and API endpoints
- Database schema creation
- API fetching functions
- Database loading functions
- Data acquisition workflow

Run all cells sequentially to:
1. Create database schema
2. Fetch TB data from WHO API (2018-2023)
3. Load data into SQLite database
4. Verify data integrity

## Database Schema

- `country_metadata`: Country codes, names, and regions
- `tb_data`: TB incidence and mortality data
- `unified_tb_data`: Unified view joining all tables

## Next Steps

- Data cleaning and exploratory data analysis
- Feature engineering
- Machine learning model development for outbreak prediction

