# DeFi Smart Contract Data Pipeline

**Timeline:** Feb 2025 - Jun 2025
**Stack:** Rust, WebSocket, Kafka, BigQuery, ClickHouse, Dagster, GCP Monitoring, incident.io, Claude AI

## Overview

Built a real-time data platform to capture smart contract events across all EVM-compatible chains, streaming blockchain data into BigQuery and ClickHouse for DeFi analytics and risk modeling.

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

- **Rust for multi-chain WebSocket:** Built the ingestion service in Rust to handle concurrent WebSocket connections to multiple RPC providers across all EVM chains. Achieved 1MB/s sustained throughput with minimal resource usage.
- **Dual sink architecture:** Streamed events to both BigQuery (for long-term analytics and SQL access) and ClickHouse (for low-latency operational queries on Morpho protocol data).
- **Dagster for ABI parsing:** Used Dagster jobs running at 5-10 minute intervals to parse blockchain logs via contract ABIs, decoding raw event data into structured tables.
- **AI-assisted extensibility:** Leveraged Claude AI agent to make the Rust service more extensible, enabling rapid onboarding of new EVM chains and contract types.
- **End-to-end observability:** GCP log-based metrics feeding into incident.io for automated alerting on ingestion failures, parsing errors, and throughput anomalies.

## Results

- Real-time event capture across all EVM-compatible chains
- 1MB/s sustained streaming throughput
- Dual-sink analytics (BigQuery + ClickHouse)
- Rapid chain onboarding via AI-assisted code generation
- Full monitoring and incident management pipeline
