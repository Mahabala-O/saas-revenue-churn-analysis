# SaaS Revenue & Churn Analysis — CloudTask Pro

**Role:** Business Analyst  
**Context:** Board meeting preparation for a B2B SaaS company  
**Tools:** Python (Pandas, SciPy, Scikit-learn), Tableau

📖 **Full write-up with interactive charts:** [portfolio-mo.vercel.app/projects/saas-revenue-churn-analysis](https://portfolio-mo.vercel.app/projects/saas-revenue-churn-analysis)

---

## 📋 Project Overview

CloudTask Pro is a fictional SaaS company (practice dataset) that has grown from 0 to 600 customers since 2022. While revenue has grown consistently, the board raised concerns about a persistently high churn rate. This project delivers a full end-to-end analysis covering churn drivers, revenue trends, unit economics, and customer risk scoring — structured as a board-ready deliverable.

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
│   ├── portfolio_checks.ipynb                   # Follow-up checks behind the portfolio write-up
│   └── SaaS_Revenue-Churn_Analysis.ipynb        # Earlier draft
│
├── tableau/
│   ├── CloudTask Pro - Board Analysis - Revenue, Churn & Risk.twb   # Tableau workbook
│   └── CloudTask Pro - Board Analysis - Revenue, Churn & Risk.pdf   # Board pack PDF (same 4 dashboards)
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

Four dashboards combined into a Tableau Story. The [board pack PDF](tableau/CloudTask%20Pro%20-%20Board%20Analysis%20-%20Revenue%2C%20Churn%20%26%20Risk.pdf) shows the same four dashboards, drawn directly from the data so every figure matches the notebooks:

1. **MRR Growth & Churn Trends** — KPI cards, MRR trend + regression overlay, monthly churn rate trend, churn rate by plan
2. **Customer Segment Risk Analysis** — Churn by region, billing cycle, industry, churn reasons stacked bar by plan
3. **Customer Lifetime Value & Profitability** — CLV:CAC ratio, CLV by plan, avg tenure by plan
4. **At-Risk Customer Indicators** — Feature usage vs NPS scatter plot, risk score box plot, at-risk customers by plan

---

## 🛠️ Tech Stack

- **Python** — Pandas, NumPy, Matplotlib, SciPy, Scikit-learn
- **Tableau Desktop** — Interactive dashboards and Tableau Story

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
- 85 active customers (29.6%) show early warning signs based on feature usage alone (~$82K of monthly revenue)
- MRR growth is statistically robust — linear trend explains 97% of revenue movement — but it slowed sharply in 2025 (+12% vs +38% in 2024), so the trend line overstates where revenue is heading

### Follow-up checks (`notebooks/portfolio_checks.ipynb`)
- **Annual billing lowers churn within each plan**, not just overall: Starter 60% vs 77%, Professional 35% vs 58%, Business 27% vs 53% (Enterprise ~22% either way)
- **No customer using 60%+ of features churned**, and no customer with an NPS survey score of 7+ churned
- **Risk score without tenure:** tenure is partly determined by churn itself (churned customers stop accruing it), so it inflates the AUC. Usage and NPS alone still reach **AUC 0.91** (vs 0.94 with tenure)
