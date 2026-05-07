# 🛒 Smart Retail Intelligence Platform

> An end-to-end retail analytics project combining Python, SQL, Machine Learning, and Power BI to deliver actionable business insights across churn prediction, demand forecasting, and inventory management.

![Python](https://img.shields.io/badge/Python-3.10-blue?logo=python) ![SQL](https://img.shields.io/badge/SQL-SQLite-lightgrey?logo=sqlite) ![PowerBI](https://img.shields.io/badge/Power%20BI-Dashboard-yellow?logo=powerbi) ![ML](https://img.shields.io/badge/ML-XGBoost%20%7C%20Prophet-green)

---

## 📌 Project Overview

This project simulates a real-world retail analytics pipeline for a business analyst or data analyst role. It ingests synthetic retail data, builds a SQL data warehouse, trains machine learning models, and surfaces everything in a 4-page Power BI dashboard.

**Business Questions Answered:**
- Which customers are at risk of churning — and why?
- What will revenue look like over the next 12 weeks?
- Which product categories drive profit, and which are at stock risk?

---

## 🗂️ Repository Structure

```
smart-retail-intelligence/
│
├── data/
│   ├── raw/                         # Raw generated CSV files
│   │   ├── customers.csv
│   │   ├── products.csv
│   │   ├── orders.csv
│   │   ├── order_items.csv
│   │   └── inventory.csv
│   │
│   └── powerbi_files/               # Clean exports for Power BI
│       ├── monthly_revenue.csv
│       ├── clv_by_segment.csv
│       ├── order_status.csv
│       ├── churn_predictions.csv
│       ├── churn_summary.csv
│       ├── demand_forecast.csv
│       ├── category_monthly_revenue.csv
│       ├── product_performance.csv
│       └── inventory_alerts.csv
│
├── notebooks/
│   ├── 01_generate_data.ipynb       # Synthetic data generation (Faker + NumPy)
│   ├── 02_eda.ipynb                 # Exploratory Data Analysis
│   ├── 03_sql_kpi_queries.ipynb     # SQLite KPI queries + exports
│   ├── 04_churn_model.ipynb         # XGBoost churn model + SHAP
│   └── 05_demand_forecast.ipynb     # Prophet demand forecasting
│
├── outputs/
│   ├── models/
│   │   └── retail.db                # SQLite database
│   └── charts/
│       ├── roc_curve.png
│       ├── feature_importance.png
│       ├── shap_summary.png
│       ├── shap_waterfall.png
│       ├── demand_forecast.png
│       └── forecast_decomposition.png
│
├── dashboard/
│   └── Smart_Retail_Dashboard.pbix  # Power BI dashboard file
│
├── requirements.txt
└── README.md
```

---

## 🧰 Tech Stack

| Layer | Tools Used |
|---|---|
| Data Generation | Python, Faker, NumPy, Pandas |
| Data Warehouse | SQLite, SQL window functions (RANK, LAG, rolling AVG) |
| Machine Learning | XGBoost, SHAP, Scikit-learn |
| Forecasting | Prophet (Meta), Cross-validation, MAPE |
| Visualization | Power BI Desktop, DAX measures |
| Version Control | Git, GitHub |

---

## 📊 Dashboard Pages

### Page 1 — Executive Summary
- Total Revenue: ₹166.63M | Total Orders: 3,196 | Avg Order Value: ₹53.24K | Churn Rate: 10.14%
- Monthly revenue trend bar chart (Jan 2022 – Jul 2024)
- Customer Lifetime Value by segment (Premium vs At-Risk: 4x difference)
- Orders by status donut chart

### Page 2 — Churn Risk ⭐
- 91 High Risk | 22 Medium Risk customers identified
- Churn % by segment bar chart — At-Risk segment at ~58% churn
- Top 10 at-risk customers table with churn probability + days inactive
- SHAP explainability charts embedded directly in Power BI

### Page 3 — Demand Forecast
- Weekly actual vs Prophet 12-week forecast line chart
- Revenue by month and category stacked bar chart
- Seasonal spike detection (April–June peak, December holiday lift)

### Page 4 — Products & Inventory
- Electronics dominates at ₹119.3M (71% of total revenue)
- 82 products flagged for restock — Home & Kitchen highest risk
- Category revenue share treemap
- Avg profit margin: 42.7%

---

## 🤖 ML Models

### 1. XGBoost Churn Prediction
- **Features:** RFM metrics, days since last order, cancellation rate, total spend, customer segment
- **Output:** Churn probability (0–1) + risk band (High / Medium / Low)
- **Performance:** AUC 0.92
- **Explainability:** SHAP values show *why* each customer is flagged — not just *that* they are

### 2. Prophet Demand Forecasting
- **Input:** Weekly revenue time series (Jan 2022 – Oct 2024)
- **Output:** 12-week revenue forecast with confidence intervals
- **Accuracy:** Validated with cross-validation MAPE scoring
- **Features:** Automatic seasonality detection + Indian holiday effects

---

## ⚙️ Setup & Installation

### 1. Clone the repository
```bash
git clone https://github.com/yourusername/smart-retail-intelligence.git
cd smart-retail-intelligence
```

### 2. Install dependencies
```bash
pip install -r requirements.txt
```

### 3. Run notebooks in order
```bash
# Open Jupyter
jupyter notebook

# Run in this exact order:
# 01_generate_data.ipynb   → creates raw CSV files
# 02_eda.ipynb             → EDA + saves customer_features.csv
# 03_sql_kpi_queries.ipynb → builds retail.db + exports KPI CSVs
# 04_churn_model.ipynb     → trains XGBoost + saves churn_predictions.csv
# 05_demand_forecast.ipynb → trains Prophet + saves demand_forecast.csv
```

### 4. Open Power BI
- Open `dashboard/Smart_Retail_Dashboard.pbix` in Power BI Desktop
- If data paths are broken: Home → Transform Data → update file paths to your local `data/powerbi_files/` folder

---

## 📦 Requirements

```
pandas>=1.5.0
numpy>=1.23.0
faker>=18.0.0
scikit-learn>=1.2.0
xgboost>=1.7.0
shap>=0.41.0
prophet>=1.1.0
matplotlib>=3.6.0
seaborn>=0.12.0
sqlalchemy>=1.4.0
jupyter>=1.0.0
```

---

## 📁 Key Output Files

| File | Description |
|---|---|
| `retail.db` | SQLite database with all 5 tables |
| `churn_predictions.csv` | 1,000 customers with churn probability + risk band |
| `demand_forecast.csv` | 12-week revenue forecast from Prophet |
| `shap_summary.png` | Global feature importance via SHAP |
| `shap_waterfall.png` | Single customer churn explanation |
| `Smart_Retail_Dashboard.pbix` | 4-page Power BI dashboard |

---

## 💡 Key Business Insights

1. **91 customers (9.1%)** are at High churn risk — targeting them with retention offers before they leave protects an estimated ₹8–15M in revenue
2. **At-Risk segment** has 4x lower CLV than Premium — prioritising Premium retention has the highest ROI
3. **Electronics** drives 71% of total revenue but **Home & Kitchen** has the most restock alerts — a stockout there would directly impact margins
4. **November–December** seasonal spike is predictable — Prophet forecasts allow inventory and marketing teams to prepare 12 weeks in advance

---

## 🙋 Author

**Sangita Kar**  
Data Analyst | Python · SQL · Power BI · Machine Learning  
[LinkedIn](https://www.linkedin.com/in/sangitakar/) · [GitHub](https://github.com/sangitakar798)

---

## 📄 License

This project is open source and available under the [MIT License](LICENSE).
