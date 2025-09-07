

## 🏗 Project: Olist E-commerce Data Pipeline using Medallion Architecture

### 🔹 Architecture Flow

1. **Bronze Layer (Raw Ingestion)**

   * Data stored in **Azure Data Lake Storage Gen2 (ADLS)** in CSV format.
   * Sources: Olist datasets (Orders, Customers, Payments, Products, Sellers, Reviews, Geolocation).

   🔧 Tool: **Azure Data Factory (ADF)** → Ingest raw files into ADLS `bronze/`.

---

2. **Silver Layer (Transformation & Enrichment)**

   * Data read & transformed in **Azure Databricks** using **PySpark**:

     * Joins across Orders, Customers, Payments, Products, Sellers.
     * Enrichment with external **MongoDB** data (`product_category_name` metadata).
     * Cleaning, type casting, duplicate removal.
   * Stored back to ADLS `silver/` in **Parquet/Delta** format.

   🔧 Tool: **Azure Databricks (PySpark)** + **MongoDB Atlas** (NoSQL enrichment).

---

3. **Gold Layer (Curated Business Data)**

   * Data loaded into **Azure Synapse Analytics**:

     * Created **views** (`gold.final`, `gold.final2`) on Silver parquet files.
     * Built **external tables** for delivered orders, revenue aggregations, and seller/customer KPIs.
   * Exposed to downstream analytics.

   🔧 Tool: **Azure Synapse Serverless SQL Pool**.

---

4. **Consumption Layer**

   * **Power BI** connected to Synapse Gold schema.
   * Dashboards for:

     * Revenue per seller
     * Orders by month
     * Customer churn/retention
     * Product category insights

---

### 🔹 High-Level Diagram (for LinkedIn post)

```
[ Olist Raw CSVs ]       [ MongoDB Atlas ]
         |                       |
         v                       v
  ┌──────────────────────────┐
  │  Azure Data Factory (ADF)│
  └──────────────┬───────────┘
                 v
         [ ADLS Gen2 - Bronze ]
                 |
                 v
       ┌───────────────────┐
       │  Azure Databricks │  <-- PySpark Joins, Cleaning, Enrichment
       └──────────┬────────┘
                  v
          [ ADLS Gen2 - Silver ]
                  |
                  v
     ┌──────────────────────────┐
     │ Azure Synapse Analytics  │ <-- Views, External Tables, Aggregations
     └──────────┬───────────────┘
                v
           [ ADLS Gen2 - Gold ]
                |
                v
           [ Power BI Reports ]
```
