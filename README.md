# 🚖 NYC Taxi Data ELT Pipeline (Azure + Databricks)

A modern data pipeline to process and analyze **NYC Green Taxi data (2023)** using **Azure Data Factory**, **Azure Databricks**, **Delta Lake**, and **Power BI** following the **Bronze → Silver → Gold** architecture.

---

## 🧱 Architecture Overview

- **Bronze**: Raw data (CSV, Parquet) ingested using Data Factory.
- **Silver**: Cleaned/transformed data via Databricks.
- **Gold**: Aggregated data stored in Delta format for Power BI.


---

## ⚙️ Tech Stack

- Azure Data Lake Storage Gen2  
- Azure Data Factory (Copy Data, ForEach, Condition)  
- Azure Databricks (PySpark + Delta Lake)  
- Power BI  
- Azure AD App (Service Principal Auth)

---

## 🔄 Pipeline Steps

1. **Data Ingestion**  
   - CSVs manually uploaded to `bronze/`  
   - Parquet pulled via URL using Azure Data Factory  

2. **Transformation**  
   - Databricks reads `bronze/`, joins metadata, and saves to `silver/`  
   - Aggregations → save to `gold/` in Delta format  

3. **Power BI**  
   - Connects to `gold/` layer for visual analysis  

---

## 🔐 Auth via Service Principal (Databricks)

```python
configs = {
  "fs.azure.account.auth.type.STORAGE.dfs.core.windows.net": "OAuth",
  "fs.azure.account.oauth.provider.type.STORAGE.dfs.core.windows.net": "org.apache.hadoop.fs.azurebfs.oauth2.ClientCredsTokenProvider",
  "fs.azure.account.oauth2.client.id.STORAGE.dfs.core.windows.net": "<CLIENT_ID>",
  "fs.azure.account.oauth2.client.secret.STORAGE.dfs.core.windows.net": "<CLIENT_SECRET>",
  "fs.azure.account.oauth2.client.endpoint.STORAGE.dfs.core.windows.net": "https://login.microsoftonline.com/<TENANT_ID>/oauth2/token"
}
```
