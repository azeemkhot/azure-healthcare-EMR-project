# Healthcare Revenue Cycle Management (RCM) Data Engineering Project

This project demonstrates the implementation of a modern data engineering pipeline for a healthcare Revenue Cycle Management (RCM) system using Azure Data Engineering services and the Medallion Architecture.

The solution involves the end-to-end data processing from data ingestion to transformation and storage in fact and dimension tables to support business analytics and reporting.

---

## 📚 Domain Overview: Healthcare Revenue Cycle Management (RCM)

RCM is the process hospitals use to manage the financial aspects from patient appointment scheduling to final payment collection.

### Key Steps in the RCM Process:
1. **Patient Visit:** Collection of patient and insurance details to determine the payer (insurance or patient).
2. **Service Delivery:** Medical services are provided to the patient.
3. **Billing:** A bill is generated for the services rendered.
4. **Claims Review:** Insurance company reviews the bill and may accept, partially pay, or decline it.
5. **Payments & Follow-ups:** Hospitals follow up for payment if the patient has outstanding dues.
6. **Tracking & Improvements:** Continuous monitoring to improve financial health.

---

## 📊 Project Objectives

- Build a robust ETL pipeline using Azure resources to transform healthcare data.
- Create **fact** and **dimension tables** to help the reporting team generate meaningful KPIs for RCM.
- Improve analytics by transforming raw data into clean, standardized models.

---

## 🏗 Solution Architecture

### Medallion Architecture
- **Bronze Layer:** Raw data stored in **Parquet format** as the source of truth.
- **Silver Layer:** Data cleaning, enrichment, and application of SCD2.
- **Gold Layer:** Aggregations and creation of **Fact** and **Dimension tables**.

### Data Sources
- **EMR Data (Azure SQL Database):** Patients, providers, departments, transactions, and encounters.
- **Claims Data (Flat files):** Monthly claims data stored in Azure Data Lake.
- **NPI Data (Public API):** National Provider Identifier details.
- **ICD Codes (Public API):** Standardized system for diagnosis codes.

---

## 🔧 Azure Services Used
- **Azure Data Factory (ADF)** for data ingestion and orchestration
- **Azure Databricks** for data transformation and processing
- **Azure SQL Database** for EMR data
- **Azure Data Lake Storage Gen2** for raw, processed, and clean data storage
- **Azure Key Vault** for secure credentials storage
- **Delta Tables** for efficient storage and incremental loads

---

## 📂 Directory Structure

```bash
/project-root
│
├── notebooks/
│   └── Azure_Data_Engineering_Project.ipynb  # Jupyter notebook with data processing logic
│
├── configs/
│   └── load_config.csv  # Metadata-driven configuration for pipeline
│
├── src/
│   └── etl_pipeline.py  # ETL pipeline for data transformation
│
└── README.md            # Project documentation


## 🔄 Data Flow Pipeline

1. **Landing Layer:** Flat files are stored in Azure Data Lake Gen2.
2. **Bronze Layer:** Data is converted to Parquet format and stored as the source of truth.
3. **Silver Layer:** Data is cleaned, enriched, and stored in Delta tables.
   - Applied **SCD2** for patient, transaction, and encounter data.
   - Implemented **Common Data Model (CDM)** for standardization.
4. **Gold Layer:** Aggregated data for fact and dimension tables to support business reporting.
   - **Fact Table:** Revenue collection metrics.
   - **Dimension Tables:** Patients, transactions, and departments.

---

## ⚙️ Key Implementation Details

### Bronze to Silver Transformation

- **Data Cleaning:** Removed duplicates and standardized schema.
- **CDM:** Common schema for consistent reporting.
- **SCD2:** Implemented Slowly Changing Dimension Type 2 for incremental data updates.

### Silver to Gold Transformation

- Filtered only records with `is_current = true` and `is_quarantined = false`.
- Created fact and dimension tables for reporting.

### Incremental Loading Logic

- Configured metadata-driven pipeline to manage **full** and **incremental** loads.
- Maintained an audit table for tracking incremental loads.

---

## ✅ Best Practices and Enhancements

- **Key Vault Integration:** Secure storage of credentials.
- **Improved Naming Conventions:** For better organization and readability.
- **Parallel Pipeline Execution:** Optimized data processing.
- **Is_active Flag Implementation:** Improved control over the pipeline processing.

---

## 📈 KPIs for Accounts Receivable (AR) Management

1. **AR > 90 days:** Percentage of overdue payments.
2. **Days in AR:** Average number of days for payment collection.

---

## 🚀 How to Run the Project

1. Clone the repository:
   ```bash
   git clone https://github.com/your-repo/healthcare-rcm-data-project.git
   cd healthcare-rcm-data-project


2. Configure your Azure services, including:
   - **Azure Data Lake Storage Gen2**
   - **Azure Databricks**
   - **Azure Key Vault**
   - **Azure SQL Database**

3. Execute the ETL pipeline:
   - Trigger the ADF pipeline to load data from EMR and claims sources.
   - Process data using Databricks for transformation and aggregation.

4. Analyze the results in Gold Layer fact and dimension tables.

---

## 🔍 Notes

1. **Data Generation:**  
   All data in this project was generated using the **Faker module**.

2. **Data Discrepancies:**  
   Joins and data relationships may vary due to synthetic data.

3. **Project Improvements:**  
   Enhanced naming conventions and better code organization.


