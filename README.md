# TB Outbreak Prediction Project

A machine learning project to track tuberculosis cases and predict potential outbreak zones using location-based analysis. This project integrates data from WHO (TB incidence, mortality, and HIV cases) and World Bank (GDP, poverty rates, population) to perform statistical analysis and machine learning modeling.

## Overview

This project focuses on data acquisition from WHO GHO API and World Bank API to gather TB incidence, mortality, HIV data, and economic indicators for 2020-2025, preparing it for machine learning analysis to identify correlations between economic factors and TB outcomes.

## Download and Setup

### Prerequisites

- Python 3.8 or higher
- Git
- pip (Python package manager)

### Step 1: Clone the Repository

```bash
git clone <repository-url>
cd datascienceproject
```

If you don't have the repository URL, you can download the project as a ZIP file from GitHub and extract it to your desired location.

### Step 2: Create a Virtual Environment (Recommended)

```bash
# Create a virtual environment
python3 -m venv venv

# Activate the virtual environment
# On macOS/Linux:
source venv/bin/activate

# On Windows:
venv\Scripts\activate
```

### Step 3: Install Dependencies

```bash
pip install -r requirements.txt
```

This will install all required packages:
- pandas (data manipulation)
- numpy (numerical computing)
- requests (API calls)
- sqlalchemy (database operations)
- jupyter (notebook environment)
- matplotlib & seaborn (visualization)
- scikit-learn (machine learning)
- statsmodels (statistical modeling)
- scipy (scientific computing)

### Step 4: Launch Jupyter Notebook

```bash
jupyter notebook
```

This will open Jupyter in your web browser. Navigate to the `notebooks/` directory.

## Project Structure

```
datascienceproject/
├── notebooks/
│   ├── WHO_Data.ipynb                    # WHO TB and HIV data acquisition
│   ├── WorldBank_Data.ipynb              # World Bank economic data acquisition
│   └── DataProcessingAndMachineLearning.ipynb  # Data joining and ML analysis
├── data/
│   ├── database/
│   │   └── tb_data.db                    # SQLite database (created after running notebooks)
│   └── raw/
│       └── *.csv                         # Raw CSV exports (created after running notebooks)
├── requirements.txt                      # Python dependencies
└── README.md                             # This file
```

## Usage

### Step 1: Acquire WHO Data

Open and run `notebooks/WHO_Data.ipynb`:

1. Run all cells sequentially
2. This will:
   - Create the database schema
   - Fetch TB incidence and mortality data from WHO API (2020-2025)
   - Fetch HIV case data from WHO API (2020-2025)
   - Load all data into SQLite database
   - Create `country_metadata`, `tb_data`, and `hiv_data` tables

**Note:** This process may take 10-15 minutes depending on API response times.

### Step 2: Acquire World Bank Data

Open and run `notebooks/WorldBank_Data.ipynb`:

1. Run all cells sequentially
2. This will:
   - Fetch GDP, poverty rates, and population data from World Bank API
   - Load data into `country_data` table
   - Match countries using ISO country codes

**Note:** This process may take 15-20 minutes depending on API response times.

### Step 3: Perform Analysis

Open and run `notebooks/DataProcessingAndMachineLearning.ipynb`:

1. Run all cells sequentially
2. This will:
   - Join WHO TB data, World Bank data, and HIV data
   - Clean and prepare data for analysis
   - Perform imputation for missing values
   - Run Linear Regression models
   - Run Random Forest models
   - Perform ANOVA tests
   - Display comparison results

## Data Sources

### WHO GHO API
- **Endpoint**: `https://ghoapi.azureedge.net/api`
- **Indicators**:
  - `TB_e_inc_tbhiv_num`: TB incidence (number of cases)
  - `TB_e_mort_exc_tbhiv_num`: TB mortality (number of deaths)
  - `HIV_0000000026`: HIV cases

### World Bank API
- **Endpoint**: `http://api.worldbank.org/v2/`
- **Indicators**:
  - `NY.GDP.MKTP.CD`: GDP (current US$)
  - `SI.POV.DDAY`: Poverty rate (% of population)
  - `SP.POP.TOTL`: Total population

## Database Schema

The SQLite database (`data/database/tb_data.db`) contains the following tables:

- **`country_metadata`**: Country codes, region codes, and region names
- **`tb_data`**: TB incidence and mortality data by country and year
- **`hiv_data`**: HIV case data by country and year
- **`country_data`**: GDP, poverty rates, and population by country
- **`unified_tb_data`**: View joining TB data with country metadata
- **`final_data`**: Joined table for analysis (created in ML notebook)

## Analysis Results

The project performs the following analyses:

1. **Linear Regression**: Predicts TB outcomes using economic and regional features
2. **Random Forest**: Non-linear modeling of TB outcomes
3. **ANOVA Tests**: Statistical significance testing for features

All results are displayed in the `DataProcessingAndMachineLearning.ipynb` notebook, including:
- R² scores for each model
- RMSE and MAE metrics
- Feature importance
- ANOVA p-values for statistical significance

## Troubleshooting

### Database Locked Error
If you encounter "database is locked" errors:
1. Close all notebook connections to the database
2. Restart the Jupyter kernel
3. Try again

### API Rate Limiting
If API calls fail:
1. Wait a few minutes before retrying
2. The notebooks include retry logic, but you may need to wait longer

### Missing Data
Some countries may have missing data for certain indicators. The ML notebook includes imputation logic to handle zeros and missing values using regional medians.

## Requirements

See `requirements.txt` for the complete list of Python packages and versions.

## License

[Add your license information here]

## Contact

[Add your contact information here]
