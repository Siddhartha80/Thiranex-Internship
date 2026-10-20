# Thiranex Data Science Internship

![Python](https://img.shields.io/badge/Python-3.12-3776AB?logo=python&logoColor=white)
![Jupyter](https://img.shields.io/badge/Jupyter-Notebook-F37626?logo=jupyter&logoColor=white)
![pandas](https://img.shields.io/badge/pandas-data%20analysis-150458?logo=pandas&logoColor=white)
![scikit-learn](https://img.shields.io/badge/scikit--learn-machine%20learning-F7931E?logo=scikitlearn&logoColor=white)

A collection of three end-to-end data science projects completed during my Data Science internship at **Thiranex**. Together they cover the core workflow of an applied data scientist: cleaning and exploring raw data, engineering features, and building and evaluating predictive models for both regression and classification.

## Projects at a Glance

| # | Project | Task | Dataset | Best result |
|---|---------|------|---------|-------------|
| 1 | [Data Cleaning & Visualization](Data%20Cleaning%20%26%20Visualization%20Project/) | Exploratory analysis of housing prices | Ames Housing (1,460 rows, 81 columns) | `OverallQual` (r = 0.76) and `GrLivArea` (r = 0.63) are the strongest price correlates |
| 2 | [Predictive Modeling Using Machine Learning](Predictive%20Modeling%20Using%20Machine%20Learning/) | Regression: predict house sale price | Ames Housing | Random Forest: **R² = 0.84**, RMSE ≈ $20.3K |
| 3 | [Pima Indians Diabetes Prediction](Pima%20Indians%20Diabetes%20Dataset/) | Binary classification: diabetes risk | Pima Indians Diabetes (768 patients) | Tuned ensemble: **89.6% accuracy** (logistic regression baseline: 77.3%) |

## Project Summaries

### 1. Data Cleaning & Visualization
Takes the raw Ames Housing training data through a full cleaning and EDA pass: median and mode imputation, dropping sparsely populated columns, duplicate removal, boxplot-based outlier detection, and a set of visualizations (correlation heatmap, scatter plots, box plots, distributions) that reveal which features drive sale price.

### 2. Predictive Modeling Using Machine Learning
Builds on the cleaned housing data. Engineers a `TotalSF` (total square footage) feature, encodes categorical variables, and compares Linear Regression, Decision Tree, and Random Forest regressors using RMSE and R².

### 3. Pima Indians Diabetes Prediction
Starts with a logistic regression baseline, then upgrades to a stronger pipeline: KNN imputation of invalid zero values, engineered interaction features, a grid-searched Random Forest, and a soft-voting ensemble of Random Forest, Gradient Boosting, and XGBoost.

## Repository Structure

```
Thiranex-Internship/
├── Data Cleaning & Visualization Project/
│   ├── Data Cleaning & Visualization Project.ipynb
│   └── README.md
├── Predictive Modeling Using Machine Learning/
│   ├── predictive-modeling-using-machine-learning.ipynb
│   └── README.md
├── Pima Indians Diabetes Dataset/
│   ├── pima-indians-diabetes.ipynb
│   └── README.md
├── requirements.txt
└── README.md
```

## Tech Stack

- **Language:** Python
- **Data processing:** pandas, NumPy
- **Visualization:** Matplotlib, Seaborn
- **Machine learning:** scikit-learn, XGBoost
- **Environment:** Jupyter Notebook / Kaggle Notebooks

## Getting Started

1. **Clone the repository**
   ```bash
   git clone https://github.com/Siddhartha80/Thiranex-Internship.git
   cd Thiranex-Internship
   ```

2. **Install dependencies**
   ```bash
   pip install -r requirements.txt
   ```

3. **Download the datasets** (they are not stored in this repository):
   - [House Prices: Advanced Regression Techniques](https://www.kaggle.com/competitions/house-prices-advanced-regression-techniques) (`train.csv`)
   - [Pima Indians Diabetes Dataset](https://www.kaggle.com/datasets/jamaltariqcheema/pima-indians-diabetes-dataset) (`diabetes.csv`)

4. **Update the data path.** The notebooks were developed on Kaggle and read from `/kaggle/input/...`. To run locally, change the `pd.read_csv(...)` path in each notebook to where you saved the CSV. Running on Kaggle needs no changes.

5. **Launch Jupyter** and open any notebook:
   ```bash
   jupyter notebook
   ```

## Key Takeaways

- Missing values were handled with **median imputation** for numeric columns and **mode imputation** for categorical ones; columns that were almost entirely empty (`Alley`, `PoolQC`, `Fence`, `MiscFeature`) were dropped.
- **Overall quality and living area** show the strongest correlation with house price.
- **Feature engineering** (`TotalSF`, `TotalBath`, `BMI_Age`, `Glucose_Insulin`) was used across the projects to give the models more informative inputs.
- **Ensemble methods** (Random Forest for regression, a voting ensemble for classification) outperformed the simpler linear baselines in both tasks.

## Author

**Siddhartha Mettu**
M.S. Data Science, Arizona State University

[LinkedIn](https://www.linkedin.com/in/siddhartha-mettu/) · [GitHub](https://github.com/Siddhartha80)
