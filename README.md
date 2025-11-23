# 🌍 OpenAQ Real-Time Air Quality Pipeline
### End-to-End ETL Pipeline using OpenAQ API, Databricks, Delta Lake & PySpark

![Badge](https://img.shields.io/badge/Python-3.10%2B-blue?logo=python)
![Badge](https://img.shields.io/badge/Databricks-Spark-red?logo=databricks)
![Badge](https://img.shields.io/badge/Apache_Spark-ETL-orange?logo=apachespark)
![Badge](https://img.shields.io/badge/Delta_Lake-ACID-green?logo=deltalake)
![Badge](https://img.shields.io/badge/MinIO-Object_Storage-yellow?logo=minio)
![Badge](https://img.shields.io/badge/ETL-Pipeline-blueviolet)
![Badge](https://img.shields.io/badge/Status-Production_Ready-brightgreen)


This project implements a complete real-time Air Quality Data Engineering pipeline built with:

- OpenAQ API (global real-time air-quality data)
- Databricks (Spark, Delta Lake, notebooks, SQL)
- PySpark (ETL transformations)
- MinIO (S3 object storage)
- GitHub (version control & documentation)

It covers: Ingestion → Bronze → Silver → Gold → Analytics → Version Control

---

# 🏗️ Architecture Overview

OpenAQ API → MinIO (Raw Storage) → Bronze (Raw Delta Table)
          → Silver (Cleaned & Standardized Table)
          → Gold (Aggregated Analytics)
          → Spark SQL & BI Dashboards

---

# 📦 Project Structure

OpenAQ-Real-Time-Air-Quality-Pipeline/
│
├── notebooks/
│   └── AirQuality_Pipeline.ipynb
├── src/
│   ├── ingestion_openaq.py
│   ├── upload_to_minio.py
│   ├── silver_cleaning.py
│   └── gold_aggregations.py
├── exports/
│   ├── pipeline.html
│   ├── pipeline.pdf
├── datasets/
│   └── sample_raw.json
└── README.md

---

# 🥇 Bronze Layer – Raw Ingestion

• Fetches full global dataset with pagination  
• JSON stored in MinIO: air-quality-raw/YYYY/MM/DD/  
• In-memory upload using BytesIO  
• Delta Bronze table created in Databricks  

---

# 🥈 Silver Layer – Cleaned & Standardized

• Flatten nested JSON structures  
• Remove arrays: licenses, instruments, sensors  
• Standardize strings: UPPER(), TRIM()  
• Remove rows missing critical fields (id, lat, lon, country_name)  
• Drop columns where all values are NULL  

Output Table:
air_quality_silver_locations

---

# 🥇 Gold Layer – Aggregated Analytics

Country-Level Metrics:
• Total stations  
• Average latitude, longitude  
• Station distribution  

Saved as:
air_quality_gold_country_stats

---

# 📊 SQL & PySpark Analytics Examples

SQL Filtering:
SELECT * FROM air_quality_silver_locations WHERE country_name = 'INDIA';

SQL Aggregation:
SELECT country_name, COUNT(*) FROM air_quality_silver_locations GROUP BY country_name;

PySpark Filter:
df_silver.filter(df_silver.country_name == "UNITED STATES").show();

---

# 🗂️ Data Storage (Delta Lake)

• Bronze: air_quality_bronze  
• Silver: air_quality_silver_locations  
• Gold: air_quality_gold_country_stats  

---

# 🚀 Future Enhancements

• Schedule pipeline (every 5 hrs)  
• ML forecasting  
• Real-time streaming  
• BI dashboards  

---

# 👤 Author
**Subham Mohanty**  
GitHub: https://github.com/skmohanty2628
