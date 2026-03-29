# ms-fabric-hospital-analytics-medallion-project
Interactive end-to-end MS Fabric Hospitality Analytics Medallion project: ingest, clean, aggregate data, and visualise business KPIs in Power BI.

# Overview

**Business Problem**

Retail locations struggle to monitor daily operational efficiency because sales revenue, labour costs, and inventory usage are tracked in separate systems, making it difficult to quickly understand profitability and make data-driven decisions.

**Why it matters:**

- Managers cannot easily identify locations with high labour costs relative to revenue.
- Inefficiencies like waste, stock-outs, or overstaffing reduce overall profitability.
- Timely, aggregated insights help optimise staffing, control costs, and maximise profit margins.
- Provides a single source of truth for reporting, enabling faster and more confident decisions.

# Architecture

![Medallion Architecture](images/architecture.png)

# Tech Stack

| Component | Purpose |
|-----------|---------|
| CSV / Text Files | Source datasets: sales, labour, inventory, reviews |
| Microsoft Fabric (OneLake, Lakehouse, Pipelines) | Data ingestion, storage, transformation, orchestration |
| PySpark | Data processing and transformations |
| Power BI | Visualisation of Gold layer metrics |

# Project Overview

This project demonstrates an **end-to-end Medallion architecture** in Microsoft Fabric:

- Bronze Layer: Raw CSV ingestion for Sales, Labour, Reviews, Inventory
- Silver Layer: Data cleaning, de-duplication, type standardization
- Gold Layer: Aggregated business metrics (`total_revenue`, `total_labour_cost`, `profit`) per `date` and `location_id`
- Power BI Report: Interactive dashboard for daily performance metrics

# Datasets
The datasets are included in the `datasets/` folder:
- `sales.csv` — transactional sales data
- `labour.csv` — employee work hours
- `reviews.csv` — customer feedback
- `inventory.csv` — stock levels

# Key Insights

- **Labour Cost % vs Revenue** – Identifies high labour cost locations/days.  
- **Profitability Analysis** – Monitors negative profits and underperforming locations.  
- **Waste & Inventory Impact** – Connects stock usage to margin impact.  
- **Daily Performance Monitoring** – Tracks revenue, labour, and profit per location/day.  

# Screenshots

**Pipelines:** Bronze ingestion pipeline from OneLake → Bronze tables.  

![Medallion Architecture](images/staging.png)

**Lakehouse:** Tables for Bronze, Silver, Gold with schema and sample data.  

![Medallion Architecture](images/lakehouse.png)

**Dashboard:** Power BI report with KPI Cards, Matrix, Column and Waterfall charts.  

![Medallion Architecture](reports/PBIReport.png)

# Project Structure

```
ms-fabric-hospitality-analytics-medallion-project/
│
├─ datasets/ Raw input files
│   ├─ sales.csv
│   ├─ reviews.csv
│   ├─ labour.csv
│   └─ inventory.csv
│
├─ images/ Architecture diagram
│   └─ architecture.png
│
├─ notebooks/ Data transformations
│   ├─ silver_transformations.ipynb
│   └─ gold_aggregations.ipynb
│
├─ pipelines/ Data ingestion (Bronze layer)
│   └─ bronze_pipeline.json
│
├─ reports/ Power BI dashboard
│   └─ gold_metrics.pbix
│
└─ README.md
```

# Steps to Reproduce

1. Upload CSV files from `/datasets` into OneLake staging (Files section of Lakehouse)

2. Run Bronze ingestion:
   - Run Fabric pipeline
   - Output: Bronze tables (`bronze_sales`, `bronze_labour`, `bronze_reviews`, `bronze_inventory`)

3. Run Silver transformations:
   - Execute `silver_transformations.ipynb`
   - Cleans data (removes duplicates, filters invalid values)

4. Run Gold aggregation:
   - Execute `gold_aggregations.ipynb`
   - Output table: `gold_daily_metrics`

5. Open Power BI report:
   - Load `gold_metrics.pbix`
   - Connect to `gold_daily_metrics`
   - View dashboard visuals
   
# Notes

- This project demonstrates a simplified Medallion Architecture using small datasets for clarity.
- Gold layer currently contains 4 aggregated rows for demonstration purposes.
- In a real-world scenario, datasets would be significantly larger and ingested via pipelines or APIs.
- The architecture is scalable — additional data sources (APIs, streaming, etc.) can be integrated into the Bronze layer.
- Power BI dashboard is designed to highlight key business KPIs such as revenue, labour cost and profitability.
