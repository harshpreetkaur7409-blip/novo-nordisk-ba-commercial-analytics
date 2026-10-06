# Commercial & Field Force Analytics — Pharma (India)

> **Personal/Academic Project** — built on 100% **synthetic** data. No real patient, HCP, employee or company data is used. Product names are generic and fictional.

## Business problem
A pharma commercial team (diabetes / metabolic portfolio) needs to know **where sales come from, whether field effort is paying off, and which HCPs need what action next**. This project builds an end-to-end analytics workflow: SQL → Python EDA → Excel KPI workbook → Streamlit dashboard → executive summary with next-best actions (NBA).

## Dataset (synthetic, 10,000 rows)
500 HCPs × 2 products × 10 months (Jan–Oct 2026), 20 Indian territories.

| Column | Meaning |
|---|---|
| territory, hcp_id, specialty, product, month | Dimensions (month = `YYYY-MM`) |
| sales | Sales in INR |
| calls | Rep calls on HCP that month |
| engagement_score | 0–100 composite engagement |
| digital_touchpoints | Emails / webinars / e-detailing contacts |

Built-in realism: diminishing returns to calls, specialty-driven potential, product growth differences, mild seasonality, ~10% of HCPs drifting away after month 5 (so the model has leakage to find).

## Folder structure
```
project1_commercial_field_force/
├── README.md
├── requirements.txt
├── data/            field_force_sales.csv, field_force.db (generated)
├── sql/             01_create_tables.sql, 02_insert_data.sql (generated), 03_analytical_queries.sql
├── src/             generate_data.py, load_sqlite.py, analytics.py, eda.py, build_excel.py
├── app/             streamlit_app.py
├── excel/           Commercial_FieldForce_Dashboard.xlsx
├── reports/         executive_summary.md, build_exec_summary.py, figures/*.png
└── outputs/         hcp_next_best_actions.csv, sql_results/Q1..Q10.csv, eda_console_output.txt
```

## How to run
```bash
python -m venv .venv && source .venv/bin/activate      # Windows: .venv\Scripts\activate
pip install -r requirements.txt
python src/generate_data.py          # 1. data + SQL inserts (seeded, reproducible)
python src/load_sqlite.py            # 2. build SQLite DB, run + export 10 queries
python src/eda.py                    # 3. EDA, trends, ML drivers, NBA list, charts
python src/build_excel.py            # 4. Excel workbook
python reports/build_exec_summary.py # 5. executive summary
streamlit run app/streamlit_app.py   # 6. dashboard
```
Note: Excel formulas calculate when opened in Excel. If you generate the file on a machine without Excel and want cached values, open and save once (or recalc with LibreOffice).

## What each deliverable shows
| Skill | Where |
|---|---|
| SQL (DDL, constraints, indexes, CTEs, window functions, NTILE, CASE pivots) | `sql/` |
| Python EDA, trend analysis, feature importance | `src/eda.py` |
| Excel (SUMIFS pivot-style grids, KPI dashboard with selector, charts, data validation, colour conventions) | `excel/` |
| Dashboard | `app/streamlit_app.py` (filters, 5 KPI cards, 4 tabs, CSV download) |
| AI/ML | Random Forest + permutation importance; within-HCP response model (diminishing returns) |
| Insight → action | Rule-based NBA engine in `src/analytics.py` (editable thresholds) |
| Communication | `reports/executive_summary.md` (1 page) |

### The 10 SQL queries
Q1 product KPIs · Q2 monthly trend + MoM + 3-mo moving avg · Q3 territory rank + cumulative share · Q4 region×product matrix · Q5 call productivity vs average · Q6 specialty×product mix · Q7 Pareto deciles · Q8 engagement bands · Q9 digital-touchpoint buckets · Q10 declining HCPs (revenue at risk).

### Next-best-action rules (priority order)
1. Sales down ≥15% (last 3 vs prior 3 months) **and** calls fell → restore call frequency
2. Sales down ≥15%, calls stable → change message / involve medical
3. Top-quintile sales → key-account plan
4. High engagement, low digital → webinar / e-detailing
5. Low engagement, above-median calls → switch channel/content
6. Bottom-30% sales per call, above-median calls → shift effort to digital
7. Otherwise maintain & monitor

## Key results (synthetic data)
See `reports/executive_summary.md`. Highlights: INR ~108.9 Cr sales, +14% Jan→Oct; GLP-1 Weekly 45% share; top 20% of HCPs = 50% of sales; extra calls show diminishing returns (2→3 calls ≈ +8%, 5→6 ≈ +4%); ~90 HCPs flagged for rescue.

## Limitations
- Synthetic data: patterns were designed in, so results show method, not real-world truth.
- Response model is observational (association, not causation); a field pilot with control territories would be needed.
- NBA is rules-based and transparent by design; thresholds need calibration with business input.
- Excel "pivots" are formula-driven grids; native PivotTables can be added via Insert → PivotTable on `tblData`.
- Power BI was not built; the Streamlit app is the dashboard deliverable (CSV/SQL outputs load directly into Power BI).

## Resume bullets (Personal/Academic Project)
- Built an end-to-end commercial analytics project on 10,000-row synthetic pharma field-force data (SQL, Python, Excel, Streamlit): 10 analytical queries, KPI dashboard and EDA identifying that the top 20% of HCPs drive ~50% of sales.
- Developed a rule-based next-best-action engine and response model (diminishing returns to calls: +8% for 2nd→3rd call vs +4% for 5th→6th) that flagged ~90 declining HCPs (~INR 1.3 Cr/quarter at risk) and a 1-page executive summary.

## Interview talking points
1. **Insight to action:** "Calls show diminishing returns, so I recommended shifting effort from over-called, low-return HCPs to digital and to declining high-potential accounts instead of adding calls everywhere."
2. **Rigor:** "Raw correlation of digital touchpoints with sales is confounded by HCP potential, so I used within-HCP fixed effects and stated it is association, proposing a test-vs-control pilot."
3. **Tooling choices:** "I used SQL window functions for trend/Pareto/decline detection, Excel for business-user reporting (selector-driven KPIs), and Streamlit for self-serve exploration, each matched to its audience."
