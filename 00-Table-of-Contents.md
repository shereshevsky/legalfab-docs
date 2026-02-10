---
layout: default
title: Table of Contents
---

# LegalFab Documentation - Table of Contents

**Version:** 1.6
**Last Updated:** February 2026

---

## Document Overview

| Document | Description | Version |
|:---------|:------------|:--------|
| [01-Introduction](./01-Introduction.md) | Platform overview and security summary | 1.2 |
| [02-Architecture](./02-Architecture.md) | System architecture and components | 1.4 |
| [03-Knowledge-Fabric](./03-Knowledge-Fabric.md) | Data integration and knowledge graph | 1.6 |
| [04-Studio](./04-Studio.md) | Agent creation and workflow design | 1.5 |
| [05-AI-LLM](./05-AI-LLM.md) | AI and LLM security architecture | 1.1 |
| [06-CI-CD](./06-CI-CD.md) | CI/CD pipeline security | 1.0 |
| [07-Security-Operations](./07-Security-Operations.md) | SOC, monitoring, and incident response | 1.0 |
| [08-AML-Compliance](./08-AML-Compliance.md) | AML rule engine, BPM workflows, screening | 1.0 |
| [09-Schema-Management](./09-Schema-Management.md) | Business domain discovery, schema registry | 1.0 |
| [10-System-Compliance](./10-System-Compliance.md) | Regulatory compliance and governance | 1.2 |
| [11-API-Security](./11-API-Security.md) | API gateway, authentication, rate limiting | 1.0 |
| [12-Dialog](./12-Dialog.md) | Conversational interface and NLU | 1.0 |
| [13-Operating-Costs](./13-Operating-Costs.md) | Self-hosted deployment operating costs | 1.0 |
| [14-Trust-Compliance](./14-Trust-Compliance.md) | Trust & Compliance for managed deployments | 1.0 |
| [15-Competitive-Analysis](./15-Competitive-Analysis.md) | Platform comparisons and differentiation | 1.0 |

---

## 01 - Introduction

- Executive Summary
- Platform Capabilities
  - Knowledge Fabric
  - Studio
  - Dialog
  - AI & LLM Layer
- Document Structure
- Security Principles
- Operational Modes
- Regulatory Compliance
- Contact

---

## 02 - Architecture

### Platform Overview
- Platform Components

### Architecture Overview

### Knowledge Fabric
- Core Capabilities
- Knowledge Graph Model
- Entity Resolution

### Studio
- Core Capabilities
- Text-to-Pipeline
- Agent Architecture
- Chain of Agents
- Operational Modes

### Dialog
- Core Capabilities
- Dialog State Machine
- Function Routing

### Schema Management
- Core Capabilities
- Schema Usage Across Platform
- Document-to-Schema Discovery

### AI & LLM Layer
- Core Capabilities
- LLM Output Consistency
- Provider Support

### AML Compliance Module
- Core Capabilities
- Risk Assessment
- BPM Workflows

### Network Architecture
- Network Segmentation
- Connectivity Patterns

### Data Flow Model

### Security Architecture
- Defense-in-Depth Model
- Cryptographic Standards

### Integration Points
- External System Integration
- MCP Protocol

### Deployment Models
- Deployment Options
- SaaS Multi-Tenant
- Dedicated Cloud Tenant
- Customer Cloud Deployment
- On-Premises Deployment
- Data Residency Configuration
- LLM Provider Configuration by Deployment
- Deployment Feature Comparison

---

## 03 - Knowledge Fabric

### Component Overview

### Architecture Overview

### Knowledge Graph
- Graph Architecture
- Entity Types
- Relationship Types
- Graph Security Controls

### Entity Resolution
- Entity Resolution Architecture
- Resolution Components
- Matching Methods
- Entity Resolution Security
- Golden Record Management

### External Source Integration
- External Source Architecture
- External Source Categories
- OSINT Integration Security
- Enrichment Workflow
- External Source Monitoring

### Customer System Connections
- Connection Architecture
- Synchronization Patterns
- Customer System Types
- Connection Security Controls
- Data Synchronization Security

### Two-Way Data Flow
- Data Flow Architecture
- Read Operations (Data Access)
- Write Operations (Data Updates)
- Write-Back Workflow
- Write-Back Security Controls
- Multi-System Coordination
- What Knowledge Fabric Stores vs. What Remains in Source Systems

### Customer System Health Monitoring

### Connectivity
- Connection Types
- Database Connectivity Security
- API Connectivity Security
- MCP Connector Security (200+ connectors)
- Corporate Ownership Data Integration
- Ownership Chain Traversal
- Ownership Threshold Considerations
- Regulatory Compliance Integration
- MCP Connector Configuration
- Source System Connectivity Patterns
- MCP Integration Lifecycle Management

### Discovery Service
- Discovery Components
- Discovery Security Controls
- Discovery Scope Management
- Discovery Audit Trail

### Active Metadata
- Active Metadata Capabilities
- Automated Classification
- Lineage Tracking

### Persistent Knowledge Graph
- Knowledge Tree Structure
- Schema-Bounded Extraction
- Source Provenance Model
- Incremental Updates

### Search Sessions
- Session Architecture
- Session Graph Accumulation
- Query Turn Processing
- Search Session Security

### Data Observability
- Observability Integration
- Data Quality Metrics
- Quality Test Integration
- Observability Alerts

### Data Insights and KPIs
- Key Performance Indicators
- Platform Analytics

### Graph Database Security
- Query Security

### Monitoring
- Health Monitoring
- Performance Monitoring
- Security Monitoring
- SIEM Integration

### Authentication and Access Control
- Authentication Mechanisms
- Session Management
- Authorization Model

### Credential Management
- Source System Credentials
- Supported Credential Types

### Data Protection
- Data Classification Framework
- Data Masking

### Audit Logging
- Logged Events
- Log Security

---

## 04 - Studio

### Component Overview

### Architecture Overview

### Text-to-Pipeline Generation
- Generation Flow
- Pipeline DSL Structure
- Natural Language Refinement
- DSL Validation
- Preview and Visualization
- Security Controls
- Execution Options

### Agents
- Agent Creation Flow
- Creation Flow Stages
- Domain Selection Options
- Agent Definition Schema
- Agent Security Architecture
- Execution Sandbox
- Agent Workflow Security

### Widgets
- Widget Architecture
- Widget Types
- Widget Creation Flow
- Widget Security Controls
- Widget Data Binding

### Datasets
- Dataset Architecture
- Dataset Types
- Dataset Creation Flow
- Dataset Security Controls
- Dataset Access Patterns
- Dataset Integration with Agents

### Tool Authorization
- Tool Categories
- Tool Permission Model
- MCP Tool Integration Security

### Chain of Agents
- Communication Patterns
- Multi-Agent Security Controls
- Orchestration Security
- Message Protocol Security
- Workflow Composition Security
- State Management Security
- Error Handling and Recovery

### Credential Handling
- Credential Vault
- Credential Types
- Credential Injection

### Operational Modes
- Mode Overview
- Mode Definitions (Modes 0-4)
- Granular Control Options
- Mode Transition
- Mode Security Controls

### Human-in-the-Loop Controls
- Risk Classification
- Approval Controls

### Testing Framework Security
- Test Isolation
- Test Types
- Simulation Security

### Audit Logging
- Logged Events
- Log Security

---

## 05 - AI & LLM

### Component Overview

### LightLLM Router Architecture
- LightLLM Security Benefits

### LLM Output Consistency
- Schema-Validated Extraction
- Ontology-Based Execution
- Reasoning Chain Transparency
- Deterministic vs. Probabilistic Components

### LLM Monitoring and Observability
- Phoenix Monitoring Integration
- Quality Metrics

### Model Version Management
- Model Update Process
- A/B Testing Framework

### LLM Provenance
- Complete Invocation Logging
- Provenance Security

### Provider Security
- Provider Assessment Requirements
- Provider Isolation

### Prompt Security
- Prompt Injection Defense
- Input Sanitization
- Instruction Hierarchy

### Data Protection in AI Pipelines
- PII Handling
- Tenant Data Isolation

### Content Safety
- Input Content Filtering
- Output Content Filtering
- Hallucination Mitigation

### Vector and Embedding Security
- Embedding Security
- Retrieval Security

### Audit Logging
- AI-Specific Events
- Security Events

### Responsible AI
- Ethical Principles
- Explainability

### Quality Assurance and Feedback
- Output Tracking Mechanisms
- Quality Adjustment Mechanisms
- Continuous Improvement

### Model Lifecycle Management
- Model Selection and Configuration
- Model-Agnostic Architecture
- Model Deprecation

---

## 06 - CI/CD

### CI/CD Overview

### Source Control Security
- Repository Security
- Branching Strategy

### Security Scanning
- Secret Scanning
- Static Application Security Testing (SAST)
- Dependency Scanning
- Container Image Scanning

### Code Quality Gates

### Vulnerability Management
- Response Times
- Vulnerability Workflow

### Continuous Deployment
- Deployment Pipeline
- Deployment Security
- Blue-Green Deployment

### Secure Development Practices
- Developer Environment
- Code Review Security

### Audit and Compliance
- CI/CD Audit Trail
- Compliance Controls

---

## 07 - Security Operations

### Security Monitoring
- Security Operations Center (SOC)
- Monitoring Coverage

### Endpoint Protection
- Mobile Device Management (MDM)
- Extended Detection and Response (XDR)
- Device Control

### Monitoring Infrastructure
- Metrics Collection
- Log Management
- Alerting

### Incident Response
- Incident Classification
- Response Phases
- Communication Plan

### Business Continuity
- Recovery Objectives
- Backup Strategy
- Disaster Recovery

### Security Training
- Awareness Program
- Training Topics

---

## 08 - AML Compliance

### Component Overview

### Architecture Overview

### Knowledge Graph for AML
- AML Entity Model
- AML Relationship Types
- Entity Resolution for AML
- Graph Queries for Compliance

### Rule Engine
- Rule Engine Architecture
- Rule Types
- Rule Definition Security
- Risk Scoring Rules
- Rule Versioning
- Rule Execution Security
- Rule Audit Trail

### BPM Workflows
- BPM Architecture
- Compliance Process Types
- Risk-Based Workflow Triggering
- Workflow Task Types
- Workflow Security Controls
- Workflow Definition Security
- Task Assignment Security
- Escalation Controls
- Process Instance Security

### External Source Integration (OSINT)
- External Source Categories
- OSINT Integration Security
- Enrichment Workflow

### Screening Service
- Screening Types
- Screening Security Controls

### Compliance Case Management
- Case Types
- Case Security Controls

### User Roles and Permissions
- AML-Specific Roles
- Permission Matrix

### Audit Logging
- AML-Specific Events
- Regulatory Retention (5-7 years)

### Reporting and Analytics
- Compliance Dashboards
- Report Security

---

## 09 - System Compliance

### Compliance Framework
- Applicable Regulations (GDPR, CCPA, SOC 2, MLR 2017, FCA SYSC)

### Data Protection
- GDPR Compliance
- CCPA/CPRA Compliance
- Data Subject Rights

### SOC 2 Alignment
- Trust Service Criteria

### AI Governance
- EU AI Act Alignment
- Responsible AI Principles

### Audit Logging
- Audit Requirements
- Log Retention (including AML-specific retention)

### Legal Hold and Retention Management
- Retention Policy Framework
- Legal Hold Capabilities
- Retention Policy Types
- Metadata-Based Policy Enforcement
- GDPR Data Subject Rights Integration
- Retention Execution
- Retention Audit Trail

### Third-Party Risk Management
- Vendor Assessment
- Contractual Requirements

### Policy Framework
- Security Policies
- Policy Management

### Data Residency

### Compliance Reporting
- Available Reports
- Audit Support

---

## 10 - Schema Management

### Component Overview

### Architecture Overview

### Business Domain Discovery
- Discovery Flow
- Supported Document Types
- Concept Extraction

### Schema Definition
- Schema Structure
- Entity Definition
- Attribute Types
- Constraint Types

### Schema Registry
- Registry Capabilities
- Version Management
- Schema Dependencies

### Schema Usage
- Studio Integration
- OSINT Extractor Integration
- MCP Connector Integration

### Schema Validation
- Validation Modes
- Validation Results
- Validation Security

### Security Controls
- Schema Access Control
- Schema Governance
- Schema Security

### Audit Logging
- Logged Events
- Audit Trail Security

---

## 11 - API Security

### Component Overview

### Architecture Overview

### API Gateway
- Gateway Capabilities
- Gateway Security Controls

### Authentication
- Authentication Methods
- OAuth 2.0 Flows
- Token Security
- API Key Management

### Authorization
- Authorization Model
- API Scopes
- Permission Enforcement

### Rate Limiting
- Rate Limit Tiers
- Rate Limit Headers
- Rate Limit Strategies
- Rate Limit Responses

### API Versioning
- Versioning Strategy
- Version Lifecycle
- Breaking Changes Policy
- Deprecation Headers

### Request Validation
- Validation Layers
- Input Sanitization
- Security Headers

### Error Handling
- Error Response Format
- Error Categories
- Error Security

### Webhook Security
- Webhook Authentication
- Webhook Headers
- Webhook Security Controls

### Service-to-Service Communication
- Internal Authentication
- Internal Authorization

### Audit Logging
- Logged Events
- Log Security

### Security Monitoring
- Monitoring Metrics
- Threat Detection

### Client SDKs
- Available SDKs
- SDK Security Features

---

## 12 - Dialog

### Component Overview

### Architecture Overview

### Dialog API Gateway
- Gateway Responsibilities
- Gateway Security Controls

### Natural Language Understanding (NLU)
- NLU Components
- Intent Classification
- NLU Security Controls

### Dialog Manager
- Core Functions
- State Machine Design
- State Definitions
- State Transition Security

### Context Manager
- Context Structure
- Context Components
- Cross-Platform Synchronization
- Context Security Controls

### Function Router
- Routing Strategy
- Routing Security
- Multi-Component Query Processing

### Document Processor
- Supported Formats
- Processing Pipeline
- Document Security Controls

### Intelligent Caching System
- Cache Architecture
- Cache Security
- Cache Invalidation

### Performance and Scalability
- Response Time Targets
- Scalability Architecture

### Error Handling and Recovery
- Error Classification
- Graceful Degradation
- Error Security

### Security and Privacy
- Data Protection
- Privacy Controls
- Security Monitoring

### Audit Logging
- Logged Events
- Log Security

### Integration with Platform Components
- Knowledge Fabric Integration
- Studio Integration
- Marketplace Integration
- Exchange Integration

---

## 13 - Operating Costs

### Overview

### LLM & AI Processing
- Option A: Cloud LLM Providers (per-token)
- Option B: Self-Hosted LLM (GPU infrastructure)

### Compute Infrastructure

### Storage & Retention

### External Data Subscriptions

### Monitoring & Observability

### Summary
- Monthly Operating Cost Ranges
- Cost Optimization Levers

---

## 14 - Trust & Compliance

### Overview

### Shared Responsibility Model
- Responsibility Matrix
- Joint Responsibilities

### Security Operations
- Continuous Security Management
- Patch Management SLAs
- Incident Response
- Incident Communication

### Compliance Management
- Continuous Compliance
- Compliance Activities
- Regulatory Change Management
- Audit Support

### Customer-Specific Controls
- Identity Integration
- Access Control Alignment
- Data Protection Configuration
- Integration Security

### Governance & Transparency
- Dedicated Support
- Transparency Mechanisms
- Change Management
- Periodic Reviews
- Reporting

---

## 15 - Competitive Analysis

### Overview
- LegalFab Key Differentiators

### LegalFab vs. Microsoft Fabric
- Executive Summary
- What Microsoft Fabric Actually Is
- LegalFab Knowledge Fabric Architecture
- Fabric IQ: Microsoft's Semantic Layer
- Head-to-Head Comparison
- Where Each Platform Excels

### LegalFab vs. DeepJudge
- Comparison Matrix
- Architectural Philosophy Comparison

### Summary

---

## Quick Reference

### Key Platform Components

| Component | Primary Document | Key Features |
|:----------|:-----------------|:-------------|
| Knowledge Graph | 03-Knowledge-Fabric | Entity storage, relationship mapping, traversal queries |
| Entity Resolution | 03-Knowledge-Fabric | Blocking, matching, clustering, golden records |
| Two-Way Data Flow | 03-Knowledge-Fabric | Read/write to source systems, metadata-only storage |
| Persistent Knowledge Graph | 03-Knowledge-Fabric | Corporate memory, schema-bounded extraction, provenance |
| Search Sessions | 03-Knowledge-Fabric | Iterative exploration, session graphs, accumulated context |
| Data Observability | 03-Knowledge-Fabric | Quality monitoring, freshness, alerts |
| Text-to-Pipeline | 04-Studio | Natural language workflow generation, DSL output |
| Agents | 04-Studio | AI agents with domain-driven creation flow |
| Widgets | 04-Studio | Agents with visual interface components |
| Datasets | 04-Studio | Structured data collections for agents |
| Chain of Agents | 04-Studio | Multi-agent orchestration patterns |
| Operational Modes | 04-Studio | Five modes from manual to fully automated |
| LightLLM Gateway | 05-AI-LLM | Provider-agnostic LLM interface |
| LLM Monitoring | 05-AI-LLM | Output consistency, A/B testing, provenance |
| Dialog Interface | 12-Dialog | Conversational NLU, state machine, context management |
| Function Router | 12-Dialog | Multi-component query routing and orchestration |
| Intelligent Caching | 12-Dialog | Exact match and semantic caching layers |
| Rule Engine | 08-AML-Compliance | Risk scoring, compliance rules |
| BPM Workflows | 08-AML-Compliance | CDD, EDD, investigation processes |
| Screening Service | 08-AML-Compliance | Sanctions, PEP, adverse media |
| Schema Registry | 09-Schema-Management | Schema versioning, validation, binding |
| Domain Discovery | 09-Schema-Management | Document-to-schema extraction |
| Legal Hold/Retention | 10-System-Compliance | Metadata-based retention, legal hold management |
| API Gateway | 11-API-Security | Authentication, rate limiting, routing |
| OAuth/Token Management | 11-API-Security | Token lifecycle, API keys, scopes |
| MCP Lifecycle Management | 03-Knowledge-Fabric | API tracking, monitoring, remediation SLAs |
| Operating Costs | 13-Operating-Costs | LLM, compute, storage, external data estimates |
| Shared Responsibility | 14-Trust-Compliance | LegalFab vs. customer responsibilities |
| Managed Security Ops | 14-Trust-Compliance | Patching SLAs, incident response, compliance |

### Security Controls by Category

| Category | Documents |
|:---------|:----------|
| Authentication & Access | 02, 03, 04, 09, 10, 11 |
| Encryption & Data Protection | 02, 03, 05, 10, 11 |
| Audit Logging | 03, 04, 05, 08, 09, 10, 11 |
| Network Security | 02, 07, 11 |
| Incident Response | 07, 14 |
| Compliance & Governance | 08, 10, 14 |
| Schema & Data Quality | 04, 09 |
| API Security | 11 |
| Service Continuity | 03, 14 |

### Regulatory Coverage

| Regulation | Primary Documents |
|:-----------|:------------------|
| GDPR | 09-System-Compliance |
| CCPA/CPRA | 09-System-Compliance |
| SOC 2 Type II | 09-System-Compliance |
| MLR 2017 | 08-AML-Compliance, 09-System-Compliance |
| FCA SYSC | 08-AML-Compliance, 09-System-Compliance |
| EU AI Act | 05-AI-LLM, 09-System-Compliance |

---

---
## Related Notes

- [[DataFab/Documentation/LegalFab/01-Introduction]] — Introduction
- [[DataFab/Documentation/LegalFab/03-Knowledge-Fabric]] — Knowledge Fabric
- [[DataFab/Documentation/LegalFab/05-AI-LLM]] — AI/LLM Layer
- [[DataFab/Documentation/LegalFab/08-AML-Compliance]] — AML Compliance
- [[DataFab/Documentation/LegalFab/12-Dialog]] — Dialog System
