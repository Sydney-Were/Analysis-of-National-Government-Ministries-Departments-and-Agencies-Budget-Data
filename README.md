# Analysis of Kenya’s National Government Ministries, Departments, and Agencies (MDAs) Budget Data  

## 1.0 Project Overview  
This project analyzes how public funds have been allocated and spent across Kenya’s national government MDAs over four financial years (2020/21 – 2023/24).  

By consolidating Auditor-General reports, National Budget Blue Books, and structured CSV datasets, the project investigates:  
- Are ministries spending within approved budgets?  
- Which MDAs consistently underspend or overspend?  
- Are budget execution challenges systemic or isolated?  
- What policy or governance reforms can address inefficiencies?  

The outcome is a data-driven, longitudinal review that supports auditors, policymakers, researchers, and civil society in strengthening fiscal accountability.  

---

## 2.0 Business Understanding  

### Problem Statement  
Kenya allocates trillions of shillings annually to ministries and agencies. However, persistent underspending and overspending undermine service delivery, weaken fiscal discipline, and raise governance risks. Traditional single-year audits provide snapshots but fail to reveal systemic inefficiencies across multiple years.  

### Objectives  
- Build a unified dataset of budget allocations vs. expenditures.  
- Quantify execution gaps (approved vs. actual).  
- Identify high-risk MDAs with persistent inefficiencies.  
- Apply statistical tests and machine learning to detect patterns.  
- Provide policy recommendations for improving budget execution.  

### Stakeholders  
- Auditor-General – Target repeat offenders for priority audits.  
- Controller of Budget – Strengthen monitoring of budget absorption.  
- Ministry Finance Teams – Improve forecasting and disbursement discipline.  
- Civil Society & Media – Build evidence for public accountability campaigns.  
- Policy Analysts & Researchers – Support fiscal reform with data insights.  

---

## 3.0 Data Understanding  

### Data Sources  
| Source | Description | Role in Project |
|--------|-------------|-----------------|
| Auditor-General Reports (2020/21–2023/24) | Authoritative audited financial statements | Budget vs. actuals, audit opinions, governance notes |
| National Budget Blue Book (2021/22) | Official approved estimates by vote/program | Baseline for approved allocations |
| Kenya_National_Govt_Budget_2021_2024.csv | Structured, machine-readable dataset | Core analysis dataset |
| MDAs Audit PDFs (2023/24) | Narrative + financial data | Context on execution gaps, pending bills |

### Features Extracted  
- MDA_name  
- Financial Year  
- Approved Budget  
- Actual Expenditure  
- Variance and pct_variance  
- Utilization Rate (%)  
- Spending Status (Overspent / Underspent / On Budget)  
- Audit Flag (significant deviation indicator)  

### Limitations  
- Data format: Mostly PDFs requiring cleaning and extraction.  
- Inconsistent naming: MDAs renamed/merged across years.  
- Granularity: Institution-level, not project-level.  
- Audit notes: Qualitative, required NLP for structure.  

---

## 4.0 Methodology  

### Data Preparation  
- Cleaned ministry names (removed duplicates, noise).  
- Standardized budgets into numeric format.  
- Aggregated duplicates into single MDA-year rows.  
- Engineered features: Utilization Rate, Spending Status, Audit Flag.  

### Exploratory Data Analysis (EDA)  
- Spending status distributions (underspent vs overspent).  
- Yearly budget vs expenditure comparison.  
- Variance distribution (top 10 MDAs by variance).  
- Correlation analysis of budget features.  

### Statistical Testing  
- Chi-square goodness-of-fit confirmed a significant bias toward underspending.  

### Machine Learning and NLP  
- Clustering (KMeans): Grouped MDAs into Efficient Spenders, Underspenders, Overspenders.  
- NLP: Cleaned and tokenized Auditor-General text reports, extracted entities and budgets.  
- Models:  
  - Baseline: TF-IDF + Linear Regression → poor fit (R² = -0.12).  
  - Tuned: XGBoost with numeric, categorical, and text features → RMSE ≈ 2.28e11, R² = 0.48.  

---

## 5.0 Key Findings  

- Systemic Execution Gaps  
  - Approved vs actual expenditure correlation ≈ 0 → MDAs spending unrelated to allocations.  
- Massive Variances  
  - KSh 2.1T underspent and KSh 2.0T overspent.  
  - One MDA overspent ~KSh 1.2T in a single year.  
- Underspending Bias  
  - Most MDAs chronically underspend budgets (Chi-square test confirms).  
- Cluster Profiles  
  - Cluster 0: Efficient spenders.  
  - Cluster 1: Chronic underspenders.  
  - Cluster 2: Overspenders.  
- Predictive Insights  
  - Budget patterns partially predictable → XGBoost explains ~48% variance.  

---

## 6.0 Policy and Audit Recommendations  

1. Address chronic underspending by resolving procurement bottlenecks and revising ceilings for repeat underspenders.  
2. Tighten oversight on overspending MDAs through automatic audit triggers for >120% utilization.  
3. Use clustering to prioritize audits for high-budget outliers.  
4. Improve forecasting and planning by tying allocations to historical absorption capacity.  
5. Provide capacity building for finance teams in planning, reporting, and execution.  
6. Adopt evidence-based budgeting tied to past performance.  
7. Introduce performance contracts linking leadership KPIs to ≥90% execution rates.  
8. Strengthen IFMIS to auto-flag anomalies and trigger alerts.  

---

## 7.0 Repository Structure  

```bash
├── Data/                         # Raw and processed data files
├── figures/                      # Visualizations (EDA, clusters, trends)
├── artifacts/                    # Intermediate outputs (clustering results, cleaned data)
├── models/                       # ML models and scalers
├── deployment/                   # Cleaned files for deployment
├── Analysis.ipynb                # Main project notebook
├── README.md                     # Project documentation
