---
layout: default
title: AML Compliance
---

# LegalFab AML Compliance

**Version:** 1.0
**Last Updated:** January 2026

---

## Component Overview

The AML (Anti-Money Laundering) Compliance module provides comprehensive capabilities for customer due diligence, risk assessment, and regulatory compliance. It leverages the Knowledge Fabric's graph-based entity resolution and the Studio's workflow capabilities to deliver an integrated compliance solution.

**Core Capabilities:**

| Capability | Description | Security Relevance |
|:-----------|:------------|:-------------------|
| Knowledge Graph Integration | Entity resolution and relationship mapping | Data integrity, access control |
| Rule Engine | Risk scoring and compliance decision rules | Rule versioning, audit trail |
| BPM Workflows | CDD and investigation process orchestration | Process authorization, escalation |
| External Enrichment | OSINT and third-party data integration | Source validation, provenance |
| Screening | Sanctions, PEP, and adverse media checks | Match verification, false positive handling |
| Case Management | Compliance case tracking and documentation | Evidence chain, retention |

---

## Architecture Overview

```
┌─────────────────────────────────────────────────────────────────────────┐
│                        AML COMPLIANCE ARCHITECTURE                      │
├─────────────────────────────────────────────────────────────────────────┤
│                                                                         │
│  ┌────────────────────────────────────────────────────────────────────┐ │
│  │                    COMPLIANCE INTERFACE                            │ │
│  │  ┌──────────────┐  ┌──────────────┐  ┌──────────────────────────┐  │ │
│  │  │  Case Queue  │  │  Dashboards  │  │  Reporting & Analytics   │  │ │
│  │  └──────────────┘  └──────────────┘  └──────────────────────────┘  │ │
│  └────────────────────────────────────────────────────────────────────┘ │
│                              │                                          │
│  ┌────────────────────────────────────────────────────────────────────┐ │
│  │                    COMPLIANCE ENGINE                               │ │
│  │  ┌─────────────┐  ┌─────────────┐  ┌─────────────┐  ┌───────────┐  │ │
│  │  │  Rule       │  │  BPM        │  │  Screening  │  │   Case    │  │ │
│  │  │  Engine     │  │  Workflows  │  │  Service    │  │  Manager  │  │ │
│  │  └─────────────┘  └─────────────┘  └─────────────┘  └───────────┘  │ │
│  └────────────────────────────────────────────────────────────────────┘ │
│                              │                                          │
│  ┌────────────────────────────────────────────────────────────────────┐ │
│  │                    KNOWLEDGE FABRIC INTEGRATION                    │ │
│  │  ┌─────────────────┐  ┌─────────────────┐  ┌────────────────────┐  │ │
│  │  │ Knowledge Graph │  │ Entity          │  │ External Source    │  │ │
│  │  │ (Entities &     │  │ Resolution      │  │ Integration        │  │ │
│  │  │  Relationships) │  │                 │  │ (OSINT)            │  │ │
│  │  └─────────────────┘  └─────────────────┘  └────────────────────┘  │ │
│  └────────────────────────────────────────────────────────────────────┘ │
│                              │                                          │
│  ┌────────────────────────────────────────────────────────────────────┐ │
│  │                    CUSTOMER SYSTEM CONNECTIONS                     │ │
│  │  Matter Management │ CRM │ Billing │ Document Management           │ │
│  └────────────────────────────────────────────────────────────────────┘ │
└─────────────────────────────────────────────────────────────────────────┘
```

---

## Knowledge Graph for AML

The Knowledge Fabric's graph database provides the foundation for AML compliance, enabling entity resolution, relationship mapping, and risk analysis across connected data sources.

### AML Entity Model

| Entity Type | Description | AML Relevance |
|:------------|:------------|:--------------|
| Person | Individual clients, contacts, UBOs | KYC subject, risk assessment |
| Organization | Corporate clients, related entities | Corporate structure, ownership |
| Compliance Case | CDD/EDD investigation record | Case management, audit trail |
| Risk Assessment | Calculated risk profile | Risk scoring, CDD level |
| Screening Result | Sanctions/PEP/adverse media matches | Alert management |
| Document | Evidence and supporting documents | Compliance documentation |

### AML Relationship Types

| Relationship | Description | Compliance Use |
|:-------------|:------------|:---------------|
| OWNS | Ownership stake in entity | UBO identification |
| CONTROLS | Control relationship | Beneficial ownership |
| RELATED_TO | Personal/business relationship | Network analysis |
| HAS_CASE | Entity linked to compliance case | Case tracking |
| HAS_SCREENING | Entity linked to screening result | Alert management |
| HAS_RISK_ASSESSMENT | Entity linked to risk profile | Risk monitoring |

### Entity Resolution for AML

The Entity Resolution Engine identifies duplicate and related records across customer systems to build a unified view of each entity.

**Resolution Security Controls:**

| Control | Implementation |
|:--------|:---------------|
| Match Decision Audit | All match decisions logged with reasoning |
| Human Review Queue | Uncertain matches routed for manual review |
| Source Attribution | Every attribute linked to source system |
| Confidence Scoring | Match confidence visible for compliance review |
| Merge History | Complete history of entity merges preserved |

### Graph Queries for Compliance

| Query Type | Purpose | Security Control |
|:-----------|:--------|:-----------------|
| Ownership Traversal | Identify UBOs through ownership chains | Traversal depth limits |
| Network Analysis | Map entity relationships | Result filtering by permission |
| Pattern Matching | Detect suspicious relationship patterns | Query audit logging |
| Risk Aggregation | Calculate network-level risk | Authorized users only |

---

## Rule Engine

![Rule Engine](./images/Pasted%20image%2020260128181311.png)
The Rule Engine enables administrators to define, version, and execute business rules for risk assessment, compliance decisions, and workflow routing.

### Rule Engine Architecture

```
┌─────────────────────────────────────────────────────────────────────┐
│                    RULE ENGINE ARCHITECTURE                         │
├─────────────────────────────────────────────────────────────────────┤
│                                                                     │
│  ┌──────────────────────────────────────────────────────────--──┐   │
│  │                    RULE DEFINITION LAYER                     │   │
│  │  ┌─────────────┐  ┌─────────────┐  ┌─────────────┐           │   │
│  │  │  Rule       │  │  Condition  │  │  Action     │           │   │
│  │  │  Builder    │  │  Editor     │  │  Designer   │           │   │
│  │  └─────────────┘  └─────────────┘  └─────────────┘           │   │
│  └───────────────────────────────────────────────────────────-──┘   │
│                              │                                      │
│  ┌────────────────────────────────────────────────────────────-─┐   │
│  │                    RULE EXECUTION ENGINE                     │   │
│  │  ┌─────────────┐  ┌─────────────┐  ┌─────────────┐           │   │
│  │  │  Evaluation │  │  Scoring    │  │  Action     │           │   │
│  │  │  Engine     │  │  Engine     │  │  Executor   │           │   │
│  │  └─────────────┘  └─────────────┘  └─────────────┘           │   │
│  └────────────────────────────────────────────────────────────-─┘   │
│                              │                                      │
│  ┌─────────────────────────────────────────────────────────────-┐   │
│  │                    GOVERNANCE LAYER                          │   │
│  │  • Version Control   • Approval Workflow   • Audit Trail     │   │
│  └────────────────────────────────────────────────────────────-─┘   │
└─────────────────────────────────────────────────────────────────────┘
```

### Rule Types

| Rule Type | Purpose | Example Use Case |
|:----------|:--------|:-----------------|
| Risk Scoring | Calculate numeric risk scores | Customer risk assessment |
| Classification | Assign categories based on conditions | CDD level determination |
| Threshold | Trigger actions when values exceed limits | Alert generation |
| Routing | Direct workflow based on conditions | Escalation to MLRO |
| Validation | Verify data meets requirements | Input data validation |

### Rule Definition Security

| Control | Implementation |
|:--------|:---------------|
| Role-Based Editing | Only authorized roles can create/modify rules |
| Version Control | All rule changes versioned with full history |
| Approval Workflow | Rule changes require approval before activation |
| Testing Required | Rules must pass test suite before deployment |
| Rollback Support | Previous versions can be restored instantly |

### Risk Scoring Rules

Risk scoring rules calculate numeric scores based on configurable factors and weights.

**Scoring Components:**

| Component         | Description                              | Security Control               |
| :---------------- | :--------------------------------------- | :----------------------------- |
| Factor Definition | Risk factors with categories and weights | Admin-only modification        |
| Score Calculation | Weighted aggregation of factors          | Audit trail on calculations    |
| Threshold Mapping | Score ranges mapped to risk levels       | Configurable per policy        |
| Override Handling | Manual score adjustments                 | Requires justification, logged |

**Risk Factor Categories:**

| Category        | Examples                       | Typical Weight Range |
| :-------------- | :----------------------------- | :------------------- |
| Geography       | Country risk, jurisdiction     | 0-30 points          |
| Industry        | Sector risk classification     | 0-25 points          |
| Product/Service | Transaction type risk          | 0-20 points          |
| Customer Type   | Individual, corporate, trust   | 0-15 points          |
| Channel         | Online, in-person, referral    | 0-10 points          |
| Behavioral      | Transaction patterns, velocity | 0-20 points          |

**Risk Level Mapping:**

| Risk Level | Score Range | CDD Level | Review Frequency |
|:-----------|:------------|:----------|:-----------------|
| Low | 0-25 | Simplified | 36 months |
| Medium | 26-50 | Standard | 24 months |
| High | 51-75 | Enhanced | 12 months |
| Very High | 76-100 | Enhanced+ | 6 months |

### Rule Versioning

| Control | Description |
|:--------|:------------|
| Immutable Versions | Published versions cannot be modified |
| Version History | Complete history of all changes preserved |
| Change Attribution | Every change linked to user and timestamp |
| Comparison View | Side-by-side comparison of versions |
| Audit Export | Version history exportable for compliance |

### Rule Execution Security

| Control | Implementation |
|:--------|:---------------|
| Execution Isolation | Rules execute in sandboxed environment |
| Input Validation | All inputs validated against schema |
| Output Verification | Results validated before action execution |
| Timeout Enforcement | Maximum execution time enforced |
| Resource Limits | Memory and CPU limits on rule execution |

### Rule Audit Trail

| Event | Logged Data | Retention |
|:------|:------------|:----------|
| Rule Created | Rule definition, creator, timestamp | 2 years |
| Rule Modified | Changes, modifier, justification | 2 years |
| Rule Activated | Version, approver, effective date | 2 years |
| Rule Executed | Input hash, score, actions triggered | 1 year |
| Rule Overridden | Override value, justification, approver | 2 years |

---

## BPM Workflows

![BPM Workflows](./images/Pasted%20image%2020260128181324.png)

The BPM (Business Process Management) system orchestrates multi-step compliance processes with human tasks, automated actions, and regulatory controls.

### BPM Architecture

```
┌─────────────────────────────────────────────────────────────────────┐
│                    BPM WORKFLOW ARCHITECTURE                        │
├─────────────────────────────────────────────────────────────────────┤
│                                                                     │
│  ┌────────────────────────────────────────────────────────-─────┐   │
│  │                    PROCESS DEFINITION                        │   │
│  │  ┌─────────────┐  ┌─────────────┐  ┌─────────────┐           │   │
│  │  │  Process    │  │  Task       │  │  Gateway    │           │   │
│  │  │  Designer   │  │  Library    │  │  Config     │           │   │
│  │  └─────────────┘  └─────────────┘  └─────────────┘           │   │
│  └────────────────────────────────────────────────────────────-─┘   │
│                              │                                      │
│  ┌───────────────────────────────────────────────────────────-──┐   │
│  │                    EXECUTION ENGINE                          │   │
│  │  ┌─────────────┐  ┌─────────────┐  ┌─────────────┐           │   │
│  │  │  Process    │  │  Task       │  │  Event      │           │   │
│  │  │  Runtime    │  │  Manager    │  │  Handler    │           │   │
│  │  └─────────────┘  └─────────────┘  └─────────────┘           │   │
│  └──────────────────────────────────────────────────────────-───┘   │
│                              │                                      │
│  ┌───────────────────────────────────────────────────────────-──┐   │
│  │                    INTEGRATION LAYER                         │   │
│  │  • Knowledge Graph   • Rule Engine   • Notification Service  │   │
│  └────────────────────────────────────────────────────────────-─┘   │
└─────────────────────────────────────────────────────────────────────┘
```

### Compliance Process Types

| Process Type | Purpose | Trigger |
|:-------------|:--------|:--------|
| Client Onboarding | New client CDD workflow | Entity creation from MMS |
| Periodic Review | Scheduled re-assessment | Timer, risk change |
| Triggered Review | Event-driven re-assessment | Alert, external event |
| Investigation | Suspicious activity review | Alert, manual referral |
| SAR Escalation | MLRO review and filing | Risk threshold, policy |

### Risk-Based Workflow Triggering

The Rule Engine integrates with BPM to automatically trigger appropriate workflows based on risk assessment outcomes.

**Workflow Trigger Flow:**

```
┌─────────────────────────────────────────────────────────────────────┐
│                    RISK-BASED WORKFLOW TRIGGERING                   │
├─────────────────────────────────────────────────────────────────────┤
│                                                                     │
│  Entity Event ──▶ [Risk Assessment] ──▶ [Rule Evaluation]           │
│       │                  │                      │                   │
│       ▼                  ▼                      ▼                   │
│  (New client,      (Score calculated)     (Rules matched)           │
│   data change,                                  │                   │
│   alert)                                        ▼                   │
│                                     [Workflow Selection]            │
│                                           │                         │
│              ┌────────────────────────────┼────────────────┐        │
│              ▼                            ▼                ▼        │
│         [Low Risk]                  [Medium Risk]    [High Risk]    │
│              │                            │                │        │
│              ▼                            ▼                ▼        │
│       Simplified CDD              Standard CDD      Enhanced CDD    │
│        Workflow                    Workflow          Workflow       │
│              │                            │                │        │
│              └────────────────────────────┼────────────────┘        │
│                                           ▼                         │
│                                    [Task Assignment]                │
│                                           │                         │
│                                           ▼                         │
│                                    [Process Execution]              │
│                                           │                         │
│                                           ▼                         │
│                                     [Audit Trail]                   │
└─────────────────────────────────────────────────────────────────────┘
```

### Workflow Task Types

| Task Type | Description | Security Control |
|:----------|:------------|:-----------------|
| User Task | Human action required | Role-based assignment |
| Service Task | Automated system action | Permission validation |
| Script Task | Custom logic execution | Sandboxed execution |
| Send Task | External communication | Message logging |
| Receive Task | Wait for external event | Event validation |

### Workflow Security Controls

| Control | Implementation |
|:--------|:---------------|
| Process Authorization | Only authorized users can start processes |
| Task Assignment | Tasks assigned based on role and workload |
| Escalation Rules | Automatic escalation on SLA breach |
| Delegation Controls | Delegation requires approval, logged |
| Completion Verification | Task completion validated before proceeding |

### Workflow Definition Security

| Control | Description |
|:--------|:------------|
| Version Control | Process definitions versioned |
| Change Approval | Process changes require multi-party approval |
| Testing Required | Processes must pass simulation before deployment |
| Rollback Support | Previous versions can be restored |
| Access Restrictions | Process definition access role-based |

### Task Assignment Security

| Control | Implementation |
|:--------|:---------------|
| Role-Based Assignment | Tasks assigned to roles, not individuals |
| Workload Balancing | Even distribution across team members |
| Conflict Avoidance | Prevent assignment to conflicted parties |
| Audit Trail | All assignments and reassignments logged |
| SLA Monitoring | Task completion tracked against SLA |

### Escalation Controls

| Trigger | Action | Security Control |
|:--------|:-------|:-----------------|
| SLA Breach | Escalate to supervisor | Automatic, logged |
| Risk Threshold | Escalate to MLRO | Rule-based, audited |
| Manual Request | Escalate per request | Requires justification |
| Timeout | Reassign or escalate | Configurable per task |

### Process Instance Security

| Control | Description |
|:--------|:------------|
| Instance Isolation | Each process instance isolated |
| Data Encryption | Process data encrypted at rest |
| Access Control | Instance access based on role and assignment |
| State Protection | State transitions validated and logged |
| Cancellation Control | Cancellation requires authorization |

---

## External Source Integration (OSINT)

The AML module integrates with external data sources for entity verification and enrichment.

### External Source Categories

| Category | Examples | Data Types |
|:---------|:---------|:-----------|
| Corporate Registries | Companies House, SEC EDGAR | Incorporation, officers, filings |
| Beneficial Ownership | PSC registers, UBO databases | Ownership chains |
| Sanctions Lists | OFAC, OFSI, UN, EU | Designated persons/entities |
| PEP Databases | Politically exposed persons | Political associations |
| Adverse Media | News aggregators, media monitors | Negative news, allegations |
| Court Records | Legal databases | Litigation history |

### OSINT Integration Security

| Control | Implementation |
|:--------|:---------------|
| Source Validation | Only approved sources in registry |
| Credential Isolation | Per-source credential management |
| Rate Limiting | Respect source API limits |
| Data Minimization | Retrieve only required fields |
| Caching Policy | Time-limited caching per source |
| Provenance Tracking | Full lineage from source to graph |

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

---

## Screening Service

The Screening Service performs sanctions, PEP, and adverse media checks against entities.

### Screening Types

| Screening Type | Sources | Frequency |
|:---------------|:--------|:----------|
| Sanctions | OFAC, OFSI, UN, EU lists | Real-time, daily batch |
| PEP | Political exposure databases | On-boarding, periodic |
| Adverse Media | News and media monitors | Continuous monitoring |

### Screening Security Controls

| Control | Implementation |
|:--------|:---------------|
| Match Verification | Potential matches require human review |
| False Positive Management | Documented false positive decisions |
| Alert Escalation | True matches escalated per policy |
| Screening Audit | All screening activity logged |
| List Update Tracking | Source list versions tracked |

---

## Compliance Case Management

Compliance cases track CDD, investigations, and regulatory actions.

### Case Types

| Case Type | Purpose | Lifecycle |
|:----------|:--------|:----------|
| New Client CDD | Onboarding due diligence | Open → Review → Approved/Rejected |
| Periodic Review | Scheduled re-assessment | Triggered → Review → Closed |
| Investigation | Alert or suspicion review | Open → Investigate → Escalate/Close |
| SAR | Suspicious activity report | Prepare → Review → File/Dismiss |

### Case Security Controls

| Control | Implementation |
|:--------|:---------------|
| Access Control | Case access based on role and assignment |
| Evidence Chain | All documents and notes timestamped |
| Decision Audit | All decisions logged with justification |
| Retention Policy | Cases retained per regulatory requirement |
| Export Controls | Case export requires authorization |

---

## User Roles and Permissions

### AML-Specific Roles

| Role | Description | Permissions |
|:-----|:------------|:------------|
| Compliance Officer | Day-to-day CDD work | Case work, screening review, standard CDD |
| Compliance Manager | Senior compliance staff | Case approval, risk override, team management |
| MLRO | Money Laundering Reporting Officer | SAR filing, escalation approval, full case access |
| Intake Coordinator | Intake staff | Create cases, basic screening, escalate |
| Auditor | External/internal auditor | View all cases, run reports, no edit |

### Permission Matrix

| Action | Officer | Manager | MLRO | Intake | Auditor |
|:-------|:--------|:--------|:-----|:-------|:--------|
| Create Case | ✓ | ✓ | ✓ | ✓ | ✗ |
| Review Case | ✓ | ✓ | ✓ | ✗ | ✓ |
| Approve Case | ✗ | ✓ | ✓ | ✗ | ✗ |
| Override Risk | ✗ | ✓ | ✓ | ✗ | ✗ |
| File SAR | ✗ | ✗ | ✓ | ✗ | ✗ |
| Modify Rules | ✗ | ✓ | ✓ | ✗ | ✗ |
| View Reports | ✓ | ✓ | ✓ | ✗ | ✓ |

---

## Audit Logging

### AML-Specific Events

| Event Category | Logged Data | Retention |
|:---------------|:------------|:----------|
| Case Created | Case ID, entity, creator, type | 7 years |
| Case Decision | Case ID, decision, approver, justification | 7 years |
| Risk Assessment | Entity, score, factors, assessor | 7 years |
| Screening Performed | Entity, sources, matches, reviewer | 7 years |
| Rule Executed | Rule ID, inputs, score, actions | 7 years |
| Process Executed | Process ID, tasks, outcomes | 7 years |
| SAR Filed | Case ID, filer, filing reference | 7 years |

### Regulatory Retention

| Regulation | Retention Period | Data Types |
|:-----------|:-----------------|:-----------|
| FCA Requirements | 5 years minimum | CDD records, decisions |
| MLR 2017 | 5 years from end of relationship | Identity documents, transaction records |
| Internal Policy | 7 years | All compliance records |

---

## Reporting and Analytics

### Compliance Dashboards

| Dashboard | Purpose | Access |
|:----------|:--------|:-------|
| Case Queue | Active cases and assignments | All compliance roles |
| Risk Overview | Entity risk distribution | Manager, MLRO |
| SLA Monitoring | Task completion against targets | Manager, MLRO |
| Screening Alerts | Pending screening matches | Officer, Manager, MLRO |
| MI Dashboard | Management information metrics | Manager, MLRO |

### Report Security

| Control | Implementation |
|:--------|:---------------|
| Role-Based Access | Reports filtered by user permissions |
| Data Aggregation | Individual data protected in summaries |
| Export Logging | All report exports logged |
| Scheduled Reports | Automated reports require authorization |

---
