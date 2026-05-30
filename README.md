# 📊 End-to-End Analytics Pipeline (dbt + PostgreSQL)

An enterprise-grade Data Engineering pipeline that transforms raw transactional sales data into a cleaned, optimized Star Schema Warehouse using **dbt Core** and **PostgreSQL**, governed by automated Data Quality testing.

---

## 🚀 Project Architecture
The project isolates raw source mutations from the analytics layer using a multi-tiered environment:
1. **Source Layer:** Raw transactional schemas (`FACT_Orders`, customer seeds) hosted on PostgreSQL.
2. **Staging Layer (`models/staging`):** Handles explicit data type casting, column standardizations, and critical data purging.
3. **Marts Layer (`models/marts/core`):** Models final business entities into fully optimized Fact and Dimension tables ready for BI ingestion (Power BI).

---

## 🛠️ Key Data Cleansing & Business Logic
During development, explicit data profiling caught severe anomalies in the raw dataset. The pipeline resolves them programmatically:

* **Granularity Protection (Deduplication):** Caught duplicate occurrences of transactional `Row ID`s (e.g., Row 4858). Resolved dynamically in `stg_orders.sql` using a window function layout:
  ```sql
  row_number() over (partition by "Row ID" order by "Row ID") as row_num
  
🧪 Data Governance & Testing
Automated testing models were built directly into the core schemas (core_schema.yml) to validate schema compliance on every pipeline run:

unique and not_null tests assigned to primary surrogate keys (customer_key, row_id).

All tests execute automatically via dbt test ensuring 100% data trust.

💻 Tech Stack
Data Transformation & Modeling: dbt (data build tool) Core

Database Engine: PostgreSQL

SQL Dialect: Postgre-SQL PL/pgSQL

Documentation Hosting: Netlify

🔗 Live Deployments
Interactive Data Documentation & Lineage DAG: [https://phenomenal-sherbet-73c932.netlify.app/#!/overview?g_v=1]
