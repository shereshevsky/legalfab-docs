# LegalFab Platform Documentation

Welcome to the LegalFab platform security and architecture documentation.

---

## Overview

LegalFab is an AI-powered legal technology platform built on a metadata-driven architecture that provides unified access to distributed data assets while maintaining strict security controls. The platform enables natural language interaction across all components, supports configurable automation levels, and integrates with 200+ data sources including specialized corporate ownership and regulatory registers.

---

## Documentation

| Document | Description | Version |
|:---------|:------------|:-------:|
| [Introduction](./01-Introduction.md) | Platform overview, capabilities, and security summary | 1.2 |
| [Architecture](./02-Architecture.md) | System architecture, deployment models, security boundaries | 1.3 |
| [Knowledge Fabric](./03-Knowledge-Fabric.md) | Knowledge graph, entity resolution, MCP connectors, corporate ownership | 1.6 |
| [Studio](./04-Studio.md) | Agent creation, widgets, datasets, operational modes | 1.5 |
| [AI & LLM](./05-AI-LLM.md) | LLM security, output consistency, model provenance | 1.1 |
| [CI/CD](./06-CI-CD.md) | CI/CD pipeline security | 1.0 |
| [Security Operations](./07-Security-Operations.md) | SOC, monitoring, incident response | 1.0 |
| [AML Compliance](./08-AML-Compliance.md) | AML rule engine, BPM workflows, screening | 1.0 |
| [Schema Management](./09-Schema-Management.md) | Business domain discovery, schema registry | 1.0 |
| [System Compliance](./10-System-Compliance.md) | Regulatory compliance, legal hold, retention | 1.2 |
| [API Security](./11-API-Security.md) | API gateway, authentication, rate limiting | 1.0 |
| [Dialog](./12-Dialog.md) | Conversational interface, NLU, context management | 1.0 |

---

## Platform Components

### Knowledge Fabric
The foundational data integration layer with 200+ MCP connectors, persistent knowledge graph, entity resolution, and corporate ownership data integration including Companies House, Bureau van Dijk, and GLEIF LEI.

### Studio
Development environment for building AI agents, widgets, and datasets with domain-driven creation flows, schema-bound processing, and five configurable operational modes.

### Dialog
Central conversational interface enabling natural language interaction across all platform components with intelligent routing, NLU, and cross-platform context management.

### AI & LLM Layer
Provider-agnostic LLM integration via LightLLM with output consistency controls, model provenance tracking, and quality assurance.

---

## Quick Links

- [Table of Contents](./00-Table-of-Contents.md) - Complete navigation with all sections
- [Security Principles](./01-Introduction.md#security-principles) - Core security approach
- [Operational Modes](./04-Studio.md#operational-modes) - Automation levels (Mode 0-4)
- [Corporate Ownership Integration](./03-Knowledge-Fabric.md#corporate-ownership-data-integration) - UK data sources

---

## Security Highlights

| Principle | Implementation |
|:----------|:---------------|
| Defense in Depth | Multiple independent security layers |
| Zero Trust | All requests authenticated regardless of source |
| Encryption Everywhere | AES-256 at rest, TLS 1.3 in transit |
| Schema-Driven Security | All extraction bounded by user-defined schemas |
| Human-in-the-Loop | Configurable automation with escalation workflows |

---

## Regulatory Compliance

The platform supports compliance with GDPR, CCPA/CPRA, Money Laundering Regulations 2017, SOC 2, FCA requirements, and legal industry standards.

---

## Contact

For security inquiries or additional documentation, please contact the LegalFab security team through your account representative.

---

*Last Updated: January 2026*
