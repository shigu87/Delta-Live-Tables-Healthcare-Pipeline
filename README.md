# Healthcare Data Processing with Delta Live Tables (DLT) in Databricks

## Table of Contents
- [Introduction](#introduction)
- [Technologies Used](#technologies-used)
- [Project Workflow](#project-workflow)
- [Setup Instructions](#setup-instructions)
- [Challenges Faced](#challenges-faced)
- [Outcome](#outcome)
- [Real-World Usefulness](#real-world-usefulness)
- [Future Improvements](#future-improvements)
- [Steps to Run the Pipeline](#steps-to-run-the-pipeline)
- [Conclusion](#conclusion)


## Introduction

This project demonstrates real-time healthcare data processing using **Delta Live Tables (DLT)** in Databricks. The pipeline ingests patient data from raw CSV files, processes it using Delta Live Tables, and performs data transformations to generate valuable insights, such as patient statistics based on diagnosis and gender.

## Technologies Used

- **Databricks**: A unified analytics platform for big data and machine learning.
- **Delta Live Tables (DLT)**: A fully managed service to build, automate, and monitor data pipelines on Databricks.
- **PySpark**: A Python API for Apache Spark, used for data processing and transformations.
- **Delta Lake**: A storage layer that brings ACID transactions to Apache Spark and big data workloads.
- **SQL**: For querying data within Databricks notebooks and Delta Live Tables.

## Project Workflow

1. **Ingest Raw Data**:  
   Raw healthcare data (patients and diagnosis) is ingested from CSV files into Delta tables.

2. **Bronze Table**:  
   In this stage, the raw ingested data is stored without any transformations, allowing for historical tracking of the raw records.

3. **Silver Table**:  
   Data is cleaned and transformed, including joins with other datasets (e.g., diagnosis descriptions) to enhance the raw data.

4. **Gold Table**:  
   Data is aggregated and enriched, creating the final tables that are ready for reporting and analysis.

5. **Delta Live Tables Pipeline**:  
   A fully managed pipeline orchestrates the processing of data in real-time from raw ingestion to analytics-ready gold tables.

## Setup Instructions

### Prerequisites

- **Databricks workspace** with access to **Delta Lake**.
- **Databricks Unity Catalog** to manage Delta tables.
- **Delta Live Tables (DLT)** enabled for real-time processing.
- **Raw data files** in CSV format (diagnosis and patient data).

### Installation

1. **Set up a Databricks workspace** if you haven't already.
2. **Upload the raw data files** into **DBFS (Databricks File System)**:
   - `dbfs:/FileStore/shivam/raw_data/diagnosis_mapping.csv`
   - `dbfs:/FileStore/shivam/raw_data/patients_daily_file_1_2024.csv`
   - `dbfs:/FileStore/shivam/raw_data/patients_daily_file_2_2024.csv`
   - `dbfs:/FileStore/shivam/raw_data/patients_daily_file_3_2024.csv`

3. **Ensure Delta Live Tables (DLT)** is enabled in your Databricks environment for processing and transforming data.


## Challenges Faced

- **Handling Large Data Volumes**:  
   The real-time nature of the pipeline meant that the raw data files were large. Processing them efficiently in near real-time required careful resource management and partitioning strategies.

- **Data Quality**:  
   Ensuring that all incoming data was of high quality (e.g., no missing values for important columns) was a challenge. This was addressed with data validation and quality checks in the Silver layer.

- **Schema Evolution**:  
   The healthcare data could evolve with new diagnosis codes or additional patient information. Managing schema changes dynamically required leveraging Delta Lake’s schema evolution features.

## Outcome

- **Real-Time Data Processing**:  
   Achieved real-time processing of healthcare data from raw ingestion to aggregated insights.

- **Data Quality**:  
   Ensured high data quality through validation checks in the Silver layer, allowing for accurate analytics.

- **Scalability**:  
   The Delta Live Tables pipeline can scale with increasing data volumes, automatically handling updates and maintaining data integrity.

- **Insights**:  
   Created valuable reports such as patient statistics by diagnosis, gender, and age, providing actionable insights for healthcare decision-makers.

## Real-World Usefulness

This solution is highly applicable in healthcare environments where timely and accurate data is crucial. By using Delta Live Tables in Databricks, healthcare organizations can:

- Monitor patient statistics in real-time for better decision-making.
- Ensure compliance with data quality standards and regulatory requirements.
- Provide actionable insights for clinicians and administrators to improve patient care and operational efficiency.

## Future Improvements

- **Anomaly Detection**:  
   Implement machine learning models in the pipeline to detect unusual patterns in patient data, such as sudden increases in specific diagnoses.

- **Integration with External Datasets**:  
   Enrich patient data by integrating with other healthcare datasets (e.g., insurance data, historical medical records) to provide more comprehensive insights.

- **Automated Reporting and Dashboards**:  
   Set up automated dashboards and reports that update in real-time with the latest data, helping healthcare professionals make informed decisions.

- **Real-Time Alerts**:  
   Add a real-time alerting system for specific diagnoses or patient demographics that require immediate attention.

## Steps to Run the Pipeline

### 1. Set Up Databricks Workspace
- Ensure to have access to a Databricks workspace.
- Create a new cluster in Databricks.
- Set up a new notebook in SQL for Delta Live Tables and a Python notebook for data ingestion.

### 2. Create Source Tables (Raw Data)
- Ingest the raw data into Delta tables using the `spark_code_to_feed_tables.ipynb` notebook. The raw data consists of two primary datasets:
   - `diagnosis_mapping.csv`: Maps diagnosis codes to descriptions.
   - `patients_daily_file_X_2024.csv`: Contains daily patient records.

### 3. Create Delta Live Tables (DLT) Pipelines
- The `healthcare_dlt_pipeline_notebook.sql` contains the SQL code to create the Delta Live Tables (DLTs). This code defines the following stages:
   - **Bronze Stage**: Raw Data Tables
   - **Silver Stage**: Data Quality and Transformation
   - **Gold Stage**: Aggregated Metrics

### 4. Run the DLT Pipeline
- Once the notebooks are configured, run the Delta Live Tables pipeline to process the data in real-time.
   - Create a new Delta Live Tables workflow.
   - Select the notebooks that define your pipeline (e.g., `healthcare_dlt_pipeline_notebook.sql`).
   - Deploy and run the pipeline in your Databricks workspace.

### 5. Monitoring and Optimizations
- Databricks provides an automated monitoring interface for DLT pipelines, ensuring that the data is processed in real-time and any failures are detected quickly.

## Conclusion

This project leverages Databricks and Delta Live Tables to build an efficient, real-time healthcare data pipeline. By transforming raw data into structured insights, it enables real-time analytics and supports decision-making in healthcare operations.
