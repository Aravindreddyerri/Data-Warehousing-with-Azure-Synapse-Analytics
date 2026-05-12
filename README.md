# End-to-End Azure Data Engineering and Analytics Pipeline

This project demonstrates an end-to-end Azure-based data engineering and analytics solution for customer booking and property analysis. The pipeline ingests raw datasets into Azure Data Lake Storage Gen2, processes them in Azure Synapse Analytics using PySpark, stores curated outputs in Delta Lake, loads analytics-ready tables into a Synapse Dedicated SQL Pool, and visualizes insights in Power BI .

## Project Overview

The objective of this project is to build a scalable cloud analytics pipeline that transforms raw booking and property data into business-ready datasets for reporting and decision-making. The implementation follows a modern Azure architecture that covers ingestion, transformation, storage, warehousing, validation, and visualization .

## Architecture

The solution follows this flow:

`Raw Data Files → Azure Data Lake Storage Gen2 (ADLS) → Azure Synapse Analytics Spark Notebook → Delta Lake Tables → Data Cleansing and Transformation → Synapse Dedicated SQL Pool → Power BI Dashboard`

This architecture supports a complete analytics lifecycle from raw data ingestion to enterprise reporting 

## Technologies Used

- Azure Data Lake Storage Gen2 (ADLS) 
- Azure Synapse Analytics
- Apache Spark with PySpark 
- Delta Lake 
- Synapse Dedicated SQL Pool 
- JDBC Connector 
- Power BI 

## Dataset

The project uses one fact table and four dimension tables sourced from Kaggle and uploaded into ADLS for processing .

### Source files

- `Fact_Bookings.csv`
- `Dim_Customer.csv`
- `Dim_Property.csv`
- `Dim_Date.csv`
- `Dim_Host.csv`

## Project Workflow

### 1. Data Ingestion

Raw booking and property datasets were uploaded into an ADLS Gen2 raw container and linked to the Synapse workspace for processing. This stage established the landing zone for all source files used in downstream transformations .

### 2. Data Processing in Synapse Spark

The raw files were loaded from ADLS into Synapse Spark notebooks, where data cleansing and standardization were applied . Joins and transformation logic were then used to prepare analytics-ready outputs for reporting .

### 3. Delta Table Creation

The transformed datasets were stored in Delta Lake format to provide reliable storage, schema enforcement, and better query performance . The project created Delta tables for customer analytics and property analytics .

### 4. SQL Pool Integration

The analytics-ready DataFrames were loaded into Synapse Dedicated SQL Pool using JDBC . The SQL tables were pre-created before loading to avoid schema mismatch and columnstore-related issues .

### 5. Data Validation

Validation was carried out in the Dedicated SQL Pool using row-count checks and sample-record queries . This step ensured that the transformed data was loaded correctly into the analytics tables.

### 6. Reporting and Visualization

Power BI was connected to Synapse Dedicated SQL Pool to build interactive dashboards and reporting visuals . The final dashboard delivered business insights on bookings, revenue, customer behavior, and property performance .

## Data Transformations

The transformation layer was implemented in Azure Synapse Analytics using PySpark . The source data included one fact table and four dimension tables, which were combined and transformed into analytics-ready datasets through cleaning, joins, aggregations, filtering, upserts, and merge operations.

### Transformation activities

- Loaded raw fact and dimension files from ADLS into Synapse Spark
- Cleaned and standardized column names and data formats 
- Joined fact and dimension tables to enrich the booking dataset 
- Applied groupBy and aggregation logic to derive business insights 
- Created two analytics DataFrames: `df_customer_analytics` and `df_property_analytics` 
- Stored the transformed outputs as Delta tables 
- Applied filter conditions to the transformed datasets before update operations 
- Performed upsert operations into Delta tables
- Merged filtered datasets back into Delta tables for refined analytics outputs 

### Transformation flow

- `df1` → Delta Table 1 
- `df2` → Delta Table 2 
- `df1_filter1` → Upsert → Delta Table 1 
- `df2_filter2` → Upsert → Delta Table 2 
- `df1_filter1` → Merge → Delta Table 1 
- `df2_filter2` → Merge → Delta Table 2 

These transformations converted raw operational data into curated datasets ready for warehousing and dashboard reporting.

## Analytics Outputs

The main analytics DataFrames created in the transformation phase were `df_customer_analytics` and `df_property_analytics` . These outputs were first stored in Delta tables and later loaded into Synapse Dedicated SQL Pool for reporting and BI use cases .

## JDBC Configuration

The Synapse Dedicated SQL Pool connection used a JDBC URL in the following format :

```python
jdbc_url = "jdbc:sqlserver://arvindwork.sql.azuresynapse.net:1433;database=dedicatedsqlpool"
```

The final analytics tables were written into SQL Pool tables such as `dbo.customer_analytics` and `dbo.property_analytics` 

## Data Validation Queries

Example validation queries used after loading data into the SQL Pool :

```sql
SELECT COUNT(*) FROM dbo.customer_analytics;
SELECT TOP 10 * FROM dbo.customer_analytics;
```

## Power BI Dashboard

The Power BI dashboard was designed using Synapse Dedicated SQL Pool as the source system . The dashboard included KPIs and analysis views such as Total Revenue, Total Bookings, Revenue by Country, Revenue by Property Type, Customer Segmentation, Weekend vs Weekday Analysis, and Host Performance Metrics .



<img width="980" height="562" alt="Screenshot 2026-05-12 at 5 06 44 PM" src="https://github.com/user-attachments/assets/a2d56f93-2410-4973-af4f-cdc842845d2b" />

<img width="923" height="546" alt="Screenshot 2026-05-12 at 5 08 02 PM" src="https://github.com/user-attachments/assets/02265b5f-4708-4cfb-84a0-185056b57cfc" />


## Key Features

- End-to-end Azure analytics pipeline 
- ADLS-based raw data ingestion 
- PySpark-based transformation logic in Synapse 
- Delta Lake storage for curated datasets 
- JDBC-based loading into Synapse Dedicated SQL Pool 
- SQL-based data validation 
- Power BI dashboard integration 
- Practical handling of schema mismatches, duplicate columns, JDBC connectivity issues, and performance bottlenecks 

## Business Value

This project shows how Azure services can be combined to build a scalable analytics platform for enterprise-style reporting . It also demonstrates hands-on experience in data ingestion, transformation, warehousing, and dashboard development using a real-world cloud data engineering workflow .

## Conclusion

This project successfully implements an end-to-end Azure analytics pipeline using ADLS, Synapse Spark, Delta Lake, Synapse Dedicated SQL Pool, and Power BI . It highlights practical cloud data engineering skills and demonstrates how raw datasets can be transformed into analytics-ready insights for business intelligence reporting .

