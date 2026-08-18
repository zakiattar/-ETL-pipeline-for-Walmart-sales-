📌 Project Overview
This project simulates a real-world data engineering workflow: ingesting raw retail sales data, cleaning it, engineering useful features, running business-critical aggregations, and persisting the results in an optimized format for downstream analytics.
Tech Stack: PySpark · Databricks (Community Edition) · Parquet / CSV
---
📂 Dataset
The dataset used is Walmart's historical weekly sales data, containing:
Column	Description
`Store`	Store identifier
`Date`	Week ending date
`Weekly_Sales`	Sales for the given store and week
`Holiday_Flag`	Whether the week included a holiday (1/0)
`Temperature`	Average temperature in the region
`Fuel_Price`	Fuel price in the region
`CPI`	Consumer Price Index
`Unemployment`	Unemployment rate in the region
---
⚙️ Pipeline Steps
1. Data Ingestion
Loaded the raw CSV into a Spark DataFrame with schema inference.
2. Data Cleaning
Checked and handled null values across all columns
Removed duplicate records
Validated the `Date` column's data type
3. Feature Engineering
Extracted `Year`, `Month`, and `Week` from the `Date` column to enable time-based analysis.
4. Transformations & Aggregations
Store-wise total sales and ranking
Month-over-month sales growth (%) per store using window functions (`lag`)
4-week rolling average of sales using `rowsBetween` window function
Pivot table — Store vs Year sales matrix
Top 5 / Bottom 5 performing stores
Holiday vs non-holiday average sales comparison
Correlation analysis between `Weekly_Sales` and external factors (`Temperature`, `Fuel_Price`, `CPI`, `Unemployment`)
5. Data Output
All cleaned data and aggregation results were saved as partitioned Parquet/CSV files, partitioned by `Year` and `Month` for efficient downstream querying.
---
📊 Key Insights
Sales performance varies significantly across stores, with a clear top and bottom tier.
Certain months show consistent seasonal spikes in sales.
Holiday weeks show a measurable difference in average sales compared to regular weeks.
External economic factors (fuel price, CPI, unemployment) show varying degrees of correlation with weekly sales.
---
🛠️ Skills Demonstrated
PySpark DataFrame operations
Data cleaning & validation
Feature engineering
Window functions (`rank`, `lag`, rolling aggregates)
Pivoting & multi-dimensional aggregation
Partitioned data output (Parquet/CSV)
Databricks notebook workflow
