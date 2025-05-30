# 🌍 Air Quality Data Pipeline Using Snowflake & Python

This project builds an end-to-end data pipeline to ingest, process, and visualize Air Quality Index (AQI) data using public APIs, Snowflake, and Streamlit. The pipeline is fully automated with GitHub Actions and demonstrates modern data engineering practices.

<img width="1202" alt="Layered-Architecture-Standard-Names" src="https://github.com/user-attachments/assets/5b4b2dc8-ae77-44b8-8b23-b8d6ff3274ee" />


## 📌 Features

- **Automated hourly data ingestion** from public air quality APIs using Python and GitHub Actions.
- **Multi-stage pipeline in Snowflake**: Ingestion → Staging → Transformation → Consumption.
- **Metadata tracking** and **MD5 hashing** to ensure data integrity and prevent duplicate file loads.
- **Fact & Dimension modeling** for scalable reporting and analytics.
- **Dynamic Tables and Tasks** in Snowflake for incremental, event-driven processing.
- **Data visualization** using Streamlit embedded in Snowflake UI.
- **Weather data integration** from Snowflake Marketplace for enriched analysis.

---

## 🧰 Tech Stack

- **Languages**: Python (Requests, Snowpark, Pandas)
- **Data Platform**: Snowflake (Internal Stage, Tasks, Dynamic Tables, Streamlit)
- **Orchestration**: GitHub Actions
- **Cloud Services**: Snowflake Marketplace (for Weather Data)
- **Data Modeling**: Star Schema (Fact/Dimension)
- **Other Tools**: Git, Docker (optional), Linux

---

## 🛠 Pipeline Architecture

1. **Ingestion Layer**
   - Python script pulls data from public API and uploads JSON files to Snowflake Internal Stage.
   - GitHub Actions triggers ingestion every hour.

2. **Staging & Metadata**
   - Data loaded into a raw staging table.
   - Metadata and MD5 hashes logged in a separate table to avoid duplicate processing.

3. **Transformation Layer**
   - Null handling and deduplication using `ROW_NUMBER()` over timestamps.
   - Flattening nested JSON structures to extract pollutants per station.
   - Use of **Dynamic Tables** with `target_lag = downstream` for reactive updates.

4. **Modeling Layer**
   - Creation of Fact Tables for AQI metrics per pollutant/station.
   - Dimension Tables for time (year, month, day, hour) and location (city, country, coordinates).
   - Aggregated tables: AQI per city per hour/day.

5. **Enrichment Layer**
   - Integration of weather data from Snowflake Marketplace.
   - Join AQI with temperature data for enhanced analytics.

6. **Visualization**
   - Interactive Streamlit dashboards within Snowflake for exploring AQI trends.

---

## 📈 Sample Outputs

![Streamlit_India_AQI_Date](https://github.com/user-attachments/assets/80d81eba-d2c8-4bd4-9906-4b63ec5b1065)


![Streamlit_India_AQI_Stations](https://github.com/user-attachments/assets/2c473c19-d832-4148-816d-82de54d97f58)


## Final DAG

![Streamlit_India_AQI_DAG](https://github.com/user-attachments/assets/ef2f0c70-67a8-4da1-818d-968fdaae0457)




## 🔒 Security & Limitations

- Only non-sensitive public data is used. (https://www.data.gov.in/resource/real-time-air-quality-index-various-locations)
- Assumes access to Snowflake and permissions to create tasks, stages, and Streamlit apps.

---



