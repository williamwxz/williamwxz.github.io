# AI Infrastructure Platform for Furniture eCommerce

**Timeline:** Oct 2025 – Present
**Role:** Solo builder (side project)
**Stack:** TypeScript, Node.js 20, Python, pgvector, Neon Postgres, Google Vertex AI, Gemini 3.1, `text-embedding-004`, vLLM, Google Pub/Sub, GKE, Cloud Run, Helm, Terraform, Workload Identity

## Overview

Self-hosted AI infrastructure for a Shopify-based furniture retailer. RAG on pgvector, an async embedding pipeline fed by Pub/Sub, a model-serving gateway, and a GPU inference layer. Agents are thin clients on top.

## High-Level Architecture

```
   ┌──────────────┐                     ┌──────────────────┐
   │  Producers   │                     │      Agents      │
   │  webhooks ·  │                     │ Portfolio        │
   │  syncs · CLI │                     │ Analysis · …     │
   └──────┬───────┘                     └────────┬─────────┘
          │                                      │
          ▼                                      ▼
   ┌──────────────┐                     ┌──────────────────┐
   │   Pub/Sub    │                     │  RAG Retriever   │
   │ content.*    │                     │ pgvector + rank  │
   └──────┬───────┘                     └────────┬─────────┘
          │                                      │
          ▼                                      │
   ┌──────────────────┐                          │
   │ Embedding        │                          │
   │ Service          │                          │
   │ (subscriber pod) │                          │
   └────────┬─────────┘                          │
            │                                    │
            ▼                                    ▼
   ┌─────────────────────────────────────────────────────────┐
   │           Serving Layer  (Model Gateway)                 │
   │     /embed   ·   /generate   ·   /rerank                 │
   │     routing · streaming · retries · token metrics        │
   └────────┬────────────────────────────────┬───────────────┘
            │                                │
            ▼                                ▼
   ┌──────────────────┐             ┌──────────────────┐
   │   Vertex AI      │             │   GPU Cluster    │
   │   (managed)      │             │   vLLM on GKE    │
   │   Gemini 3.1     │             │   (planned)      │
   └──────────────────┘             └──────────────────┘

            ┌──────────────────────────┐
            │   Vector Store           │
            │   pgvector / Neon Postgres│
            │   embedding · scope · ttl │
            └──────────────────────────┘
```

## RAG Layer

- **Vector store:** `pgvector` on Neon Postgres, same DB as application state — RAG queries can JOIN to relational metadata.
- **Embedding model:** Gemini `text-embedding-004` (768-dim), accessed through the serving layer.
- **Hybrid ranking:** `0.7 × cosine + 0.3 × decayed_relevance`, similarity floor 0.3.
- **Time decay:** `relevance × 0.98^days_since_last_access`.
- **Dedup on ingest:** reject when cosine ≥ 0.92 within the same scope.
- **Multi-scope index:** `scope` column (`agent_memory`, `product`, `policy`, …) — one index, many logical stores.

## Embedding Service

- Subscriber to Pub/Sub topic `content.updated`, horizontally scaled.
- Pipeline: fetch source-of-truth row → chunk + normalize → checksum → call serving layer `/embed` → upsert to pgvector.
- **Checksum skip** — no GPU call when content is unchanged.
- **Persist-first webhook ingestion** — events durably persisted before processing; retry sweeper handles failures.
- **Backpressure** through Pub/Sub flow control — GPU pool never sees thundering herds during reindex.

## Serving Layer (Model Gateway)

- Stable interface: `embed`, `generate`, `rerank`. Agents never call a model SDK directly.
- **Backend routing:** managed (Vertex AI) and self-hosted (vLLM) behind one URL.
- **Per-workload model selection** — Pro for reasoning, Flash for high-volume, embedding model for indexing.
- **Streaming generation** (SSE) with bounded tool-call iteration (max 5) and per-request timeout budgets.
- **Observability:** structured per-request metrics — `model`, `prompt_tokens`, `completion_tokens`, `latency_ms`.

## GPU Cluster

- **Managed today:** Vertex AI endpoints for Gemini models.
- **Self-hosted (planned):** dedicated GPU node pool on GKE running **vLLM** for open-weight embedding and reranker models.
- **Autoscaling:** HPA on QPS + queue depth; cluster autoscaler with min-replicas = 0 for off-hours.
- **Workload Identity** for model-weight bucket + Secret Manager access — no static credentials.

## AI Agents

Thin clients over the serving layer and RAG retriever.

- **Portfolio Analysis Agent.** Scheduled run; retrieves prior analyses and merchant context from pgvector; scores live products across sales velocity, listing quality, pricing, sentiment, visual quality; writes scorecards to Postgres; persists durable insights back through the embedding pipeline.

## Cloud Infrastructure

- **Terraform** — all GCP resources, IAM, secrets, Pub/Sub, GKE, GCS, API enablement.
- **Helm** — API deployment, HPA, NGINX ingress + cert-manager, parameterized CronJob template.
- **Workload Identity** — no static credentials anywhere.
- **Neon Postgres** with `pgvector`, per-PR preview branches.
- **CI/CD:** GitHub Actions — test → Prisma migrate → `terraform apply` → Docker → Helm upgrade.

## Stack Summary

| Layer | Technology |
|:------|:-----------|
| AI / Models | Gemini 3.1 Pro / 3 Flash, `text-embedding-004` (768-dim), vLLM (planned) |
| Inference | Vertex AI (managed) · GKE GPU node pool (planned, self-hosted) |
| Serving | Model gateway — `/embed` `/generate` `/rerank`, streaming, retries, metrics |
| RAG / Vector store | pgvector on Neon Postgres |
| Ingestion | Google Pub/Sub, persist-first, dedicated Embedding Service subscriber |
| API runtime | Node.js 20, TypeScript 5.3, Hono |
| Data | Neon serverless Postgres, Prisma 5.22, pgvector |
| Infra | GCP — GKE, Cloud Run, Helm, Terraform, NGINX ingress, cert-manager, Workload Identity |
| Observability | Cloud Logging, structured token + latency metrics |
| CI/CD | GitHub Actions, Neon preview branches per PR |
