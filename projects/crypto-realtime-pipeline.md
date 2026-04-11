# Crypto Market Data Platform

**Timeline:** Nov 2025 - Present
**Stack:** Rust, Kafka, StarRocks, ClickHouse, Dagster, AWS EKS, S3, Grafana

## Overview

Architected a high-throughput crypto market data platform on AWS S3 with medallion architecture (raw/aggregated/production) to serve crypto quant analysis. The platform ingests real-time and historical data from multiple exchanges, supports sub-2-second analytical queries, and powers Grafana dashboards for quant strategy performance.

## Architecture

```
Exchanges (REST/WebSocket)
   Amberdata, Binance, etc.
        |
   Rust Ingestion Service (300GB+/day)
        |
      Kafka
       ┌┴┐
       | |
  ClickHouse   S3 Data Lake (10TB+)
  (real-time)   (medallion: raw/agg/prod)
       |              |
    Grafana      StarRocks
  (dashboards)  (historical OLAP)
```

## Key Technical Decisions

- **AWS S3 as data lake:** Applied medallion architecture to manage raw data, aggregated data, and production data across 10TB+ of exchange data with tiered storage.
- **Rust for ingestion:** Built WebSocket ingestion services streaming market data from Amberdata, Binance, and exchange APIs into Kafka at 300GB+/day. Achieved 99.9% uptime with minimal resource footprint.
- **ClickHouse for real-time:** Streamed real-time data into ClickHouse with optimized schemas, reducing analytical query times to under 2 seconds.
- **StarRocks for historical:** Configured StarRocks for historical OLAP queries across the full data lake.
- **Kubernetes DevOps:** Deployed and operated StarRocks, ClickHouse, Kafka, and Grafana on Kubernetes, managing the full DevOps lifecycle.
- **Dagster for orchestration:** Orchestrated batch ETL and historical backfills across the medallion architecture with full data lineage tracking.
- **Grafana dashboards:** Built dashboards visualizing quant strategy performance metrics for the research team.

## Results

- 10TB+ data lake with medallion architecture on AWS S3
- 300GB+/day ingestion throughput across multiple crypto exchanges
- Sub-2-second analytical query latency on ClickHouse
- Full Kubernetes-managed infrastructure (StarRocks, ClickHouse, Kafka, Grafana)
- Real-time Grafana dashboards serving quant research team
