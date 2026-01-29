---
layout: default
title: Knowledge Fabric
---

# LegalFab Knowledge Fabric

**Version:** 1.6
**Last Updated:** January 2026

---

## Component Overview

The Knowledge Fabric serves as the foundational data integration and intelligence layer for the LegalFab platform. It implements a metadata-driven architecture that provides unified access to distributed data assets while leaving source data in place. The Knowledge Fabric is fundamentally an access enabler, not a data repository—it maintains mappings and relationships rather than duplicating data, ensuring a single source of truth while providing unified investigative capabilities.

**Core Capabilities:**

| Capability        | Description                                  |
| :---------------- | :------------------------------------------- |
| Knowledge Graph   | Graph-native storage with entity resolution  |
| Entity Resolution | Cross-source entity matching and linking     |
| Connectivity      | Direct DB/API connections, MCP connectors    |
| Two-Way Data Flow | Read from and write back to source systems   |
| Discovery Service | Automated identification and cataloging      |
| Active Metadata   | Continuous metadata analysis and enrichment  |
| External Sources  | OSINT and external data integration          |
| Data Lineage      | End-to-end tracking of data flow             |
| MCP Creation      | Model Context Protocol connector generation  |
| Monitoring        | Health, performance, and security monitoring |

---

## Architecture Overview

```
┌─────────────────────────────────────────────────────────────────────────┐
│                        PRESENTATION LAYER                               │
│  ┌──────────────┐  ┌──────────────┐  ┌──────────────────────────────┐   │
│  │   Search UI  │  │  API Gateway │  │  Platform Integration APIs   │   │
│  └──────────────┘  └──────────────┘  └──────────────────────────────┘   │
│                              │                                          │
│                   [Authentication, Rate Limiting, Input Validation]     │
├─────────────────────────────────────────────────────────────────────────┤
│                          SERVICE LAYER                                  │
│  ┌──────────┐ ┌──────────┐ ┌──────────┐ ┌────────────┐ ┌────────────┐   │
│  │  Search  │ │ Lineage  │ │ Quality  │ │ Discovery  │ │ Governance │   │
│  │ Service  │ │ Service  │ │ Service  │ │  Service   │ │  Service   │   │
│  └──────────┘ └──────────┘ └──────────┘ └────────────┘ └────────────┘   │
│                              │                                          │
│                   [Service-to-Service AuthN/AuthZ, mTLS]                │
├─────────────────────────────────────────────────────────────────────────┤
│                      KNOWLEDGE GRAPH LAYER                              │
│  ┌──────────────┐  ┌──────────────────┐  ┌──────────────────────┐       │
│  │ Entity Store │  │ Relationship     │  │    Query Engine      │       │
│  │              │  │ Store            │  │                      │       │
│  └──────────────┘  └──────────────────┘  └──────────────────────┘       │
│                              │                                          │
│                   [Encryption at Rest, Access Control Lists]            │
├─────────────────────────────────────────────────────────────────────────┤
│                     CONNECTIVITY LAYER                                  │
│  ┌──────────────┐  ┌──────────────┐  ┌──────────────┐  ┌────────────┐   │
│  │  Database    │  │    API       │  │     MCP      │  │   Event    │   │
│  │  Connectors  │  │  Connectors  │  │  Connectors  │  │  Streams   │   │
│  └──────────────┘  └──────────────┘  └──────────────┘  └────────────┘   │
│                              │                                          │
│               [Credential Vault, Secure Connections, Data Sampling]     │
├─────────────────────────────────────────────────────────────────────────┤
│                       SOURCE SYSTEMS                                    │
│  ┌──────────┐ ┌───────────┐ ┌──────────┐ ┌──────────┐ ┌──────────────┐  │
│  │Databases │ │  Document │ │  APIs    │ │  Legal   │ │   External   │  │
│  │          │ │  Stores   │ │          │ │  Systems │ │   Sources    │  │
│  └──────────┘ └───────────┘ └──────────┘ └──────────┘ └──────────────┘  │
│                              │                                          │
│                [Customer-Managed, Customer Credentials]                 │
└─────────────────────────────────────────────────────────────────────────┘
```
![Architecture Overview](./images/Pasted%20image%2020260128180037.png)
---

## Knowledge Graph

The Knowledge Graph serves as the foundation for entity management, relationship tracking, and data integration across the LegalFab platform.
![Knowledge Graph](./images/Pasted%20image%2020260128180119.png)
### Graph Architecture

```
┌─────────────────────────────────────────────────────────────────────┐
│                    KNOWLEDGE GRAPH ARCHITECTURE                     │
├─────────────────────────────────────────────────────────────────────┤
│                                                                     │
│  ┌─────────────────────────────────────────────────────────────┐    │
│  │                    ENTITY RESOLUTION ENGINE                 │    │
│  │  ┌─────────────┐  ┌─────────────┐  ┌─────────────┐          │    │
│  │  │  Matching   │  │  Merging    │  │  Linking    │          │    │
│  │  │  Service    │  │  Service    │  │  Service    │          │    │
│  │  └─────────────┘  └─────────────┘  └─────────────┘          │    │
│  └─────────────────────────────────────────────────────────────┘    │
│                              │                                      │
│  ┌─────────────────────────────────────────────────────────────┐    │
│  │                    GRAPH STORAGE LAYER                      │    │
│  │  ┌─────────────┐  ┌─────────────┐  ┌─────────────┐          │    │
│  │  │  Entities   │  │Relationships│  │  Properties │          │    │
│  │  │  (Nodes)    │  │   (Edges)   │  │   (Attrs)   │          │    │
│  │  └─────────────┘  └─────────────┘  └─────────────┘          │    │
│  └─────────────────────────────────────────────────────────────┘    │
│                              │                                      │
│  ┌─────────────────────────────────────────────────────────────┐    │
│  │                    QUERY & TRAVERSAL                        │    │
│  │  • Graph Queries   • Path Finding   • Pattern Matching      │    │
│  │  • Aggregations    • Subgraph Extraction   • Analytics      │    │
│  └─────────────────────────────────────────────────────────────┘    │
└─────────────────────────────────────────────────────────────────────┘
```

### Entity Types

| Entity Type | Description | Key Attributes |
|:------------|:------------|:---------------|
| Person | Individual entities | Name variants, identifiers, demographics |
| Organization | Corporate entities | Legal name, registration, jurisdiction |
| Matter | Legal engagements | Matter ID, type, status, dates |
| Document | Legal documents | Type, classification, retention |
| Address | Physical/mailing addresses | Components, geolocation, validation |
| Identifier | External IDs | Type, value, issuer, validity |

### Relationship Types

| Relationship | From | To | Properties |
|:-------------|:-----|:---|:-----------|
| OWNS | Person/Organization | Organization | Percentage, start/end dates |
| CONTROLS | Person/Organization | Organization | Control type, effective date |
| RELATED_TO | Person | Person | Relationship type |
| EMPLOYS | Organization | Person | Role, department, dates |
| REPRESENTS | Organization | Person/Organization | Matter reference |
| LOCATED_AT | Person/Organization | Address | Address type, validity |
| HAS_IDENTIFIER | Person/Organization | Identifier | Primary flag |

---

## Entity Resolution

The Entity Resolution Engine identifies and links records that refer to the same real-world entity across multiple data sources.

### Entity Resolution Architecture

```
┌─────────────────────────────────────────────────────────────────────┐
│                    ENTITY RESOLUTION PIPELINE                       │
├─────────────────────────────────────────────────────────────────────┤
│                                                                     │
│  Source Records ──▶ [Blocking] ──▶ [Matching] ──▶ [Clustering]      │
│        │                │              │               │            │
│        ▼                ▼              ▼               ▼            │
│  (Raw ingestion)   (Candidate     (Similarity      (Entity          │
│                     pairs)         scoring)        assignment)      │
│                                        │               │            │
│                                        ▼               ▼            │
│                              [Human Review] ──▶ [Golden Record]     │
│                                (Uncertain        (Merged entity)    │
│                                 matches)                |           │
│                                        │                │           │
│                                        ▼                ▼           │
│                              [Audit Trail] ◀────────────┘           │
└─────────────────────────────────────────────────────────────────────┘
```

### Resolution Components

| Component | Function | Security Controls |
|:----------|:---------|:------------------|
| Blocking | Reduces comparison space | Configurable rules, no false negatives |
| Matching | Calculates similarity scores | Deterministic + probabilistic methods |
| Clustering | Groups related records | Configurable thresholds |
| Golden Record | Creates authoritative entity | Merge rules, conflict resolution |
| Human Review | Handles uncertain matches | Role-based assignment, audit trail |

### Matching Methods

| Method | Use Case | Accuracy |
|:-------|:---------|:---------|
| Exact Match | Identifiers, codes | 100% (when available) |
| Fuzzy Name Match | Person/organization names | Configurable threshold |
| Phonetic Match | Name variations, misspellings | Soundex, Metaphone |
| Address Standardization | Location matching | USPS/Royal Mail standards |
| ML-Based Scoring | Complex entity types | Model-dependent |

---

## External Source Integration

The Knowledge Fabric connects to external data sources for entity enrichment and verification.

### External Source Architecture

```
┌─────────────────────────────────────────────────────────────────────┐
│                    EXTERNAL SOURCE INTEGRATION                      │
├─────────────────────────────────────────────────────────────────────┤
│                                                                     │
│  ┌─────────────────────────────────────────────────────────────┐    │
│  │                    SOURCE REGISTRY                          │    │
│  │  • Source Catalog   • Credential Store   • Rate Limits      │    │
│  └─────────────────────────────────────────────────────────────┘    │
│                              │                                      │
│         ┌────────────────────┼────────────────────┐                 │
│         ▼                    ▼                    ▼                 │
│  ┌─────────────┐      ┌─────────────┐      ┌─────────────┐          │
│  │  Corporate  │      │  Identity   │      │   OSINT     │          │
│  │  Registries │      │  Providers  │      │  Sources    │          │
│  └─────────────┘      └─────────────┘      └─────────────┘          │
│         │                    │                    │                 │
│         └────────────────────┼────────────────────┘                 │
│                              ▼                                      │
│  ┌─────────────────────────────────────────────────────────────┐    │
│  │                    ENRICHMENT ENGINE                        │    │
│  │  • Entity Matching   • Data Fusion   • Provenance Tracking  │    │
│  └─────────────────────────────────────────────────────────────┘    │
│                              │                                      │
│                              ▼                                      │
│  ┌─────────────────────────────────────────────────────────────┐    │
│  │                    KNOWLEDGE GRAPH                          │    │
│  └─────────────────────────────────────────────────────────────┘    │
└─────────────────────────────────────────────────────────────────────┘
```

### External Source Categories

| Category | Examples | Data Types |
|:---------|:---------|:-----------|
| Corporate Registries | Companies House, SEC EDGAR | Incorporation, officers, filings |
| Identity Verification | ID document validation | Identity confirmation |
| Beneficial Ownership | PSC registers, UBO databases | Ownership chains |
| Sanctions Lists | OFAC, OFSI, UN, EU | Designated persons/entities |
| PEP Databases | Politically exposed persons | Political associations |
| Adverse Media | News aggregators, media monitors | Negative news, allegations |
| Court Records | Legal databases | Litigation history |
| Credit Bureaus | Business credit agencies | Financial standing |

### OSINT Integration Security

| Control | Implementation |
|:--------|:---------------|
| Source Validation | Only approved sources in registry |
| Credential Isolation | Per-source credential management |
| Rate Limiting | Respect source API limits |
| Data Minimization | Retrieve only required fields |
| Caching Policy | Time-limited caching per source |
| Provenance Tracking | Full lineage from source to graph |
| Schema Binding | Extracted data aligned to user-controlled schemas |

### Schema-Controlled Extraction

OSINT extractors use schemas defined by the user to structure incoming data. This ensures external data conforms to the organization's domain model.

| Capability | Description |
|:-----------|:------------|
| Schema Assignment | Each extractor bound to target schema |
| Field Mapping | External fields mapped to schema attributes |
| Type Conversion | External data converted to schema types |
| Validation | Extracted data validated against schema constraints |
| Default Values | Missing fields populated with schema defaults |

For detailed schema management, see [09-Schema-Management](09-Schema-Management.md).

### Enrichment Workflow

| Stage | Description | Security Control |
|:------|:------------|:-----------------|
| Request | Entity submitted for enrichment | Authorization check |
| Matching | Entity matched against external source | Matching rules applied |
| Retrieval | Data fetched from external source | Encrypted transport |
| Fusion | External data merged with existing | Conflict resolution rules |
| Validation | Enriched data validated | Schema validation |
| Storage | Enriched entity persisted | Access control inherited |
| Audit | Enrichment event logged | Full audit trail |

### External Source Monitoring

| Metric | Description | Alert Threshold |
|:-------|:------------|:----------------|
| Source Availability | External source uptime | < 99% over 24h |
| Response Latency | External source response time | > 5 seconds |
| Match Rate | Successful entity matches | < 70% (source-dependent) |
| Error Rate | Failed enrichment requests | > 5% |
| Credential Expiry | Days until credential expires | < 30 days |

---

## Customer System Connections

The Knowledge Fabric maintains live connections to customer source systems, keeping the graph synchronized with operational data.

![External Source Integration](./images/Pasted%20image%2020260128180258.png)
### Connection Architecture

```
┌─────────────────────────────────────────────────────────────────────┐
│                    CUSTOMER SYSTEM CONNECTIONS                      │
├─────────────────────────────────────────────────────────────────────┤
│                                                                     │
│                    ┌─────────────────────┐                          │
│                    │   KNOWLEDGE GRAPH   │                          │
│                    └─────────┬───────────┘                          │
│                              │                                      │
│              ┌───────────────┼───────────────┐                      │
│              ▼               ▼               ▼                      │
│  ┌───────────────────┐ ┌──────────────┐ ┌───────────────────┐       │
│  │  SYNC MANAGER     │ │ CHANGE DATA  │ │  MCP GATEWAY      │       │
│  │  (Batch/Schedule) │ │ CAPTURE      │ │  (Real-time)      │       │
│  └─────────┬─────────┘ └──────┬───────┘ └─────────┬─────────┘       │
│            │                  │                   │                 │
│            └──────────────────┼───────────────────┘                 │
│                               │                                     │
│  ┌─────────────────────────────────────────────────────────────┐    │
│  │                    CONNECTOR LAYER                          │    │
│  │  ┌─────────┐ ┌─────────┐ ┌─────────┐ ┌─────────┐ ┌───────┐  │    │
│  │  │  CRM    │ │ Practice│ │ Document│ │ Finance │ │ Custom│  │    │
│  │  │ Systems │ │ Mgmt    │ │  Mgmt   │ │ Systems │ │  APIs │  │    │
│  │  └─────────┘ └─────────┘ └─────────┘ └─────────┘ └───────┘  │    │
│  └─────────────────────────────────────────────────────────────┘    │
│                               │                                     │
│  ┌─────────────────────────────────────────────────────────────┐    │
│  │                    CUSTOMER SYSTEMS                         │    │
│  │  Matter Mgmt │ CRM │ Billing │ Document Mgmt │ HR Systems   │    │
│  └─────────────────────────────────────────────────────────────┘    │
└─────────────────────────────────────────────────────────────────────┘
```

### Customer System Types

| System Type         | Integration Method | Data Extracted                     |
| :------------------ | :----------------- | :--------------------------------- |
| Practice Management | API, database      | Matters, clients, contacts         |
| CRM Systems         | API                | Relationships, interactions        |
| Document Management | API                | Document metadata, classifications |
| Billing Systems     | API, database      | Financial relationships            |
| Email Archives      | API                | Communication metadata             |

### Connection Security Controls

| Control | Implementation |
|:--------|:---------------|
| Credential Vault | All connection credentials encrypted at rest |
| Connection Encryption | TLS 1.2+ required for all connections |
| IP Allowlisting | Customer can restrict to LegalFab IPs |
| Read-Only Access | Metadata extraction uses read-only credentials |
| Query Auditing | All queries to source systems logged |
| Data Sampling | Only statistical samples, no bulk data |

### Data Synchronization Security

| Control | Description |
|:--------|:------------|
| Conflict Resolution | Configurable rules for conflicting updates |
| Tombstone Handling | Deleted records tracked, not purged |
| Version Tracking | All entity versions preserved |
| Sync Validation | Checksums verify data integrity |
| Rollback Support | Sync batches can be reversed |

---

## Two-Way Data Flow

The Knowledge Fabric operates as a bidirectional system, enabling both read access and write-back to source systems while maintaining data governance and audit requirements.
![Customer System Connections](./images/Pasted%20image%2020260128180608.png)
### Data Flow Architecture

```
┌─────────────────────────────────────────────────────────────────────┐
│                    TWO-WAY DATA FLOW                                │
├─────────────────────────────────────────────────────────────────────┤
│                                                                     │
│                    ┌─────────────────────┐                          │
│                    │   KNOWLEDGE FABRIC  │                          │
│                    │   (Unified View)    │                          │
│                    └─────────┬───────────┘                          │
│                              │                                      │
│                    ┌─────────┴───────────┐                          │
│                    │   MCP CONNECTORS    │                          │
│                    │   (Bidirectional)   │                          │
│                    └─────────┬───────────┘                          │
│                              │                                      │
│         ┌────────────────────┼────────────────────┐                 │
│         │                    │                    │                 │
│         ▼                    ▼                    ▼                 │
│  ┌─────────────┐      ┌─────────────┐      ┌─────────────┐          │
│  │    READ     │      │    READ     │      │    READ     │          │
│  │  ─────────  │      │  ─────────  │      │  ─────────  │          │
│  │   CRM       │      │  Document   │      │   Data      │          │
│  │   WRITE     │      │  Mgmt       │      │   Lake      │          │
│  │  ─────────  │      │  WRITE      │      │   WRITE     │          │
│  └─────────────┘      └─────────────┘      └─────────────┘          │
│                                                                     │
│         READ: Query, retrieve, enrich                               │
│         WRITE: Update, create, enrich source data                   │
└─────────────────────────────────────────────────────────────────────┘
```

### Read Operations (Data Access)

| Operation            | Description                                            |
| :------------------- | :----------------------------------------------------- |
| Cross-Source Query   | Query across multiple sources simultaneously           |
| Entity Retrieval     | Retrieve entity information from authoritative systems |
| Document Access      | Access documents and case files where they're stored   |
| Relationship Queries | Pull relationship data from existing graph databases   |
| Real-Time Access     | Direct data access without ETL or replication          |

### Write Operations (Data Updates)

| Operation | Description |
|:----------|:------------|
| Record Updates | Update person/organization records at the source |
| Data Enrichment | Enrich source data with investigation findings |
| Entity Creation | Create new entities in authoritative systems |
| Audit Logging | Log investigative actions to audit databases |
| Relationship Write-back | Write discovered relationships to graph stores |

### Write-Back Workflow

When a user updates information through the Knowledge Fabric:

| Step                  | Activities                                            | Security Controls           |
| :-------------------- | :---------------------------------------------------- | :-------------------------- |
| User Action           | User updates data in Knowledge Fabric interface       | Authentication verified     |
| Source Identification | System identifies which source system owns the record | Authoritative source lookup |
| Permission Check      | Verify user has write access to source system         | Role-based authorization    |
| Format Validation     | Validate data meets source system requirements        | Schema validation           |
| Policy Check          | Verify update allowed per governance policies         | Data governance rules       |
| Write Execution       | MCP connector executes write to source system         | Encrypted transport         |
| Source Response       | Source system applies its own validation              | Native validation           |
| View Refresh          | Knowledge Fabric refreshes unified view               | Cache invalidation          |
| Propagation           | Related systems see updated data via connectors       | Cross-system consistency    |
| Audit Trail           | Complete logging of update chain                      | Immutable audit record      |

### Multi-System Coordination

When an entity exists in multiple systems:

| Control | Description |
|:--------|:------------|
| Primary Source Definition | Define authoritative source for each entity type |
| Multi-Write Option | Optionally write to multiple systems |
| Master Record Designation | Designate which system holds master record |
| Conflict Resolution | Handle when same entity has different values across sources |
| Cascade Control | Control whether updates cascade to related records |

### What Knowledge Fabric Stores vs. What Remains in Source Systems

**Stored in Knowledge Fabric:**

| Data Type                  | Purpose                                           |
| :------------------------- | :------------------------------------------------ |
| Entity Resolution Mappings | Person A in CRM = Person A in case management     |
| Cross-System Relationships | Person connected to organization across databases |
| Investigation Annotations  | Tags, notes, and classifications                  |
| Derived Insights           | Agent conclusions and analysis results            |
| Temporal Snapshots         | Point-in-time views for investigation history     |

**Remains in Source Systems:**

| Data Type | Location |
|:----------|:---------|
| Actual Records | Names, addresses, phone numbers in CRM/source |
| Document Files | Case files and evidence in document management |
| Transaction Records | Financial data in source systems |
| Communication Logs | Emails, messages in their native systems |
| Operational Data | All authoritative business data |

This architecture ensures you get a unified investigative view without moving or duplicating operational data. Updates to source systems are reflected immediately in the Knowledge Fabric view.

### Customer System Health Monitoring

| Health Check | Description | Frequency |
|:-------------|:------------|:----------|
| Connectivity | Source system reachable | 5 minutes |
| Authentication | Credentials valid | Hourly |
| Data Freshness | Last successful sync | Continuous |
| Schema Drift | Source schema changes | Daily |
| Performance | Sync latency and throughput | Per sync |

---

## Connectivity

The Connectivity layer provides secure access to heterogeneous data sources through multiple connection patterns.

### Connection Types

| Type            | Description                                   | Security Controls                       |
| :-------------- | :-------------------------------------------- | :-------------------------------------- |
| Direct Database | JDBC/ODBC connections to relational databases | Encrypted connections, credential vault |
| API Connections | REST/GraphQL/SOAP integrations                | OAuth/API key auth, TLS transport       |
| MCP Connectors  | Model Context Protocol for AI integration     | Schema validation, permission scoping   |
| Event Streams   | Kafka, message queue integrations             | mTLS, message encryption                |
| File Systems    | Cloud storage, network shares                 | Access tokens, encryption               |

### Database Connectivity Security

| Control | Implementation |
|:--------|:---------------|
| Connection Encryption | TLS 1.2+ required for all database connections |
| Connection Pooling | Managed pools with configurable limits |
| Query Timeout | Maximum query execution time enforced |
| Read-Only Mode | Optional read-only connections for metadata extraction |
| IP Allowlisting | Source system can restrict to LegalFab IPs |

### API Connectivity Security

| Authentication Method | Use Case | Security Properties |
|:----------------------|:---------|:--------------------|
| OAuth 2.0 | Modern APIs, cloud services | Token-based, scoped, refreshable |
| API Keys | Simple integrations | Rotatable, rate-limited |
| mTLS | High-security endpoints | Certificate-based mutual auth |
| Basic Auth (over TLS) | Legacy systems | Encrypted transport required |

### MCP Connector Security

The Knowledge Fabric can both consume and generate MCP (Model Context Protocol) connectors. With 200+ data source connectors available, the platform enables federated queries across diverse systems.

**MCP Connector Catalog:**

| Category            | Examples                                                                               |
| :------------------ | :------------------------------------------------------------------------------------- |
| Databases           | PostgreSQL, MySQL, MongoDB, Neo4j, Snowflake, BigQuery, ClickHouse, Oracle, SQL Server |
| SaaS Applications   | Salesforce, HubSpot, Slack, Gmail, Google Drive, Jira, GitHub, Airtable, Notion        |
| Cloud Storage       | AWS S3, Azure Blob, Google Cloud Storage, Dropbox, OneDrive                            |
| Document Management | SharePoint, iManage, NetDocuments, Box                                                 |
| Legal Systems       | Aderant, Elite, Clio, PracticePanther                                                  |
| AI/ML               | OpenAI, Anthropic Claude, ChromaDB, LanceDB                                            |


**MCP Connector Configuration:**

| Configuration | Description |
|:--------------|:------------|
| OAuth2 Flow | Secure authentication for SaaS connectors |
| API Key/Connection String | Database and API authentication |
| Sync Frequency | Hourly, daily, weekly, or on-demand sync |
| Enable/Disable | Toggle connectors without deletion |
| Custom Filters | Include/exclude rules for data indexing |

**MCP Schema Integration:**

MCP connectors utilize user-defined schemas to ensure extracted data aligns with the organization's domain model.

| Capability | Description |
|:-----------|:------------|
| Schema Provision | Schema provided to MCP tool for data extraction |
| Response Mapping | Tool response mapped to schema structure |
| Contract Enforcement | Tool outputs validated against expected schema |
| Type Safety | Strong typing prevents data inconsistencies |

For detailed schema management, see [09-Schema-Management](09-Schema-Management.md).

### Source System Connectivity Patterns

| Pattern | Description | Use Case |
|:--------|:------------|:---------|
| Direct TLS | Encrypted connection over internet | Cloud-hosted sources |
| VPN Tunnel | Site-to-site encrypted tunnel | On-premises sources |
| Private Link | Cloud provider private connectivity | Same-cloud sources |
| Agent-Based | Customer-deployed agent connects outbound | Air-gapped environments |

---

## Discovery Service

The Discovery Service automatically identifies and catalogs data assets across connected sources.
![Connectivity](./images/Pasted%20image%2020260128180801.png)
### Discovery Components

| Component        | Function                           | Security Controls                   |
| :--------------- | :--------------------------------- | :---------------------------------- |
| Crawler Engine   | Traverses source structures        | Depth limits, exclusion patterns    |
| Schema Extractor | Extracts table/column metadata     | Read-only access, no data retrieval |
| Profiler         | Computes statistical profiles      | Sampling limits, aggregation only   |
| Classifier       | Identifies sensitive data patterns | ML-based PII/sensitive detection    |

### Discovery Security Controls

| Control | Implementation |
|:--------|:---------------|
| Scan Scheduling | Configurable scan windows to minimize source impact |
| Rate Limiting | Throttled requests to prevent source overload |
| Sampling Limits | Maximum sample size for profiling (configurable) |
| Exclusion Rules | Ability to exclude specific schemas/tables |
| Metadata Only | No bulk data extraction; metadata and statistics only |

### Discovery Scope Management

| Scope Setting | Description | Default |
|:--------------|:------------|:--------|
| Schema Filter | Include/exclude specific schemas | All accessible |
| Table Filter | Include/exclude specific tables | All accessible |
| Column Sampling | Enable/disable column profiling | Enabled |
| Sample Size | Maximum rows for statistical profiling | 10,000 |
| Scan Depth | Maximum relationship traversal depth | 3 levels |

### Discovery Audit Trail

| Event | Logged Data | Retention |
|:------|:------------|:----------|
| Scan Initiated | Source, initiator, scope configuration | 1 year |
| Asset Discovered | Asset type, location, classification | 1 year |
| Schema Change Detected | Old/new schema, change type | 2 years |
| Scan Completed | Duration, assets discovered, errors | 1 year |
| Scan Failed | Error details, partial results | 1 year |

---

## Active Metadata

The Active Metadata system provides continuous metadata analysis, enrichment, and intelligence.

### Active Metadata Capabilities

| Capability             | Description                        |
| :--------------------- | :--------------------------------- |
| Change Detection       | Monitors schema and data changes   |
| Auto-Classification    | ML-based sensitive data detection  |
| Relationship Discovery | Identifies entity relationships    |
| Quality Monitoring     | Continuous data quality assessment |
| Usage Analytics        | Tracks metadata access patterns    |

### Automated Classification

**Classification Categories:**

| Category | Patterns Detected | Handling |
|:---------|:------------------|:---------|
| PII | Names, addresses, SSN, phone, email | Restricted access, masking |
| Legal Privileged | Matter IDs, attorney-client markers | Highly restricted |
| Financial | Account numbers, billing data | Confidential, encryption |
| Health | Medical records, diagnoses | Restricted, HIPAA controls |
| Custom | Organization-defined patterns | Configurable handling |

**Classification Security:**

| Control | Implementation |
|:--------|:---------------|
| ML Model Security | Models trained on synthetic data only |
| Classification Audit | All classification decisions logged |
| Override Controls | Manual classification with approval workflow |
| Propagation | Classifications propagate through lineage |

### Lineage Tracking
![Discovery Service](./images/Pasted%20image%2020260128180815.png)

| Lineage Type | Description | Security Use |
|:-------------|:------------|:-------------|
| Technical Lineage | Data flow through systems | Impact analysis |
| Business Lineage | Business process relationships | Compliance mapping |
| Column Lineage | Field-level transformations | Sensitive data tracking |
| Operational Lineage | Runtime execution paths | Audit trail |

**Lineage Security Controls:**

| Control | Description |
|:--------|:------------|
| Immutable History | Lineage records cannot be modified |
| Access Inheritance | Downstream inherits upstream restrictions |
| Impact Analysis | Identify affected assets on changes |
| Compliance Evidence | Lineage serves as audit evidence |

---

## Persistent Knowledge Graph

The Persistent Knowledge Graph (PKG) serves as "corporate memory," storing all information extracted from connected sources according to defined schemas. Unlike transient query results, the PKG maintains a durable, indexed knowledge base that accumulates insights over time.

### Knowledge Tree Structure

The PKG organizes knowledge in a hierarchical structure that enables both detailed and global context retrieval:

| Level | Content | Purpose |
|:------|:--------|:--------|
| Level 1 | Attributes | Entity property information (names, dates, values) |
| Level 2 | Relations | Entity-entity relationship triples |
| Level 3 | Keywords | Semantic keyword indexing for search |
| Level 4 | Communities | Hierarchical clustering for global context |

### Schema-Bounded Extraction

Entity extraction is constrained through seed schemas that define targeted extraction:

| Schema Component | Description | Example |
|:-----------------|:------------|:--------|
| Entity Types (E_types) | Allowed entity categories | Person, Organization, Contract |
| Relation Types (R_types) | Allowed relationship types | OWNS, REPRESENTS, SIGNED |
| Attribute Types (A_types) | Allowed entity attributes | Name, Date, Amount, Jurisdiction |

**Benefits of Schema-Bounded Extraction:**

| Benefit | Description |
|:--------|:------------|
| Hallucination Prevention | System cannot invent entities outside schema |
| Focused Extraction | Only relevant information captured |
| Consistency | Uniform entity structure across sources |
| Validation | All extractions validated against schema |

### Source Provenance Model

Each entity and relationship maintains complete provenance linking back to source documents:

| Provenance Element | Description |
|:-------------------|:------------|
| Connector ID | Source system connector reference |
| Document Reference | Document ID, title, and URL |
| Precise Location | Page, paragraph, character offset, or cell range |
| Extracted Text | Exact text from which entity was derived |
| Confidence Score | Extraction confidence level (0-1) |
| Extraction Timestamp | When the extraction occurred |

### Incremental Updates

| Capability | Description |
|:-----------|:------------|
| Change Detection | Detect modified documents on each sync |
| Differential Processing | Only process changed content |
| Entity Merging | Merge updated information with existing entities |
| Conflict Resolution | Handle conflicting information with rules |
| Version Tracking | Maintain history of entity changes |

---

## Search Sessions

Search Sessions provide an interactive exploration context where users ask questions and accumulate discoveries across multiple query turns.

### Session Architecture

```
┌─────────────────────────────────────────────────────────────────────────┐
│                       SEARCH SESSION MODEL                               │
├─────────────────────────────────────────────────────────────────────────┤
│                                                                         │
│  ┌───────────────────┐     ┌───────────────────────────────────────┐    │
│  │   Project         │────▶│     Persistent Knowledge Graph        │    │
│  │   Configuration   │     │     (Corporate Memory)                │    │
│  └───────────────────┘     └───────────────────────────────────────┘    │
│           │                              │                              │
│           ▼                              ▼                              │
│  ┌───────────────────┐     ┌───────────────────────────────────────┐    │
│  │   Search Session  │────▶│     Session Graph                     │    │
│  │   (User Context)  │     │     (Accumulated Discoveries)         │    │
│  └───────────────────┘     └───────────────────────────────────────┘    │
│           │                              │                              │
│           ▼                              ▼                              │
│  ┌───────────────────┐     ┌───────────────────────────────────────┐    │
│  │   Query Turns     │────▶│     Results with Provenance           │    │
│  │   (NL Queries)    │     │     (Sources, Reasoning Chain)        │    │
│  └───────────────────┘     └───────────────────────────────────────┘    │
│                                                                         │
└─────────────────────────────────────────────────────────────────────────┘
```

### Session Graph Accumulation

The Session Graph builds cumulatively across queries, providing context-aware exploration:

| Feature | Description |
|:--------|:------------|
| Cumulative Discovery | Entities discovered in earlier queries available in later ones |
| Context Preservation | Session maintains full context of exploration path |
| Relationship Building | New queries can reference previously discovered entities |
| History Tracking | All queries and findings preserved in session history |

### Query Turn Processing

| Stage | Description | Security Control |
|:------|:------------|:-----------------|
| Query Input | Accept natural language query | Input sanitization |
| Context Assembly | Combine session context with PKG | Permission filtering |
| Reasoning Chain | Generate step-by-step reasoning | Audit logging |
| Subgraph Retrieval | Extract relevant portion of PKG | Access control enforcement |
| Source Display | Show document references | Provenance verification |
| Session Update | Add discoveries to session graph | Session isolation |

---

## Data Observability

The Knowledge Fabric integrates data observability capabilities to monitor data health, quality, and pipeline performance.
![Active Metadata](./images/Pasted%20image%2020260128180925.png)
### Observability Integration

| Capability | Description | Purpose |
|:-----------|:------------|:--------|
| Test Outcomes in Lineage | Quality test results displayed on lineage | Identify issues in data flow |
| Freshness Monitoring | Track data currency and staleness | Ensure data timeliness |
| Quality Alerts | Automated notifications on test failures | Proactive issue detection |
| Pipeline Health | Monitor extraction and sync pipelines | Operational visibility |

### Data Quality Metrics

| Metric | Description | Tracking |
|:-------|:------------|:---------|
| Completeness | Percentage of non-null values | Per-field, per-source |
| Uniqueness | Duplicate detection rate | Per-entity type |
| Validity | Conformance to schema constraints | Per-field validation |
| Consistency | Cross-source agreement | Entity resolution metrics |
| Timeliness | Data freshness indicators | Last sync, staleness alerts |

### Quality Test Integration

| Test Type | Description |
|:----------|:------------|
| Schema Tests | Validate data structure conformance |
| Relationship Tests | Verify relationship integrity |
| Business Rule Tests | Apply domain-specific validation |
| Anomaly Detection | Statistical outlier identification |
| Freshness Tests | Data currency validation |

### Observability Alerts

| Alert Type | Trigger | Response |
|:-----------|:--------|:---------|
| Quality Failure | Test fails below threshold | Notification to data owners |
| Pipeline Error | Sync or extraction failure | Operations alert |
| Freshness Warning | Data exceeds staleness threshold | Reprocess or escalate |
| Drift Detection | Schema or pattern changes | Review and validate |

---

## Data Insights and KPIs

The Knowledge Fabric provides analytics and reporting to track data governance health.

### Key Performance Indicators

| KPI | Description | Target |
|:----|:------------|:-------|
| Documentation Coverage | Percentage of entities with descriptions | 80%+ |
| Ownership Assignment | Percentage of assets with owners | 95%+ |
| Classification Coverage | Percentage of fields classified | 90%+ |
| Lineage Completeness | Percentage of assets with full lineage | 85%+ |
| Data Quality Score | Aggregate quality across sources | 90%+ |

### Platform Analytics

| Report | Description |
|:-------|:------------|
| Asset Inventory | Total entities, relationships, sources |
| Usage Patterns | Most accessed entities and queries |
| Quality Trends | Quality metrics over time |
| Governance Compliance | Policy adherence and exceptions |
| Discovery Activity | New entities and relationships found |

---

## Graph Database Security

### Query Security

| Control | Description |
|:--------|:------------|
| Input Validation | Query parameters validated and sanitized |
| Injection Prevention | Parameterized queries, no string concatenation |
| Rate Limiting | Per-user query rate limits |
| Resource Limits | Query timeout and memory limits |

---

## Monitoring

The Monitoring system provides comprehensive observability across the Knowledge Fabric.

### Health Monitoring

| Component | Health Checks | Frequency |
|:----------|:--------------|:----------|
| API Services | Endpoint availability, response time | 30 seconds |
| Database | Connection pool, query latency | 1 minute |
| Connectors | Source connectivity status | 5 minutes |
| Background Jobs | Job completion, queue depth | 1 minute |

### Performance Monitoring

| Metric | Description | Alert Threshold |
|:-------|:------------|:----------------|
| API Latency (P95) | 95th percentile response time | > 2 seconds |
| Query Latency | Graph query execution time | > 5 seconds |
| Discovery Duration | Time to complete scan | > configured window |
| Error Rate | Failed requests percentage | > 1% |

### Security Monitoring

| Monitor | Detection | Response |
|:--------|:----------|:---------|
| Authentication Failures | Multiple failed login attempts | Account lockout, alert |
| Anomalous Access | Unusual data access patterns | Alert, investigation |
| Credential Usage | Unexpected credential access | Alert, audit review |
| Configuration Changes | Security setting modifications | Audit, approval verification |

**Security Alert Categories:**

| Category | Examples                                        | Response SLA |
| :------- | :---------------------------------------------- | :----------- |
| Critical | Breach indicators, data exfiltration            | 15 minutes   |
| High     | Multiple auth failures, privilege escalation    | 1 hour       |
| Medium   | Policy violations, configuration drift          | 4 hours      |
| Low      | Certificate expiration, best practice deviation | 24 hours     |

### SIEM Integration

| Integration Method | Format | Use Case |
|:-------------------|:-------|:---------|
| Syslog | CEF, RFC 5424 | Traditional SIEM |
| Webhook | JSON | Cloud-native SIEM |
| API Pull | REST/JSON | Custom integration |
| Event Stream | Kafka | High-volume environments |

---

## Authentication and Access Control

![Search Sessions](./images/Pasted%20image%2020260128181119.png)

### Authentication Mechanisms

| Method            | Use Case                          | Security Properties             |
| :---------------- | :-------------------------------- | :------------------------------ |
| OAuth 2.0 + OIDC  | User authentication               | Federated identity, token-based |
| API Keys          | Machine-to-machine communication  | Scoped permissions, rotatable   |
| Mutual TLS (mTLS) | Service-to-service authentication | Certificate-based verification  |
| SAML 2.0          | Enterprise SSO integration        | Federated identity              |

### Session Management

| Parameter | Value | Rationale |
|:----------|:------|:----------|
| Access Token Lifetime | 15 minutes | Limits exposure window |
| Refresh Token Lifetime | 8 hours | Balances security with usability |
| Idle Timeout | 30 minutes | Prevents abandoned session exploitation |
| Absolute Timeout | 24 hours | Forces re-authentication |

### Authorization Model

**Role-Based Access Control (RBAC):**

| Role | Permissions | Typical Assignment |
|:-----|:------------|:-------------------|
| Viewer | Read catalog, search, view lineage | Business analysts |
| Contributor | Viewer + add descriptions, tags | Data stewards |
| Editor | Contributor + modify classifications | Data engineers |
| Admin | Full access including governance policies | Platform administrators |
| Auditor | Read-only access to all data including audit logs | Compliance officers |

---

## Credential Management

### Source System Credentials

| Control | Description |
|:--------|:------------|
| Encrypted Storage | AES-256 with HSM-backed key management |
| Just-in-Time Access | Credentials retrieved only at connection time |
| Scoped Retrieval | Only authorized connectors access specific credentials |
| Audit Trail | All credential access logged with requester identity |
| Separation of Duties | Different roles for creation, modification, and usage |

### Supported Credential Types

| Type | Storage Method | Rotation Support |
|:-----|:---------------|:-----------------|
| Username/Password | Encrypted vault | Manual or automated |
| API Keys | Encrypted vault | Automated |
| OAuth Tokens | Encrypted vault with refresh | Automatic refresh |
| Certificates | Certificate store | Automated with CA integration |

---

## Data Protection

### Data Classification Framework

| Level | Description | Handling Requirements |
|:------|:------------|:----------------------|
| Public | Non-sensitive data | Standard controls |
| Internal | Business confidential | Authentication required |
| Confidential | Sensitive business data | Encryption, access logging |
| Restricted | PII, privileged legal data | Enhanced encryption, masking |
| Highly Restricted | Credentials, privileged matter data | HSM encryption, privileged access |

### Data Masking

| Technique | Use Case |
|:----------|:---------|
| Full Masking | Highly sensitive fields |
| Partial Masking | Identification fields |
| Format Preserving | Testing scenarios |
| Tokenization | Cross-system correlation |

---

## Audit Logging

### Logged Events

| Event Category | Logged Data | Retention |
|:---------------|:------------|:----------|
| Authentication | User ID, timestamp, IP, result | 1 year |
| Authorization | Subject, resource, action, decision | 1 year |
| Data Access | User ID, asset ID, fields accessed | 1 year |
| Configuration Changes | Setting, old/new value, changed by | 2 years |
| Credential Access | Credential ID, accessor, purpose | 2 years |
| Discovery Events | Scan scope, results, errors | 1 year |
| Connectivity Events | Connection attempts, status, duration | 1 year |
| Entity Resolution | Match decisions, merge events, source attribution | 2 years |
| External Enrichment | Source queried, entity enriched, data fused | 1 year |

### Log Security

| Control | Implementation |
|:--------|:---------------|
| Integrity | Cryptographic hash chain prevents tampering |
| Confidentiality | Logs encrypted at rest |
| Access Control | Auditor role required; no delete capability |
| Retention | Configurable per regulation (default 1 year) |

---
