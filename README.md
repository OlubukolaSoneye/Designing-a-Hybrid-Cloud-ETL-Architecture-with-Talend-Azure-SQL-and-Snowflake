## ☁️ Hybrid Cloud ETL Pipeline (Talend + Azure SQL + Snowflake)

<img src="Screenshot 2026-02-24 at 17.34.00.png" width="500"/>

📊 The Business Problem
Organisations running hybrid environments often face a critical gap — operational databases and analytical platforms don't talk to each other. The result is manual data transfers, siloed reporting, and delayed decision-making.
This project addresses that directly by designing and implementing an automated ETL pipeline that moves structured data from flat files into both an operational layer (Azure SQL) and an analytical warehouse (Snowflake) — with Talend Open Studio as the orchestration engine.

## 📌 What I Built
A modular, production-aligned ETL architecture that:
Extracts data from structured flat files
Transforms and standardises datasets to meet target schema requirements
Loads cleaned data into Azure SQL Database for operational storage
Pushes analytical-ready data into Snowflake for warehouse querying
Uses context-driven configuration (tContextLoad) to separate dev and production environments — making the pipeline reusable and environment-agnostic

## 🛠️ Tech Stack
SQL
Microsoft Azure SQL Database (operational layer)
Snowflake (analytical warehouse)
Talend Open Studio (ETL orchestration)
Context Variables & tContextLoad

## 🔍 Architecture Decisions
Why Azure SQL for operational, Snowflake for analytical?
Azure SQL handles transactional, row-level queries efficiently — ideal for operational workloads. Snowflake's columnar storage and separation of compute and storage make it purpose-built for analytical queries at scale. Keeping the two layers separate avoids performance bottlenecks and mirrors real-world enterprise data architecture.
Why context-driven configuration?
Hardcoding credentials and environment settings into ETL jobs creates brittle pipelines. Using tContextLoad with external context files allows the same job to run across dev, staging, and production without modification — a pattern used in production data engineering teams.

<img src="Screenshot 2026-02-24 at 17.34.00.png" width="500"/>

## 📈 Outcomes
Eliminated manual file uploads by fully automating ingestion from flat files to cloud targets
Standardised schema across both cloud platforms ensuring consistent, reliable reporting outputs
Separated transactional and analytical workloads to prevent performance degradation under load
Built a reusable, environment-agnostic pipeline deployable across dev and production
Designed to production standards — modular jobs, clean separation of concerns, and scalable architecture
