# Credit Card Consumption Prediction

## Project Overview

This project uses customer consumption, behavioral, and demographic information to predict credit card consumption. It is a supervised learning regression task with `cc_cons` as the target; it is not a credit-risk classification project.

## Objective

Estimate customer credit card consumption from available customer attributes and compare regression models using a reproducible train/test workflow.

## Dataset

The notebook combines three Excel files on `ID`. The source files are not included in this repository; place authorized copies in `data/` before running the notebook.

| Dataset | Purpose | Example columns | Target |
|---|---|---|---|
| `CreditConsumptionData.xlsx` | Target and customer identifier | `ID`, `cc_cons` | `cc_cons` |
| `CustomerBehaviorData.xlsx` | Customer behavior and account-related attributes | `cc_cons_apr`, `credit_count_apr`, `investment_1`, `loan_enq`, `emi_active` | None |
| `CustomerDemographics.xlsx` | Demographic and channel attributes | `account_type`, `gender`, `age`, `Income`, `region_code` | None |

Column descriptions and the target time horizon are not fully documented. The notebook therefore avoids assigning undocumented meanings to fields and flags temporal leakage as a limitation to resolve.

## Workflow

Load and inspect the three tables → merge and one-hot encode categorical columns → split rows with known targets → cap selected outliers → fill selected missing values → scale features → compare baseline regressors and tuned models.

## Models and Metrics

The notebook evaluates a baseline Linear Regression, K-Nearest Neighbors, Decision Tree, and LightGBM regressors. GridSearchCV uses five folds and its default estimator score; final outputs report training/test RMSE, MSE, and RMSPE. The RMSPE function is used on this dataset, whose labeled targets are nonzero.

The following values were produced by running the restored notebook with the current local files and fixed 20% holdout (`random_state=12`). Linear Regression is the baseline; the other listed models use the final grid-search estimators.

| Model | Train RMSE | Test RMSE | Test RMSPE |
|---|---:|---:|---:|
| Linear Regression (baseline) | 2,657.73 | 2,779.54 | 26.70% |
| KNN (tuned) | 0.00 | 5,182.26 | 67.37% |
| Decision Tree (tuned) | 5,514.11 | 5,604.31 | 77.51% |
| LightGBM (tuned) | 2,792.94 | 3,713.16 | 28.58% |

Linear Regression had the lowest test RMSE among these runs. KNN's zero training error alongside its larger test error indicates overfitting. These results describe one holdout sample and are not a guarantee of future performance.

## Data Preparation

- Categorical object columns are one-hot encoded before the train/test split, matching the original notebook workflow.
- Selected numeric columns are filled with training-set medians; `debit_count_apr` and `emi_active` are filled with training-set modes. The same values are applied to the test set.
- IQR limits are calculated from training data and used to cap selected numeric columns in both splits.
- `StandardScaler` is fit on the training features and then applied to the test features.
- The notebook contains no charts, as requested.

## Repository Structure

```text
Credit_card_prediction/
├── README.md
├── requirements.txt
├── .gitignore
├── data/
│   └── README.md
└── notebooks/
	└── Cred_card_pred.ipynb
```

## Installation and Usage

Install dependencies:

```bash
pip install -r requirements.txt
```

Place the three authorized Excel files in `data/`, open `notebooks/Cred_card_pred.ipynb`, and run the cells from top to bottom. The notebook can be started from the repository root or the `notebooks/` directory. Local data files are excluded from version control by `.gitignore`.

## Limitations and Future Work

The source data is not included, feature definitions and the target horizon are incomplete, and evaluation uses one random holdout rather than an out-of-time test. Because categorical encoding happens before splitting, category discovery uses both training and test rows; this should be moved into a training-fitted preprocessing step before treating the scores as an unbiased estimate. Confirm that monthly predictors precede the target period before interpreting performance for future customers. Further work could add temporal validation, broader cross-validation and tuning, additional behavioral data, explainability, and deployment monitoring.

## Author

- GitHub: [https://github.com/Singhaditya0506]
- LinkedIn: [https://www.linkedin.com/in/aditya-singh-analytics/]
