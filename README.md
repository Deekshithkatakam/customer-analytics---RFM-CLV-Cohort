# Customer Analytics — Online Retail II

Customer segmentation, lifetime value, and retention analysis on 2 years of transaction data from a UK-based online retailer, built to identify which customers drive the most revenue and where retention effort should be focused.

## Business Question

Which customers drive the most value for this business, and where should retention effort be focused to protect revenue?

## Dataset

[Online Retail II](https://www.kaggle.com/datasets/mashlyn/online-retail-ii-uci) (UCI Machine Learning Repository, via Kaggle) — ~1.07M transaction-level rows from a UK-based online retailer, Dec 2009–Dec 2011. Columns: Invoice, StockCode, Description, Quantity, InvoiceDate, Price, Customer ID, Country.

## Tools

- **Python** (pandas, numpy) — data cleaning, feature engineering, RFM scoring, CLV, cohort analysis
- **Matplotlib / Seaborn** — exploratory visualization, cohort retention heatmap
- **Power BI** — interactive dashboard (KPIs, segment breakdown, CLV by segment, cohort retention matrix)

## Process

1. **Data Cleaning** — explored and resolved real-world data quality issues: 243K rows with missing Customer ID (dropped, unattributable to a customer), non-sale stock-adjustment rows (dropped), cancelled orders (kept separately for return-rate analysis), and duplicate line items (kept — verified they reflect genuine repeat purchases, not data errors). See `notebooks/01_cleaning_and_analysis.ipynb` for the full reasoning behind each decision.
2. **RFM Feature Engineering** — built Recency, Frequency, Monetary, Tenure, Average Order Value, and Return Rate for each of 5,878 customers.
3. **RFM Segmentation** — scored customers into quintiles and grouped them into six segments: Champions, Loyal Customers, At Risk, New Customers, Needs Attention, and Lost.
4. **Customer Lifetime Value (CLV)** — estimated CLV per customer (`AOV × Frequency × Lifespan`) and aggregated by segment.
5. **Cohort Retention Analysis** — grouped customers by first-purchase month and tracked what percentage of each cohort remained active in each subsequent month.
6. **Dashboard** — brought segments, CLV, and retention data into an interactive Power BI report.

## Key Findings

- **Champions (22.1% of customers) generate ~73% of total estimated CLV** (£21.8M of the customer base's combined value) — a small core of customers drives the overwhelming majority of value.
- **At Risk customers are individually as valuable as Loyal customers** (avg. CLV £3,502 vs. £3,461) but are actively disengaging — the clearest, highest-ROI win-back target.
- **65–85% of first-time customers never return the following month**, across nearly every monthly cohort — the core retention problem is converting first-time buyers into repeat ones, not preventing gradual long-term drift.
- **The earliest cohort (Dec 2009)** shows unusually durable retention among the ~35% of customers who survived past month 1, sustaining significantly higher engagement than later cohorts over the following two years.

## Recommendations

1. Protect Champions with a dedicated retention/loyalty program — losing even a few has an outsized revenue impact.
2. Launch a targeted win-back campaign for At Risk customers — their proven spend justifies real marketing investment.
3. Introduce a post-first-purchase engagement campaign (e.g. a second-order discount within 30 days) to address the sharp month-1 drop-off.
4. Deprioritize marketing spend on the Lost segment — low CLV and long inactivity suggest limited ROI on re-engagement.

## Repository Structure

```
customer-analytics-project/
├── data/
│   ├── raw/                  → original Kaggle file
│   └── processed/             → cleaned_transactions.csv, cancellations.csv, customer_features.csv
├── notebooks/
│   └── 01_cleaning_and_analysis.ipynb
├── dashboards/
│   └── customer_analytics.pbix
├── outputs/
│   ├── cohort_retention_heatmap.png
│   ├── segment_summary.csv
│   ├── clv_by_segment.csv
│   └── cohort_retention.csv
│   └── retention_table_for_dashboard.csv
└── README.md
```

## Dashboard Preview

*![alt text](<outputs/Customer analytics dashboard.png>): `![Dashboard](outputs/dashboard_screenshot.png)`)*

