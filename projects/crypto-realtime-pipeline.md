# Crypto Exchange Batch & Real-Time Pipeline

**Timeline:** Nov 2025 - Mar 2026
**Stack:** Rust, Kafka, ClickHouse, Dagster, AWS EKS, S3, Grafana

## Overview

Designed and built a high-throughput data platform for ingesting, storing, and analyzing crypto exchange data in real time. The system supports both streaming and batch workloads, serving quant researchers and traders with sub-second data freshness.

## Architecture

```
Exchanges (REST/WebSocket)
        │
   Rust Ingestion Service (300GB+/day)
        │
      Kafka
       ┌┴┐
       │ │
  ClickHouse   S3 (zstd compressed)
  (real-time)   (historical archive)
       │
    Grafana
  (dashboards)
```

## Key Technical Decisions

- **Rust for ingestion:** Chose Rust over Python for the data ingestion layer to handle high-throughput, low-latency publishing to Kafka across multiple exchanges simultaneously. Achieved 99.9% uptime with minimal resource footprint.
- **ClickHouse over Redshift:** Migrated from batch-only Redshift to ClickHouse for real-time OLAP queries. Reduced end-to-end latency by 60%.
- **Dagster for orchestration:** Used Dagster (over Airflow) for backfilling 20TB+ of historical trading data from Amberdata, leveraging its asset-based orchestration model for better lineage tracking.
- **Cost optimization:** Applied zstd compression and tiered S3 Glacier storage for historical data, significantly reducing long-term storage costs.

## Results

- 300GB+/day ingestion throughput across multiple crypto exchanges
- 60% reduction in end-to-end data latency
- 20TB+ historical backfill completed with full lineage tracking
- Real-time Grafana dashboards serving quant research team
