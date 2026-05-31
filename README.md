# 💉 Flu Shot Learning: Predicting H1N1 and Seasonal Flu Vaccines

> Academic project — **Applied Machine Learning**
> City College Dublin | Data Analytics Program | 2026

[![Grade](https://img.shields.io/badge/Grade-78%2F100-success?style=flat-square)](#-grade--feedback)
[![Python](https://img.shields.io/badge/Python-3776AB?style=flat-square&logo=python&logoColor=white)](https://www.python.org)
[![scikit-learn](https://img.shields.io/badge/scikit--learn-F7931E?style=flat-square&logo=scikit-learn&logoColor=white)](https://scikit-learn.org)
[![Jupyter](https://img.shields.io/badge/Jupyter-F37626?style=flat-square&logo=jupyter&logoColor=white)](https://jupyter.org)

---

## 📋 Overview

This project builds and evaluates machine learning models to predict whether individuals received the **H1N1** and **seasonal flu** vaccines, based on the 2009 U.S. National H1N1 Flu Survey. The goal: help public health teams identify individuals with a low probability of vaccination so outreach can be targeted effectively.

The work follows the **CRISP-DM** methodology end-to-end — from business understanding and data preprocessing through modeling, hyperparameter tuning, and business-impact evaluation.

**Dataset:** [DrivenData — Flu Shot Learning](https://www.drivendata.org/competitions/66/flu-shot-learning/) (26,707 respondents, 35 features, 2 binary targets)

---

## 🎯 Problem & Approach

Influenza vaccination coverage remains low despite vaccine availability. A predictive model that flags individuals unlikely to vaccinate allows health services to direct limited resources where they matter most.

This is a **dual binary classification** problem:
- Target 1: `h1n1_vaccine` (received H1N1 vaccine — yes/no)
- Target 2: `seasonal_vaccine` (received seasonal vaccine — yes/no)

---

## 🔬 Methodology (CRISP-DM)

```
Business Understanding → Data Understanding → Data Preparation
        → Modeling → Evaluation → (Deployment design)
```

1. **Data Preparation** — median imputation (numerical), mode/"unknown" imputation (categorical), one-hot encoding, StandardScaler, stratified 60/20/20 train/validation/test split
2. **Modeling** — baseline Logistic Regression, then GridSearchCV tuning across `C ∈ {0.001…100}`, `penalty ∈ {L1, L2}`, `solver ∈ {liblinear, saga}` with 5-fold stratified cross-validation; Random Forest as a comparison model
3. **Evaluation** — ROC-AUC, F1, precision, recall; confusion-matrix and threshold-optimization analysis; business-impact framing (false positive vs false negative costs)

---

## 📊 Key Results

| Target | Model | ROC-AUC |
|--------|-------|---------|
| H1N1 | Logistic Regression (tuned) | ~0.84 |
| H1N1 | Random Forest | ~0.86 |
| Seasonal | Logistic Regression (tuned) | ~0.86 |
| Seasonal | Random Forest | ~0.85 |

**Key findings:**
- Hyperparameter tuning produced only marginal gains (Δ ROC-AUC +0.0046 for H1N1, +0.0008 for seasonal) — suggesting scikit-learn defaults are already near-optimal for this dataset
- The H1N1 target has a **78.8% class imbalance**, producing a precision–recall gap that points to systematic under-identification of the vaccinated minority class
- **Doctor recommendation** emerged as one of the strongest predictors of vaccine uptake for both targets

---

## 💼 Business Impact Analysis

The project frames model errors in real-world public health terms:

- **False Positive** (predicted vaccinated, actually not) → wasted outreach: < €10 per person
- **False Negative** (missed someone who would benefit from outreach) → preventable transmission, treatment, productivity loss: > €1,000 per case

Because false negatives are far costlier, the analysis recommends **lowering the classification threshold (0.3–0.4)** to maximize recall, accepting more false positives for greater public-health benefit.

**Deployment design** (conceptual): REST API integration with Electronic Health Record systems for real-time risk stratification during appointments, plus weekly model retraining to handle concept drift in vaccination attitudes.

---

## 📈 Exploratory Visualizations

The analysis includes 10 visualizations (5 univariate, 5 multivariate):

- Age group distribution, vaccine uptake distributions, risk perception, concern levels
- Correlation heatmap, doctor-recommendation vs uptake (stacked bars), missing-values heatmap, key-predictor pairplot

---

## 📁 Repository Structure

```
flu-shot-ml-prediction/
├── README.md
├── requirements.txt
├── .gitignore
├── notebooks/
│   ├── 01_full_analysis.ipynb       # Complete pipeline: Q3 preprocessing → Q4 modeling → Q5 evaluation
│   └── 02_model_comparison.ipynb    # LR vs Random Forest comparison (both targets)
└── report/
    ├── 01_business_methodology.pdf  # Business problem + CRISP-DM methodology
    └── 02_modelling_evaluation.pdf  # GridSearchCV, metrics, business impact
```

---

## 🚀 How to Run

```bash
# 1. Install dependencies
pip install -r requirements.txt

# 2. Download the dataset from DrivenData and place the CSVs in notebooks/
#    - training_set_features.csv
#    - training_set_labels.csv
#    (https://www.drivendata.org/competitions/66/flu-shot-learning/)

# 3. Launch Jupyter
jupyter notebook

# 4. Open and run notebooks/01_full_analysis.ipynb top to bottom
```

> **Note:** The dataset CSVs are not included in this repository — they belong to the DrivenData competition and must be downloaded from the source.

---

## 🛠️ Tech Stack

**Python** · **pandas** · **NumPy** · **scikit-learn** (LogisticRegression, RandomForest, GridSearchCV, StratifiedKFold) · **matplotlib** · **seaborn** · **missingno**

---

## 🎓 Grade & Feedback

**Final Grade: 78/100**

Selected highlights from the lecturer's feedback:

**Modelling & GridSearchCV (23/25):**
> *"LR with a wide GridSearchCV grid... the delta improvements are produced precisely at +0.0046 for H1N1 and +0.0008 for seasonal. The three limitations of the model (linearity assumption, class imbalance with asymmetric precision and recall, and sensitivity to scaling and multicollinearity) are all clearly stated with supporting references."*

**Evaluation & Conclusions (10/10):**
> *"The business impact analysis is really good, quantifying FP costs at less than €10 per person and FN costs at over €1,000... an excellent level of applied business framing."*

**Code artefact (well commented, fully executable):**
> *"Well commented code and use of markdowns. Good job. Fully executable."*

**Areas identified for improvement** (incorporated as learnings): evaluating the final model on the held-out test set (not only validation), including the full metrics table in the report, and detailing the data source and drift monitoring for the retraining pipeline.

---

## 📚 Course Details

| | |
|---|---|
| **Course** | Applied Machine Learning |
| **Program** | Data Analytics |
| **Institution** | City College Dublin |
| **Year** | 2026 |

---

## 👤 Author

**Marcelo da Fonseca Oliveira**
Data Analytics @ City College Dublin 🇮🇪

[![LinkedIn](https://img.shields.io/badge/LinkedIn-0077B5?style=flat&logo=linkedin&logoColor=white)](https://www.linkedin.com/in/ofonsecamarcelo)

---

*Academic project submitted as coursework. Dataset courtesy of DrivenData's "Flu Shot Learning" competition (U.S. National 2009 H1N1 Flu Survey).*
