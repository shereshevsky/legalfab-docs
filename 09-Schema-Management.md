# LegalFab Schema Management & Business Domain Discovery

**Version:** 1.0
**Last Updated:** January 2026

---

## Component Overview

The Schema Management system provides a unified approach to defining, discovering, and managing business domain schemas across the LegalFab platform. It enables users to describe their business domain through document analysis and creates structured schemas that control data extraction, agent behavior, and integration patterns.

**Core Capabilities:**

| Capability | Description | Usage Context |
|:-----------|:------------|:--------------|
| Business Domain Discovery | Extract domain concepts from user documents | Studio onboarding |
| Schema Definition | Create and manage structured data schemas | Platform-wide |
| Document-to-Schema | AI-powered schema extraction from documents | Studio, Knowledge Fabric |
| Schema Versioning | Track schema evolution with full history | Governance |
| Schema Binding | Link schemas to agents, extractors, and MCPs | Execution |
| Schema Validation | Ensure data conformance to defined schemas | Data quality |

---

## Architecture Overview

```
┌─────────────────────────────────────────────────────────────────────────┐
│                    SCHEMA MANAGEMENT ARCHITECTURE                       │
├─────────────────────────────────────────────────────────────────────────┤
│                                                                         │
│  ┌────────────────────────────────────────────────────────────────────┐ │
│  │                    SCHEMA DISCOVERY LAYER                          │ │
│  │  ┌──────────────────┐  ┌──────────────────┐  ┌─────────────────┐   │ │
│  │  │  Document        │  │  Domain Concept  │  │  Schema         │   │ │
│  │  │  Analyzer        │  │  Extractor       │  │  Generator      │   │ │
│  │  └──────────────────┘  └──────────────────┘  └─────────────────┘   │ │
│  └────────────────────────────────────────────────────────────────────┘ │
│                              │                                          │
│  ┌────────────────────────────────────────────────────────────────────┐ │
│  │                    SCHEMA REGISTRY                                 │ │
│  │  ┌──────────────────┐  ┌──────────────────┐  ┌─────────────────┐   │ │
│  │  │  Schema Store    │  │  Version         │  │  Dependency     │   │ │
│  │  │                  │  │  Control         │  │  Manager        │   │ │
│  │  └──────────────────┘  └──────────────────┘  └─────────────────┘   │ │
│  └────────────────────────────────────────────────────────────────────┘ │
│                              │                                          │
│  ┌────────────────────────────────────────────────────────────────────┐ │
│  │                    SCHEMA CONSUMERS                                │ │
│  │  ┌───────────┐  ┌───────────┐  ┌───────────┐  ┌─────────────────┐  │ │
│  │  │  Studio   │  │  OSINT    │  │  Agent    │  │  MCP            │  │ │
│  │  │  Agents   │  │ Extractors│  │  Logic    │  │  Connectors     │  │ │
│  │  └───────────┘  └───────────┘  └───────────┘  └─────────────────┘  │ │
│  └────────────────────────────────────────────────────────────────────┘ │
│                              │                                          │
│  ┌────────────────────────────────────────────────────────────────────┐ │
│  │                    VALIDATION & GOVERNANCE                         │ │
│  │  ┌──────────────────┐  ┌──────────────────┐  ┌─────────────────┐   │ │
│  │  │  Schema          │  │  Compliance      │  │  Audit          │   │ │
│  │  │  Validator       │  │  Checker         │  │  Logger         │   │ │
│  │  └──────────────────┘  └──────────────────┘  └─────────────────┘   │ │
│  └────────────────────────────────────────────────────────────────────┘ │
└─────────────────────────────────────────────────────────────────────────┘
```

---

## Business Domain Discovery

The Business Domain Discovery feature enables users to describe their domain by providing documents, from which the system extracts relevant concepts and generates structured schemas.

### Discovery Flow

```
┌─────────────────────────────────────────────────────────────────────────┐
│                    BUSINESS DOMAIN DISCOVERY                            │
├─────────────────────────────────────────────────────────────────────────┤
│                                                                         │
│  ┌─────────────────┐                                                    │
│  │  User Documents │  Policies, procedures, contracts, forms,           │
│  │  (Input)        │  data dictionaries, specifications                 │
│  └────────┬────────┘                                                    │
│           │                                                             │
│           ▼                                                             │
│  ┌─────────────────┐                                                    │
│  │  Document       │  Extract text, structure, and metadata:            │
│  │  Analysis       │  • Document type classification                    │
│  │                 │  • Section identification                          │
│  │                 │  • Table and list extraction                       │
│  └────────┬────────┘                                                    │
│           │                                                             │
│           ▼                                                             │
│  ┌─────────────────┐                                                    │
│  │  Concept        │  Identify domain concepts:                         │
│  │  Extraction     │  • Entities (Person, Organization, Matter)         │
│  │                 │  • Attributes (name, date, amount)                 │
│  │                 │  • Relationships (owns, represents, related_to)    │
│  └────────┬────────┘                                                    │
│           │                                                             │
│           ▼                                                             │
│  ┌─────────────────┐                                                    │
│  │  Schema         │  Generate structured schemas:                      │
│  │  Generation     │  • Entity definitions                              │
│  │                 │  • Attribute types and constraints                 │
│  │                 │  • Relationship mappings                           │
│  └────────┬────────┘                                                    │
│           │                                                             │
│           ▼                                                             │
│  ┌─────────────────┐                                                    │
│  │  User Review    │  Interactive refinement:                           │
│  │  & Refinement   │  • Approve/reject concepts                         │
│  │                 │  • Modify attributes and types                     │
│  │                 │  • Add missing elements                            │
│  └────────-────────┘                                                    │
│                                                                         │
└─────────────────────────────────────────────────────────────────────────┘
```

### Supported Document Types

| Document Type | Extraction Focus | Example Concepts |
|:--------------|:-----------------|:-----------------|
| Policies & Procedures | Workflows, rules, roles | Process steps, approval levels, responsibilities |
| Contracts & Agreements | Parties, terms, obligations | Party types, clause types, obligation categories |
| Data Dictionaries | Field definitions, types | Attribute names, data types, validation rules |
| Forms & Templates | Input fields, validations | Field names, required vs optional, formats |
| Organizational Charts | Hierarchy, departments | Role types, reporting relationships |
| Regulatory Documents | Requirements, controls | Compliance entities, control types |

### Concept Extraction

The system uses AI-powered extraction to identify domain concepts from documents.

**Extraction Capabilities:**

| Capability | Description |
|:-----------|:------------|
| Entity Recognition | Identify business entities (Client, Matter, Document, etc.) |
| Attribute Discovery | Extract attributes and their data types |
| Relationship Mapping | Identify relationships between entities |
| Constraint Detection | Discover validation rules and constraints |
| Enumeration Extraction | Identify fixed value sets (status codes, categories) |
| Hierarchy Detection | Recognize parent-child and classification structures |

**Extraction Security:**

| Control | Implementation |
|:--------|:---------------|
| Document Isolation | Each user's documents processed in isolation |
| PII Detection | Sensitive data identified and flagged |
| Content Filtering | Inappropriate content filtered before processing |
| Audit Trail | All extraction activities logged |

---

## Schema Definition

Schemas provide structured definitions for business domain concepts used across the platform.

### Schema Structure

| Component | Description | Purpose |
|:----------|:------------|:--------|
| Schema Metadata | Name, version, description, owner | Identification and governance |
| Entities | Business object definitions | Core domain concepts |
| Attributes | Entity properties with types | Data structure |
| Relationships | Connections between entities | Domain model |
| Constraints | Validation rules and restrictions | Data quality |
| Enumerations | Fixed value sets | Controlled vocabularies |

### Entity Definition

| Element | Description |
|:--------|:------------|
| Entity ID | Unique identifier |
| Name | Human-readable name |
| Description | Purpose and usage |
| Attributes | List of entity properties |
| Primary Key | Unique identifier attribute(s) |
| Inheritance | Parent entity (if applicable) |

### Attribute Types

| Type | Description | Examples |
|:-----|:------------|:---------|
| String | Text values | Name, description, notes |
| Number | Numeric values | Amount, quantity, score |
| Boolean | True/false values | Active, verified, approved |
| Date | Date values | Created date, due date |
| DateTime | Date and time values | Timestamp, scheduled time |
| Enum | Fixed value set | Status, category, type |
| Reference | Link to another entity | Client ID, matter reference |
| Array | List of values | Tags, categories |
| Object | Nested structure | Address, contact details |

### Constraint Types

| Constraint | Description | Example |
|:-----------|:------------|:--------|
| Required | Field must have a value | Client name is required |
| Unique | Value must be unique | Email must be unique |
| Format | Value must match pattern | Phone format validation |
| Range | Numeric bounds | Amount between 0 and 1M |
| Length | String length limits | Description max 500 chars |
| Enumeration | Value from fixed set | Status in [Active, Closed] |
| Reference | Valid entity reference | Client must exist |
| Custom | User-defined validation | Business rule validation |

---

## Schema Registry

The Schema Registry provides centralized storage, versioning, and access control for all schemas.

### Registry Capabilities

| Capability | Description |
|:-----------|:------------|
| Schema Storage | Persistent storage of schema definitions |
| Version Control | Full version history with diff tracking |
| Dependency Tracking | Track schema dependencies and consumers |
| Access Control | Role-based schema access |
| Search & Discovery | Find schemas by name, attribute, or content |
| Export/Import | Schema portability across environments |

### Version Management

| Operation | Description | Use Case |
|:----------|:------------|:---------|
| Create | Initial schema version | New domain concept |
| Update | Create new version with changes | Schema evolution |
| Deprecate | Mark version as deprecated | Migration preparation |
| Archive | Remove from active use | End of life |
| Rollback | Restore previous version | Error recovery |

**Version Compatibility:**

| Compatibility | Description | Impact |
|:--------------|:------------|:-------|
| Backward Compatible | New version accepts old data | Safe upgrade |
| Forward Compatible | Old version accepts new data | Flexible consumers |
| Breaking Change | Incompatible changes | Migration required |

### Schema Dependencies

| Dependency Type | Description |
|:----------------|:------------|
| Entity Reference | Schema references entity from another schema |
| Inheritance | Schema extends another schema |
| Composition | Schema includes elements from another schema |
| Consumer | Agent, extractor, or MCP using the schema |

---

## Schema Usage

### Studio Integration

Schemas control data processing in Studio agents and pipelines.

**Agent Schema Binding:**

| Binding Type | Description |
|:-------------|:------------|
| Input Schema | Defines expected input structure |
| Output Schema | Defines produced output structure |
| Internal Schema | Defines intermediate data structures |
| Validation Schema | Defines validation rules for agent data |

**Pipeline Schema Flow:**

```
┌─────────────────────────────────────────────────────────────────────────┐
│                    SCHEMA-DRIVEN PIPELINE                               │
├─────────────────────────────────────────────────────────────────────────┤
│                                                                         │
│  ┌───────────┐     ┌───────────┐     ┌───────────┐     ┌───────────┐    │
│  │  Input    │     │  Agent A  │     │  Agent B  │     │  Output   │    │
│  │  Data     │────▶│           │────▶│           │────▶│  Data     │    │
│  └───────────┘     └───────────┘     └───────────┘     └───────────┘    │
│       │                 │                 │                 │           │
│       ▼                 ▼                 ▼                 ▼           │
│  ┌───────────┐     ┌───────────┐     ┌───────────┐     ┌───────────┐    │
│  │  Input    │     │  Schema A │     │  Schema B │     │  Output   │    │
│  │  Schema   │     │  (I/O)    │     │  (I/O)    │     │  Schema   │    │
│  └───────────┘     └───────────┘     └───────────┘     └───────────┘    │
│                                                                         │
│  Schema validation occurs at each step boundary                         │
└─────────────────────────────────────────────────────────────────────────┘
```

### OSINT Extractor Integration

External data sources use schemas to structure extracted data.

**Extractor Schema Binding:**

| Component | Description |
|:----------|:------------|
| Source Mapping | Map external data fields to schema attributes |
| Transformation Rules | Convert external formats to schema types |
| Validation Rules | Validate extracted data against schema constraints |
| Default Values | Apply defaults for missing fields |

**OSINT Schema Flow:**

| Stage | Description |
|:------|:------------|
| Raw Data | Unstructured data from external source |
| Field Mapping | Map external fields to schema attributes |
| Type Conversion | Convert to schema-defined types |
| Validation | Validate against schema constraints |
| Enrichment | Add computed or derived attributes |
| Output | Schema-conformant data for Knowledge Graph |

### MCP Connector Integration

MCP connectors use schemas to ensure data consistency across tool integrations.

**MCP Schema Capabilities:**

| Capability | Description |
|:-----------|:------------|
| Schema Provision | Provide schema to MCP tool for data extraction |
| Response Mapping | Map tool response to schema structure |
| Request Validation | Validate tool inputs against schema |
| Contract Enforcement | Ensure tool outputs match expected schema |

**MCP Schema Binding:**

```
┌─────────────────────────────────────────────────────────────────────────┐
│                    MCP SCHEMA INTEGRATION                               │
├─────────────────────────────────────────────────────────────────────────┤
│                                                                         │
│  ┌─────────────────┐                     ┌─────────────────┐            │
│  │  Agent Request  │                     │  External Tool  │            │
│  │  (Schema-bound) │────────────────────▶│  (MCP Server)   │            │
│  └─────────────────┘                     └────────┬────────┘            │
│           │                                       │                     │
│           │                                       │                     │
│           ▼                                       ▼                     │
│  ┌─────────────────┐                     ┌─────────────────┐            │
│  │  Request        │                     │  Response       │            │
│  │  Schema         │                     │  Data           │            │
│  │  Validation     │                     │                 │            │
│  └─────────────────┘                     └────────┬────────┘            │
│                                                   │                     │
│                                                   ▼                     │
│                                          ┌─────────────────┐            │
│                                          │  Response       │            │
│                                          │  Schema         │            │
│                                          │  Mapping        │            │
│                                          └────────┬────────┘            │
│                                                   │                     │
│                                                   ▼                     │
│                                          ┌─────────────────┐            │
│                                          │  Schema-        │            │
│                                          │  Conformant     │            │
│                                          │  Output         │            │
│                                          └─────────────────┘            │
└─────────────────────────────────────────────────────────────────────────┘
```

---

## Schema Validation

All data processed through the platform is validated against its bound schema.

### Validation Modes

| Mode | Description | Use Case |
|:-----|:------------|:---------|
| Strict | All constraints enforced, reject on failure | Production data |
| Lenient | Log warnings, accept partial compliance | Data migration |
| Report | Generate validation report without rejection | Data quality assessment |

### Validation Results

| Result | Description | Action |
|:-------|:------------|:-------|
| Valid | Data conforms to schema | Continue processing |
| Warning | Minor issues, data acceptable | Log and continue |
| Error | Schema violation, data rejected | Reject with details |
| Critical | Security or integrity concern | Reject and alert |

### Validation Security

| Control | Implementation |
|:--------|:---------------|
| Injection Prevention | Schema definitions sanitized before use |
| Type Safety | Strong typing prevents type confusion attacks |
| Constraint Enforcement | All constraints validated server-side |
| Audit Logging | All validation results logged |

---

## Security Controls

### Schema Access Control

| Permission | Description | Roles |
|:-----------|:------------|:------|
| schema.read | View schema definitions | All authenticated users |
| schema.create | Create new schemas | Schema designers, admins |
| schema.update | Modify existing schemas | Schema owners, admins |
| schema.delete | Remove schemas | Admins only |
| schema.publish | Publish schema versions | Schema owners, admins |
| schema.bind | Bind schemas to consumers | Agent developers, admins |

### Schema Governance

| Control | Implementation |
|:--------|:---------------|
| Ownership | Each schema has designated owner |
| Approval Workflow | Schema changes require approval |
| Impact Analysis | Changes analyzed for downstream impact |
| Change Notification | Consumers notified of schema changes |
| Deprecation Policy | Minimum notice period before removal |

### Schema Security

| Control | Implementation |
|:--------|:---------------|
| Integrity | Schema definitions cryptographically signed |
| Immutability | Published versions cannot be modified |
| Isolation | Tenant schemas isolated from each other |
| Encryption | Schemas encrypted at rest |

---

## Audit Logging

### Logged Events

| Event Category | Events | Retention |
|:---------------|:-------|:----------|
| Schema Lifecycle | Create, update, delete, publish, deprecate | 2 years |
| Schema Access | Read, export, clone | 1 year |
| Validation Events | Validation success, failure, warnings | 1 year |
| Binding Events | Bind, unbind, consumer registration | 2 years |
| Discovery Events | Document analysis, concept extraction | 1 year |

### Audit Trail Security

| Control | Implementation |
|:--------|:---------------|
| Integrity | Tamper-evident logging |
| Completeness | All schema operations logged |
| Confidentiality | Logs encrypted at rest |
| Access Control | Auditor role required for log access |

---
