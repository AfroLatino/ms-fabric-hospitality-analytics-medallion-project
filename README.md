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
- Microsoft Fabric
- PySpark
- Power BI

# Medallion Design 

The Medallion Architecture ensures data quality, traceability, and readiness for analytics through three layers:

**Bronze Layer (Raw Data)**

- Stores original source files exactly as ingested.
- Minimal transformations to preserve fidelity.
Example: Raw sales.csv with all transactions, including duplicates and invalid entries. \

**Silver Layer (Cleaned / Standardised Data)**

- Cleans data: removes duplicates, fixes nulls, and filters invalid values.
- Standardises column types for analytical consistency.
Example: Negative sales quantities removed, duplicate labour records removed.

**Gold Layer (Business Aggregates)**

- Aggregates business metrics for reporting and analytics.
- Output: total_revenue, total_labour_cost, profit by date and location_id.
Example: Gold table shows location MCR01 had £40 revenue, £156 labour cost, profit -£116 on 2025-01-01.

**Flow:**
Bronze (Raw) → Silver (Cleaned) → Gold (Aggregated) → Power BI Dashboards

# Key Insights

From the Gold layer and dashboards, we can highlight:

**Labour Cost % vs Revenue**
 - Locations where labour cost is disproportionately high (e.g., MCR01 on 2025-01-01: -£116 profit).
 - This helps to optimise staffing and scheduling.

**Profitability Analysis**
 - Identifies underperforming locations/days and take corrective action.
 - Gold metrics allow daily profit monitoring.

**Waste and Inventory Impact**
- Low stock or inventory mismanagement reflected in sales and profitability trends.
- Combined with labour costs, shows overall operational efficiency.

**Daily Performance Monitoring**
- Tracks total revenue, labour cost, and profit by location/day.
- Enables quick decisions and performance comparisons across stores.
