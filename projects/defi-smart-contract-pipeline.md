# DeFi Smart Contract Data Pipeline

**Timeline:** Feb 2025 - Jun 2025
**Stack:** Rust, WebSocket, Kafka, BigQuery, ClickHouse, Dagster, GCP Monitoring, incident.io, Claude AI

## Overview

Built a real-time data platform ingesting all EVM chain blocks, transactions, and logs, with extended parsing for Morpho and Aave smart contract events. Streams blockchain data into BigQuery and ClickHouse for DeFi analytics and risk modeling.

## Architecture

```
Multiple RPC Providers (WebSocket)
         │
   Rust Ingestion Service
   (all EVM chains, 1MB/s)
         │
       Kafka
      ┌──┴──┐
BigQuery   ClickHouse
(analytics) (low-latency)
      │
   Dagster
  (ABI parsing, 5-10 min)
      │
  GCP Monitoring
      │
  incident.io
```

## Key Technical Decisions

- **Rust for multi-chain WebSocket:** Built the ingestion service in Rust to capture all EVM chain blocks, transactions, and logs via concurrent WebSocket connections to multiple RPC providers. Achieved 1MB/s sustained throughput with minimal resource usage.
- **Dual sink architecture:** Streamed raw chain data to both BigQuery (for long-term analytics and SQL access) and ClickHouse (for low-latency operational queries).
- **Morpho & Aave event parsing:** Extended the service to parse Morpho and Aave smart contract events into ClickHouse, with ETL and event parsing orchestrated by Dagster.
- **Claude-powered chain expansion:** Developed Claude skills for rapid chain expansion, enabling new EVM chain onboarding with minimal code changes.
- **End-to-end observability:** GCP log-based metrics feeding into incident.io for automated alerting on ingestion failures, parsing errors, and throughput anomalies.

## Results

- Real-time ingestion of all EVM chain blocks, transactions, and logs
- 1MB/s sustained streaming throughput
- Morpho and Aave event parsing into ClickHouse via Dagster orchestration
- Rapid chain onboarding via Claude-powered skills
- Full monitoring and incident management pipeline
