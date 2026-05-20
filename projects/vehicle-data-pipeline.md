# Perception ML Training Data Platform — Autonomous Driving

**Timeline:** Dec 2021 – May 2022
**Stack:** Python, Spark Streaming, Kafka, RabbitMQ, Protobuf, Parquet, Apache Iceberg, Kubernetes, Elasticsearch, S3 / HDFS

## Overview

Built the data infrastructure that fed an autonomous driving company's perception ML training pipelines. Converted raw vehicle sensor streams from Protobuf into ML-ready Parquet on an Iceberg data lake at 10TB+/day, across multiple data centers in a hybrid cloud, with a Python SDK that let perception data scientists pull versioned training datasets and submit Spark jobs on Kubernetes without touching infra.

The platform did not train models — it produced the curated, columnar, point-in-time-correct training data that downstream perception ML teams consumed.

## Architecture

```
   Autonomous Vehicles
   (Protobuf streams · 100MB–10GB per file)
              │
   ┌──────────┴──────────┐
   │  Kafka  ·  RabbitMQ │
   │  high-volume sensor │
   │  + control messages │
   └──────────┬──────────┘
              │
              ▼
   ┌──────────────────────────────┐
   │  Spark Streaming on K8s      │
   │  Protobuf → Parquet          │
   │  auto-scaling per data center│
   └──────────┬───────────────────┘
              │
              ▼
   ┌──────────────────────────────┐
   │  Apache Iceberg Data Lake    │
   │  schema evolution · time-    │
   │  travel · partition mgmt     │
   │  S3 / HDFS                   │
   └──────────┬───────────────────┘
              │
              ▼
   ┌──────────────────────────────┐
   │  Python SDK (self-service)   │
   │  query Iceberg datasets      │
   │  submit Spark jobs on K8s    │
   └──────────┬───────────────────┘
              │
              ▼
       Perception ML Teams
       (training data consumers)

   Elasticsearch (data lineage + pipeline health · cross-DC)
```

## ML Training Data Infrastructure

- **Iceberg as ML dataset versioning.** Time-travel and snapshot isolation gave perception teams reproducible training cuts — "train on the dataset as it was on March 14" was a single argument to the SDK, not a manual data wrangle. Schema evolution let new sensor fields land without breaking historical training runs.
- **Columnar Parquet for training data loaders.** Custom Protobuf-to-Parquet conversion preserved nested sensor structures (LiDAR, camera, control signals) while making partition-pruned, projected reads cheap — the shape of access perception data loaders actually do.
- **Python SDK as the data-scientist contract.** Wrapped Iceberg queries and Kubernetes Spark-job submission behind a single SDK; perception engineers requested training samples and ran feature-derivation jobs without writing Kubernetes manifests or Spark configs.
- **Hybrid-cloud, multi-DC ingestion.** Spark Streaming jobs auto-scaled on K8s in each data center; Elasticsearch tracked lineage and per-job status across DCs so dataset freshness for downstream training was always observable.
- **Dual-queue ingestion path.** Kafka for the high-throughput sensor data, RabbitMQ for lower-volume control messages — each path tuned independently for throughput vs. latency.

## Results

- 10TB+/day of perception sensor data converted into ML-ready Parquet on Iceberg.
- 70% reduction in workflow execution time after the Spark Streaming migration.
- 50% reduction in infrastructure cost.
- 80% reduction in resource usage by replacing custom micro-batch jobs with native Spark Streaming.
- Self-service training-data access for perception data scientists via the Python SDK — eliminated the data-engineering bottleneck on training-cut requests.
