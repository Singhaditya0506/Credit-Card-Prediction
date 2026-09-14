# Credit Card Consumption Prediction

## Overview
This project analyzes customer-level credit card usage patterns and develops regression models to predict the target variable `cc_cons`. The workflow combines three customer-related Excel datasets, cleans and transforms the data, and compares several regression approaches.

## Problem Statement
Credit card consumption varies significantly across customers. The project aims to predict a customer’s credit card consumption using behavioral, demographic, and consumption-related features so that usage can be better understood and estimated from available customer information.

## Objective
The primary objective is to build a reliable regressor for `cc_cons` using customer data while keeping the workflow transparent and reproducible.

## Dataset
The notebook uses three Excel files that were originally stored locally as part of the project:

- `CreditConsumptionData.xlsx`
- `CustomerBehaviorData.xlsx`
- `CustomerDemographics.xlsx`

These files are not included in this public repository. The project expects them to be placed in the `data/` folder before running the notebook.

The target variable is `cc_cons`.

Important features in the merged dataset include customer identifiers, transaction behavior, account status, demographic variables, and consumption metrics. The exact set of columns is defined in the notebook during the merge and preprocessing workflow.

## Technologies Used
- Python
- pandas
- NumPy
- Matplotlib
- scikit-learn
- statsmodels
- openpyxl

## Project Workflow
Data
→ Cleaning
→ EDA
→ Feature Engineering
→ Modeling
→ Evaluation
→ Results

## Models Used
- Linear Regression
- K-Nearest Neighbors Regressor
- Decision Tree Regressor

## Evaluation Metrics
The notebook uses RMSPE (Root Mean Squared Percentage Error), which is calculated as:

RMSPE = sqrt(mean(((y_true - y_pred) / y_true)^2)) * 100

This metric is used for both training and test performance comparisons.

## Results
The notebook evaluates model performance using train and test RMSPE values. Exact results are generated when the project is run locally with the dataset files available. The model comparison and final metric values remain in the notebook outputs rather than a separate persisted report.

## Key Insights
- Missing values were handled with median and mode imputation depending on the feature type.
- Outliers were clipped using an IQR-based method to reduce skewed extreme values.
- Categorical variables were converted to numeric format using one-hot encoding.
- A train/test split was created using a fixed random state to keep the analysis reproducible.
- Feature scaling was applied before the distance-based KNN models.

## Visualizations
The notebook includes exploratory boxplots and summary statistics for key variables, especially customer behavior and demographic distributions. These plots are intended to support the outlier handling and feature analysis steps.

## Repository Structure

```text
Credit_card_prediction/
├── README.md
├── requirements.txt
├── .gitignore
├── data/
│   └── README.md
├── notebooks/
│   └── Cred_card_pred.ipynb
└── .gitignore
```

## Installation
Install project dependencies:

```bash
pip install -r requirements.txt
```

## Usage
1. Place the three Excel files in the `data/` folder.
2. Open the notebook in `notebooks/Cred_card_pred.ipynb`.
3. Run the cells sequentially from top to bottom.

## Limitations
- The original dataset files are not included in this repository.
- The project uses a local Excel dataset rather than a public benchmark dataset.
- The notebook is primarily an exploratory and model-comparison workflow, not a packaged production pipeline.
- No model artifact or deployment pipeline is included.

## Future Improvements
- Add a more structured model comparison table in the notebook.
- Save final evaluation metrics to a CSV file for easier reporting.
- Experiment with additional regression models such as Random Forest, XGBoost, or LightGBM.
- Add a lightweight feature importance summary for recruiter-friendly presentation.

## Author
- GitHub: [https://github.com/Singhaditya0506]
- LinkedIn: [https://www.linkedin.com/in/aditya-singh-analytics/]

---

This repository is intentionally kept simple and notebook-focused so the analytical story remains easy to understand for recruiters and hiring managers.
