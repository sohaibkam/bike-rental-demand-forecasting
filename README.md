# Bike Rental Demand Forecasting
biggest problem which disappoints cycling enthusiasts 

## Idea
An AWS-based data platform that predicts bikeshare rental demand — 
covering the data pipeline, the infrastructure it runs on, and an 
agentic AI layer that monitors pipeline health.

## Problem

Bikeshare operators need to predict demand by time and location to 
rebalance bikes across stations efficiently. This project builds a 
forecasting pipeline, then treats it as a platform: infrastructure-as-code, 
automated data quality checks, and an AI agent that watches over it.

## What's Implemented vs Planned

| Layer | Status |
|---|---|
| Data ingestion & transformation (S3, PySpark) | ✅ Implemented |
| Regression model (R² 0.98) | ✅ Implemented |
| Airflow retraining schedule | ✅ Implemented |
| Power BI reporting | ✅ Implemented |
| Infrastructure as Code (Terraform) | 🔧 In progress |
| CI/CD + automated data quality checks | 🔧 In progress |
| Containerized transform step (Docker) | 📋 Planned |
| Agentic pipeline-health assistant (Claude API) | 📋 Planned |

## Architecture

See [docs/ARCHITECTURE.md](docs/ARCHITECTURE.md) for the full system design, 
including the DataOps and DevOps layers and the agentic AI component.

## Tech Stack

- **Ingestion & Storage:** Amazon S3
- **Transformation:** PySpark
- **Modeling:** scikit-learn (regression)
- **Orchestration:** Apache Airflow
- **Reporting:** Power BI
- **Infrastructure as Code:** Terraform *(in progress)*
- **CI/CD:** GitHub Actions *(in progress)*
- **Agentic AI:** Claude API, tool-use for log/metric analysis *(planned)*

## Results

- Regression model achieved R² of 0.98 on held-out test data
- Automated retraining pipeline keeps the model current as new data arrives

## Project Structure


## Status

Actively building out the DataOps, DevOps, and agentic AI layers on top 
of the working forecasting pipeline. See the roadmap for what's next.

