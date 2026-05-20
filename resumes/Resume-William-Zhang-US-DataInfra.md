# WEIXIN (WILLIAM) ZHANG

206-388-6391 — Bothell, WA 98021 — williamwxz@gmail.com

GitHub — LinkedIn — williamwxz.github.io

## Professional Summary

Software Engineer with 8+ years of experience building data pipelines and infrastructure for ML/AI and Web3 applications. Skilled in designing large-scale real-time and batch pipelines, lakehouse and feature store architectures, and cloud-native infrastructure end to end.

## Professional Experience

**Senior Data Engineer — Gauntlet** *— Nov 2024 to Present*

Architect real-time and batch data infrastructure for quantitative crypto analytics. Streaming pipelines on WebSocket, Kafka, Redpanda, and Flink; OLAP on ClickHouse, StarRocks, and BigQuery; Dagster orchestration, Kubernetes-deployed services, and full DevOps lifecycle ownership.

**Senior Data Engineer — Oracle Health AI** *— Apr 2023 to Nov 2024*

Built high-throughput data pipelines on Oracle Cloud Infrastructure for the Health AI team. Consolidated distributed sources into an Iceberg data lake; designed Spark and Airflow ETL workflows powering enterprise healthcare reporting and real-time dashboarding.

**Senior Data Engineer — Weride.ai** *— Apr 2021 to Apr 2023*

Optimized big data infrastructure for autonomous driving on Scala Spark and Kubernetes in a hybrid cloud environment. 1TB+/day throughput; 50% storage cost reduction; 70% workflow time reduction; 80% resource usage reduction.

**Software Development Engineer — Amazon** *— Sep 2018 to Apr 2021*

Built serverless IoT applications for the Robotic Infrastructure team on AWS Lambda, Greengrass, CDK, and IoT Core. Orchestrated 10+ AGVs per site; saved $500K/year per warehouse.

**Software Engineer — Evertz Microsystems** *— May 2015 to Sep 2018*

Developed embedded software for real-time video streaming devices; low-latency signal processing across broadcast infrastructure.

## Key Projects

**AI Infrastructure Platform for Furniture eCommerce** *— Mar 2026 to Present*

- Built self-hosted AI infrastructure on GCP for a Shopify furniture retailer using TypeScript, Python, Pub/Sub, pgvector on Neon Postgres, Vertex AI, vLLM on GKE, Cloud Run, Helm, and Terraform; consolidated RAG, embedding pipeline, and model serving into a shared platform, enabling new AI agents to be built against a unified API.
- Kept product and merchant context fresh for every agent by streaming Shopify webhooks through a Pub/Sub embedding pipeline into pgvector, providing sub-500ms retrieval across ~1.9K products and ~2.7K SKU variants; reused the Neon Postgres database as the vector store, eliminating the operational overhead of a dedicated vector DB.
- Designed a model-agnostic serving gateway exposing /embed, /generate, and /rerank endpoints as the single entry point for all agent inference, with per-workload routing directing bulk tasks to Gemini and a planned path to self-hosted vLLM on GKE; sustained sub-2-second first-token latency on streaming generation.

**Crypto Market Data Platform** *— Nov 2025 to Present*

- Designed end-to-end crypto market data platform on AWS using WebSocket, Redpanda, Flink, ClickHouse Cloud, Dagster, StarRocks, and S3, deployed across ECS Fargate and Kubernetes with 100% Terraform IaC and GitHub Actions OIDC.
- Built real-time streaming PnL pipeline ingesting closed 1-minute candles from multi-exchange WebSocket feeds, fanning out MB/s of strategy state through Redpanda and Flink to ClickHouse Cloud with sub-minute end-to-end latency.
- Orchestrated historical backfill with Dagster across a 10TB+ S3 data lake in medallion architecture, powering StarRocks cross-exchange OLAP at sub-2-second latency; reduced monthly AWS spend substantially via S3 Glacier cold-tiering, RDS to Supabase metadata migration, and EKS to ECS Fargate consolidation.

**DeFi Smart Contract Data Pipeline** *— Feb 2025 to Jun 2025*

- Built a Rust WebSocket ingestion service capturing all EVM chain blocks, transactions, and logs in real time; 5MB/s throughput into Kafka and BigQuery; deployed to Kubernetes via Helm and Terraform.
- Designed blockchain data models and parsed Morpho and Aave smart contract events into ClickHouse for low-latency analytical queries; ETL and event parsing orchestrated by Dagster.
- Built Claude-powered skills for rapid EVM chain onboarding with minimal code changes; monitored via GCP log-based metrics with incident.io escalation.

**ML Feature Store for Quantitative Analytics** *— Apr 2024 to Oct 2024*

- Centralized ML feature store on Hopsworks and Snowflake serving 90+ features to data scientists and quant researchers; standardized Python SDK; medallion architecture in dbt.
- Snowflake native agent for natural-language data exploration; reduced ad-hoc analytics turnaround from hours to seconds across teams.
- Feature pipelines orchestrated with Y42 and dbt; consistent freshness and data quality across batch and on-demand serving paths.

**Autonomous Driving Data Pipeline** *— Dec 2021 to May 2022*

- Near real-time pipeline consuming RabbitMQ events; converted custom Protobuf raw files from 100MB up to 10GB each on S3 to Parquet on an Iceberg data lake; 10TB+/day across multiple data centers.
- Native Spark Streaming migration with Kubernetes auto-scaling; 70% workflow time reduction; 50% infrastructure cost reduction.
- Extended internal Scala Spark SDK for custom Protobuf formats; Python SDK for Iceberg queries and Spark job submission on Kubernetes.

**Robotic Orchestrator** *— Nov 2019 to Feb 2021*

- Full-stack IoT application on AWS orchestrating 10+ warehouse AGVs per site; reduced human-robot interaction risks; saved $500K/year per warehouse.
- Event-driven cloud infrastructure with AWS CDK; 100+ MQTT messages per AGV processed via Lambda and Greengrass at the edge.
- Serverless data ingestion and real-time telemetry pipelines on AWS IoT Core, Lambda, and DynamoDB for fleet monitoring and operational analytics.

## Education

**McMaster University** — B.Eng. in Mechatronic Engineering — Dean's List — CGPA 3.6 / 4.0 *— Sep 2012 to Apr 2017*

## Technical Skills

Languages — Python, Java, Scala, C++, TypeScript, SQL, Rust, Go, Solidity, Terraform

Streaming & Data Infrastructure — Kafka, Redpanda, Flink, Spark, ClickHouse, StarRocks, BigQuery, Snowflake, Redshift, Iceberg, Dagster, Airflow, dbt, Hopsworks, Trino, S3, Athena, AWS Glue, Elasticsearch, PostgreSQL

Data Modeling & Processing — WebSocket Streaming, CDC, Event-Driven Architecture, Medallion Architecture, Data Lakehouse, ML Feature Stores, Snowflake Cortex, Schema Evolution, Protobuf, Parquet, Avro, REST/gRPC APIs, Data Quality Frameworks

DevOps & Cloud — Kubernetes, Docker, AWS EKS, AWS Lambda, AWS CDK, AWS SQS, AWS Greengrass, GCP BigQuery, GCP KMS, GCP Monitoring, Prometheus, Grafana, Terraform, CI/CD

Portfolio — williamwxz.github.io
