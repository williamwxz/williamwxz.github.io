# Robotic Orchestrator

**Timeline:** Nov 2019 - Feb 2021
**Stack:** AWS Lambda, AWS Greengrass, AWS CDK, MQTT, IoT Core, TypeScript

## Overview

Built a full-stack IoT application on AWS to orchestrate warehouse autonomous guided vehicles (AGVs), reducing human-robot interaction risks and enabling fully automated material transport across fulfillment centers.

## Architecture

```
Warehouse AGVs (10+ per site)
         │
    MQTT (100+ msgs/AGV)
         │
   AWS IoT Core + Greengrass
         │
    AWS Lambda (event processing)
         │
   Orchestration Layer
   (path planning, task assignment)
         │
   AWS CDK (infrastructure as code)
```

## Key Technical Decisions

- **AWS Greengrass at the edge:** Deployed Greengrass on local compute at each warehouse site, enabling low-latency decision-making for AGV coordination without round-tripping to the cloud.
- **MQTT for real-time telemetry:** Each AGV published 100+ MQTT messages for position, status, and sensor data. Used IoT Core rules to route messages to Lambda for real-time event processing.
- **AWS CDK for infrastructure:** Managed cloud infrastructure for 10+ AGVs per site using CDK, enabling repeatable deployments across multiple warehouse locations.
- **Serverless orchestration:** Used Lambda functions for stateless event processing, scaling automatically with the number of AGVs and message volume per site.

## Results

- $500K/year savings per warehouse through reduced human-AGV interaction
- 10+ AGVs orchestrated per site with 100+ MQTT messages each
- Fully automated material transport workflow
- Repeatable infrastructure deployments via AWS CDK
