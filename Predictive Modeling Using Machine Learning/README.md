# Predictive Modeling: House Price Regression

![Python](https://img.shields.io/badge/Python-3.12-3776AB?logo=python&logoColor=white)
![scikit-learn](https://img.shields.io/badge/scikit--learn-regression-F7931E?logo=scikitlearn&logoColor=white)

## Overview

This project predicts house sale prices from the Ames Housing dataset. It cleans the data, engineers a total-square-footage feature, and compares three regression models (Linear Regression, Decision Tree, and Random Forest) on held-out data using RMSE and R².

**Notebook:** [`predictive-modeling-using-machine-learning.ipynb`](predictive-modeling-using-machine-learning.ipynb)

## Dataset

[House Prices: Advanced Regression Techniques](https://www.kaggle.com/competitions/house-prices-advanced-regression-techniques) (`train.csv`): 1,460 homes with 81 columns. The target is `SalePrice`.

> The data is not stored in this repository. Download `train.csv` from Kaggle and update the path in the first `pd.read_csv` cell if you are not running on Kaggle.

## Workflow

1. **Cleaning:** dropped `Alley`, `PoolQC`, `Fence`, `MiscFeature` (mostly empty); median imputation for numeric columns; mode imputation for categorical columns; removed duplicates; kept homes with `SalePrice` below $300,000.
2. **Feature engineering:** `TotalSF` = `TotalBsmtSF` + `1stFlrSF` + `2ndFlrSF`.
3. **Encoding:** categorical columns converted to integer codes with `LabelEncoder`.
4. **Split:** 80% train / 20% test, `random_state=42`.
5. **Modeling:** three regressors trained and compared:
   - Linear Regression
   - Decision Tree (`max_depth=5`)
   - Random Forest (`n_estimators=100`)
6. **Evaluation:** RMSE and R² on the test set, an actual-vs-predicted scatter plot, and a top-10 feature importance chart for the Random Forest.

## Results

| Model | RMSE | R² |
|-------|------|----|
| Linear Regression | $24,391 | 0.772 |
| Decision Tree (depth 5) | $26,378 | 0.733 |
| **Random Forest** | **$20,305** | **0.842** |

The Random Forest performs best, explaining about 84% of the variance in sale price with an average error of roughly $20K. It improves on the linear baseline because it can capture non-linear relationships and interactions between features.

## Limitations and Next Steps

- Models are trained and evaluated only on homes under $300,000, so they should not be expected to price high-end properties well.
- `LabelEncoder` assigns arbitrary integer order to nominal categories. One-hot or target encoding would likely suit linear models better.
- Hyperparameters were not tuned, and evaluation uses a single train/test split. Cross-validation and a grid or random search would give a more reliable estimate.
- Next steps: try gradient boosting (XGBoost, LightGBM), regularized linear models (Ridge, Lasso), and a log-transformed target.

## Tech Stack

Python · pandas · NumPy · Matplotlib · Seaborn · scikit-learn
