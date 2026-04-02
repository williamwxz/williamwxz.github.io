# Kamino Solana Vault Curation

**Timeline:** Oct 2025 - Dec 2025
**Stack:** TypeScript, Bun, Kamino SDK, Solana, GCP KMS, Dagster, incident.io

## Overview

Designed and built a vault curation service on the Kamino protocol (Solana-based), managing over $60M in assets with automated fund allocation driven by internal quantitative strategies.

## Architecture

```
Internal Strategy Engine
         │
  TypeScript Service (Bun)
         │
    Kamino SDK
   (vault instructions)
         │
    GCP KMS Signing
   (secure tx execution)
         │
    Solana Blockchain
         │
    Dagster (periodic jobs)
         │
    GCP Log-Based Metrics
         │
    incident.io (alerting)
```

## Key Technical Decisions

- **Bun over Node.js:** Chose Bun as the TypeScript runtime for faster startup and native performance, critical for time-sensitive vault rebalancing operations.
- **GCP KMS for signing:** Integrated with GCP Key Management Service to ensure every Kamino transaction is signed securely without exposing private keys to the application layer.
- **Dagster for scheduling:** Deployed as periodic Dagster jobs rather than cron to leverage asset-based orchestration, retry logic, and observability out of the box.
- **incident.io integration:** Connected GCP log-based metrics to incident.io for automated failure detection and escalation.

## Results

- $60M+ in managed vault assets
- Automated fund reallocation based on internal strategies
- Secure on-chain transaction execution via GCP KMS
- Full observability with Dagster + incident.io alerting
