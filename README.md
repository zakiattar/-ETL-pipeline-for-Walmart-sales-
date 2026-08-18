

## 📑 Table of Contents
- [Project Overview](#-project-overview)
- [Dataset](#-dataset)
- [Pipeline Steps](#️-pipeline-steps)
- [Key Insights](#-key-insights)
- [Skills Demonstrated](#️-skills-demonstrated)
- [How to Run](#-how-to-run)
- [Project Structure](#-project-structure)

---

## 📌 Project Overview

This project simulates a real-world data engineering workflow: ingesting raw retail sales data, cleaning it, engineering useful features, running business-critical aggregations, and persisting the results in an optimized format for downstream analytics.

**Tech Stack:** PySpark · Databricks (Community Edition) · Parquet / CSV

---

## 📂 Dataset

The dataset used is Walmart's historical weekly sales data, containing:

| Column | Description |
|---|---|
| `Store` | Store identifier |
| `Date` | Week ending date |
| `Weekly_Sales` | Sales for the given store and week |
| `Holiday_Flag` | Whether the week included a holiday (1/0) |
| `Temperature` | Average temperature in the region |
| `Fuel_Price` | Fuel price in the region |
| `CPI` | Consumer Price Index |
| `Unemployment` | Unemployment rate in the region |

> 📁 Dataset file: [`Walmart_Sales.csv`](./Walmart_Sales.csv)

---

## ⚙️ Pipeline Steps

### 1️⃣ Data Ingestion
Loaded the raw CSV into a Spark DataFrame with schema inference.

### 2️⃣ Data Cleaning
- ✅ Checked and handled null values across all columns
- ✅ Removed duplicate records
- ✅ Validated the `Date` column's data type

### 3️⃣ Feature Engineering
Extracted `Year`, `Month`, and `Week` from the `Date` column to enable time-based analysis.

### 4️⃣ Transformations & Aggregations
| Transformation | Purpose |
|---|---|
| 🏪 Store-wise total sales & ranking | Identify top/bottom performing stores |
| 📈 Month-over-month growth % (`lag`) | Track sales momentum per store |
| 📉 4-week rolling average (`rowsBetween`) | Smooth out weekly volatility |
| 🔄 Pivot table (Store × Year) | Compare yearly performance side-by-side |
| 🎉 Holiday vs non-holiday sales | Measure holiday sales lift |
| 🔗 Correlation analysis | Sales vs Temperature, Fuel Price, CPI, Unemployment |

### 5️⃣ Data Output
All cleaned data and aggregation results were saved as **partitioned Parquet/CSV files**, partitioned by `Year` and `Month` for efficient downstream querying.

---

## 📊 Key Insights

> 💡 Sales performance varies significantly across stores, with a clear top and bottom tier.
>
> 💡 Certain months show consistent seasonal spikes in sales.
>
> 💡 Holiday weeks show a measurable difference in average sales compared to regular weeks.
>
> 💡 External economic factors (fuel price, CPI, unemployment) show varying degrees of correlation with weekly sales.

---

## 🛠️ Skills Demonstrated

`PySpark DataFrames` `Data Cleaning` `Feature Engineering` `Window Functions` `Pivoting` `Partitioned I/O` `Databricks`

---

## 🚀 How to Run

```bash
1. Upload Walmart_Sales.csv to Databricks DBFS  →  /FileStore/tables/
2. Open walmart_sales_pipeline.py in a Databricks notebook
3. Attach the notebook to a running cluster
4. Run all cells in order (top to bottom)
5. Outputs are saved to  →  /FileStore/tables/walmart_output_csv/
```

---

## 📁 Project Structure

```
walmart-sales-pyspark-project/
├── walmart_sales_pipeline.py   # Full PySpark ETL pipeline
├── Walmart_Sales.csv           # Raw dataset
└── README.md                   # Project documentation
```

---

<p align="center"><i>⭐ Built as part of a Data Engineering portfolio project — feel free to fork and extend!</i></p>
