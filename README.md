# SQL Server Medallion Data Warehouse (Bronze → Silver → Gold)

A reproducible **data engineering** portfolio project that builds a **SQL Server** data warehouse from raw CSV extracts (ERP + CRM), applies **medallion-style** transformations (Bronze → Silver → Gold), and publishes **analytics-ready marts** modeled as a **star schema**.

This repository is designed to demonstrate practical DE skills: **repeatable ETL, data quality checks, dimensional modeling, and clear documentation**.

---


## Project visuals (at a glance)

### Overall architecture (Medallion)
![Medallion Architecture](docs/data_architecture.png)

### Data flow (Source → Bronze → Silver → Gold)
![Data Flow](docs/data_flow.png)

---
## What this project delivers

- **Bronze layer**: raw ingestion from CSV sources into SQL Server tables (minimal transformation)
- **Silver layer**: cleansing + standardisation + conformance rules to make data reliable
- **Gold layer**: curated, business-ready **star schema** (fact + dimensions) for reporting/analytics
- **Data quality checks**: SQL-based tests for duplicates, nulls, and referential integrity
- **Reproducible local setup**: run everything locally using Docker Compose

---

## Architecture

This project follows the Medallion Architecture:

- **Bronze (Raw / Landing)**
  - Loads ERP and CRM CSVs as-is
  - Preserves source structure for traceability

- **Silver (Cleansed / Conformed)**
  - Standardises data types and formats
  - Handles common quality issues (e.g., trimming, casing, invalid codes, null handling)
  - Produces consistent entities across sources

- **Gold (Curated / Serving)**
  - Builds a **star schema** optimised for analytics
  - Provides clean fact/dimension tables for BI and ad-hoc SQL

> Diagrams and supporting documentation are available in `docs/`.

---

## Data model (Gold)

The Gold layer is modeled as a star schema:

- **Fact tables** capture measurable business events (e.g., sales transactions)
- **Dimension tables** describe entities used for slicing and filtering (e.g., customer, product, date)

Design goals:
- clear grain definition
- BI-friendly naming
- performant joins for analytical queries

---

### Star schema diagram
![Star Schema](docs/data_model.png)

### Source integration mapping (ERP + CRM)
![Integration Model](docs/integration_model.png)

---

## Analytics use cases

Example SQL analytics are designed to answer common stakeholder questions:

- **Customer behavior**
  - customer segmentation
  - repeat purchase / retention signals
- **Product performance**
  - top products by revenue/volume
  - product contribution analysis
- **Sales trends**
  - month-over-month trends
  - rolling summaries


---

## Tech stack

- **SQL Server** (T-SQL)
- **Docker Compose** (reproducible local environment)
- **SSMS** (recommended client for running scripts)
- Draw.io / markdown documentation (in `docs/`)

---

## Repository structure

```text
.
├── datasets/                           # Source CSVs (ERP + CRM)
├── docs/                               # Architecture + model docs
│   ├── data_architecture.png
│   ├── data_flow.png
│   ├── data_model.png
│   ├── integration_model.png
│   └── data_catalog.md
├── scripts/
│   ├── bronze/                         # Raw ingestion scripts
│   ├── silver/                         # Cleansing + standardisation scripts
│   └── gold/                           # Star schema + marts
├── tests/                              # Data quality checks (SQL)
├── docker-compose.yml                  # Local SQL Server setup
└── README.md
