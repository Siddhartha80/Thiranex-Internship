# Diabetes Risk Prediction: Pima Indians Dataset

![Python](https://img.shields.io/badge/Python-3.12-3776AB?logo=python&logoColor=white)
![scikit-learn](https://img.shields.io/badge/scikit--learn-classification-F7931E?logo=scikitlearn&logoColor=white)
![XGBoost](https://img.shields.io/badge/XGBoost-ensemble-189AB4)

## Overview

This project predicts whether a patient has diabetes from diagnostic measurements such as glucose level, BMI, and age. It follows an end-to-end workflow: preprocessing, exploratory analysis, a logistic regression baseline, and then an improved pipeline built around feature engineering, hyperparameter tuning, and a model ensemble.

**Notebook:** [`pima-indians-diabetes.ipynb`](pima-indians-diabetes.ipynb)

## Dataset

[Pima Indians Diabetes Dataset](https://www.kaggle.com/datasets/jamaltariqcheema/pima-indians-diabetes-dataset) (`diabetes.csv`): 768 patients, 8 predictors, and a binary target.

| Feature | Description |
|---------|-------------|
| `Pregnancies` | Number of pregnancies |
| `Glucose` | Plasma glucose concentration |
| `BloodPressure` | Diastolic blood pressure |
| `SkinThickness` | Triceps skinfold thickness |
| `Insulin` | Serum insulin |
| `BMI` | Body mass index |
| `DiabetesPedigreeFunction` | Genetic risk score based on family history |
| `Age` | Age in years |
| `Outcome` | **Target**: 0 = no diabetes, 1 = diabetes |

> The data is not stored in this repository. Download `diabetes.csv` from Kaggle and update the path in the data-loading cell if you are not running on Kaggle.

## Workflow

### Part 1: Baseline
1. **Preprocessing:** zeros in `Glucose`, `BloodPressure`, `SkinThickness`, `Insulin`, and `BMI` are physiologically invalid, so they were replaced with the column median.
2. **EDA:** correlation heatmap and feature distribution histograms.
3. **Model:** 80/20 train-test split, `StandardScaler`, and Logistic Regression.
4. **Evaluation:** accuracy, classification report, and confusion matrix.

### Part 2: Improved pipeline
1. **Imputation:** invalid zeros set to missing and filled with `KNNImputer` (k = 5), which uses similar patients rather than a single global median.
2. **Feature engineering:** `BMI_Age` (BMI × Age) and `Glucose_Insulin` (Glucose × Insulin).
3. **Split:** stratified 80/20 split so both sets keep the same class balance.
4. **Tuning:** `GridSearchCV` (5-fold) over a Random Forest (`n_estimators` in {100, 200}, `max_depth` in {5, 10, None}).
5. **Ensemble:** soft-voting classifier combining the tuned Random Forest, Gradient Boosting, and XGBoost.

## Results

Evaluated on the held-out 20% test set (154 patients):

| Model | Accuracy | Precision (diabetic) | Recall (diabetic) | F1 (diabetic) |
|-------|----------|----------------------|-------------------|---------------|
| Logistic Regression (baseline) | 77.3% | 0.69 | 0.65 | 0.67 |
| **Voting ensemble (RF + GB + XGBoost)** | **89.6%** | **0.85** | **0.85** | **0.85** |

The ensemble improves recall on the diabetic class from 0.65 to 0.85, which matters in a screening setting where missing a true case is costly.

## Limitations and Next Steps

- In the improved pipeline, `KNNImputer` is fitted on the full dataset before the train/test split, which can leak a small amount of test-set information into training. The 89.6% figure may therefore be somewhat optimistic. Wrapping the imputer in a scikit-learn `Pipeline` and cross-validating would give a cleaner estimate. (The scaler is already fitted on the training data only.)
- The test set is small (154 patients), so a single split produces noisy estimates. Repeated or stratified k-fold cross-validation is recommended.
- Next steps: add a feature importance / SHAP analysis to explain predictions, report ROC-AUC, and tune the decision threshold for recall.

## Tech Stack

Python · pandas · NumPy · Matplotlib · Seaborn · scikit-learn · XGBoost
