# GCP Healthcare Data Pipeline

This project demonstrates how to build a clean, production-style data pipeline on Google Cloud Platform using BigQuery and Airflow-style orchestration.  

The goal is to transform raw healthcare appointment data into reliable, analytics-ready datasets that can be used to understand and reduce patient no-shows.

---

## Why this project?

Missed medical appointments are a real operational problem for healthcare providers.  
This pipeline focuses on analyzing **appointment no-shows by age group and neighborhood**, which are common dimensions used by operations and analytics teams to improve scheduling and outreach strategies.

---

## What this pipeline does

1. Loads raw appointment data into **BigQuery**
2. Cleans and standardizes the data in a **staging** layer  
3. Applies **data quality and validation** checks  
4. Builds an **analytics mart** with aggregated metrics  
5. Orchestrates the workflow using an **Airflow DAG** pattern

The result is a dataset that can be directly used for dashboards, reporting, or downstream analytics.

---

## Architecture Overview

The pipeline follows a layered design commonly used in production data platforms:

Raw BigQuery Table
↓
Staging Layer (cleaned & typed)
↓
Analytics Mart (aggregated metrics)
↓
Dashboards / Reporting / ML


Each layer has a clear responsibility and can be independently validated.

---


### Architecture Diagram

![Architecture Diagram](diagrams/architecture.png)


## Repository Structure

gcp-healthcare-data-pipeline/
│
├── dags/
│ └── healthcare_etl_dag.py # Airflow DAG (Composer-style)
│
├── sql/
│ ├── staging/
│ │ └── stg_appointments.sql # Raw → Staging transformations
│ └── marts/
│ └── appointments_mart.sql # Staging → Analytics mart
│
├── python/
│ └── data_quality_checks.py # Data validation logic
│
├── data/
│ └── raw/ # Reference to raw dataset
│
├── requirements.txt
└── README.md


---

## Data Quality & Validation

Several checks are applied during the staging process to ensure reliability:

- Primary key validation (`appointment_id`, `patient_id`)
- Age validation (restricted to realistic values)
- Boolean normalization for no-show indicators
- Duplicate appointment detection
- Temporal sanity checks between scheduled and appointment dates

Minor anomalies are documented rather than silently dropped.

---

## Analytics Output

The final analytics table is designed for easy reporting and contains:

- Neighborhood
- Age group
- Total appointments
- Number of no-shows
- No-show rate

This structure is intentionally simple so it can plug directly into BI tools or be used for further analysis.

---

## Tools & Technologies

- Google BigQuery
- SQL
- Apache Airflow (Cloud Composer pattern)
- Python
- Git & GitHub

---

## What this project demonstrates

- Designing cloud-based data pipelines
- Writing production-ready SQL transformations
- Applying practical data quality checks
- Building analytics marts for business use cases
- Organizing code in a maintainable repository structure

---

## Dataset

Source: Kaggle – *Medical Appointment No Shows*  
Used strictly for learning and portfolio demonstration purposes.

---

## Author

**Ananya Rachuri**  
Data Engineer | Cloud & Analytics
