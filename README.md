# CareSync Azure Data Engineering Platform

End-to-end Azure data engineering project demonstrating scalable batch ingestion, incremental data processing, medallion architecture, and cloud-based analytics using the Microsoft Azure data ecosystem.

> **Project Status:** 🚧 In Development

## Overview

CareSync is a hands-on data engineering project designed to simulate a production-style Azure data platform.

The project ingests relational and file-based source data using Azure Data Factory, stores raw and curated data in Azure Data Lake Storage Gen2, and processes data through Bronze, Silver, and Gold layers using Azure Databricks.

The project focuses on reusable pipeline design, incremental ingestion, scalable transformations, data quality, security, and maintainable cloud data architecture.

## Architecture

```text
              Source Systems
         ┌──────────┴──────────┐
         │                     │
    Relational DB          File Sources
         │                     │
         └──────────┬──────────┘
                    │
                    ▼
           Azure Data Factory
                    │
         Batch / Incremental Load
                    │
                    ▼
              ADLS Gen2
        ┌─────────────────────┐
        │     Bronze Layer    │
        │       Raw Data      │
        └──────────┬──────────┘
                   │
                   ▼
            Azure Databricks
             PySpark / Delta
                   │
                   ▼
        ┌─────────────────────┐
        │     Silver Layer    │
        │ Cleaned / Validated │
        └──────────┬──────────┘
                   │
                   ▼
            Azure Databricks
                   │
                   ▼
        ┌─────────────────────┐
        │      Gold Layer     │
        │   Analytics Ready   │
        └──────────┬──────────┘
                   │
                   ▼
          Analytics / Serving
```

A detailed architecture diagram will be added under `architecture/` as the implementation is completed.

## Technology Stack

| Area | Technologies |
|---|---|
| Cloud | Microsoft Azure |
| Orchestration | Azure Data Factory |
| Data Lake | Azure Data Lake Storage Gen2 |
| Processing | Azure Databricks |
| Data Processing | PySpark |
| Lakehouse | Delta Lake |
| Database | Azure SQL / PostgreSQL |
| Secrets | Azure Key Vault |
| Languages | Python, SQL |
| Source Control | Git, GitHub |

## Data Engineering Architecture

The platform follows a medallion data architecture.

### Bronze Layer

The Bronze layer stores source data with minimal transformation.

Responsibilities include:

- Raw source-data ingestion
- Historical data preservation
- Batch ingestion
- Incremental ingestion
- Source-level auditability

### Silver Layer

The Silver layer contains cleaned and standardized data.

Processing includes:

- Schema enforcement
- Data type normalization
- Null handling
- Deduplication
- Data-quality validation
- Business-rule transformations

### Gold Layer

The Gold layer provides analytics-ready datasets.

The layer is designed to support:

- Business reporting
- Aggregations
- Analytical queries
- Curated business entities
- Downstream dashboards and applications

## Azure Data Factory

Azure Data Factory is used as the primary orchestration and ingestion service.

The project is being designed around reusable rather than one-off pipelines.

Planned and implemented capabilities include:

- Parameterized pipelines
- Reusable datasets
- Linked services
- Lookup activities
- ForEach processing
- Copy activities
- Metadata-driven ingestion
- Incremental loading
- Pipeline dependencies
- Failure handling and monitoring

### ADF Source Repository

The Azure Data Factory instance uses a dedicated Git-integrated repository for ADF-generated artifacts.

The ADF repository contains resources such as:

```text
dataset/
factory/
linkedService/
pipeline/
```

This repository remains separate from the portfolio repository so Azure Data Factory can maintain its native Git integration while this repository documents the complete end-to-end solution.

## Incremental Data Loading

One of the primary engineering goals of the project is avoiding unnecessary full-table reloads.

The architecture is being designed to support incremental ingestion using metadata and watermark-based processing.

Conceptually:

```text
Read previous watermark
        │
        ▼
Determine new/changed records
        │
        ▼
ADF incremental extraction
        │
        ▼
ADLS Bronze
        │
        ▼
Databricks processing
        │
        ▼
Delta Lake MERGE
        │
        ▼
Update watermark
```

This pattern reduces unnecessary data movement and provides a reusable approach for ingesting multiple source tables.

## Azure Databricks

Azure Databricks is used for transformation and lakehouse processing.

Databricks workloads are organized around the medallion architecture:

```text
databricks/
├── bronze/
├── silver/
└── gold/
```

The project will use PySpark and Delta Lake for tasks such as:

- Data cleansing
- Data standardization
- Schema enforcement
- Deduplication
- Data-quality validation
- Incremental processing
- Delta Lake MERGE operations
- Business transformations

## Security

The project is designed to avoid embedding credentials directly in pipeline or notebook code.

Azure security components include:

- Azure Key Vault
- Managed identities where applicable
- Secret management
- Principle of least privilege
- Separation of configuration from application logic

> No passwords, access keys, connection strings, or other secrets should be committed to this repository.

## Monitoring and Reliability

Production-oriented data pipelines need to handle failures predictably.

The project will incorporate:

- ADF pipeline monitoring
- Activity-level failure handling
- Data validation
- Retry strategies where appropriate
- Pipeline logging
- Record-count validation
- Incremental-load verification

## Repository Structure

```text
caresync_azure_project/
│
├── README.md
│
├── architecture/
│   └── # Architecture diagrams
│
├── databricks/
│   ├── bronze/
│   ├── silver/
│   └── gold/
│
├── sql/
│   ├── source/
│   ├── metadata/
│   └── gold/
│
├── sample-data/
│   └── # Non-sensitive sample datasets
│
└── docs/
    └── # Implementation documentation
```

## Design Goals

The project focuses on the following engineering principles:

1. **Reusable ingestion**
   - Avoid creating a separate pipeline for every source table.

2. **Incremental processing**
   - Move only new or changed data whenever possible.

3. **Separation of concerns**
   - ADF handles orchestration and ingestion while Databricks handles distributed transformations.

4. **Medallion architecture**
   - Separate raw, validated, and business-ready data.

5. **Secure configuration**
   - Keep credentials and secrets outside source code.

6. **Observability**
   - Make pipeline failures and data-quality problems diagnosable.

7. **Source control**
   - Maintain data-engineering artifacts through Git-based development workflows.

## Current Progress

- [x] Azure project repository initialized
- [x] Azure Data Factory Git integration established
- [ ] Source-system ingestion
- [ ] Metadata-driven ADF framework
- [ ] Incremental loading
- [ ] ADLS Gen2 Bronze layer
- [ ] Databricks Bronze processing
- [ ] Databricks Silver transformations
- [ ] Gold data model
- [ ] Delta Lake incremental processing
- [ ] Azure Key Vault integration
- [ ] Data-quality validation
- [ ] Monitoring and error handling
- [ ] Architecture diagram
- [ ] End-to-end documentation

The checklist will be updated as each component is implemented and validated.

## Key Learning Objectives

This project is being built to deepen hands-on experience with:

- Azure Data Factory pipeline development
- Batch and incremental data ingestion
- Metadata-driven data engineering
- Azure Data Lake Storage Gen2
- Azure Databricks
- PySpark
- Delta Lake
- Medallion architecture
- Production-oriented pipeline design
- Azure security and secret management
- Data quality and monitoring

