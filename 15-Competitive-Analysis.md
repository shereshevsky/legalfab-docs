---
layout: default
title: Competitive Analysis
---

# LegalFab Competitive Analysis

**Version:** 1.0
**Last Updated:** February 2026

---

## Overview

This document provides technical comparisons between LegalFab and alternative platforms. The comparisons focus on architectural differences, capability gaps, and LegalFab's key differentiators.

### LegalFab Key Differentiators

| Differentiator | Description |
|:---------------|:------------|
| **True Data Fabric** | Data stays in source systems; metadata-driven federation, not centralized storage |
| **Persistent Knowledge Graph** | Cross-source entity resolution with relationship modeling and provenance tracking |
| **OSINT & Regulatory Intelligence** | Native integration with sanctions, PEP, corporate registries, adverse media |
| **Deployment Flexibility** | SaaS, dedicated, customer cloud, on-premises, air-gapped options |
| **Legal Domain Ontology** | Purpose-built 4-level schema evolution for legal practice areas |

---

## LegalFab vs. Microsoft Fabric

### Executive Summary

LegalFab implements a **true data fabric pattern** — keeping data in place, federating queries across sources, and building intelligence through a persistent knowledge graph with built-in entity resolution. Microsoft Fabric implements a **data lakehouse pattern** that centralizes data into OneLake. Fabric IQ (announced November 2025) adds ontology and graph capabilities on top of this lakehouse, but does not change the underlying architecture: data still moves to OneLake, and entity resolution still requires third-party tools.

> **Key Distinction:** Microsoft does not primarily market Fabric as a "data fabric." Their documentation positions it as a "unified analytics platform" built on a lakehouse architecture. The name "Fabric" is a product brand, not an architectural descriptor.

### What Microsoft Fabric Actually Is

Microsoft Fabric is a SaaS analytics platform built on a data lakehouse architecture. Its foundational storage layer, OneLake, is logically unified but physically backed by Azure Data Lake Storage Gen2 (ADLS Gen2). All data in OneLake is stored in Delta Lake format (Parquet files with ACID transaction logs). Multiple compute engines — Spark, T-SQL (Synapse), Analysis Services (Power BI) — read from the same physical OneLake copy. This is **engine virtualization, not source data virtualization**.

The primary data integration pattern is ETL/ELT via Data Factory and Dataflows Gen2. Data is extracted from source systems, transformed, and loaded into OneLake — traditional data movement where data leaves its source system.

### LegalFab Knowledge Fabric Architecture

LegalFab's Knowledge Fabric is a metadata-driven integration layer that implements the data fabric pattern. Source data remains in its original systems. The Knowledge Fabric stores only: entity resolution, cross-system relationships, annotations, insights, and temporal snapshots. Actual records — documents, transaction records, communications, files — stay in their source systems and are accessed at runtime.

**The Persistent Knowledge Graph** models entities (Persons, Organizations, Matters, Documents, Addresses, Identifiers) and relationships (OWNS, CONTROLS, RELATED_TO, EMPLOYS, REPRESENTS, LOCATED_AT). This is not a metadata catalog — it is an active intelligence layer that resolves entities across sources, tracks lineage, and enables graph traversal for investigative queries.

Microsoft Fabric has no equivalent. Its metadata management relies on Purview — a separate Azure service — that provides catalog-based governance but does not perform entity resolution, does not build graph-based relationships across data sources, and does not provide semantic intelligence.

### Fabric IQ: Microsoft's Semantic Layer (November 2025)

> **Status:** Public Preview — No GA Date Announced. Entered public preview November 19, 2025. Production deployments carry preview-stage risk.

Fabric IQ is a semantic intelligence layer with two components: an **Ontology** (entity type definitions, relationship types, business rules) and a **Fabric Graph** (graph-compute layer for traversals). Microsoft positions Fabric IQ for "agentic AI" grounding.

**Critical Distinction:** Fabric IQ's ontology stores entity **type definitions** (e.g., "Customer has properties: Name, Revenue, Segment"). It does **not** store entity **instances** — the actual resolved records. LegalFab's knowledge graph stores resolved entity instances and their relationships persistently — it knows that "John Smith at 123 Main St" in System A is the same person as "J. Smith" in System B.

**DirectLake-Only Limitation:** Fabric IQ's AI agents can only bind to DirectLake semantic models. Power BI models using Import or DirectQuery mode are not supported, creating a substantial adoption barrier.

### Head-to-Head Comparison

| Dimension | LegalFab Knowledge Fabric | Microsoft Fabric |
|:----------|:--------------------------|:-----------------|
| **Architecture Pattern** | Data Fabric — metadata-driven, federated, data stays in place | Data Lakehouse — centralized OneLake storage, Delta Lake format |
| **Data Location** | Remains in source systems; only metadata/mappings stored centrally | Ingested into OneLake via ETL/ELT; shortcuts offer limited read-only federation |
| **Knowledge Graph** | Persistent graph with entity resolution, relationship modeling, provenance | No native graph; Purview (separate service) for metadata catalog |
| **Entity Resolution** | Built-in: blocking, matching, clustering across all sources | Not available; requires custom implementation |
| **OSINT Integration** | Native: sanctions, PEP, corporate registries, beneficial ownership, adverse media | None; general-purpose analytics platform |
| **Data Integration** | 200+ MCP connectors with federated queries; two-way data flow | Data Factory ETL/ELT; shortcuts for limited sources (read-only) |
| **Data Duplication** | Eliminated by design — single source of truth in source systems | Reduced between engines, but data duplicated from source |
| **Metadata Approach** | Active metadata: continuous analysis, enrichment, discovery, quality monitoring | Passive metadata scanning; Purview catalog and lineage |
| **Vendor Lock-In** | Low — data stays in existing systems; provider-agnostic LLM layer | High — data consolidated in OneLake; Microsoft stack dependency |
| **AI Layer** | Provider-agnostic: OpenAI, Anthropic, Google, Llama, Mistral via LightLLM | Microsoft Copilot, primarily Azure OpenAI |
| **Deployment** | SaaS, dedicated cloud, customer cloud, on-premises, hybrid, air-gapped | SaaS only (Azure-hosted); no on-premises or air-gapped |

### Where Each Platform Excels

**LegalFab Advantages:**

- **True data-in-place architecture:** Metadata-driven federation keeps source data where it lives — not a feature, but the design philosophy
- **Knowledge graph intelligence:** Persistent knowledge graph with cross-source entity resolution — Microsoft has no equivalent
- **OSINT and regulatory intelligence:** Native integration with sanctions, PEP, corporate registries — federated through the knowledge graph
- **Deployment flexibility:** On-premises, air-gapped, hybrid options. Microsoft Fabric is SaaS-only on Azure

**Microsoft Fabric Advantages:**

- **Ecosystem breadth:** Deep integration across Power BI, Azure, Microsoft 365, Teams, Copilot
- **General-purpose analytics:** Data science, real-time analytics, data warehousing, BI in a single platform
- **Open format commitment:** Delta Lake on Parquet is open-source; data format is portable

### The Fundamental Difference

| LegalFab Approach | Microsoft Fabric Approach |
|:------------------|:--------------------------|
| Data stays in source systems | Data copied into centralized OneLake |
| Persistent knowledge graph stores resolved entities | Fabric IQ ontology defines entity types (preview) |
| Federated queries at runtime | Queries run against OneLake copies |
| No data duplication by design | Reduced inter-engine duplication only |

> **Microsoft Fabric consolidates your data into its platform. LegalFab builds intelligence on top of your data where it already lives.**

---

## LegalFab vs. DeepJudge

### Comparison Matrix

| Category | Capability | DeepJudge | LegalFab |
|:---------|:-----------|:----------|:---------|
| **Data Architecture** | Core approach | Centralized index via connectors | True federation (query-time joins) |
| | Data location | Remains in source systems | Remains in source systems |
| | Schema handling | Normalized at indexing | Schema-on-read preserves source schemas |
| | Index requirement | Unified search index required | No centralized index required |
| **External Data (OSINT)** | Web search/news | ❌ | ✅ |
| | Sanctions / PEP feeds | ❌ | ✅ Continuous monitoring |
| | Market intelligence | ❌ | ✅ Capital IQ, PitchBook, D&B |
| | Company registries | ❌ | ✅ Companies House, SEC filings |
| | Regulatory feeds | ❌ | ✅ Alert monitoring |
| **Discovery & Lineage** | Connection method | Manual connector configuration | Automatic discovery |
| | FK/constraint detection | Per-connector mapping | ✅ Metadata scanning |
| | Implicit relationships | ❌ | ✅ Statistical inference |
| | Provenance (source attribution) | ✅ "Answer from Document X" | ✅ |
| | Data lineage (query path) | ❌ | ✅ Full visualization (PMS→DMS→CRM) |
| | Relationship discovery audit | ❌ | ✅ How systems connect |
| **Knowledge Graph** | Graph database | ❌ | ✅ PostgreSQL + Apache AGE |
| | Defined entity types | ❌ | ✅ 6 core types |
| | Defined edge types | ❌ | ✅ Defined relationship types |
| | Entity resolution | Basic (document-level) | Advanced (cross-system, aliases, subsidiaries) |
| | Community detection | ❌ | ✅ Leiden algorithm |
| **Ontology & Schema** | Schema model | Implicit in index structure | Explicit 4-level evolution (L0→L3) |
| | Practice-specific schemas | ❌ | ✅ Corporate, Litigation, etc. |
| | Firm customization | Via workflow builder | L3 firm-specific schemas |
| **Expertise Discovery** | Document authorship | ✅ | ✅ 1.0× weight |
| | Matter participation | Not detailed | ✅ Lead 0.9×, Support 0.7× |
| | Time entries | Not detailed | ✅ 0.8× weight |
| | Self-declared profiles | Not detailed | ✅ 0.4× weight (discounted) |
| | Temporal decay | Not mentioned | ✅ e^(-0.002 × days) |
| | Transitive expertise | ❌ | ✅ Graph traversal queries |
| **Multi-Tenant / Mergers** | Multi-firm isolation | ❌ | ✅ VPC-per-tenant |
| | Encryption separation | Not detailed | ✅ Separate KMS keys per firm |
| | Vector store isolation | Not addressed | ✅ Namespace separation |
| | Cross-firm queries | ❌ | ✅ Authorized federation |
| | Conflict detection | ❌ | ✅ Cross-firm conflicts check |
| | Shared client identification | ❌ | ✅ Entity resolution across firms |
| **AI Workflows & Agents** | Pre-built legal workflows | ✅ | ✅ |
| | Contract analysis | ✅ | ✅ |
| | Matter summarization | ✅ | ✅ |
| | HR queries | Not shown | ✅ |
| | BD/pipeline analysis | Not shown | ✅ Cross-CRM federation |
| | Regulatory monitoring | Not shown | ✅ External feed integration |
| | Workflow builder | ✅ Low-code/no-code | ✅ |

### Architectural Philosophy Comparison

| Feature | DeepJudge (Index-Centric) | LegalFab (Semantic-Centric) | Why LegalFab Wins |
|:--------|:--------------------------|:----------------------------|:------------------|
| **Discovery Philosophy** | Passive Ingestion — Connects to APIs and ingests text "as-is" | Active Reconnaissance — Scans schemas, FKs, statistically infers relationships | LegalFab finds "hidden" connections that search indexes miss |
| **Entity Resolution** | Text-Based Matching — Relies on keyword matches | Graph-Based Unification — Recognizes "Acme Corp," "Acme Inc," and aliases as same entity | Creates Single Source of Truth virtual layer |
| **Knowledge Structure** | Flattened Index — Rich data simplified to Document + Tags | Ontology-Driven Graph — Maps to 4-level Legal Ontology preserving hierarchy | Understands Legal Context — "Plaintiff" vs. "Lender" relationships |
| **Connecting Systems** | Manual Connectors — Pre-configured, manual implementation | Automatic Join Discovery — Detects how systems can be joined | Instant Federation — Query across merged firms immediately |
| **Trust & Lineage** | Provenance — "Answer from Document X" | Full Lineage — "Derived by joining Table A (System A) to Table B (System B) with 94% confidence" | Auditability of Logic — Critical for compliance |

---

## Summary

| Platform | Architecture | Entity Resolution | OSINT | Deployment Options |
|:---------|:-------------|:------------------|:------|:-------------------|
| **LegalFab** | True data fabric — data in place | ✅ Built-in, cross-source | ✅ Native integration | Full range including on-prem |
| **Microsoft Fabric** | Data lakehouse — centralized OneLake | ❌ Requires third-party | ❌ None | SaaS only (Azure) |
| **DeepJudge** | Centralized search index | Basic (document-level) | ❌ None | Not detailed |

---
