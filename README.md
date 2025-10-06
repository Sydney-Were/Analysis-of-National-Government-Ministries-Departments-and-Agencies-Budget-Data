# **Analysis of Kenya’s National Government Ministries, Departments, and Agencies (MDAs) Budget Data**

<img width="1000" height="400" alt="Iconic-budget-briefcase" src="https://github.com/user-attachments/assets/fd238356-c809-45e0-b0ab-b3a70b300dff" />

[Source](https://www.standardmedia.co.ke/article/2001284097/the-history-of-kenya-s-iconic-budget-briefcase)
## **1.0 Project Overview**
This project analyzes how public funds have been allocated and spent across Kenya’s National Government Ministries, Departments, and Agencies (MDAs) over four financial years (2020/21 – 2023/24).  

By consolidating Auditor-General reports, National Budget Blue Books, and structured CSV datasets, the study explores:
- Whether ministries spend within approved budgets  
- Which MDAs consistently **underspend** or **overspend**  
- Whether inefficiencies are **systemic or isolated**  
- What reforms can improve **budget execution and accountability**

The result is a **longitudinal, data-driven analysis** that supports auditors, policymakers, and civil society in strengthening fiscal governance.

---

## **2.0 Business Understanding**

### **Problem Statement**
Kenya allocates trillions annually to its MDAs, yet recurring underspending and overspending weaken fiscal discipline and public trust.  
While Auditor-General reports provide yearly audits, they fail to reveal **persistent inefficiencies** across time.

### **Objectives**
- Build a unified, multi-year dataset of approved vs. actual expenditures  
- Quantify and visualize execution gaps  
- Detect patterns of inefficiency via clustering and trend analysis  
- Apply statistical and ML methods to reveal systemic risks  
- Recommend data-driven policy reforms

### **Stakeholders**
- **Auditor-General:** Identify repeat offenders for follow-up audits  
- **Controller of Budget:** Strengthen monitoring of absorption capacity  
- **Treasury & MDAs:** Improve forecasting and execution discipline  
- **Civil Society & Media:** Promote transparency through open data  
- **Policy Analysts:** Support fiscal reform through empirical evidence  

---

## **3.0 Data Understanding**

| **Source** | **Description** | **Purpose** |
|-------------|-----------------|--------------|
| Auditor-General Reports (FY 2020/21 – 2023/24) | Official audited financials | Budget vs. actuals, audit findings |
| National Budget “Blue Book” (FY 2021/22) | Approved allocations by vote/program | Baseline for approved budget |
| Kenya_National_Govt_Budget_2021_2024.csv | Consolidated structured dataset | Core data for analysis |
| MDAs Audit PDFs (2023/24) | Narrative + financial sections | Contextual explanations |

**Core Features:**  
- MDA_name  
- Financial Year  
- Approved Budget / Actual Expenditure  
- Variance (+/–) and %Variance  
- Utilization Rate (%)  
- Spending Status (Overspent / Underspent / On Budget)  
- Audit Flag (±10% deviation trigger)

---

## **4.0 Methodology**

### **Data Preparation**
- Extracted and cleaned data from PDFs using `pdfplumber`  
- Standardized names across years and removed duplicates  
- Engineered analytical features (variance, utilization, audit flag)

### **Exploratory Data Analysis (EDA)**
- Spending status pie charts → underspending dominates  
- Yearly performance bars → inconsistent budget absorption  
- Correlation heatmaps → weak relationship between budget size and execution  
- Variance analysis → KSh 1.79 T underspent vs KSh 1.98 T overspent  

### **Statistical Tests**
- **Chi-Square Test** confirmed a significant bias toward underspending (p < 0.05).  

### **Machine Learning**
#### 🔹 **Clustering (K-Means)**
Grouped MDAs based on:
- Approved Budget  
- Utilization Rate (%)  
- Variance  

| **Cluster** | **Label** | **Characteristics** |
|--------------|-----------|----------------------|
| 0 | Efficient Executors | High utilization, low variance |
| 1 | Chronic Underspenders | Low utilization, large positive variance |
| 2 | Overspending Risks | Negative variance (spent beyond budget) |

**Key Visuals:**
- Elbow & Silhouette plots → *k = 3 optimal*  
- PCA projection → clear separation of fiscal behavior clusters  
- Yearly cluster composition → efficiency improving post-2021  

#### 🔹 **Trend Analysis**
- Aggregated yearly totals and cluster-specific trends  
- Visualized:
  - **Utilization Rate Trends** per cluster  
  - **Variance patterns** over time  
  - **Budget vs Expenditure lines** (2020 – 2024)

**Insights:**
- Utilization improved after FY 2021/22  
- Variance volatility fell, showing tightening fiscal discipline  
- Some MDAs remain chronically inefficient despite reforms  

#### 🔹 **NLP Pipeline**
Extracted entities and budget mentions from narrative text using:
- Tokenization, lemmatization, stop-word removal  
- Entity recognition (e.g. “Ministry of Health”, “National Treasury”)  
- Regex-based budget extraction and fuzzy mapping  

#### 🔹 **Predictive Modeling**
| **Model** | **Description** | **RMSE** | **R²** | **Interpretation** |
|------------|-----------------|-----------|---------|--------------------|
| TF-IDF + Linear Regression | Baseline text model | 1.1e11 | 0.20 | Poor linear fit |
| Tuned XGBoost | Numeric + Categorical + Text features | 3.68e11 | 0.90 | Strong predictive performance |

---

## **5.0 Key Findings**

| **Theme** | **Insight** |
|------------|-------------|
| Execution Gaps | Approved vs Actual Expenditure correlation ≈ 0 → spending patterns unrelated to allocations |
| Variance Magnitude | ± KSh 2 Trillion in total execution gaps over four years |
| Bias | Majority of MDAs chronically underspend |
| Clustering | Clear segmentation into Efficient, Under-, and Overspenders |
| Trends | Gradual improvement in budget utilization post-2021 |
| Predictive Insight | Budget allocations follow systematic patterns captured by ML models |

---

## **6.0 Policy & Audit Recommendations**
1. **Address Chronic Underspending:** Resolve procurement delays and revise ceilings for repeat offenders.  
2. **Tighten Oversight:** Auto-flag MDAs spending >120 % of approved budget.  
3. **Use Clusters for Audit Prioritization:** Target high-budget risks first.  
4. **Improve Forecasting:** Link allocations to historical absorption rates.  
5. **Capacity Building:** Train finance teams in planning and execution.  
6. **Performance Contracts:** Tie leadership KPIs to ≥ 90 % budget utilization.  
7. **Digital Oversight:** Enhance IFMIS to auto-track variance and flag anomalies in real time.  

---


## **7.0 Repository Structure**
```bash
├── Data/                         # Raw and processed data
├── figures/                      # Plots: EDA, clustering, trends
├── artifacts/                    # Intermediate outputs
├── models/                       # Saved scalers and trained models
├── deployment/                   # Processed datasets for deployment
├── Analysis.ipynb                # Main notebook
├── README.md                     # Project documentation
```

## **8.0 Links to Tableau and Search Tool Deployment**

1. [Tableau](https://public.tableau.com/app/profile/daniel.akwabi/viz/Group3AnalysisofNationalGovernmentMinistriesDepartmentsandAgenciesBudgetData_/Dashboard1)
2. [Search Tool](https://kenya-budget-app-a992f046cac2.herokuapp.com/)







