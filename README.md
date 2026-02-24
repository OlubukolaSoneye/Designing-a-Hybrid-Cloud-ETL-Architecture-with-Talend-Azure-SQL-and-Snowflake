## ☁️ Cloud-Based ETL Pipeline | Exporting Data for Financial Analysis (Talend + Azure SQL + Snowflake)

## 📊 The Business Problem
The Bank in this case study relied on fragmented data sources across cloud and on-premise systems, with manual extraction processes that were error-prone and non-scalable. Transactional data and customer records existed in separate environments, limiting the ability to perform unified financial analysis.

The challenge was to design a scalable cloud-based ETL architecture that automates data ingestion, maintains relational integrity, and separates operational and analytical workloads without compromising performance.

## 📌 What I Built
Develop a Robust ETL Pipeline: Create a reliable and efficient ETL pipeline capable of extracting data from diverse cloud sources..
Load Data into Azure SQL Database and Snowflake: Establish the infrastructure and procedures required to load transformed data into Azure SQL Database and Snowflake.
Streamline Data Export Process: Automate the data export process to enhance efficiency and reduce manual effort.

<p align="center">
  <img src="Screenshot 2026-02-24 at 13.42.20.png" width="550"/>
</p>

## 🗄️ Data Design & Modelling
Before building the pipeline, I designed a relational schema that enforces clean separation between operational and analytical workloads while maintaining referential integrity across both platforms.

## 🔄 Data Transformation Strategy
The transformation layer ensures data consistency across both cloud platforms before loading. This transformation step guarantees reliable integration between operational and analytical layers while maintaining referential integrity.
1. Standardised column naming conventions across Snowflake and Azure SQL
2. Enforced consistent data types between platforms to prevent schema drift
3. Applied join logic to align customer and transaction datasets
4. Validated schema structure before loading into cloud targets

## Snowflake — Financial_Transactions (Analytical Layer)
Designed for high-volume analytical queries. Captures transaction metadata — amount, type, date, status, location, and currency — structured to align with Snowflake's columnar storage model.
Primary Key: Transaction_ID

## Azure SQL — Customer_Details (Operational Layer)
Core customer reference data optimised for fast row-level reads. Kept in Azure SQL to support low-latency operational access rather than warehouse-scale compute.
Primary Key: Customer_ID
<p align="center">
  <img src="Screenshot 2026-02-24 at 13.57.52.png" width="550"/>
</p>

## Mapping Layer
Connects Customer_ID and Account_Number across both platforms, maintaining referential integrity without tightly coupling the two systems.
Splitting customer and transactional data across platforms was a deliberate architectural choice — operational systems handle writes and lookups, analytical platforms handle aggregation and reporting. The mapping layer bridges them cleanly.

## 🔍 Architecture Decisions
Why Azure SQL for operational, Snowflake for analytical?
Azure SQL handles transactional, row-level queries efficiently, which is ideal for operational workloads. Snowflake's columnar storage and separation of compute and storage make it purpose-built for analytical queries at scale. Keeping the two layers separate avoids performance bottlenecks and mirrors real-world enterprise data architecture.

Why context-driven configuration?
Hardcoding credentials and environment settings into ETL jobs creates brittle pipelines. Using tContextLoad with external context files allows the same job to run across dev, staging, and production without modification — a pattern used in production data engineering teams.

## 📈 Outcomes
Eliminated manual file uploads by fully automating ingestion from flat files to cloud targets
Standardised schema across both cloud platforms ensuring consistent, reliable reporting outputs
Separated transactional and analytical workloads to prevent performance degradation under load
Built a reusable, environment-agnostic pipeline deployable across dev and production
Designed to production standards — modular jobs, clean separation of concerns, and scalable architecture

## 🛠️ Tech Stack
SQL
Microsoft Azure SQL Database (operational layer)
Snowflake (analytical warehouse)
Talend Open Studio (ETL orchestration)


