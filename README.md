# Credit Risk Modelling

An end-to-end machine learning project for predicting loan defaults, covering data exploration and cleaning, logistic regression, and gradient boosted trees (XGBoost). The project includes financial impact analysis to translate model performance into real-world expected-loss estimates.

---

## Table of Contents

- [Project Overview](#project-overview)
- [Repository Structure](#repository-structure)
- [Dataset](#dataset)
- [Notebooks](#notebooks)
  - [1. Exploring and Preparing Data](#1-exploring-and-preparing-data)
  - [2. Logistic Regression](#2-logistic-regression)
  - [3. Gradient Boosted Tree Using XGBoost](#3-gradient-boosted-tree-using-xgboost)
- [Models & Results](#models--results)
- [Installation](#installation)
- [Usage](#usage)

---

## Project Overview

Credit risk modelling estimates the probability that a borrower will default on a loan. This project walks through the full ML pipeline:

1. **Data Exploration & Cleaning** – detect and remove outliers, handle missing values, and visualize key patterns.
2. **Logistic Regression** – build univariate and multivariate models, tune the classification threshold, and quantify financial impact.
3. **Gradient Boosted Trees (XGBoost)** – compare a more powerful, non-linear model against logistic regression using portfolio-level expected loss.

---

## Repository Structure

```
CreditRiskModelling/
│
├── data/
│   ├── raw/
│   │   └── cr_loan2.xls          # Original raw dataset
│   ├── clean/
│   │   └── clean.xls             # Cleaned dataset (outliers & nulls removed)
│   └── final/
│       └── final_data.csv        # One-hot encoded dataset ready for modelling
│
├── Exploring_and Preparing_Data.ipynb
├── Logistic Regression.ipynb
└── GradientBoostedTreeUsingXGBoost.ipynb
```

---

## Dataset

| Property | Value |
|---|---|
| Source file | `data/raw/cr_loan2.xls` |
| Final rows | 29,465 loans |
| Final columns | 27 (26 features + 1 target) |
| Target variable | `loan_status` (0 = non-default, 1 = default) |
| Default rate | ~21.94% |

### Features

| Type | Features |
|---|---|
| Numeric (8) | `person_age`, `person_income`, `person_emp_length`, `loan_amnt`, `loan_int_rate`, `loan_percent_income`, `cb_person_cred_hist_length` |
| Categorical (one-hot encoded, 18 columns) | `person_home_ownership` (4), `loan_intent` (6), `loan_grade` (7), `cb_person_default_on_file` (2) |

---

## Notebooks

### 1. Exploring and Preparing Data

**File:** `Exploring_and Preparing_Data.ipynb`

Steps performed:
- Load and inspect `cr_loan2.xls`.
- Visualise distributions (histograms, scatter plots, box plots).
- Detect and remove outliers:
  - `person_emp_length > 60` years.
  - `person_age > 100` years.
- Handle missing values:
  - Fill `person_emp_length` nulls with the median.
  - Drop rows with missing `loan_int_rate`.
- Cross-tabulation analysis of defaults by home ownership, loan grade, and loan intent.
- Save the cleaned dataset to `data/clean/clean.xls`.

### 2. Logistic Regression

**File:** `Logistic Regression.ipynb`

Steps performed:
- One-hot encode categorical features and concatenate with numeric features.
- Save the modelling-ready dataset to `data/final/final_data.csv`.
- Train a **single-feature** logistic regression model on `loan_int_rate`.
- Train a **multi-feature** logistic regression model on all 26 features.
- Evaluate with:
  - Accuracy, Precision, Recall, F1-Score.
  - ROC curve and AUC score (~76%).
  - Confusion matrix at thresholds 0.4 and 0.5.
- Threshold analysis: plot default recall, non-default recall, and accuracy across multiple threshold values to find the optimal cut-off.
- Estimate **expected financial loss** for unfound defaults at each threshold.

### 3. Gradient Boosted Tree Using XGBoost

**File:** `GradientBoostedTreeUsingXGBoost.ipynb`

Steps performed:
- Load `data/final/final_data.csv`.
- Train an `XGBClassifier` (70 / 30 train-test split, `random_state=16`).
- Generate probability-of-default predictions.
- Compute **expected loss** per loan using the formula:

  ```
  Expected Loss = P(Default) × Loss Given Default (LGD) × Exposure at Default (EAD)
  ```

  Assumed LGD = 20% for the portfolio.
- Compare total portfolio expected loss between logistic regression and XGBoost.

---

## Models & Results

| Model | AUC | Notes |
|---|---|---|
| Logistic Regression (single feature) | ~0.72 | `loan_int_rate` only |
| Logistic Regression (all features) | ~0.76 | 26 one-hot encoded features |
| XGBoost (all features) | > LR | Captures non-linear relationships; better probability calibration |

Key takeaway: XGBoost produces more accurate default probabilities and a lower portfolio-level expected loss compared to logistic regression.

---

## Installation

```bash
# Clone the repository
git clone https://github.com/prabhat-twr/CreditRiskModelling.git
cd CreditRiskModelling

# (Optional) create and activate a virtual environment
python -m venv venv
source venv/bin/activate   # Windows: venv\Scripts\activate

# Install dependencies
pip install pandas numpy matplotlib scikit-learn xgboost openpyxl xlrd jupyter
```

---

## Usage

Run the notebooks in order:

```bash
jupyter notebook
```

1. Open and run **`Exploring_and Preparing_Data.ipynb`** – produces `data/clean/clean.xls`.
2. Open and run **`Logistic Regression.ipynb`** – produces `data/final/final_data.csv` and logistic regression results.
3. Open and run **`GradientBoostedTreeUsingXGBoost.ipynb`** – produces XGBoost results and portfolio comparison.
