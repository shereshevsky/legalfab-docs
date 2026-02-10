---
layout: default
title: Operating Costs
---

# LegalFab Operating Costs

**Version:** 1.0
**Last Updated:** February 2026

---

## Overview

This document provides estimated ongoing operating costs for LegalFab platform deployments within customer-managed infrastructure (self-hosted). These estimates cover infrastructure, consumption, and third-party service costs required to run the platform. License fees are not included and are covered under separate commercial terms.

---

## 1. LLM & AI Processing

### Option A: Cloud LLM Providers (per-token)

**Cost drivers:** Token consumption, model selection

| Workload | Monthly Estimate |
|:---------|:-----------------|
| Light (10K queries/month) | $500 - $1,500 |
| Medium (50K queries/month) | $2,000 - $6,000 |
| Heavy (200K+ queries/month) | $8,000 - $25,000 |

- Average query: ~2K input tokens, ~500 output tokens
- Embedding generation: ~$0.10 per 1M tokens
- Intelligent caching layer: **-30% to -50%**

### Option B: Self-Hosted LLM (GPU infrastructure)

**Cost drivers:** Model size, concurrency requirements, GPU selection

| Model Size | GPU Requirement | Monthly Estimate |
|:-----------|:----------------|:-----------------|
| 7-13B parameters | 1× A10/L4 (24GB) | $1,500 - $3,000 |
| 30-70B parameters | 2-4× A100 (80GB) | $8,000 - $20,000 |
| 70B+ parameters | 4-8× A100/H100 | $20,000 - $50,000 |

- Includes GPU instance + supporting infrastructure
- Scales with concurrent user load
- Embedding model: additional 1× A10/L4 recommended
- Intelligent caching layer: reduces GPU load by **30-50%**

---

## 2. Compute Infrastructure

**Cost drivers:** Concurrent users, query complexity, agent workloads

| Deployment Size | Monthly Estimate |
|:----------------|:-----------------|
| Small (≤50 users) | $2,000 - $4,000 |
| Medium (50-200 users) | $5,000 - $10,000 |
| Large (200+ users) | $12,000 - $30,000 |

- Base cluster: 3-5 nodes minimum
- Auto-scaling buffer: +20-30% for peak loads
- Graph compute scales with relationship density

---

## 3. Storage & Retention

**Cost drivers:** Document volume, retention period, backup policy

| Data Volume | Monthly Estimate |
|:------------|:-----------------|
| Small (<1TB) | $200 - $500 |
| Medium (1-10TB) | $500 - $2,000 |
| Large (10TB+) | $2,000 - $8,000 |

- Metadata DB: ~$0.10/GB/month
- Object storage: ~$0.02/GB/month
- Vector store: ~$0.15/GB/month
- AML log retention (5-7 years): plan for 10-20% annual growth

---

## 4. External Data Subscriptions

**Cost drivers:** Lookup volume, selected data providers

| Service Type | Typical Cost |
|:-------------|:-------------|
| Companies House API | Free tier / £50-500/month |
| Commercial ownership data (Bureau van Dijk, D&B) | $10K - $50K/year |
| Sanctions/PEP screening | $0.05 - $0.50 per lookup |
| Adverse media feeds | $5K - $20K/year |

- Volume discounts apply
- Customer provides existing subscriptions where available

---

## 5. Monitoring & Observability

**Cost drivers:** Log volume, retention requirements

| Component | Monthly Estimate |
|:----------|:-----------------|
| Metrics & APM | $300 - $1,500 |
| Log aggregation | $200 - $1,000 |
| Security monitoring | $200 - $500 |

---

## Summary

### Monthly Operating Cost Ranges

| Deployment Size | Monthly Total* |
|:----------------|:---------------|
| Small org | $3,000 - $6,500 |
| Mid-size org | $8,000 - $20,000 |
| Enterprise | $22,000 - $65,000 |

*Excludes external data subscriptions (Section 4); customers often leverage existing enterprise agreements.*

### Cost Optimization Levers

| Lever | Impact |
|:------|:-------|
| Intelligent caching | -30% to -50% on LLM costs |
| Reserved instances | -20% to -40% on compute |
| Tiered storage | -30% to -50% on storage |
| Self-hosted LLM | Variable; cost-effective at high volume |

---

## Notes

- All estimates based on major cloud providers (AWS, Azure, GCP)
- Actual costs vary by region, negotiated rates, and usage patterns
- External data provider costs depend on existing customer agreements
- Estimates assume standard high-availability configuration

---
