🏥 Hospital Patient Recovery Analytics Dashboard
> **Transforming raw patient records into actionable clinical intelligence combining statistical rigor, machine learning, and interactive visualization.**
![Python](https://img.shields.io/badge/Python-3.10%2B-3776AB?logo=python&logoColor=white)
![Power BI](https://img.shields.io/badge/Power_BI-Dashboard-F2C811?logo=powerbi&logoColor=black)
![Excel](https://img.shields.io/badge/Excel-Pivot_Analytics-217346?logo=microsoftexcel&logoColor=white)
![scikit-learn](https://img.shields.io/badge/scikit--learn-ML_Clustering-F7931E?logo=scikit-learn&logoColor=white)
![pandas](https://img.shields.io/badge/pandas-Data_Wrangling-150458?logo=pandas&logoColor=white)
![License: MIT](https://img.shields.io/badge/License-MIT-green.svg)


# 🏥 Hospital Patient Recovery Analysis

<div align="center">

![Python](https://img.shields.io/badge/Python-3.10%2B-3776AB?style=for-the-badge&logo=python&logoColor=white)
![Jupyter](https://img.shields.io/badge/Jupyter-Notebook-F37626?style=for-the-badge&logo=jupyter&logoColor=white)
![Scikit-Learn](https://img.shields.io/badge/Scikit--Learn-ML-F7931E?style=for-the-badge&logo=scikit-learn&logoColor=white)
![Pandas](https://img.shields.io/badge/Pandas-Data-150458?style=for-the-badge&logo=pandas&logoColor=white)
![Status](https://img.shields.io/badge/Status-Complete-brightgreen?style=for-the-badge)

**End-to-end data science project** · Exploratory Data Analysis · Statistical Hypothesis Testing · Machine Learning Regression

[Overview](#-project-overview) · [Dataset](#-dataset) · [EDA](#-exploratory-data-analysis) · [Statistics](#-statistical-analysis) · [ML Models](#-machine-learning) · [Results](#-key-results) · [Setup](#-setup)

</div>

---

## 📌 Project Overview

This project performs a **comprehensive clinical data analysis** on a hospital patient treatment dataset to uncover factors that influence patient recovery. It follows a structured data science pipeline from raw data ingestion through to predictive machine learning modelling.

### 🎯 Objectives
- Understand distributions and relationships in patient-level clinical data
- Apply rigorous statistical hypothesis tests to identify significant group differences
- Build and compare multiple regression models to predict the **Recovery Score**
- Derive actionable, evidence-based insights for clinical decision-making

---

## 📂 Dataset

| Property | Detail |
|---|---|
| **File** | `hospital_patient_treatment_dataset.csv` |
| **Records** | 200 patients |
| **Features** | 9 columns |
| **Target** | `Recovery Score` (range 40–100) |
| **Missing Values** | ✅ None |

### Feature Descriptions

| Feature | Type | Description |
|---|---|---|
| `Patient ID` | Categorical | Unique patient identifier |
| `Department` | Categorical | Medical department (6 departments) |
| `Treatment Type` | Categorical | Medication / Surgery / Therapy / Observation |
| `Doctor Name` | Categorical | Attending physician |
| `Gender` | Categorical | Male / Female / Other |
| `Age` | Numerical | Patient age in years (1–90) |
| `Treatment Cost` | Numerical | Total cost in ₹ (₹5,444 – ₹1,49,340) |
| `Hospital Stay (Days)` | Numerical | Length of inpatient stay (1–30 days) |
| `Recovery Score` | **Target** | Patient recovery outcome (40–100) |

---

## 📊 Exploratory Data Analysis

### Dataset Overview – Categorical Distributions
![Dataset Overview](images/01_dataset_overview.png)

> Gastroenterology leads in patient count (41), while Cardiology has the fewest (24). Treatment types are roughly balanced, with Medication slightly more common (55 patients). Gender distribution spans Male (81), Other (62), and Female (57).

---

### Numerical Feature Distributions
![Numerical Distributions](images/02_numerical_distributions.png)

> **Key observations:**
> - **Age** is uniformly distributed (1–90 yrs), reflecting a diverse patient population
> - **Treatment Cost** is right-skewed — a small subset of patients incur very high costs
> - **Hospital Stay** is nearly uniform across 1–30 days
> - **Recovery Score** is approximately normal (mean ≈ 70.4, std ≈ 17.7)

---

### Pearson Correlation Matrix
![Correlation Heatmap](images/03_correlation_heatmap.png)

> All pairwise correlations between numerical features are **weak (|r| < 0.15)**, indicating low multicollinearity and that no single feature dominates recovery prediction. This suggests non-linear relationships that tree-based models are better suited to capture.

---

### Recovery Score by Department
![Recovery by Department](images/04_recovery_by_department.png)

> Recovery scores are relatively consistent across departments (mean ≈ 68–73), with overlapping IQRs. Diamond markers indicate group means. ANOVA confirms no statistically significant departmental effect (see Statistical Analysis).

---

### Recovery Score by Treatment Type
![Recovery by Treatment](images/05_recovery_by_treatment.png)

> The violin plots reveal similar recovery distributions across all four treatment types. The width of each violin indicates density — Medication and Therapy show slightly broader spread at higher recovery values.

---

### Key Features vs Recovery Score
![Scatter Plots](images/06_scatter_vs_recovery.png)

> Trend lines and Pearson r values confirm that Age (r=0.041), Treatment Cost (r=0.089), and Hospital Stay (r=0.125) all have **weak, non-significant linear relationships** with Recovery Score, highlighting the complexity of recovery prediction.

---

### Department × Treatment Type – Mean Recovery Heatmap
![Dept Treatment Heatmap](images/07_dept_treatment_heatmap.png)

> The interaction heatmap reveals nuanced patterns invisible in univariate analysis — e.g., Oncology patients receiving Observation therapy show relatively higher mean recovery than Surgery within the same department. These interactions motivate the use of ensemble ML models.

---

### Age Group Analysis
![Age Group Analysis](images/08_age_group_analysis.png)

> Recovery scores (±1 std) are broadly consistent across age groups, but **Elderly patients (76+) show greater variability in treatment cost**, suggesting more complex or prolonged care needs. Children show tighter cost distributions, implying more standardised paediatric protocols.

---

## 📐 Statistical Analysis

### Statistical Tests Summary
![Statistical Tests](images/09_statistical_tests_summary.png)

### Hypothesis Tests in Detail

#### 1. 🔬 Shapiro-Wilk Normality Test
```
H₀: Recovery Score is normally distributed
W = 0.951, p < 0.0001 → ❌ Reject H₀ (non-normal)
```
Despite appearing bell-shaped, the Recovery Score distribution deviates from strict normality, justifying the use of robust non-parametric checks alongside parametric tests.

---

#### 2. 📊 Independent T-Test – Recovery Score by Gender
```
H₀: Mean Recovery Score is equal for Male and Female patients
Levene's test: equal variances assumed
t = 0.216, p = 0.8295 → ❌ Fail to reject H₀
```
**No significant difference** in recovery between male and female patients. Gender alone is not a predictor of recovery outcome in this dataset.

---

#### 3. 📈 One-Way ANOVA – Recovery Score by Department
```
H₀: Mean Recovery Score is equal across all departments
F = 0.833, p = 0.5276 → ❌ Fail to reject H₀
```
No statistically significant variation in Recovery Score across departments (Gastroenterology, Pediatrics, Orthopedics, Oncology, Neurology, Cardiology). Post-hoc Tukey HSD was not required.

---

#### 4. 📈 One-Way ANOVA – Recovery Score by Treatment Type
```
H₀: Mean Recovery Score is equal across all treatment types
Tested across: Medication, Surgery, Therapy, Observation
```
Results indicate treatment type does not significantly differentiate recovery outcomes at α = 0.05.

---

#### 5. 🔗 Correlation Analysis

| Feature | Pearson r | p-value | Significant? |
|---|---|---|---|
| Age | 0.041 | 0.567 | ❌ No |
| Treatment Cost | 0.089 | 0.211 | ❌ No |
| Hospital Stay (Days) | 0.125 | 0.079 | ❌ No |

> None of the numerical features show a statistically significant linear correlation with Recovery Score. This is a crucial finding — it indicates that **recovery is governed by complex, non-linear interactions**, not by any single measurable variable. This motivates the use of ensemble methods over linear regression.

---

#### 6. 🧮 Chi-Square Test – Department vs Treatment Type
Tests whether treatment type selection is independent of department, revealing potential departmental treatment preferences.

---

## 🤖 Machine Learning

### Approach

A multi-model regression framework was implemented to predict `Recovery Score`, comparing linear and non-linear approaches.

```
Pipeline:
Raw Data → Label Encoding → Train/Test Split (80/20) → StandardScaling → Model Training → Evaluation
```

### Models Trained

| Model | Type | Hyperparameters |
|---|---|---|
| Linear Regression | Linear | Default |
| Ridge Regression | Regularised Linear | α = 1.0 |
| Lasso Regression | Regularised Linear | α = 1.0 |
| Decision Tree | Non-linear | max_depth = 5 |
| Random Forest | Ensemble | n_estimators = 200 |
| Gradient Boosting | Ensemble | n_estimators = 100 |

### Model Comparison
![Model Comparison](images/10_model_comparison.png)

### Best Model – Diagnostics
![Model Diagnostics](images/11_best_model_diagnostics.png)

### Feature Importance (Random Forest)
![Feature Importance](images/12_feature_importance.png)

---

## 📋 Key Results

### Model Performance Summary

| Model | R² | RMSE | MAE |
|---|---|---|---|
| Linear Regression | -0.031 | 19.69 | 17.37 |
| Ridge Regression | -0.031 | 19.69 | 17.38 |
| Lasso Regression | -0.064 | 20.01 | 17.68 |
| Decision Tree | -0.145 | 20.75 | 17.84 |
| **Random Forest** | **-0.161** | **20.90** | **18.60** |
| Gradient Boosting | -0.390 | 22.87 | 20.14 |

> ⚠️ **Important Finding:** All models yield negative R² scores, indicating that the features in this dataset do not carry sufficient predictive signal to outperform a simple mean-baseline model for Recovery Score. This is consistent with the near-zero correlations observed during statistical analysis and underscores a key real-world insight: **recovery is inherently multi-factorial and likely driven by unmeasured clinical variables** (diagnosis severity, comorbidities, medication response, patient compliance) not present in this dataset.

### 🔍 Analytical Insights

| # | Finding | Evidence |
|---|---|---|
| 1 | Recovery Score follows a non-normal distribution | Shapiro-Wilk: p < 0.0001 |
| 2 | Gender does not significantly affect recovery | T-test: p = 0.83 |
| 3 | Department does not significantly affect recovery | ANOVA: F=0.83, p = 0.53 |
| 4 | No numerical feature linearly predicts recovery | Max Pearson \|r\| = 0.125 |
| 5 | Recovery has complex, non-linear structure | All ML models struggle |
| 6 | Hospital Stay is the strongest (weak) numerical predictor | r = 0.125 |
| 7 | Elderly patients show higher treatment cost variability | Age group boxplot |
| 8 | Treatment type shows no significant recovery differential | ANOVA on treatment groups |

---

## 💡 Recommendations

1. **Enrich the dataset** — collect diagnosis codes (ICD-10), comorbidity indices, discharge status, and medication adherence to improve ML predictive power
2. **Apply dimensionality reduction** (PCA, UMAP) to explore latent patient subgroups that may reveal hidden recovery patterns
3. **Investigate cost outliers** — high-cost, average-recovery patients represent optimisation targets for value-based care strategies
4. **Department-level protocols** — although departmental differences are not statistically significant at α = 0.05, the interaction heatmap (Dept × Treatment) reveals nuanced patterns worth investigating prospectively
5. **Extend to classification** — binarising Recovery Score (e.g., ≥ 70 = "good recovery") may yield better-performing models for clinical decision support

---

## 🛠️ Setup

### Prerequisites
```
Python 3.10+
Jupyter Notebook
```

### Installation

```bash
git clone https://github.com/Dishabhadauria30/Hospital-Recovery-Analysis.git
cd Hospital-Recovery-Analysis
pip install -r requirements.txt
jupyter notebook Hospital_Recovery_Analysis.ipynb
```

### Requirements

```txt
pandas>=1.5.0
numpy>=1.23.0
matplotlib>=3.6.0
seaborn>=0.12.0
scipy>=1.10.0
scikit-learn>=1.2.0
statsmodels>=0.13.0
nbformat>=5.7.0
```

---

## 📁 Repository Structure

```
Hospital-Recovery-Analysis/
│
├── 📓 Hospital_Recovery_Analysis.ipynb   ← Main analysis notebook
├── 📊 hospital_patient_treatment_dataset.csv
├── 📄 README.md
│
└── 📁 images/
    ├── 01_dataset_overview.png
    ├── 02_numerical_distributions.png
    ├── 03_correlation_heatmap.png
    ├── 04_recovery_by_department.png
    ├── 05_recovery_by_treatment.png
    ├── 06_scatter_vs_recovery.png
    ├── 07_dept_treatment_heatmap.png
    ├── 08_age_group_analysis.png
    ├── 09_statistical_tests_summary.png
    ├── 10_model_comparison.png
    ├── 11_best_model_diagnostics.png
    └── 12_feature_importance.png
```

---

## 🧰 Tech Stack

| Category | Tools |
|---|---|
| **Language** | Python 3.10 |
| **Data Manipulation** | Pandas, NumPy |
| **Visualisation** | Matplotlib, Seaborn |
| **Statistical Analysis** | SciPy, Statsmodels |
| **Machine Learning** | Scikit-Learn |
| **Environment** | Jupyter Notebook |

---

## 👩‍💻 Author

**Disha Bhadauria**  
[GitHub](https://github.com/Dishabhadauria30)

---

<div align="center">
⭐ If you found this project useful, please consider giving it a star!
</div>
