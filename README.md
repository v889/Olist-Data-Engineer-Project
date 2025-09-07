🏗 Project: Olist E-commerce Data Pipeline using Medallion Architecture
🔹 Architecture Flow

Bronze Layer (Raw Ingestion)

Data stored in Azure Data Lake Storage Gen2 (ADLS) in CSV format.

Sources: Olist datasets (Orders, Customers, Payments, Products, Sellers, Reviews, Geolocation).

🔧 Tool: Azure Data Factory (ADF) → Ingest raw files into ADLS bronze/.

Silver Layer (Transformation & EnrichmentGot it 🚀 Vishal! Since you’re preparing to share this project on **LinkedIn**, the best way is to present your work as a **modern Medallion Architecture pipeline** (Bronze → Silver → Gold) showing how you’ve integrated **Azure Data Factory, Databricks, ADLS Gen2, Synapse, MongoDB, and Power BI**.

Here’s a clean **architecture you can showcase**:

---

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

---

### 🔹 LinkedIn Post Draft

🚀 Excited to share my latest **Data Engineering project** where I implemented the **Medallion Architecture (Bronze → Silver → Gold)** using Azure services on the **Olist E-commerce dataset**!

🔹 **Tech Stack Used**:

* **Azure Data Factory (ADF)** → Ingestion from raw CSVs into ADLS Gen2 (Bronze).
* **Azure Databricks (PySpark)** → Data cleaning, joins, enrichment with MongoDB, stored in Parquet/Delta (Silver).
* **Azure Synapse Analytics** → Created views & external tables for business-ready datasets (Gold).
* **Power BI** → Interactive dashboards for revenue, customer retention, and product insights.

💡 Key Highlights:

* Designed an **end-to-end data pipeline** with modern **Lakehouse architecture**.
* Enriched datasets using external **MongoDB** metadata.
* Automated data flow from **raw to analytics-ready** tables.

📊 Outcome: Business stakeholders can now explore **real-time insights** on sales performance, product categories, and customer trends through **Power BI dashboards**.

