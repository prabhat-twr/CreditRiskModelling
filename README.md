# Credit Risk Modelling — Probability of Default Prediction

> **Resume-ready project** showcasing end-to-end machine learning for credit risk assessment in banking & financial services.

---

## 🏦 Project Overview

Built a complete **Credit Risk Modelling pipeline** to predict the probability of loan default for 29,000+ borrowers. The project mirrors real-world workflows used by banks and fintech companies to quantify credit risk, optimize lending decisions, and minimize expected portfolio losses.

**Business Impact:**
- Estimated **expected portfolio loss** at different risk thresholds (e.g., ~$12.2M at threshold 0.40), enabling data-driven lending decisions.
- Compared two industry-standard models — Logistic Regression and XGBoost — and demonstrated that XGBoost produces better-calibrated risk scores, improving default detection.

---

## 🎯 Key Highlights (for Resume)

| Area | Detail |
|------|--------|
| **Domain** | Credit Risk / Banking & Financial Services |
| **Problem Type** | Binary Classification (Default vs. Non-Default) |
| **Dataset Size** | 32,581 records → 29,465 after cleaning; 27 features |
| **Class Distribution** | 78.1% Non-Default / 21.9% Default |
| **Best Model** | XGBoost — stronger discrimination, lower expected loss |
| **Logistic Regression AUC** | **79.95%** |
| **Portfolio Analysis** | Expected Loss = P(Default) × LGD × Exposure at Default |
| **Tools** | Python, Pandas, Scikit-learn, XGBoost, Matplotlib |

---

## 🛠️ Tech Stack & Skills Demonstrated

- **Languages:** Python 3
- **Machine Learning:** Logistic Regression, Gradient Boosted Trees (XGBoost)
- **Libraries:** `pandas`, `numpy`, `scikit-learn`, `xgboost`, `matplotlib`
- **Techniques:**
  - Exploratory Data Analysis (EDA) and outlier removal
  - Missing value imputation (median fill & row dropping)
  - One-Hot Encoding of categorical features
  - Train/test splitting (70/30)
  - ROC-AUC analysis, confusion matrices, precision-recall trade-off
  - Decision threshold optimization
  - Financial risk metric: **Expected Loss = PD × LGD × EAD**
  - Model comparison and selection

---

## 📊 Results

### Logistic Regression (Threshold = 0.50)

| Class | Precision | Recall | F1-Score | Support |
|-------|-----------|--------|----------|---------|
| Non-Default (0) | 0.814 | 0.962 | 0.882 | 9,194 |
| Default (1) | 0.624 | 0.223 | 0.328 | 2,592 |
| **AUC-ROC** | | | **0.7995** | |

### Logistic Regression (Threshold = 0.40 — Optimized)

| Metric | Value |
|--------|-------|
| Confusion Matrix | [[8074, 1120], [1477, 1115]] |
| Expected Portfolio Loss | **~$12.2 Million** |

### XGBoost vs. Logistic Regression — Sample Prediction Comparison

| Record | Actual | XGBoost Probability | Logistic Regression |
|--------|--------|---------------------|---------------------|
| 0 | Non-Default | 0.000036 | ~0.20 |
| 1 | **Default** | **0.990029** | Lower |
| 2 | Non-Default | 0.399850 | — |
| 3 | Non-Default | 0.006196 | — |

> **Takeaway:** XGBoost produces more extreme, confident predictions — probabilities closer to 0 for non-defaults and closer to 1 for defaults — indicating better model separation and calibration. This translates to a lower expected portfolio loss compared to Logistic Regression.

---

## 📁 Project Structure

```
CreditRiskModelling/
│
├── Exploring_and Preparing_Data.ipynb    # EDA, outlier removal, imputation
├── Logistic Regression.ipynb             # LR model, threshold optimization, portfolio loss
├── GradientBoostedTreeUsingXGBoost.ipynb # XGBoost model, comparison with LR
│
└── data/
    ├── raw/
    │   └── cr_loan2.xls                 # Original dataset (32,581 records × 12 features)
    ├── clean/
    │   └── clean.xls                    # Cleaned dataset (post EDA)
    └── final/
        └── final_data.csv               # One-hot encoded, model-ready (29,465 × 27)
```

---

## 🔄 Methodology

```
Raw Data (32,581 records)
        │
        ▼
 EDA & Data Quality
  • Remove age > 100, emp_length > 60
  • Impute emp_length with median
  • Drop rows with null interest rate
        │
        ▼
 Feature Engineering
  • One-hot encode: home_ownership, loan_intent, loan_grade, default_on_file
  • Final: 26 features + 1 target
        │
        ▼
 Model Training (70% train / 30% test)
  ┌─────────────────┐   ┌──────────────────────────┐
  │ Logistic        │   │ XGBoost                  │
  │ Regression      │   │ (Gradient Boosted Trees) │
  └────────┬────────┘   └────────────┬─────────────┘
           │                         │
           └────────────┬────────────┘
                        ▼
          Model Evaluation & Comparison
           • ROC-AUC, Precision, Recall, F1
           • Threshold optimization (~0.275)
           • Expected Loss = PD × LGD × EAD
```

---

## 💡 Key Insights

1. **Interest Rate** is the strongest single predictor of default — higher rate → higher default probability.
2. **Loan-to-Income Ratio** (`loan_percent_income`) strongly correlates with default risk.
3. **Threshold Matters:** At 0.50, the model catches only 22% of actual defaults. Lowering to 0.40 significantly improves default recall, reducing portfolio risk.
4. **XGBoost outperforms Logistic Regression** in prediction confidence and expected loss minimization, making it the preferred model for production deployment.
5. **Class Imbalance** (78% vs. 22%) requires threshold tuning rather than relying on accuracy alone.

---

## 🚀 How to Run

1. **Clone the repository:**
   ```bash
   git clone https://github.com/prabhat-twr/CreditRiskModelling.git
   cd CreditRiskModelling
   ```

2. **Install dependencies:**
   ```bash
   pip install pandas numpy scikit-learn xgboost matplotlib openpyxl jupyter
   ```

3. **Run the notebooks in order:**
   ```
   1. Exploring_and Preparing_Data.ipynb
   2. Logistic Regression.ipynb
   3. GradientBoostedTreeUsingXGBoost.ipynb
   ```

---

## 📌 Resume Summary (Copy-Paste Ready)

> **Credit Risk Modelling | Python, Scikit-learn, XGBoost**
> Developed an end-to-end credit risk pipeline on 32,000+ loan records to predict probability of default. Performed EDA, feature engineering (one-hot encoding, outlier removal, imputation), and trained Logistic Regression and XGBoost classifiers. Achieved AUC-ROC of ~80% with Logistic Regression; XGBoost demonstrated superior discrimination. Implemented financial risk metrics (Expected Loss = PD × LGD × EAD) to quantify portfolio exposure (~$12.2M), enabling threshold-optimized lending decisions.

---

*This project demonstrates applied machine learning skills relevant to roles in Data Science, Risk Analytics, Quantitative Finance, and Financial Technology (FinTech).*
