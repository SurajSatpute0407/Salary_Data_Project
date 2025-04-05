# Salary Data Pipeline with Azure Databricks

This repository contains three notebooks that demonstrate a basic data pipeline using the **medallion architecture** (Raw → Bronze → Silver → Gold) in Azure Databricks. The source data is salary-related and goes through ingestion, cleaning, transformation, and aggregation phases.

---

## 📘 Notebooks

### 1. `Bronze_Raw.ipynb`
> Ingests raw CSV data and stores it in the Bronze layer in a parquet format.

**Steps:**
- Connects to Azure Blob Storage using `dbutils.fs.mount`
- Reads raw CSV from `/mnt/blob_storage`
- Performs cleaning:
  - Drops null or malformed rows
  - Renames columns
  - Applies necessary data formatting
- Writes the cleaned data to the **Bronze Delta table** (`/mnt/adls_storage/Bronze/salary_data`)

---

### 2. `Bronze_to_silver.ipynb`
> Processes Bronze data into cleaned, enriched Silver layer tables.

**Steps:**
- Reads the Delta table from the Bronze layer
- Applies additional transformations:
  - Filters irrelevant records
  - Selects meaningful columns
  - Ensures data integrity and consistency
- Writes final dataset to the **Silver Delta table** (`/mnt/adls_storage/Silver/salary_data`)

---

### 3. `silver_to_gold_tables.ipynb`
> Final transformation step to generate Gold-level analytics tables. Final step that exports or integrates Gold layer data into **SQL Server Management Studio (SSMS)**.

**Steps:**
- Reads cleaned data from the **Silver Delta table**
- Applies advanced transformations:
  - Aggregations (e.g., average salary, totals)
  - Joins with other reference data (if any)
  - Creates business-focused metrics or summaries
- Writes final analytics dataset to the **Gold Delta table** (`/mnt/adls_storage/Gold/salary_summary`)

---

## 🚀 How to Use

1. **Clone the repo** and open in Azure Databricks.
2. **Run notebooks sequentially** from 01 to 03.
3. Make sure `file_paths` and dependencies (e.g., PySpark, mount, SQL connectors) are configured correctly.

> ⚠️ Note: Each notebook begins with a `%run file_paths_updt` to load global file paths and configurations. Ensure this file/script exists.

---

## 🧱 Architecture Used

```
 Raw Storage (CSV) 
     ↓
 Bronze Layer (Cleaned & Stored as Delta)
     ↓
 Silver Layer (Transformed, Filtered, Optimized)
     ↓
 Gold Layer (Aggregated, Business-level Tables)

```
---


## 💡 Key Technologies

- Apache Spark (PySpark)
- Azure Databricks
- Azure Blob Storage
- SQL Server / SSMS
- Delta Lake
- Azure Data Factory

---

## 📎 Notes
- Make sure your Azure credentials are updated for `dbutils.fs.mount`
- This pipeline is modular and can be extended to a Gold layer for aggregations or analytics
- This pipeline is modular and can be extended with streaming or ML models

---

## 👨‍💻 Author
Suraj Satpute
