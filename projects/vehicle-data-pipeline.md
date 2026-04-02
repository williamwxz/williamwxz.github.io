# Vehicle Data ETL Pipeline

**Timeline:** Dec 2021 - May 2022
**Stack:** Python, Spark Streaming, Kafka, RabbitMQ, Protobuf, Parquet, Kubernetes, Elasticsearch

## Overview

Developed a near real-time data pipeline for an autonomous driving company, converting vehicle sensor data from Protobuf to Apache Parquet at 1TB+/day scale across multiple data centers in a hybrid cloud environment.

## Architecture

```
Autonomous Vehicles (Protobuf streams)
            │
     Kafka + RabbitMQ
      (200K msgs/day)
            │
     Spark Streaming
   (Protobuf → Parquet)
            │
    ┌───────┴───────┐
  HDFS/S3         Elasticsearch
 (Parquet)       (lineage & monitoring)
```

## Key Technical Decisions

- **Spark Streaming over micro-batch:** Migrated from custom micro-batch jobs to native Spark Streaming, improving system stability and reducing resource usage by 80%.
- **Dual message queue:** Used Kafka for high-throughput sensor data and RabbitMQ for lower-volume control messages, optimizing each path independently.
- **Protobuf → Parquet:** Direct schema-aware conversion preserving nested structures, enabling efficient columnar queries downstream.
- **Elasticsearch for observability:** Tracked data lineage and ETL job status in Elasticsearch, providing real-time visibility into pipeline health across data centers.

## Results

- 1TB+/day processing throughput across multiple data centers
- 70% reduction in workflow execution time
- 50% reduction in infrastructure costs
- 80% reduction in resource usage via Spark Streaming migration
