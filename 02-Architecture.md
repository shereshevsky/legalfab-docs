# LegalFab System Architecture

**Version:** 1.3
**Last Updated:** January 2026

---

## Platform Overview

LegalFab is an AI-powered legal technology platform built on a metadata-driven architecture. The platform provides unified access to distributed data assets, intelligent automation through AI agents, and compliance capabilities for regulated legal practices.

### Platform Components

| Component | Purpose | Key Capabilities |
|:----------|:--------|:-----------------|
| Knowledge Fabric | Data integration and intelligence layer | Knowledge Graph, Entity Resolution, Connectivity, Discovery, Lineage |
| Studio | Creation and execution environment | Agent Builder, Chain of Agents, Workflow Designer, Testing Framework |
| Schema Management | Business domain definition and control | Domain Discovery, Schema Registry, Schema Validation |
| AI & LLM Layer | Intelligent processing and inference | LightLLM Gateway, Provider Abstraction, Prompt Management |
| AML Compliance | Regulatory compliance module | Rule Engine, BPM Workflows, Screening, Case Management |
| DevOps Infrastructure | Deployment and operations | CI/CD Pipelines, Monitoring, Security Operations |

---

## Architecture Overview

```
┌─────────────────────────────────────────────────────────────────────────┐
│                        PRESENTATION LAYER                               │
│  ┌──────────────┐  ┌──────────────┐  ┌──────────────────────────────┐   │
│  │   Web UI     │  │  API Gateway │  │  Platform Integration APIs   │   │
│  │              │  │  (REST)      │  │                              │   │
│  └──────────────┘  └──────────────┘  └──────────────────────────────┘   │
│                              │                                          │
│                   [Authentication, Rate Limiting, Input Validation]     │
├─────────────────────────────────────────────────────────────────────────┤
│                          APPLICATION LAYER                              │
│                                                                         │
│  ┌─────────────────────────────────────────────────────────────────┐    │
│  │                          STUDIO                                 │    │
│  │  ┌───────────┐  ┌───────────────┐  ┌──────────────────────┐     │    │
│  │  │  Agent    │  │  Chain of     │  │  Workflow Designer   │     │    │
│  │  │  Builder  │  │  Agents       │  │                      │     │    │
│  │  └───────────┘  └───────────────┘  └──────────────────────┘     │    │
│  └─────────────────────────────────────────────────────────────────┘    │
│                                                                         │
│  ┌─────────────────────────────────────────────────────────────────┐    │
│  │                     AML COMPLIANCE MODULE                       │    │
│  │  ┌───────────┐  ┌───────────────┐  ┌───────────┐  ┌──────────┐  │    │
│  │  │   Rule    │  │  BPM          │  │ Screening │  │  Case    │  │    │
│  │  │  Engine   │  │  Workflows    │  │  Service  │  │ Manager  │  │    │
│  │  └───────────┘  └───────────────┘  └───────────┘  └──────────┘  │    │
│  └─────────────────────────────────────────────────────────────────┘    │
│                                                                         │
│  ┌──────────┐ ┌──────────┐ ┌──────────┐ ┌────────────┐ ┌────────────┐   │
│  │  Search  │ │ Lineage  │ │ Quality  │ │ Discovery  │ │ Governance │   │
│  │ Service  │ │ Service  │ │ Service  │ │  Service   │ │  Service   │   │
│  └──────────┘ └──────────┘ └──────────┘ └────────────┘ └────────────┘   │
│                              │                                          │
│                   [Service-to-Service AuthN/AuthZ, mTLS]                │
├─────────────────────────────────────────────────────────────────────────┤
│                      KNOWLEDGE FABRIC LAYER                             │
│                                                                         │
│  ┌─────────────────────────────────────────────────────────────────┐    │
│  │                    KNOWLEDGE GRAPH                              │    │
│  │  ┌──────────────┐  ┌──────────────────┐  ┌──────────────────┐   │    │
│  │  │ Entity Store │  │ Relationship     │  │  Query Engine    │   │    │
│  │  │   (Nodes)    │  │ Store (Edges)    │  │  (Traversal)     │   │    │
│  │  └──────────────┘  └──────────────────┘  └──────────────────┘   │    │
│  └─────────────────────────────────────────────────────────────────┘    │
│                                                                         │
│  ┌─────────────────────────────────────────────────────────────────┐    │
│  │                  ENTITY RESOLUTION ENGINE                       │    │
│  │  ┌───────────┐  ┌───────────┐  ┌───────────┐  ┌─────────────┐   │    │
│  │  │ Blocking  │  │ Matching  │  │ Clustering│  │ Golden      │   │    │
│  │  │ Service   │  │ Service   │  │ Service   │  │ Record Mgmt │   │    │
│  │  └───────────┘  └───────────┘  └───────────┘  └─────────────┘   │    │
│  └─────────────────────────────────────────────────────────────────┘    │
│                              │                                          │
│                   [Encryption at Rest, Access Control Lists]            │
├─────────────────────────────────────────────────────────────────────────┤
│                        AI & LLM LAYER                                   │
│  ┌─────────────────────────────────────────────────────────────────┐    │
│  │  ┌────────────┐  ┌──────────────┐  ┌────────────────────────┐   │    │
│  │  │  LightLLM  │  │   Provider   │  │  Prompt Management     │   │    │
│  │  │  Gateway   │  │  Abstraction │  │  & Template Engine     │   │    │
│  │  └────────────┘  └──────────────┘  └────────────────────────┘   │    │
│  └─────────────────────────────────────────────────────────────────┘    │
│                              │                                          │
│                   [Input Filtering, Output Validation, PII Detection]   │
├─────────────────────────────────────────────────────────────────────────┤
│                       CONNECTIVITY LAYER                                │
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

---

## Knowledge Fabric

The Knowledge Fabric serves as the foundational data integration and intelligence layer for the LegalFab platform.

### Core Capabilities

| Capability | Description |
|:-----------|:------------|
| Knowledge Graph | Graph-native storage for entities and relationships with traversal queries |
| Entity Resolution | Cross-source entity matching using blocking, matching, and clustering algorithms |
| Connectivity | Direct database connections, API integrations, and MCP protocol connectors |
| Discovery Service | Automated identification and cataloging of data assets |
| Active Metadata | Continuous metadata analysis, profiling, and enrichment |
| Data Lineage | End-to-end tracking of data flow from source to consumption |
| External Sources | Integration with OSINT, corporate registries, and third-party data providers |

### Knowledge Graph Model

The Knowledge Graph stores entities as nodes and relationships as edges, enabling complex traversal queries and network analysis.

**Entity Types:**

| Entity | Description | Use Cases |
|:-------|:------------|:----------|
| Person | Individual clients, contacts, beneficial owners | KYC, risk assessment, relationship mapping |
| Organization | Corporate clients, counterparties, related entities | Corporate structure, ownership analysis |
| Matter | Legal matters, cases, engagements | Matter management, conflict checking |
| Document | Contracts, filings, correspondence | Document management, search |
| Address | Physical and registered addresses | Location analysis, verification |
| Identifier | Tax IDs, registration numbers, LEIs | Cross-reference, verification |

**Relationship Types:**

| Relationship | Description |
|:-------------|:------------|
| OWNS | Ownership stake between entities |
| CONTROLS | Control relationship (voting, management) |
| RELATED_TO | Personal or business relationship |
| EMPLOYS | Employment relationship |
| REPRESENTS | Legal representation relationship |
| LOCATED_AT | Entity-address relationship |

### Entity Resolution

The Entity Resolution Engine identifies duplicate and related records across connected sources to build unified entity profiles (Golden Records).

**Resolution Pipeline:**

```
Source Records → Blocking → Candidate Pairs → Matching → Clusters → Golden Records
                    │             │              │           │
              (Key generation) (Comparison)  (Scoring)  (Merge rules)
```

---

## Studio

The Studio provides the creation and execution environment for AI agents and workflows.

### Core Capabilities

| Capability | Description |
|:-----------|:------------|
| Text-to-Pipeline | Natural language pipeline generation with DSL output and iterative refinement |
| Agent Builder | Create AI agents with defined inputs, outputs, and behaviors |
| Chain of Agents | Orchestrate multiple agents in sequential or parallel patterns |
| Workflow Designer | Visual workflow builder with conditional logic and branching |
| Testing Framework | Test agents and workflows in sandboxed environments |
| MCP Tool Integrator | Connect agents to external tools via Model Context Protocol |

### Text-to-Pipeline

Users describe desired workflows in natural language, and the system generates a structured DSL representation:

| Stage | Description |
|:------|:------------|
| Intent Analysis | Parse natural language to identify data sources, operations, and conditions |
| DSL Generation | Generate structured pipeline definition with steps and dependencies |
| Validation | Verify permissions, tool availability, and type compatibility |
| Visual Preview | Display interactive flow diagram with step details |
| Refinement | Iterate using natural language commands to modify the pipeline |
| Execution | Run immediately, schedule, or save as reusable template |

### Agent Architecture

Agents are the fundamental execution unit in Studio. Each agent has:

| Component | Description |
|:----------|:------------|
| Definition | Name, version, description, category |
| Inputs | Input parameters with schemas and validation rules |
| Workflow | Execution steps, tool calls, conditional logic |
| Outputs | Result definitions with transformation rules |
| Permissions | Required data access scopes and tool authorizations |

### Chain of Agents

Chains enable complex workflows by orchestrating multiple agents:

| Pattern | Description | Use Case |
|:--------|:------------|:---------|
| Sequential | Agents execute in order, passing results | Document review pipeline |
| Parallel | Agents execute concurrently | Multi-source research |
| Conditional | Agent selection based on runtime conditions | Risk-based routing |
| Loop | Repeated execution until condition met | Iterative refinement |

---

## Schema Management

The Schema Management system provides a unified approach to defining, discovering, and managing business domain schemas across the platform.

### Core Capabilities

| Capability | Description |
|:-----------|:------------|
| Business Domain Discovery | Extract domain concepts from user documents |
| Schema Registry | Centralized storage with versioning and access control |
| Schema Validation | Ensure data conformance across all platform components |
| Schema Binding | Link schemas to agents, extractors, and MCP connectors |

### Schema Usage Across Platform

| Component | Schema Role |
|:----------|:------------|
| Studio Agents | Input/output validation, data transformation control |
| OSINT Extractors | Structure external data according to domain model |
| MCP Connectors | Ensure data consistency across tool integrations |
| Knowledge Graph | Entity and relationship type definitions |
| Pipelines | Data flow validation between processing steps |

### Document-to-Schema Discovery

| Stage | Description |
|:------|:------------|
| Document Analysis | Extract text, structure, and metadata from user documents |
| Concept Extraction | Identify entities, attributes, and relationships |
| Schema Generation | Create structured schema definitions |
| User Refinement | Interactive review and modification |
| Publication | Register schema in central registry |

---

## AI & LLM Layer

The AI & LLM Layer provides intelligent processing capabilities through a provider-agnostic gateway.

### Core Capabilities

| Capability | Description |
|:-----------|:------------|
| LightLLM Gateway | Unified interface for multiple LLM providers |
| Provider Abstraction | Swap providers without code changes |
| Prompt Management | Template library with version control |
| Response Processing | Output parsing, validation, and transformation |

### Provider Support

| Provider Type | Examples | Integration |
|:--------------|:---------|:------------|
| Commercial APIs | OpenAI, Anthropic, Google | API key authentication |
| Self-Hosted | Llama, Mistral, custom models | Private endpoint |
| Enterprise | Azure OpenAI, AWS Bedrock | Cloud provider auth |

---

## AML Compliance Module

The AML Compliance module provides comprehensive capabilities for customer due diligence and regulatory compliance.

### Core Capabilities

| Capability | Description |
|:-----------|:------------|
| Rule Engine | Risk scoring and compliance decision rules |
| BPM Workflows | CDD, EDD, and investigation process orchestration |
| Screening Service | Sanctions, PEP, and adverse media checking |
| Case Management | Compliance case tracking and documentation |
| Reporting | Regulatory reporting and analytics |

### Risk Assessment

The Rule Engine calculates risk scores based on configurable factors:

| Risk Category | Factors |
|:--------------|:--------|
| Geographic | Country risk, jurisdiction, sanctions exposure |
| Industry | Sector risk, regulatory intensity |
| Product/Service | Complexity, cash intensity, cross-border |
| Customer Type | Individual, corporate, PEP status |
| Behavioral | Transaction patterns, anomalies |

### BPM Workflows

| Workflow | Purpose | Trigger |
|:---------|:--------|:--------|
| Client Onboarding | Initial CDD for new clients | Client intake |
| Periodic Review | Regular risk reassessment | Time-based |
| Triggered Review | Event-driven reassessment | Risk event |
| Investigation | Detailed inquiry process | Alert escalation |
| SAR Escalation | Suspicious activity reporting | Investigation finding |

---

## Network Architecture

### Network Segmentation

| Zone | Purpose | Components |
|:-----|:--------|:-----------|
| Edge/DMZ | External entry point | Load balancers, WAF, API Gateway |
| Application | Service execution | Studio, Services, AI Layer |
| Data | Persistent storage | Knowledge Graph, Document Store |
| Management | Operations | Monitoring, Logging, Admin tools |

### Connectivity Patterns

| Pattern | Description | Use Case |
|:--------|:------------|:---------|
| Direct TLS | Encrypted connection over internet | Cloud-hosted sources |
| VPN Tunnel | Site-to-site encrypted tunnel | On-premises sources |
| Private Link | Cloud provider private connectivity | Same-cloud sources |
| Agent-Based | Customer-deployed agent connects outbound | Air-gapped environments |

---

## Data Flow Model

LegalFab operates on a metadata-first principle. Source data remains in place while metadata flows through the platform.

| Data Type | Handling | Storage |
|:----------|:---------|:--------|
| Structural Metadata | Extracted and stored | Knowledge Graph |
| Statistical Profiles | Computed via aggregation | Knowledge Graph |
| Sample Data | Optional, user-controlled | Ephemeral cache |
| Query Results | Pass-through federation | Never persisted |
| Source Credentials | Encrypted storage | Secure Vault |

---

## Security Architecture

### Defense-in-Depth Model

```
┌─────────────────────────────────────────────────────────────────────┐
│                    PERIMETER SECURITY                               │
│    DDoS Protection │ WAF │ Rate Limiting │ Geographic Filtering     │
├─────────────────────────────────────────────────────────────────────┤
│                    NETWORK SECURITY                                 │
│    VPC Isolation │ Network Segmentation │ Private Endpoints         │
├─────────────────────────────────────────────────────────────────────┤
│                    APPLICATION SECURITY                             │
│    Input Validation │ Output Encoding │ CSRF Protection │ CSP       │
├─────────────────────────────────────────────────────────────────────┤
│                    IDENTITY & ACCESS                                │
│    OAuth 2.0/OIDC │ RBAC │ ABAC │ MFA │ Session Management          │
├─────────────────────────────────────────────────────────────────────┤
│                    DATA SECURITY                                    │
│    Encryption │ Tokenization │ Data Masking │ Classification        │
├─────────────────────────────────────────────────────────────────────┤
│                    INFRASTRUCTURE SECURITY                          │
│    Hardened Images │ Patch Management │ Container Security          │
└─────────────────────────────────────────────────────────────────────┘
```

### Cryptographic Standards

| Purpose | Algorithm | Key Length |
|:--------|:----------|:-----------|
| Data at Rest | AES-256-GCM | 256-bit |
| Data in Transit | TLS 1.3 | 256-bit |
| Key Encryption | RSA-OAEP | 2048-bit minimum |
| Digital Signatures | ECDSA | P-256 |
| Hashing | SHA-256 | N/A |

---

## Integration Points

### External System Integration

| System Type          | Integration Method       | Data Exchange                       |
| :------------------- | :----------------------- | :---------------------------------- |
| Practice Management  | API / Database connector | Matters, clients, time entries      |
| CRM Systems          | API / Webhook            | Contacts, organizations, activities |
| Document Management  | API / File system        | Documents, metadata                 |
| Billing Systems      | API / Database           | Invoices, payments, AR              |
| Corporate Registries | API                      | Company filings, ownership          |
| Screening Providers  | API                      | Sanctions, PEP, adverse media       |

### MCP Protocol

The Model Context Protocol (MCP) provides a standardized interface for tool integration:

| Component | Purpose |
|:----------|:--------|
| Tool Registry | Catalog of available tools and capabilities |
| Schema Definition | Input/output contracts for each tool |
| Authentication | Tool-specific credential management |
| Execution | Secure tool invocation with timeout handling |

---

## Deployment Models

LegalFab is available in multiple deployment configurations to meet varying security, compliance, and operational requirements.

### Deployment Options

| Model | Description | Use Case |
|:------|:------------|:---------|
| SaaS Multi-Tenant | Shared infrastructure, isolated data | Standard deployment, cost-effective |
| Dedicated Cloud Tenant | Dedicated infrastructure in LegalFab cloud | Enterprise, enhanced isolation |
| Customer Cloud | Deploy in customer's cloud tenant (AWS, Azure, GCP) | Data sovereignty, infrastructure control |
| On-Premises | Fully customer-managed within data centers | Maximum control, air-gapped environments |
| Hybrid | SaaS control plane, on-premises data plane | Balance of convenience and control |

### SaaS Multi-Tenant

| Aspect | Details |
|:-------|:--------|
| Infrastructure | Shared compute, isolated data stores |
| Data Isolation | Logical tenant isolation with encryption |
| Compliance | SOC 2, GDPR compliant infrastructure |
| Updates | Automatic platform updates |
| Best For | Standard requirements, rapid deployment |

### Dedicated Cloud Tenant

| Aspect | Details |
|:-------|:--------|
| Infrastructure | Dedicated resources within LegalFab cloud |
| Data Isolation | Physical separation of compute and storage |
| Compliance | Enhanced compliance posture |
| Updates | Coordinated update windows |
| Best For | Enterprise customers requiring dedicated resources |

### Customer Cloud Deployment

| Aspect | Details |
|:-------|:--------|
| Infrastructure | Customer's own cloud tenant (AWS, Azure, GCP) |
| Data Control | Customer maintains full infrastructure control |
| Region Selection | Deploy in preferred cloud region |
| Management | LegalFab manages application, customer manages infrastructure |
| Best For | Data sovereignty, existing cloud investments |

### On-Premises Deployment

| Aspect | Details |
|:-------|:--------|
| Infrastructure | Customer data centers |
| Data Control | Complete data custody |
| Network | Air-gapped capability available |
| Management | Customer-managed with LegalFab support |
| Best For | Strict regulatory requirements, maximum control |

### Data Residency Configuration

| Region Option | Data Location | LLM Processing |
|:--------------|:--------------|:---------------|
| UK-Only | UK data centers | UK-based providers or on-premises |
| EU-Only | EU data centers (Ireland common) | EU-based providers |
| US-Only | US data centers | US-based providers |
| Customer-Specified | Any supported region | Region-aligned providers |
| On-Premises | Customer data centers | Self-hosted models |

### LLM Provider Configuration by Deployment

| Deployment | LLM Options |
|:-----------|:------------|
| SaaS | Cloud providers (OpenAI, Anthropic, Google) |
| Dedicated Tenant | Cloud providers with dedicated keys |
| Customer Cloud | Cloud providers or self-hosted in customer cloud |
| On-Premises | Self-hosted models (Llama, Mistral) for complete data control |
| Hybrid | Cloud for non-sensitive, on-premises for sensitive |

### Deployment Feature Comparison

| Feature | SaaS | Dedicated | Customer Cloud | On-Premises |
|:--------|:-----|:----------|:---------------|:------------|
| Knowledge Fabric | ✓ | ✓ | ✓ | ✓ |
| Studio & Agents | ✓ | ✓ | ✓ | ✓ |
| Multi-Tenancy | ✓ | ✓ | ✓ | ✓ |
| LLM Integration | ✓ | ✓ | ✓ | ✓ |
| Custom Region | Limited | ✓ | ✓ | N/A |
| Air-Gap Support | ✗ | ✗ | ✗ | ✓ |
| Self-Hosted LLMs | ✗ | ✗ | ✓ | ✓ |

---

*For detailed security controls, see individual component documents: Knowledge Fabric, Studio, AI-LLM, and AML Compliance.*
