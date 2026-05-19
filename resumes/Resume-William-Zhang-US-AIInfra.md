# WEIXIN (WILLIAM) ZHANG

206-388-6391 — Bothell, WA 98021 — williamwxz@gmail.com

GitHub — LinkedIn — williamwxz.github.io

## Professional Summary

AI/ML Infrastructure Engineer with 8+ years of experience building production data and ML platforms. Expert in real-time streaming systems including Rust, Kafka, and WebSocket at 300GB+/day; ML feature stores, data lakehouses, and GPU-ready cloud-native infrastructure on Kubernetes. Bridges the gap between data engineering and model serving — builds the infrastructure AI systems run on at scale.

## Professional Experience

**Senior Data & ML Infrastructure Engineer — Gauntlet** *— Nov 2024 to Present*

Architect real-time and batch ML data infrastructure for quantitative crypto analytics. Streaming pipelines on WebSocket, Kafka, Redpanda, and Flink; OLAP on ClickHouse, StarRocks, and BigQuery; Dagster orchestration and Kubernetes-deployed services delivering production-ready data to ML pipelines and quant researchers.

**System Architect Consultant — Svim Labs, Part-time** *— Apr 2024 to Oct 2024*

Designed ML feature platform architecture for a fintech startup. Centralized feature store on Hopsworks and Snowflake serving 90+ features; Snowflake native agent for natural-language data exploration; event-driven on-chain data pipelines feeding ML models.

**Senior Data & ML Infrastructure Engineer — Oracle Health AI** *— Apr 2023 to Nov 2024*

Built high-throughput data pipelines on Oracle Cloud Infrastructure for the Health AI team. Consolidated distributed sources into an Iceberg data lake; Spark and Airflow workflows powering ML-ready datasets for healthcare AI models and real-time dashboarding.

**Senior Data Engineer — Weride.ai** *— Apr 2021 to Apr 2023*

Optimized big data infrastructure for autonomous driving ML pipelines on Spark and Kubernetes in a hybrid cloud environment. 1TB+/day of sensor and perception data; 50% storage cost reduction; 70% workflow time reduction; 80% resource usage reduction.

**Software Development Engineer — Amazon** *— Sep 2018 to Apr 2021*

Built serverless IoT data infrastructure for the Robotic Infrastructure team on AWS Lambda, Greengrass, CDK, and IoT Core. Real-time telemetry pipelines orchestrating 10+ AGVs per site; saved $500K/year per warehouse.

**Software Engineer — Evertz Microsystems** *— May 2015 to Sep 2018*

Developed embedded software for real-time video streaming devices; low-latency signal processing across broadcast infrastructure.

## Key Projects

**Crypto Market Data Platform — ML-Ready Data Lake** *— Nov 2025 to Present*

- Designed end-to-end crypto market data platform on AWS using WebSocket, Redpanda, Flink, ClickHouse Cloud, Dagster, StarRocks, and S3, deployed across ECS Fargate and Kubernetes with 100% Terraform IaC and GitHub Actions OIDC.
- Built real-time streaming PnL pipeline ingesting closed 1-minute candles from multi-exchange WebSocket feeds, fanning out MB/s of strategy state through Redpanda and Flink to ClickHouse Cloud with sub-minute end-to-end latency.
- Orchestrated historical backfill with Dagster across a 10TB+ ML-ready S3 data lake in medallion architecture, powering StarRocks cross-exchange OLAP at sub-2-second latency; reduced monthly AWS spend substantially via S3 Glacier cold-tiering, RDS to Supabase metadata migration, and EKS to ECS Fargate consolidation.

**DeFi Smart Contract Data Pipeline — Real-Time ML Feature Ingestion** *— Feb 2025 to Jun 2025*

- Built a Rust WebSocket ingestion service capturing all EVM chain blocks, transactions, and logs in real time; 5MB/s throughput into Kafka and BigQuery for downstream ML feature computation; deployed to Kubernetes via Helm and Terraform.
- Designed blockchain data models and parsed Morpho and Aave smart contract events into ClickHouse for low-latency analytical queries feeding quantitative ML models; ETL and event parsing orchestrated by Dagster.
- Built Claude-powered skills for rapid EVM chain onboarding with minimal code changes; monitored via GCP log-based metrics with incident.io escalation.

**ML Feature Store for Quantitative Analytics** *— Apr 2024 to Oct 2024*

- Centralized ML feature store on Hopsworks and Snowflake serving 90+ features to data scientists and quant researchers; standardized Python SDK; medallion architecture in dbt.
- Snowflake native agent for natural-language data exploration; reduced ad-hoc analytics turnaround from hours to seconds for ML teams.
- Feature pipelines orchestrated with Y42 and dbt; consistent freshness and data quality across batch and on-demand serving paths for ML model training and inference.

**Autonomous Driving Data Pipeline — Perception ML Training Infrastructure** *— Dec 2021 to May 2022*

- Near real-time pipeline consuming sensor events from RabbitMQ; converted custom Protobuf raw files from 100MB up to 10GB each on S3 to Parquet on an Iceberg data lake; 10TB+/day for perception ML model training.
- Native Spark Streaming migration with Kubernetes auto-scaling; 70% workflow time reduction; 50% infrastructure cost reduction.
- Extended internal Python SDK for Iceberg queries and Spark training job submission on Kubernetes; accelerated the ML model development iteration cycle.

**Robotic Orchestrator — IoT Data Infrastructure** *— Nov 2019 to Feb 2021*

- Full-stack IoT application on AWS orchestrating 10+ warehouse AGVs per site; reduced human-robot interaction risks; saved $500K/year per warehouse.
- Serverless data ingestion and real-time telemetry pipelines on AWS IoT Core, Lambda, and DynamoDB for fleet monitoring and operational analytics.

## Education

**McMaster University** — B.Eng. in Mechatronic Engineering — Dean's List — CGPA 3.6 / 4.0 *— Sep 2012 to Apr 2017*

## Technical Skills

Languages — Python, Java, TypeScript, SQL, Rust, Go, Solidity, Terraform

AI/ML Infrastructure — Spark, Kafka, Redpanda, Dagster, Airflow, dbt, Hopsworks Feature Store, Snowflake Cortex, BigQuery, ClickHouse, StarRocks, Snowflake, Iceberg, Trino, S3, Athena, AWS Glue, Elasticsearch, PostgreSQL

Data & ML Patterns — ML Feature Stores, Medallion Architecture, Data Lakehouse, Schema Evolution, CDC, Protobuf, Parquet, Avro, WebSocket Streaming, REST/gRPC APIs, Data Quality Frameworks, Feature Engineering Pipelines

DevOps & Cloud — Kubernetes, Docker, AWS EKS, AWS Lambda, AWS CDK, AWS SQS, AWS Greengrass, GCP BigQuery, GCP KMS, GCP Monitoring, Terraform, Grafana, CI/CD

Portfolio — williamwxz.github.io
