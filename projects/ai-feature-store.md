# ML Feature Store for Quantitative Analytics

**Timeline:** Apr 2024 - Oct 2024
**Stack:** Python, dbt, Snowflake, Snowflake Cortex, Y42, Hopsworks

## Overview

Built a centralized ML feature store serving 90+ features to internal data scientists and external customers, enabling trading strategy development and DeFi risk analysis at scale.

## Architecture

```
Raw On-Chain Data + Exchange Data
            │
     Snowflake (warehouse)
            │
    dbt on Y42 (medallion layers)
     ┌──────┴──────┐
  Bronze → Silver → Gold
            │
      Hopsworks (feature store)
            │
    ┌───────┴───────┐
Python SDK        AI Agent
(data frames)   (NL queries)
```

## Key Technical Decisions

- **Medallion architecture:** Applied bronze/silver/gold layering via dbt to enforce data quality contracts at each stage. Raw ingestion stays untouched in bronze; silver handles deduplication and type casting; gold serves curated, business-ready features.
- **Hopsworks for feature serving:** Chose Hopsworks over Feast for its native Snowflake integration and built-in feature monitoring. Wrapped access in a custom Python SDK to provide standardized DataFrame interfaces.
- **Snowflake native agent for data exploration:** Built a natural-language query agent using Snowflake Cortex, allowing non-technical stakeholders to ask questions about external-facing datasets without writing SQL.
- **Y42 for orchestration:** Used Y42 as the orchestration layer on top of dbt, managing periodic refresh schedules across all 90+ feature tables.

## Results

- 90+ ML features serving both internal and external consumers
- Standardized Python SDK adopted by data science team
- AI agent reduced ad-hoc data request turnaround from hours to seconds
