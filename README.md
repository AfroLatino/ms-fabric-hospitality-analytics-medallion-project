# ms-fabric-hospital-analytics-medallion-project
“Interactive end-to-end MS Fabric Hospitality Analytics Medallion project: ingest, clean, aggregate data, and visualise business KPIs in Power BI.”

# Overview

**Business Problem**

Retail locations struggle to monitor daily operational efficiency because sales revenue, labour costs, and inventory usage are tracked in separate systems, making it difficult to quickly understand profitability and make data-driven decisions.

**Why it matters:**

- Managers cannot easily identify locations with high labour costs relative to revenue.
- Inefficiencies like waste, stock-outs, or overstaffing reduce overall profitability.
- Timely, aggregated insights help optimise staffing, control costs, and maximise profit margins.
- Provides a single source of truth for reporting, enabling faster and more confident decisions.

# Architecture

![Medallion Architecture](architecture.png)

# Tech Stack

| Component | Purpose |
|-----------|---------|
| Microsoft Fabric (OneLake, Lakehouse, Pipelines) | Data ingestion, storage, transformation, orchestration |
| PySpark | Data processing and transformations |
| Power BI | Visualisation of Gold layer metrics |
| CSV / Text Files | Source datasets: sales, labour, inventory, reviews |

# Medallion Design

**Bronze Layer (Raw Data):** Preserves original CSVs, minimal changes.  
**Silver Layer (Cleaned / Standardized):** Remove duplicates, fix nulls, standardise types.  
**Gold Layer (Aggregated Metrics):** Business-ready table for dashboards (`total_revenue`, `total_labour_cost`, `profit`).  

**Flow:**  
`Bronze → Silver → Gold → Power BI Dashboards`

# Key Insights

- **Labour Cost % vs Revenue** – Identifies high labour cost locations/days.  
- **Profitability Analysis** – Monitors negative profits and underperforming locations.  
- **Waste & Inventory Impact** – Connects stock usage to margin impact.  
- **Daily Performance Monitoring** – Tracks revenue, labour, and profit per location/day.  

# Screenshots

**Pipelines:** Bronze ingestion pipeline from OneLake → Bronze tables.  

![Medallion Architecture](staging.png)

**Lakehouse:** Tables for Bronze, Silver, Gold with schema and sample data.  

![Medallion Architecture](lakehouse.png)

**Dashboard:** Power BI report with KPI Cards, Matrix, Column and Waterfall charts.  

![Medallion Architecture](PBIReport.png)

# Project Structure

ms-fabric-medallion-project/
│
├─ README.md
├─ datasets/
│ ├─ sales.csv
│ ├─ labour.csv
│ ├─ reviews.csv
│ └─ inventory.csv
├─ notebooks/
│ ├─ bronze_ingestion.ipynb
│ ├─ silver_transforms.ipynb
│ └─ gold_aggregation.ipynb
├─ pipelines/
│ └─ bronze_pipeline.json
└─ reports/
└─ powerbi/
└─ gold_metrics.pbix


