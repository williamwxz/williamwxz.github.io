# Vehicle Data ETL Pipeline

**Timeline:** Dec 2021 - May 2022
**Stack:** Python, Spark Streaming, Kafka, RabbitMQ, Protobuf, Parquet, Apache Iceberg, Kubernetes, Elasticsearch

## Overview

Developed a near real-time data pipeline for an autonomous driving company, converting vehicle sensor data from Protobuf to Apache Parquet at 1TB+/day scale across multiple data centers in a hybrid cloud environment.

## Architecture

```
Autonomous Vehicles (Protobuf streams, 100MB–10GB/file)
            │
     Kafka + RabbitMQ
      (200K msgs/day)
            │
     Spark Streaming
   (Protobuf → Parquet)
            │
    ┌───────┼───────────┐
 Iceberg    │      Elasticsearch
 Data Lake  │     (lineage & monitoring)
 (S3/HDFS)  │
            │
     Python SDK
  (query + Spark job submission)
            │
    Data Scientists (self-service)
```

## Key Technical Decisions

- **Spark Streaming over micro-batch:** Migrated from custom micro-batch jobs to native Spark Streaming, improving system stability and reducing resource usage by 80%.
- **Dual message queue:** Used Kafka for high-throughput sensor data and RabbitMQ for lower-volume control messages, optimizing each path independently.
- **Customized Protobuf → Parquet:** Updated the Spark SDK to support customized Protobuf formats, converting raw files (100MB–10GB each) stored on S3 to Parquet while preserving nested structures for efficient columnar queries.
- **Iceberg data lake:** Used Apache Iceberg to manage data ingestion, providing schema evolution, time-travel, and partition management on top of S3/HDFS storage.
- **Auto-scaling on Kubernetes:** Implemented auto-scaling for Spark jobs on Kubernetes to handle variable data volumes across data centers.
- **Python SDK for self-service:** Extended an internal Python SDK enabling data scientists to query Iceberg tables directly and submit Spark jobs on Kubernetes.
- **Elasticsearch for observability:** Tracked data lineage and ETL job status in Elasticsearch, providing real-time visibility into pipeline health across data centers.

## Results

- 1TB+/day processing throughput across multiple data centers
- 70% reduction in workflow execution time
- 50% reduction in infrastructure costs
- 80% reduction in resource usage via Spark Streaming migration
- Self-service data access for internal data scientists via Python SDK and Iceberg
