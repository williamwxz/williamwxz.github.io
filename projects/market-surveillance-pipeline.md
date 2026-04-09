# Crypto Market Surveillance ETL Pipeline

**Timeline:** Jan 2024 - May 2024
**Stack:** Python, Airflow, dbt, Redshift, Redshift Spectrum, S3, Apache Iceberg, Parquet, PostgreSQL CDC

## Overview

Built a batch ETL pipeline for a crypto exchange's compliance team to detect abnormal trading activity. Aggregated data from multiple upstream sources into a Redshift-based analytics layer with automated alerting.

## Architecture

```
Market Price APIs    Solidus Labs    PostgreSQL (CDC)
       │                  │                │
    Airflow (orchestration)  ←─────────────┘
       │
   S3 (raw JSON / CDC events)
       │
   Parquet + Iceberg
   (partitioned by date)
       │
  Redshift Spectrum → Redshift
       │
    dbt (medallion layers)
       │
  Compliance Dashboards + Slack Alerts
```

## Key Technical Decisions

- **CDC from PostgreSQL:** Captured change data from PostgreSQL into the S3 data lake, enabling near real-time synchronization of transactional data into the analytics layer.
- **Iceberg data lake:** Adopted Apache Iceberg for the lakehouse layer, enabling schema evolution and time-travel queries on S3-backed Parquet files without reprocessing.
- **Redshift Spectrum:** Used Spectrum to query S3 data in-place, avoiding costly full loads into Redshift while maintaining SQL compatibility for the compliance team.
- **Medallion architecture with dbt:** Applied bronze/silver/gold layering for progressive data refinement — raw JSON in bronze, cleaned and typed in silver, aggregated compliance metrics in gold.
- **Automated alerting:** Built anomaly detection rules that trigger Slack notifications for the compliance team when transaction patterns deviate from baselines.

## Results

- Multi-source data aggregation with daily refresh cadence
- Iceberg-based lakehouse reducing storage costs vs. full Redshift loads
- Automated compliance alerting with Slack integration
