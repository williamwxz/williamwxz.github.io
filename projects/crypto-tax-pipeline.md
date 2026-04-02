# Crypto Tax Calculation Pipeline

**Timeline:** Jan 2024 - Mar 2024
**Stack:** Python, Dagster, Apache Iceberg, S3, Redshift, PostgreSQL, AWS

## Overview

Architected an automated crypto tax calculation platform computing annual tax obligations across multiple organizations and individual users, covering diverse on-chain and off-chain transaction types including trades, staking rewards, airdrops, and DeFi yield.

## Architecture

```
PostgreSQL (raw transactions)
         │
      Dagster (orchestration)
         │
   ┌─────┴─────┐
   │  Iceberg   │
   │  Data Lake │
   │   (S3)     │
   └─────┬─────┘
         │
  Medallion Architecture
  ┌──────┼──────┐
Bronze  Silver  Gold
(raw)  (cost   (annual tax
        basis)  summaries)
         │
      Redshift
   (tax reports)
         │
  Per-Org & Per-User
  Tax Statements
```

## Key Technical Decisions

- **Dagster over Airflow:** Chose Dagster for its asset-based orchestration model, which maps naturally to the medallion architecture — each layer (bronze, silver, gold) is a materialized asset with clear lineage and dependency tracking.
- **Iceberg data lake:** Used Apache Iceberg on S3 for the lakehouse layer, enabling schema evolution as new transaction types emerged and time-travel queries for audit trail requirements.
- **Cost-basis engine:** Implemented multiple cost-basis calculation methods (FIFO, LIFO, HIFO) in the silver layer, allowing organizations to select their preferred accounting method per jurisdiction.
- **Multi-org architecture:** Designed the pipeline to compute tax obligations in parallel across multiple organizations, with per-user roll-ups within each org, enabling both corporate-level and individual tax reporting.
- **Redshift for reporting:** Materialized finalized gold-layer summaries into Redshift for fast SQL access by compliance teams and integration with downstream tax filing systems.

## Results

- Automated annual tax calculation across multiple organizations
- Support for FIFO, LIFO, and HIFO cost-basis methods
- Full audit trail via Iceberg time-travel queries
- Per-organization and per-user tax summary generation
- Medallion architecture enabling compliance reporting and audit readiness
