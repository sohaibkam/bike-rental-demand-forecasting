# Architecture

## Overview

The system has four layers: data pipeline, infrastructure, data quality/CI-CD, 
and an agentic AI layer that observes the other three.

## 1. Data Pipeline (Implemented)
```
Raw bikeshare data → S3 (raw zone) → PySpark transform → S3 (curated zone)
→ Feature table → Regression model → Power BI report
```
Apache Airflow schedules periodic retraining so the model reflects recent 
demand patterns rather than going stale.

## 2. Infrastructure Layer (In Progress)

Terraform provisions:
- S3 buckets (raw and curated zones) with lifecycle policies
- IAM roles scoped to least-privilege for each pipeline stage
- Glue/Redshift resources for the warehousing layer

Goal: infrastructure is defined as code and reproducible from a clean 
AWS account, not manually clicked together in the console.

## 3. DataOps Layer (In Progress)

- `quality_checks.py` runs schema validation, null-rate checks, and 
  row-count sanity checks after each ingest
- GitHub Actions runs these checks on every push, plus a smoke test 
  of the transform step, before any change reaches the retraining DAG
- Failures block the pipeline rather than silently producing a bad model

## 4. Agentic AI Layer (Planned)

A scoped agent — not a general chatbot — that reads Airflow run logs and 
model metrics after each retraining cycle and produces a plain-English 
summary using the Claude API:

- Records processed, anomalies flagged, R² drift vs. the previous run
- Flags likely causes when quality checks fail (e.g. "null rate spike 
  in `station_id` — check ingestion source")
- Posts the summary as a GitHub issue comment or Slack message

This uses tool-use (reading real pipeline data) plus reasoning (explaining 
what changed and why), rather than just wrapping an LLM around static text.

## Design Principles

- Each layer is independently useful — the pipeline works without the 
  agent, and the agent works without adding new infrastructure risk
- Nothing here is over-engineered for a personal project — each addition 
  maps to a real gap professional data platforms have to solve
