# Crypto Market Data Platform

**Timeline:** Nov 2025 – Present
**Stack:** Python, Flink, Redpanda, ClickHouse Cloud, StarRocks, Dagster, AWS (ECS Fargate, S3, S3 Glacier), Supabase, Terraform, Grafana

## Overview

End-to-end crypto market data platform serving quantitative research with both **real-time streaming PnL** and a **10TB+ historical data lake**. Live PnL lands in ClickHouse within seconds of each closed candle; the historical lake powers cross-exchange backtesting and ad-hoc OLAP — all on a cost-optimized AWS footprint under $100/month.

## Architecture

```
Real-time:   Binance WS ──► WebSocket client ──► Redpanda ──► Flink job ──► ClickHouse Cloud ──► Grafana
Historical:  Dagster ──► exchange REST APIs ──► S3 data lake (medallion) ──► StarRocks
                                                       │
                                                       └──► S3 Glacier (cold tier)
```

## Highlights

- **Sub-minute end-to-end PnL latency** from exchange close to per-strategy PnL row in ClickHouse Cloud and on to the Grafana dashboards.
- **10TB+ multi-exchange historical lake** on S3 with medallion architecture across raw, aggregated, and production tiers; StarRocks delivers cross-exchange historical OLAP at sub-2-second latency for quant research and backtesting.
- **Idempotent by design** — rolling-window full-recompute with ClickHouse `ReplacingMergeTree` means any minute of any day is safe to re-run with no double-counting; cold-start replay crashes on >0.2% PnL deviation, catching silent corruption before it reaches dashboards.
- **100% IaC, zero static credentials** — Terraform owns every AWS resource and GitHub Actions deploys via OIDC role assumption with no long-lived keys.
- **Substantial AWS cost reduction** by cold-tiering historical data to **S3 Glacier**, migrating Dagster metadata from **RDS Postgres to Supabase**, and consolidating workloads off **EKS onto ECS Fargate** after pruning unnecessary services.
