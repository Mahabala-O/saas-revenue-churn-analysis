# SaaS Revenue & Churn Analysis — CloudTask Pro

**Role:** Business Analyst  
**Context:** Board meeting preparation for a B2B SaaS company  
**Tools:** Python (Pandas, SciPy, Scikit-learn), Tableau, Notion

📓 **Full documentation & findings:** [Notion Doc](https://mahabala.notion.site/SaaS-Revenue-Churn-Analysis-33de583fcafd8009a6d8e67e02d43719)

---

## 📋 Project Overview

CloudTask Pro is a SaaS company that has grown from 0 to 600 customers since 2022. While revenue has grown consistently, the board raised concerns about a persistently high churn rate. This project delivers a full end-to-end analysis covering churn drivers, revenue trends, unit economics, and customer risk scoring — structured as a board-ready deliverable.

---

## 📁 Repository Structure

```
saas-revenue-churn-analysis/
│
├── data/
│   ├── subscriptions.csv              # Raw customer-level dataset
│   ├── monthly_revenue.csv            # Raw monthly MRR dataset
│   ├── subscriptions_enriched.csv     # Enriched with tenure and risk score columns
│   └── mrr_trends_enriched.csv        # Enriched with NRR and churned loss columns
│
├── notebooks/
│   ├── tabl_SaaS_Revenue-Churn_Analysis.ipynb   # Full analysis notebook (primary)
│   └── SaaS_Revenue-Churn_Analysis.ipynb        # Earlier draft
│
├── tableau/
│   ├── CloudTask Pro - Board Analysis - Revenue, Churn & Risk.twb   # Tableau workbook
│   └── CloudTask Pro - Board Analysis - Revenue, Churn & Risk.pdf   # Static PDF export
│
├── README.md
└── requirements.txt
```

> **Note:** The Tableau file is a `.twb` (workbook) rather than `.twbx` (packaged workbook), meaning it references the CSV files externally. To open it correctly in Tableau Desktop, ensure the data files in the `data/` folder are accessible.

---

## 🔍 Analysis Summary

### 1. Churn Analysis
- **Overall churn rate: 52.17%** — just over half of all customers have churned
- **Starter plan** is the only segment above average at 70.51% — clear standout
- **Annual billing** customers churn at 40.32% vs 60.51% for monthly — a 20pt gap
- Top churn reasons: Budget Cuts + Price Too High (~33% of all churn combined)
- Price sensitivity dominates lower tiers; product gaps dominate higher tiers

### 2. Revenue Trends
- MRR grew from ~$7K to ~$290K — strong linear trend (R² = 0.97, slope ~$6,466/month)
- Monthly churn rate stabilized from mid-2023 onward into a 2–6% range
- NRR dips clustered around months where above-average churn and below-average acquisition coincided

### 3. Unit Economics
| Plan | CLV | CLV:CAC Ratio | Avg Tenure |
|---|---|---|---|
| Enterprise | $76,106 | 379x | 25.5 months |
| Business | $24,787 | 123x | 19.0 months |
| Professional | $8,137 | 40.5x | 16.4 months |
| Starter | $2,016 | 10.0x | 9.4 months |

All plans clear the 3x benchmark. CAC used as blended average ($200.79) — plan-level CAC not available in dataset.

### 4. At-Risk Indicators
- Churned customers averaged **27.45% feature usage** vs **55.02%** for active customers
- Churned customers averaged **NPS of 3.04** vs **5.81** for active customers
- Single-variable threshold (38.85% feature usage): **85 at-risk customers (29.6% of active base)**
- Composite risk score (feature usage 50%, NPS 30%, tenure 20%): **14 highest-risk customers (4.9%)**
- Composite model AUC: **0.937** — strong discriminative performance

---

## 📊 Tableau Dashboards

Four dashboards combined into a Tableau Story:

1. **MRR Growth & Churn Trends** — KPI cards, MRR trend + regression overlay, monthly churn rate trend, churn rate by plan
2. **Customer Segment Risk Analysis** — Churn by region, billing cycle, industry, churn reasons stacked bar by plan
3. **Customer Lifetime Value & Profitability** — CLV:CAC ratio, CLV by plan, avg tenure by plan
4. **At-Risk Customer Indicators** — Feature usage vs NPS scatter plot, risk score box plot, at-risk customers by plan

---

## 🛠️ Tech Stack

- **Python** — Pandas, NumPy, Matplotlib, SciPy, Scikit-learn
- **Tableau Desktop** — Interactive dashboards and Tableau Story
- **Notion** — Project documentation and findings: [View Doc](https://mahabala.notion.site/SaaS-Revenue-Churn-Analysis-33de583fcafd8009a6d8e67e02d43719)

---

## ▶️ How to Run

1. Clone the repository
2. Install dependencies: `pip install -r requirements.txt`
3. Open `notebooks/tabl_SaaS_Revenue-Churn_Analysis.ipynb` in Jupyter
4. Run all cells in order
5. Open `tableau/CloudTask Pro - Board Analysis - Revenue, Churn & Risk.twb` in Tableau Desktop
   - Ensure the `data/` folder CSVs are accessible when Tableau prompts for data source location

---

## 📌 Key Findings

- Starter plan is the primary churn risk — 70.51% churn rate vs 52.17% average
- Annual billing significantly improves retention — worth prioritizing as a conversion lever
- Cost-related churn (budget cuts + price) accounts for ~33% of all exits
- 85 active customers (29.6%) show early warning signs based on feature usage alone
- MRR growth is statistically robust — linear trend explains 97% of revenue movement
