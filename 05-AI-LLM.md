---
layout: default
title: AI & LLM
---

# LegalFab AI & LLM

**Version:** 1.1
**Last Updated:** January 2026

---

## Component Overview

The AI & LLM Architecture provides the intelligence layer for the LegalFab platform. Built on LightLLM, the platform is LLM-provider-agnostic, enabling flexible model selection while maintaining consistent security controls. The architecture ensures reproducible, auditable AI operations through schema validation, ontology-based execution, and comprehensive provenance tracking.

**Key Security Characteristics:**

- Multi-layer prompt injection defense
- Data isolation prevents cross-tenant information leakage
- Secure API integration with LLM providers
- Comprehensive content filtering and safety guardrails
- Privacy-preserving retrieval
- Human-in-the-loop controls for high-risk operations
- Output consistency through schema validation and deterministic workflows
- Complete provenance tracking for audit and reproducibility

---

## LightLLM Router Architecture

LegalFab uses LightLLM as a unified routing layer for all LLM provider access:

```
┌─────────────────────────────────────────────────────────────────────┐
│                    LIGHTLLM ROUTER                                  │
├─────────────────────────────────────────────────────────────────────┤
│  ┌─────────────┐  ┌─────────────┐  ┌─────────────────────┐          │
│  │  Unified    │  │  Load       │  │  Fallback           │          │
│  │  API        │  │  Balancing  │  │  Routing            │          │
│  └─────────────┘  └─────────────┘  └─────────────────────┘          │
│                              │                                      │
│         ┌────────────────────┼────────────────────┐                 │
│         ▼                    ▼                    ▼                 │
│  ┌─────────────┐      ┌─────────────┐      ┌─────────────┐          │
│  │  Provider A │      │  Provider B │      │  Self-      │          │
│  │             │      │             │      │  Hosted     │          │
│  └─────────────┘      └─────────────┘      └─────────────┘          │
└─────────────────────────────────────────────────────────────────────┘
```

### LightLLM Security Benefits

| Benefit | Description |
|:--------|:------------|
| Unified Security Controls | Single point for authentication, logging, and filtering |
| Provider Abstraction | Security controls applied consistently across all providers |
| Automatic Failover | Seamless switching to backup providers |
| Centralized Credential Management | All API keys managed in one secure location |
| Consistent Audit Logging | Uniform logging regardless of backend provider |
| Cost Controls | Budget limits enforced across all providers |

---

## LLM Output Consistency

Traditional LLM applications can produce different outputs for identical inputs. LegalFab addresses this through a multi-layered architectural approach that constrains and validates LLM outputs at every step.

### Schema-Validated Extraction

| Control | Implementation |
|:--------|:---------------|
| Template Validation | All LLM extractions validated against user-defined schemas |
| Field Type Enforcement | Extracted values must match schema-defined data types |
| Constraint Checking | Values validated against defined ranges and formats |
| Hallucination Prevention | System cannot invent fields or values outside schema definitions |
| Flagging Non-Conformance | Extractions that don't match schema are flagged for review |

### Ontology-Based Execution

The ontology defines relationships between entities, execution sequences, and dependencies among analytical steps. This ensures consistent reasoning pathways regardless of when or how often an analysis is performed.

| Control | Implementation |
|:--------|:---------------|
| Execution Order | Ontology dictates the sequence of data science flows |
| Dependency Enforcement | Steps execute only when dependencies are satisfied |
| Workflow Consistency | Same dataset follows same logical pathways every time |
| Computational Graph | Reasoning chains follow deterministic graph structure |

### Reasoning Chain Transparency

Each analytical step documents its reasoning for complete traceability:

| Captured Element | Description |
|:-----------------|:------------|
| Input Data | Source data and documents consulted |
| Reasoning Process | Analytical methods applied |
| Intermediate Conclusions | Stepwise findings with justification |
| Confidence Scores | Certainty levels at each step |
| Supporting Facts | Specific evidence with document references |

### Deterministic vs. Probabilistic Components

| Component Type | Behavior | Examples |
|:---------------|:---------|:---------|
| Deterministic | Always produces identical results | Database queries, schema validation, rule-based logic |
| Probabilistic (Constrained) | LLM operations with controls | Temperature minimization, structured output formats, ensemble validation |

**LLM Variability Controls:**

| Control | Implementation |
|:--------|:---------------|
| Temperature Settings | Minimized to reduce output variability |
| Structured Output | Format enforced through schema layer |
| Validation Checks | Outputs deviating from expected patterns rejected |
| Ensemble Approaches | Multiple LLM calls must agree for critical decisions |

---

## LLM Monitoring and Observability

### Phoenix Monitoring Integration

LegalFab integrates with LLM observability tools for comprehensive monitoring:

| Metric | Description | Purpose |
|:-------|:------------|:--------|
| Prompt/Response Pairs | Complete input/output capture | Audit, debugging |
| Token Usage | Tokens consumed per request | Cost tracking |
| Latency | Response time metrics | Performance monitoring |
| Embedding Quality | Vector similarity and retrieval accuracy | RAG optimization |
| Drift Detection | Statistical measures of output distribution changes | Model stability |

### Quality Metrics

| Metric | Description | Tracking |
|:-------|:------------|:---------|
| Factual Grounding % | Proportion of conclusions with clear evidence attribution | Per-model, over time |
| Hallucination Rate | Outputs lacking factual basis | Alert threshold |
| Schema Validation Pass Rate | Outputs conforming to expected structures | Per-task type |
| Confidence Score Distribution | Statistical profile of model certainty | Baseline comparison |
| Q&A Correctness | Verified accuracy against ground truth | Benchmark testing |

---

## Model Version Management

### Model Update Process

When LLM models are updated, organizations need assurance that investigative conclusions remain credible and traceable.

**Pre-Deployment Testing:**

| Stage | Activities |
|:------|:-----------|
| Historical Case Testing | Run new model on cases with known outcomes |
| Output Comparison | Compare against established conclusions |
| Metric Analysis | Measure changes across golden test set |
| Regression Detection | Identify any degradation in performance |

**Controlled Rollout:**

| Phase | Description |
|:------|:------------|
| Canary Deployment | Deploy to subset of workloads |
| Real-Time Monitoring | Compare metrics between model versions |
| Gradual Expansion | Increase traffic only after validation |
| Full Deployment | Complete rollout after confidence threshold met |

**Rollback Capability:**

| Control | Implementation |
|:--------|:---------------|
| Version Retention | Previous model versions maintained |
| Instant Rollback | One-click reversion if issues detected |
| Traffic Shifting | Gradual migration between versions |
| State Preservation | No data loss during model transitions |

### A/B Testing Framework

| Capability | Description |
|:-----------|:------------|
| Traffic Splitting | Route percentage of requests to each model version |
| Metric Comparison | Side-by-side performance analysis |
| Statistical Significance | Automated determination of winner |
| Audience Targeting | Test on specific user segments or use cases |

---

## LLM Provenance

### Complete Invocation Logging

Every LLM invocation captures:

| Data Point | Description | Retention |
|:-----------|:------------|:----------|
| Prompt Template | Exact prompt sent to model | 1 year |
| Model Version | Specific model and parameters used | 1 year |
| Retrieved Context | Documents/data provided to model | 1 year |
| Complete Response | Full model output | 1 year |
| Reasoning Chain | Logic from context to conclusion | 2 years |
| Supporting Facts | Document references for conclusions | 2 years |

### Provenance Security

| Control | Implementation |
|:--------|:---------------|
| Immutability | Provenance records cannot be modified |
| Tamper Evidence | Cryptographic hash chain prevents alteration |
| Cross-Reference | Links between related invocations preserved |
| Version Comparison | Side-by-side analysis when model changes affect conclusions |

---

## Provider Security

### Provider Assessment Requirements

| Assessment Area | Requirements |
|:----------------|:-------------|
| Data Handling | No training on customer data |
| API Security | TLS 1.3, secure API key management |
| Compliance | SOC 2, GDPR compliance |
| Data Residency | Regional processing options |
| Incident Response | Breach notification commitment |

### Provider Isolation

| Control | Implementation |
|:--------|:---------------|
| Credential Separation | Each provider has separate, rotated credentials |
| Request Isolation | No cross-provider request correlation |
| Response Isolation | Provider responses not shared across tenants |
| Failure Isolation | Provider failures don't cascade |

---

## Prompt Security

### Prompt Injection Defense

```
┌─────────────────────────────────────────────────────────────────────┐
│                    PROMPT INJECTION DEFENSE                          │
├─────────────────────────────────────────────────────────────────────┤
│  LAYER 1: INPUT PREPROCESSING                                       │
│  • Character filtering    • Length limits    • Encoding validation  │
├─────────────────────────────────────────────────────────────────────┤
│  LAYER 2: INJECTION DETECTION                                       │
│  • ML-based classifier    • Pattern matching    • Semantic analysis │
├─────────────────────────────────────────────────────────────────────┤
│  LAYER 3: PROMPT ARCHITECTURE                                       │
│  • Instruction hierarchy    • Delimiter separation    • Anchoring   │
├─────────────────────────────────────────────────────────────────────┤
│  LAYER 4: OUTPUT VALIDATION                                         │
│  • Format validation    • Action authorization    • Anomaly check   │
└─────────────────────────────────────────────────────────────────────┘
```

### Input Sanitization

| Control | Implementation |
|:--------|:---------------|
| Character Filtering | Whitelist allowed characters |
| Length Limits | 10,000 character limit per input |
| Encoding Validation | Reject malformed encoding |
| Pattern Detection | Regex + ML classifier |

### Instruction Hierarchy

| Level | Source | Authority |
|:------|:-------|:----------|
| System | Platform code | Highest (cannot be overridden) |
| Application | Component configuration | High |
| Context | Retrieved documents | Medium (clearly delimited) |
| User | User input | Lowest (sandboxed) |

---

## Data Protection in AI Pipelines

### PII Handling

**Pre-Processing (Before LLM):**

| Stage | Control |
|:------|:--------|
| Input Reception | PII detection scan |
| Context Retrieval | Access control enforcement |
| Prompt Assembly | PII redaction or tokenization |

**Post-Processing (After LLM):**

| Stage | Control |
|:------|:--------|
| Response Reception | PII detection scan |
| Content Filtering | Unexpected PII flagged |
| Response Delivery | Final PII scrubbing |

### Tenant Data Isolation

| Control | Implementation |
|:--------|:---------------|
| Namespace Isolation | Each tenant's data in separate namespace |
| Embedding Isolation | Tenant-specific vector collections |
| Query Filtering | Automatic tenant filter on all queries |
| Cache Isolation | Per-tenant response caching |

---

## Content Safety

### Input Content Filtering

| Filter Type | Detection Method | Action |
|:------------|:-----------------|:-------|
| Toxicity | ML classifier | Block + log |
| Hate Speech | ML classifier + keywords | Block + report |
| Illegal Content | Pattern matching + ML | Block + report |

### Output Content Filtering

| Filter Type | Detection Method | Action |
|:------------|:-----------------|:-------|
| Harmful Instructions | Pattern matching + ML | Redact or block |
| Personal Information | PII detection | Redact |
| Confidential Data | Classification check | Redact |

### Hallucination Mitigation

| Control | Implementation |
|:--------|:---------------|
| Grounding | Responses grounded in retrieved context |
| Citation | Required citations for factual claims |
| Confidence | Low-confidence responses flagged |
| Verification | Critical facts verified against knowledge base |

---

## Vector and Embedding Security

### Embedding Security

| Control | Implementation |
|:--------|:---------------|
| Encryption at Rest | AES-256-GCM for vector data |
| Encryption in Transit | TLS 1.3 for all connections |
| Access Control | Role-based access, no direct user access |
| Tenant Isolation | Separate collections per tenant |

### Retrieval Security

| Stage | Control |
|:------|:--------|
| Query Reception | User authentication verified |
| Similarity Search | Tenant filter applied automatically |
| Result Filtering | ACL check on each result |
| Context Assembly | Only accessible documents included |

---

## Audit Logging

### AI-Specific Events

| Event | Logged Data | Retention |
|:------|:------------|:----------|
| AI Request | User ID, request type, timestamp | 1 year |
| Input Processing | Input hash, sanitization actions | 1 year |
| LLM Invocation | Provider, model, token count, latency | 1 year |
| Output Processing | Filtering actions, content flags | 1 year |

### Security Events

| Event | Logged Data | Retention |
|:------|:------------|:----------|
| Injection Attempt | Input pattern, detection method, user ID | 2 years |
| Content Violation | Violation type, content hash, action taken | 2 years |
| Authorization Failure | Requested action, denial reason | 2 years |

---

## Responsible AI

### Ethical Principles

| Principle | Implementation |
|:----------|:---------------|
| Fairness | Bias detection and monitoring |
| Transparency | Clear AI involvement disclosure |
| Accountability | Clear ownership, audit trails |
| Privacy | Data minimization |
| Human-Centered | AI augments human judgment |

### Explainability

| Feature | Description |
|:--------|:------------|
| Source Attribution | Responses cite sources from knowledge base |
| Confidence Indication | AI indicates confidence level |
| Reasoning Transparency | Key reasoning steps exposed |
| Decision Logging | Automated decisions logged with rationale |

---

## Quality Assurance and Feedback

### Output Tracking Mechanisms

Model outputs are tracked through three complementary mechanisms:

| Mechanism | Description | Feedback Loop |
|:----------|:------------|:--------------|
| Ontology Review | Users validate auto-generated legal concepts | Refinement of extraction patterns |
| Dialogue Feedback | Response quality ratings on conversational outputs | Prompt optimization |
| Search Provenance | Trace results back to sources, verify grounding | Metadata and entity corrections |

### Quality Adjustment Mechanisms

When quality falls short, adjustments occur without traditional ML retraining:

| Adjustment Type | When Used | Implementation |
|:----------------|:----------|:---------------|
| Agent Logic Refinement | Specific extraction failures | Modify confidence thresholds, extraction patterns |
| Ontology Regeneration | Systemic quality issues | Ingest additional/updated domain sources |
| Prompt Engineering | Dialogue quality issues | Refine prompt templates and examples |
| Validation Rule Updates | Schema violations | Adjust validation constraints |

### Continuous Improvement

| Process | Description |
|:--------|:------------|
| Feedback Collection | Structured capture of user corrections |
| Root Cause Analysis | Identify patterns in quality failures |
| Targeted Intervention | Apply fixes to specific components |
| Validation Testing | Verify improvements on representative samples |

---

## Model Lifecycle Management

### Model Selection and Configuration

| Consideration | Options |
|:--------------|:--------|
| Provider Selection | Cloud APIs, self-hosted, enterprise offerings |
| Model Size | Balance accuracy vs. latency/cost |
| Specialization | General-purpose vs. domain-tuned models |
| Regional Compliance | Data residency requirements |

### Model-Agnostic Architecture

The Knowledge Fabric and agent infrastructure consume structured metadata outputs regardless of which LLM generated them:

| Benefit | Description |
|:--------|:------------|
| Provider Flexibility | Swap models without workflow changes |
| Best-of-Breed | Different models for different tasks |
| Cost Optimization | Route to appropriate model tier |
| Compliance Routing | Direct data to compliant providers |

### Model Deprecation

| Stage | Activities |
|:------|:-----------|
| Deprecation Notice | Advance warning before model retirement |
| Migration Path | Clear upgrade path to replacement model |
| Parallel Running | Both models available during transition |
| Validation Period | Extended testing before old model removal |

---
