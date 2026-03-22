
# LegalFab Competitive Analysis

**Version:** 3.0
**Last Updated:** March 2026

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

## LegalFab vs. Intapp Open

### Executive Summary

LegalFab and Intapp Open both address client and matter onboarding, conflicts, and compliance — but they come from fundamentally different architectural eras. Intapp Open is the direct evolution of The Frayman Group's Compliguard suite (acquired 2014), built on a **workflow-centric, relational data model** with AI capabilities bolted on over time. LegalFab is an **AI-native platform** built from the ground up around a graph-based Knowledge Fabric, agentic automation, and continuous intelligence. The comparison is not feature-by-feature — it is generational.

> **Key Distinction:** Intapp Open centralises data into a separate index and executes rules through a monolithic workflow engine. LegalFab keeps data in source systems, resolves entities through graph operations, and orchestrates compliance through composable agentic workflows.

### What Intapp Open Actually Is

Intapp Open is a workflow and conflicts management platform for law firms, anchored by the Intapp Integration Builder. Its core architecture — structured data model, centralised pipelines, point-to-point connectors — traces back to The Frayman Group's Compliguard suite. Since acquisition, Intapp has added ethical walls, risk scoring, AML/KYC orchestration, AI-assisted conflicts relevance, and Azure cloud hosting. However, the foundational workflow engine and relational data model remain unchanged. AI capabilities function as an enhancement layer, not as the architectural foundation.

### Head-to-Head Comparison

| Dimension | LegalFab Knowledge Fabric | Intapp Open |
|:----------|:--------------------------|:------------|
| **Architecture Pattern** | AI-native Knowledge Fabric — graph-based, data stays in place | Workflow-centric — relational data model, centralised index |
| **Data Location** | Remains in source systems; only metadata/mappings stored centrally | Extracted into separate Intapp index via ETL pipelines |
| **Knowledge Graph** | Persistent graph with entity resolution, relationship modelling, provenance | No native graph; relational schema with bolt-on corporate tree modules |
| **Entity Resolution** | Graph-native: attribute comparison + structural analysis + similarity edges; continuous | Text-based: name normalisation, fuzzy matching; batch processing |
| **False Positive Rate** | Low — structural context (graph neighbourhood) eliminates ambiguous matches | High — keyword/name matching returns broad results requiring manual review |
| **OSINT Integration** | Native: autonomous, schema-driven collection from open sources across jurisdictions | Pre-configured integrations with specific commercial providers (BvD, World-Check) |
| **Perpetual KYC (pKYC)** | ✅ Continuous OSINT re-collection, change detection, automatic BPM triggers | ❌ Periodic reviews; changes detected only on manual re-check or scheduled cycle |
| **Perpetual AML/Conflicts** | ✅ Event-driven; every data change triggers re-evaluation across graph | ❌ Point-in-time at intake; ongoing monitoring requires external configuration |
| **Rules Engine** | Multi-paradigm: schema matching, natural language, text-to-graph, GTA (DAG agents) | Single paradigm: form-based conditional logic; complex rules require custom scripting |
| **Risk Configuration** | Dynamic, rule-type-agnostic; continuous re-assessment as data changes | Tightly coupled to workflow engine; static risk scoring at intake |
| **Screening** | FCA-compliant; 70+ matching algorithms; real-time + batch + delta-delta; adverse media via GenAI NLP | Standard sanctions/PEP screening via third-party provider integrations |
| **AI Layer** | Foundational — agentic workflows, compound AI orchestration, provider-agnostic LLM | Bolt-on — AI-assisted conflicts relevance ranking; not architecturally integrated |
| **Integration Model** | MCP-first; 200+ connectors; federated queries | Point-to-point connectors; fragile during upgrades; manual data mapping |
| **Data Duplication** | Eliminated by design — single source of truth in source systems | Required — separate index, ETL pipelines, ongoing data cleansing |
| **Implementation Time** | Days (ontology-based, no upfront schema definition) | Months (specialist configuration, data migration, custom integrations) |
| **Deployment Options** | Public cloud, private cloud, managed service, hybrid/phased | Azure-hosted; monolithic architecture limits cloud-native flexibility |
| **Corporate Hierarchies** | Native to graph model — ownership is a relationship type | Bolt-on module — requires separate licence and configuration |
| **Multi-Tenant / Mergers** | ✅ VPC-per-tenant, cross-firm entity resolution, authorised federation | Limited — separate deployments, no native cross-firm resolution |

### Architectural Philosophy Comparison

| Feature | Intapp Open (Workflow-Centric) | LegalFab (AI-Native Graph) | Why LegalFab Wins |
|:--------|:-------------------------------|:---------------------------|:------------------|
| **Data Philosophy** | Centralise & Index — data extracted into Intapp's own repository | Federate & Analyse in Place — data stays in source systems | No data duplication, no ETL pipelines, always current |
| **Entity Resolution** | Text-Based Matching — name normalisation, fuzzy strings, batch runs | Graph-Native Unification — attributes + structural position + continuous resolution | Low false positives, near-zero false negatives |
| **Compliance Model** | Point-in-Time — checks at intake, periodic scheduled reviews | Perpetual & Event-Driven — every data change triggers re-evaluation | Always-current risk posture, not stale snapshots |
| **Rules & Risk** | Single Paradigm — form-configured conditions, coupled to workflow engine | Multi-Paradigm — schema, NL, text-to-graph, GTA agents; rule-agnostic risk scoring | Compliance teams define rules in natural language; complex scenarios compose as DAGs |
| **External Intelligence** | Provider-Dependent — pre-configured integrations with commercial databases | Autonomous OSINT — schema-driven, traverses open sources as deep as needed | Eliminates single-provider dependency; richer, more current entity intelligence |
| **Deployment** | Monolithic on Azure — long cycles, specialist configuration, expensive upgrades | Cloud-native — public/private cloud, managed service, phased adoption | Days to deploy vs. months; lower TCO; data sovereignty flexibility |

### Where Each Platform Excels

**LegalFab Advantages:**

- **Graph-native entity resolution:** Combines attribute matching with structural graph analysis — dramatically reduces false positives while catching matches text-based systems miss
- **Autonomous OSINT & pKYC:** Schema-driven intelligence collection from open sources with continuous change detection and BPM triggers — no dependence on single commercial provider
- **Multi-paradigm rules engine:** Schema matching, natural language rules, text-to-graph extraction, and Game-Tree Agent DAG orchestration — compliance teams can define rules at any complexity level
- **Perpetual compliance:** AML, conflicts, and KYC assessments run continuously and event-driven, not point-in-time
- **Deployment flexibility:** Cloud, managed service, hybrid/phased — deployed in days, not months

**Intapp Open Advantages:**

- **Market incumbency:** Dominant installed base in large law firms; established vendor relationships and switching costs
- **Workflow maturity:** Decades of refinement in legal intake workflow orchestration; extensive best-practice templates
- **Ecosystem breadth:** Integration with broader Intapp suite (Walls, DealCloud, Time) and Microsoft 365 ecosystem
- **Compliance track record:** Long regulatory history provides comfort to risk-averse decision-makers

### The Fundamental Difference

| LegalFab Approach | Intapp Open Approach |
|:------------------|:---------------------|
| Data stays in source systems | Data copied into centralised Intapp index |
| Graph-native entity resolution (attributes + structure) | Text-based name matching (batch) |
| Perpetual, event-driven compliance | Point-in-time checks at intake |
| Multi-paradigm rules (schema, NL, text-to-graph, GTA) | Single-paradigm form-based conditions |
| Autonomous OSINT with pKYC change detection | Pre-configured commercial provider integrations |
| Deployed in days; cloud/managed/hybrid options | Deployed in months; Azure-hosted monolith |

> **Intapp Open reflects the best thinking of an earlier era — workflow automation over structured data with point-in-time compliance. LegalFab is built for how risk actually manifests: through evolving relationships, incomplete information, and continuous change.**

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

| Platform | Architecture | Entity Resolution | OSINT | pKYC | Rules Engine | Perpetual AML/Conflicts | Deployment Options |
|:---------|:-------------|:------------------|:------|:-----|:-------------|:------------------------|:-------------------|
| **LegalFab** | True data fabric — data in place | ✅ Graph-native (attributes + structure); continuous | ✅ Autonomous, schema-driven | ✅ Change detection + BPM triggers | Multi-paradigm (schema, NL, text-to-graph, GTA) | ✅ Event-driven, continuous | Cloud, managed service, hybrid, on-prem |
| **Intapp Open** | Workflow-centric — centralised index | Basic (text-based, batch) | ❌ Pre-configured providers only | ❌ Periodic manual reviews | Single paradigm (form-based conditions) | ❌ Point-in-time at intake | Azure-hosted monolith |
| **Microsoft Fabric** | Data lakehouse — centralised OneLake | ❌ Requires third-party | ❌ None | ❌ None | N/A (general-purpose analytics) | N/A | SaaS only (Azure) |
| **DeepJudge** | Centralised search index | Basic (document-level) | ❌ None | ❌ None | Workflow builder (single paradigm) | ❌ Not detailed | Not detailed |

---
