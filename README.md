# **hr-analytics-data-pipeline**

## 📌 Overview
This project demonstrates an **end-to-end data engineering pipeline** built in **Microsoft Fabric**, covering data ingestion, transformation, modeling, and KPI generation.

Technologies used:
- **Dataflow Gen2** – for ingestion & basic transformations
- **Notebook (PySpark)** – for advanced transformations
- **Data Warehouse (T-SQL)** – for modeling & aggregation
- **Data Pipeline** – for orchestration
- **Stored Procedures** – for KPI metrics

The goal is to load employee, payroll, and leave data into a Data Warehouse, transform it into **Gold layer tables**, and generate **KPI metrics**.

---

## 🚀 Pipeline Flow
1. **Dataflow Gen2**  
   - Reads raw CSV data for employees, payroll, and leaves.  
   - Cleans & outputs to Lakehouse tables.

2. **Notebook (PySpark)**  
   - Performs extra transformations (e.g., `full_name`, filtering latest `loaded_at`).

3. **Copy Data Activities**  
   - Lakehouse → Data Warehouse Temp tables.

4. **SQL Script Activity**  
   - Creates **Gold layer tables** (`dim_employee`, `fact_payroll_monthly`, `fact_tds_obligation`).

5. **Stored Procedure Activity**  
   - Runs `getmonth` procedure to produce KPI metrics:
     - Total Gross Payroll
     - Total Net Payroll
     - Total TDS
     - Active Employees

---

## 🛠 Pipeline Design
<img src="https://github.com/user-attachments/assets/833c4d9e-44ba-41cd-8680-acda6e977e42" width="1062" height="316">

*The pipeline consists of Dataflow Gen2, PySpark Notebook, Copy Data activities, SQL Script, and Stored Procedure execution.*


---

## 📊 KPI Stored Procedure Example
```sql
EXEC getmonth @month = 5;
