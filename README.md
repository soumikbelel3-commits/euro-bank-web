# 📊 Customer Retention Analytics — Interactive Power BI-Style Dashboard

> **The European Central Bank · 2025**  
> A fully interactive, browser-based analytics dashboard built in HTML/CSS/JavaScript that replicates a Microsoft Power BI experience — no Power BI licence required. Includes a built-in step-by-step guide to rebuild the same dashboard in real Power BI Desktop.

---

## 🖥️ Live Preview

Open `PowerBI_Dashboard.html` directly in any modern browser. No installation. No server. No dependencies.

```bash
# Just double-click the file, or:
open PowerBI_Dashboard.html        # macOS
start PowerBI_Dashboard.html       # Windows
xdg-open PowerBI_Dashboard.html   # Linux
```

---

## 📁 File

```
PowerBI_Dashboard.html    # Single self-contained file — everything included
```

That's it. One file. No external CSS, no npm, no Python.  
Chart.js is loaded via CDN — an internet connection is required on first load.

---

## 📋 Dashboard Pages

The dashboard is structured as 7 pages, accessible via the left sidebar:

| Page | Icon | Content |
|------|------|---------|
| Overview | 📊 | Churn donut, geography bars, age group trend, geo×gender heatmap |
| Engagement | 👥 | Tier distribution, churn by tier, active vs inactive rings, score histogram |
| Products | 📦 | Product-churn relationship, portfolio donut, products×engagement matrix |
| Financial | 💰 | Balance segments, salary quartiles, credit score bands, country deep-dive |
| Risk Segments | ⚠️ | HVD profile, Silent Churner profile, retention tier breakdown, scatter |
| Recommendations | 📝 | Full prioritized action table + churn reduction impact bar chart |
| PBI Guide | 🗺️ | Step-by-step instructions to rebuild in real Power BI Desktop |

---

## 🔢 Key Metrics Displayed

| KPI | Value |
|-----|-------|
| Portfolio Churn Rate | **20.4%** |
| Active Members | **51.5%** |
| Average Engagement Score | **5.38 / 9.0** |
| High-Value Disengaged | **1,247 customers** |
| Silent Premium Churners | **371 customers** |
| Germany Churn Rate | **32.4%** (vs 16.2% France) |
| Peak Age Group Churn | **50.6%** (46–55 bracket) |
| 2-Product Churn Rate | **7.6%** (vs 27.7% for 1 product) |

---

## ✨ Features

- **7-page navigation** via sidebar — each page loads charts on demand
- **Filter bar** at the top — clickable chips for Geography, Member Status, and Engagement Tier
- **10+ interactive charts** powered by Chart.js (hover tooltips on every data point)
- **KPI strip** on every page with colour-coded metric cards
- **Insight banners** — plain-English callouts highlighting the most critical finding per page
- **Geography × Gender heatmap** with colour-scaled cells
- **Risk segment cards** — dedicated HVD and SPC panels with key stats
- **Recommendations table** — prioritized action list with badge labels (CRITICAL / HIGH / MEDIUM)
- **Impact projection chart** — waterfall showing churn reduction roadmap
- **Built-in Power BI Guide** — DAX formulas, visual recommendations, theme colours, slicer setup

---

## 🗺️ Power BI Implementation Guide (Built In)

The final page of the dashboard (`🗺️ PBI Guide`) contains everything needed to rebuild this in **Microsoft Power BI Desktop**:

### DAX Calculated Columns
```dax
EngagementScore =
    [IsActiveMember]*3 + MIN([NumOfProducts],3) + [HasCrCard] + MIN([Tenure]/2, 2)

EngagementTier =
    IF([EngagementScore]>=7, "High", IF([EngagementScore]>=4, "Medium", "Low"))

RetentionStrength =
    [EngagementScore]*0.4 + ([NumOfProducts] + [HasCrCard]*0.5)*0.6

HighValueDisengaged =
    IF([Balance] > PERCENTILE([Balance], 0.75) && [IsActiveMember]=0, 1, 0)
```

### DAX Measures
```dax
Churn Rate         = DIVIDE(COUNTROWS(FILTER(Table,[Exited]=1)), COUNTROWS(Table))
HVD Count          = COUNTROWS(FILTER(Table, [HighValueDisengaged]=1))
Avg Engagement     = AVERAGE(Table[EngagementScore])
Active Member %    = DIVIDE(COUNTROWS(FILTER(Table,[IsActiveMember]=1)), COUNTROWS(Table))
```

### Recommended Visuals Per Page
| Page | Visuals |
|------|---------|
| Overview | Card KPIs, Donut, Clustered Bar, Line Chart, Matrix Heatmap |
| Engagement | Bar, Gauge, Scatter (EngagementScore vs Balance, colour = Exited) |
| Products | Bar, Treemap, Clustered Bar (Products × EngagementTier) |
| Risk | Funnel, Card, **Decomposition Tree** (AI-powered churn breakdown) |

### Theme Colours
| Role | Hex |
|------|-----|
| Primary (Navy) | `#1F3B73` |
| Secondary (Blue) | `#2E6FD8` |
| Alert (Orange) | `#E8580A` |
| Positive (Teal) | `#0E9B8A` |
| Churn (Red) | `#C0392B` |
| Safe (Green) | `#1A9641` |
| Background | `#F0F2F8` |

---

## 📊 Data Source

**Dataset:** `European_Bank.csv` — 10,000 customer records from The European Central Bank (2025)

| Column | Description |
|--------|-------------|
| `CreditScore` | Customer creditworthiness (350–850) |
| `Geography` | France / Germany / Spain |
| `Gender` | Male / Female |
| `Age` | Customer age |
| `Tenure` | Years with bank (0–10) |
| `Balance` | Account balance in Euros |
| `NumOfProducts` | Products held (1–4) |
| `HasCrCard` | Credit card ownership |
| `IsActiveMember` | Active member flag |
| `EstimatedSalary` | Annual salary estimate |
| `Exited` | **TARGET** — Churned (1) or Retained (0) |

The dashboard has the dataset values **hardcoded** from the pre-computed analysis, so it works entirely offline without needing the CSV file present.

---

## 🛠️ Tech Stack

| Technology | Purpose |
|-----------|---------|
| HTML5 / CSS3 | Layout, styling, sidebar, filter bar |
| Vanilla JavaScript | Page routing, filter logic, chart initialization |
| [Chart.js 4.4.1](https://www.chartjs.org/) | All interactive charts (via CDN) |
| Google Fonts | DM Sans typeface (via CDN) |

No frameworks. No build tools. No package managers.

---

## 🗂️ Related Project Files

This dashboard is part of a larger analytics project. The full repository includes:

| File | Description |
|------|-------------|
| `European_Bank.csv` | Raw dataset (10,000 customers) |
| `PowerBI_Dashboard.html` | This file — interactive browser dashboard |
| `Bank_Retention_Analytics.ipynb` | Jupyter notebook — full EDA with matplotlib/seaborn charts |
| `streamlit_app.py` | Streamlit live analytics app |
| `Research_Paper.docx` | Full EDA research paper (8 sections) |
| `Executive_Summary.docx` | Government stakeholder brief |
| `European_Bank_Analysis.xlsx` | 9-sheet Excel analytics workbook |
| `README.md` | Main project README |

---

## 🚀 Quick Start

**Option 1 — Just open the file:**
```bash
open PowerBI_Dashboard.html
```

**Option 2 — Serve locally (avoids any browser CORS quirks):**
```bash
python -m http.server 8080
# then visit: http://localhost:8080/PowerBI_Dashboard.html
```

---

## 📄 License

This project is for academic and analytical purposes.  
Dataset sourced from The European Central Bank public analytics programme.

---

<div align="center">
  <sub>Built with HTML · CSS · Chart.js · Vanilla JavaScript &nbsp;|&nbsp; No build tools required</sub>
</div>
