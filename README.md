🏥 Hospital Patient Recovery Analytics Dashboard
> **Transforming raw patient records into actionable clinical intelligence — combining statistical rigor, machine learning, and interactive visualization.**
![Python](https://img.shields.io/badge/Python-3.10%2B-3776AB?logo=python&logoColor=white)
![Power BI](https://img.shields.io/badge/Power_BI-Dashboard-F2C811?logo=powerbi&logoColor=black)
![Excel](https://img.shields.io/badge/Excel-Pivot_Analytics-217346?logo=microsoftexcel&logoColor=white)
![scikit-learn](https://img.shields.io/badge/scikit--learn-ML_Clustering-F7931E?logo=scikit-learn&logoColor=white)
![pandas](https://img.shields.io/badge/pandas-Data_Wrangling-150458?logo=pandas&logoColor=white)
![License: MIT](https://img.shields.io/badge/License-MIT-green.svg)
---
**Project Overview**

---
This project performs a full-stack analytics pipeline on a 200-patient hospital dataset — from raw Excel data through statistical hypothesis testing to unsupervised machine learning — and surfaces findings through both a Python-generated multi-panel dashboard and a Power BI interactive report.
The dataset covers 6 departments, 5 doctors, and 4 treatment types, tracking recovery scores, treatment costs, hospital stay duration, patient demographics, and more.

**What This Project Does**

---
Layer	What Happens
Data Engineering	Feature engineering — Recovery Efficiency, Cost per Day, Age Bands, High-Performer flag
Exploratory Analysis	KPI summary, distribution analysis, cross-dimensional breakdowns
Statistical Testing	One-way ANOVA (departmental recovery), Pearson correlation (cost vs. recovery)
Machine Learning	K-Means clustering with elbow method, PCA dimensionality reduction, patient segmentation
Visualization	3-figure Python dashboard (9 charts), Power BI interactive report, Excel pivot tables

---
**Key Findings & Insights**

---
**1. Therapy is the Most Recovery-Efficient Treatment**
---
When measuring Recovery Score per Hospital Day, Therapy outperforms Surgery, Medication, and Observation — suggesting it produces faster, more durable outcomes relative to length of stay.

**2. Cardiology Has the Highest High-Performer Rate**
---
45.8% of Cardiology patients achieve a Recovery Score ≥ 80, compared to only 26.3% in Orthopedics — a near 20-point gap that warrants protocol benchmarking across departments.

**3. Higher Cost ≠ Better Recovery**
---
Pearson correlation between Treatment Cost and Recovery Score is r = 0.089 (p = 0.21) — statistically non-significant. Spending more does not reliably improve outcomes. This is a critical insight for cost-optimization strategies.

**4. Dr. M. Patel Leads in Recovery Outcomes**
---
Among all doctors, Dr. M. Patel achieves the highest average recovery score (73.2), consistently outperforming the overall average of 70.4. This creates an opportunity for peer learning and best-practice sharing.

**5. Children/Teens Recover Fastest**
---
Age-banded analysis reveals the youngest cohort (under 18) recovers most effectively. Recovery scores decline progressively with age, with Senior patients (60+) scoring ~8 points lower on average.

**6. ML Identifies 4 Distinct Patient Profiles**
---
K-Means (k=4) segmentation uncovers clinically meaningful patient archetypes:
Segment	Profile
Low-Cost Rapid Recovery	Young patients, short stays, efficient treatment
High-Cost Slow Recovery	Elderly, complex cases, high treatment expenditure
Young Quick Responders	Mid-range cost, high recovery efficiency
Elderly Complex Cases	Long stays, multiple treatment types, moderate recovery

**7. Neurology and Orthopedics Need Attention**
---
Both departments show the lowest high-performer rates (<30%) and below-average Recovery Efficiency scores — flagging these as priority areas for protocol review.

---
**Tools & Technologies**

---
Category	Tool
Languages	Python 3.10+
Data Wrangling	`pandas`, `numpy`
Statistical Analysis	`scipy.stats` (ANOVA, Pearson r, distributions)
Machine Learning	`scikit-learn` (K-Means, PCA, StandardScaler)
Visualization	`matplotlib`, `seaborn`
BI & Reporting	Microsoft Power BI Desktop
Spreadsheet Analytics	Microsoft Excel (Pivot Tables, Slicers, Charts)
IDE	VS Code / Jupyter Notebook


📁 Project Structure
```
hospital-recovery-analytics/
│
├── hospital_analysis.py              # Main analysis script (all charts + insights)
├── Hospital_Dashboard_in_Excel.xlsx  # Source data + Excel pivot dashboard
├── hospital_dashboard_on_powerbi.pdf # Power BI report export
│
├── outputs/
│   ├── 01_executive_dashboard.png    # KPI banner + 6-panel overview
│   ├── 02_statistical_insights.png   # ANOVA, correlation, violin plots
│   └── 03_ml_clustering.png          # K-Means elbow, PCA scatter, cluster profiles
│
└── README.md
```
---
🚀 Getting Started
Prerequisites
```bash
pip install pandas numpy matplotlib seaborn scipy scikit-learn openpyxl
```
Run the Analysis
```bash
git clone https://github.com/yourusername/hospital-recovery-analytics.git
cd hospital-recovery-analytics
python hospital_analysis.py
```
**Output charts will be saved to the `outputs/` folder. The terminal will also print a full insight report.**

---
Recommendations (For Clinical Decision-Making)
Standardize Therapy protocols across departments — it yields the best recovery-per-day ratio.
Audit Orthopedics and Neurology — below-average outcomes despite comparable costs suggest protocol gaps.
Deploy Dr. Patel's case-management approach as a training baseline for lower-performing peers.
Use ML segmentation to triage incoming patients — fast-responder profiles can be treated in shorter stays, freeing beds for complex cases.
Stop conflating cost with quality — the near-zero cost-recovery correlation confirms that higher spend is not a proxy for better outcomes. Budget allocation should target treatment type and doctor assignment instead.
Build age-adjusted recovery benchmarks — comparing a Senior's 60-point score to a Child's 85-point score on the same scale is clinically misleading.

 
**Skills Demonstrated**

--
End-to-end data analytics pipeline design
Statistical hypothesis testing (ANOVA, Pearson r) with interpretation
Unsupervised machine learning (K-Means, PCA) applied to healthcare data
Multi-panel dashboard creation with matplotlib/seaborn
Cross-tool BI workflow (Python → Excel → Power BI)
Feature engineering and domain-aware metric creation
Data storytelling: translating numbers into clinical recommendations

Build to demonstrate how data analytics can improve real-world healthcare outcomes.
