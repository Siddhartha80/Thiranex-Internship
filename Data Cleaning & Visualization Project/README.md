# Data Cleaning & Visualization: Ames Housing Prices

![Python](https://img.shields.io/badge/Python-3.12-3776AB?logo=python&logoColor=white)
![pandas](https://img.shields.io/badge/pandas-data%20cleaning-150458?logo=pandas&logoColor=white)
![Seaborn](https://img.shields.io/badge/Seaborn-visualization-4C72B0)

## Overview

This project cleans and explores the Ames Housing dataset to understand which property characteristics drive sale price. It covers the full exploratory workflow: profiling missing data, imputing and dropping columns, removing duplicates and outliers, engineering a new feature, and building a set of visualizations that surface the main price drivers.

**Notebook:** [`Data Cleaning & Visualization Project.ipynb`](Data%20Cleaning%20%26%20Visualization%20Project.ipynb)

## Dataset

[House Prices: Advanced Regression Techniques](https://www.kaggle.com/competitions/house-prices-advanced-regression-techniques) (`train.csv`): **1,460 rows and 81 columns** describing residential homes in Ames, Iowa, including lot size, quality ratings, living area, garage, basement, and sale details. The target is `SalePrice`.

> The data is not stored in this repository. Download `train.csv` from Kaggle and update the path in the first `pd.read_csv` cell if you are not running on Kaggle.

## Workflow

### 1. Data cleaning
| Step | Approach |
|------|----------|
| Missing-value profiling | Counted nulls per column (top offenders: `PoolQC` 1,453, `MiscFeature` 1,406, `Alley` 1,369, `Fence` 1,179) |
| Numeric imputation | `LotFrontage` filled with the median; `MasVnrArea` filled with 0 |
| Categorical imputation | Remaining object columns filled with the mode |
| Column removal | Dropped `Alley`, `PoolQC`, `Fence`, `MiscFeature` (more than 80% missing) |
| Duplicates | Removed with `drop_duplicates` |
| Outliers | Inspected `SalePrice` with a boxplot, then kept homes priced below $300,000 |

### 2. Feature engineering
- `TotalBath` = `FullBath` + 0.5 × `HalfBath`
- `LogPrice` = `log1p(SalePrice)` to examine the effect of a log transform on skewness

### 3. Visualization
- Sale price distribution (histogram with KDE) and boxplot
- Correlation heatmap across all numeric features
- Living area, garage area, and basement area vs. price (scatter plots)
- Overall quality and overall condition vs. price (bar plots)
- Neighborhood and sale condition vs. price (box plots)
- Year built vs. price (line plot) and house style distribution
- Pair plot of `SalePrice`, `GrLivArea`, `OverallQual`, `GarageArea`

## Key Findings

The five features most correlated with `SalePrice` (after cleaning):

| Feature | Correlation |
|---------|-------------|
| `OverallQual` | 0.76 |
| `GrLivArea` | 0.63 |
| `GarageCars` | 0.61 |
| `FullBath` | 0.58 |
| `GarageArea` | 0.58 |

- **Build quality and living area** are the strongest drivers of price.
- Garage capacity and size also carry a strong positive relationship with price.
- Skewness of `SalePrice` was 0.43 before and -0.52 after the log transform. Because outliers had already been trimmed, the original skew was mild, so the log transform slightly over-corrected rather than improved it.

## Limitations

- Capping `SalePrice` at $300,000 removes the high end of the market, so conclusions apply to mid-range homes rather than luxury properties.
- Filling missing categorical values with the mode treats "not present" (e.g., no garage) the same as "most common value". For columns where `NA` means the feature is absent, a dedicated "None" category would be more faithful to the data.

## Tech Stack

Python · pandas · NumPy · Matplotlib · Seaborn
