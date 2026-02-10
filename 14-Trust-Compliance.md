---
layout: default
title: Trust & Compliance
---

# LegalFab Trust & Compliance

**Version:** 1.0
**Last Updated:** February 2026

---

## Overview

This document describes how LegalFab managed deployments (SaaS and Dedicated Cloud Tenant) are operated to meet customer security, regulatory, and compliance requirements. For self-hosted deployment options, see [02-Architecture](./02-Architecture.md) and [13-Operating-Costs](./13-Operating-Costs.md).

---

## 1. Shared Responsibility Model

LegalFab operates under a clear shared responsibility model that delineates security and compliance obligations between LegalFab and the customer.

### Responsibility Matrix

| Domain | LegalFab Responsibility | Customer Responsibility |
|:-------|:------------------------|:------------------------|
| **Infrastructure** | Platform hosting, patching, availability | N/A (managed by LegalFab) |
| **Application Security** | Code security, vulnerability management, updates | N/A (managed by LegalFab) |
| **Data Security** | Encryption at rest/transit, secure storage | Data classification decisions, sensitivity tagging |
| **Access Control** | RBAC framework, authentication infrastructure | User provisioning, role assignment, access policies |
| **Identity** | SSO integration support, MFA enforcement | IdP configuration, user lifecycle management |
| **Compliance** | Platform compliance (SOC 2, infrastructure controls) | Business process compliance, regulatory interpretation |
| **Monitoring** | Platform monitoring, security alerting | Review of reports, response to customer-specific alerts |
| **Incident Response** | Detection, containment, platform remediation | Customer notification response, business impact assessment |
| **Data Residency** | Region configuration, data location controls | Residency requirements definition |
| **Retention** | Retention policy enforcement mechanisms | Retention policy definition per business/regulatory needs |

### Joint Responsibilities

| Activity | Collaboration Model |
|:---------|:--------------------|
| Security Incident Response | LegalFab leads technical response; customer informed per SLA; joint post-incident review |
| Compliance Evidence | LegalFab provides platform evidence; customer provides business process evidence |
| Risk Assessment | LegalFab provides platform risk posture; customer assesses business risk |
| Audit Support | LegalFab provides SOC 2 reports and attestations; supports customer audit requests |

---

## 2. Security Operations

### Continuous Security Management

| Activity | Frequency | Description |
|:---------|:----------|:------------|
| Vulnerability Scanning | Daily | Automated scanning of infrastructure and application components |
| Penetration Testing | Annual (minimum) | Third-party penetration testing with customer report availability |
| Patch Management | Per severity SLA | Critical: 24-72 hours; High: 7 days; Medium: 30 days |
| Security Monitoring | 24/7 | Continuous monitoring via Security Operations Center |
| Threat Intelligence | Continuous | Integration with threat intelligence feeds |

### Patch Management SLAs

| Severity | Description | Remediation Timeline |
|:---------|:------------|:---------------------|
| Critical | Active exploitation, data breach risk | 24-72 hours |
| High | Significant vulnerability, no active exploit | 7 days |
| Medium | Moderate risk, limited exposure | 30 days |
| Low | Minimal risk, defense-in-depth measure | Next release cycle |

### Incident Response

| Severity | Definition | Response SLA | Customer Notification |
|:---------|:-----------|:-------------|:----------------------|
| P1 - Critical | Active breach, service outage | 1 hour | Immediate (within 1 hour) |
| P2 - High | Potential breach, degraded service | 4 hours | Within 4 hours |
| P3 - Medium | Security event, no immediate impact | 8 hours | Next business day |
| P4 - Low | Minor issue, process improvement | 24 hours | Included in periodic reports |

### Incident Communication

| Phase | Communication |
|:------|:--------------|
| Detection | Initial notification to customer security contact |
| Investigation | Regular updates (hourly for P1, daily for P2) |
| Resolution | Resolution summary with root cause |
| Post-Incident | Detailed post-incident report within 5 business days |

---

## 3. Compliance Management

### Continuous Compliance

| Framework | Status | Evidence |
|:----------|:-------|:---------|
| SOC 2 Type II | Certified | Annual audit report available under NDA |
| UK GDPR | Compliant | DPA executed, Article 32 measures documented |
| Cyber Essentials Plus | Aligned | Self-assessment documentation available |
| ISO 27001 | Aligned | Control mapping available |

### Compliance Activities

| Activity | Frequency | Output |
|:---------|:----------|:-------|
| Internal Audit | Quarterly | Internal audit findings and remediation tracking |
| External Audit (SOC 2) | Annual | SOC 2 Type II report |
| Penetration Test | Annual | Third-party penetration test report |
| Compliance Review | Quarterly | Compliance status dashboard |
| Policy Review | Annual | Updated security policies |

### Regulatory Change Management

| Activity | Process |
|:---------|:--------|
| Regulatory Monitoring | Continuous monitoring of UK/EU regulatory developments |
| Impact Assessment | Assessment of new regulations on platform and customers |
| Customer Communication | Notification of material regulatory changes |
| Platform Updates | Implementation of required compliance changes |

### Audit Support

| Support Type | Description |
|:-------------|:------------|
| SOC 2 Report | Annual Type II report provided under NDA |
| Compliance Questionnaires | Response to customer security questionnaires |
| Evidence Requests | Specific control evidence upon request |
| Auditor Access | Read-only access for customer auditors (with approval) |

---

## 4. Customer-Specific Controls

### Identity Integration

| Capability | Description |
|:-----------|:------------|
| SSO Integration | SAML 2.0 and OIDC integration with customer IdP |
| MFA Enforcement | Multi-factor authentication required for all users |
| Conditional Access | Support for customer conditional access policies |
| Session Management | Configurable session timeouts and controls |

### Access Control Alignment

| Control | Customer Configuration |
|:--------|:-----------------------|
| Role Definitions | Custom roles aligned to customer organizational structure |
| Permission Sets | Granular permissions per customer security policies |
| Segregation of Duties | Configurable controls to prevent conflicting access |
| Access Reviews | Quarterly access review reports for customer validation |

### Data Protection Configuration

| Control | Customer Options |
|:--------|:-----------------|
| Data Residency | UK-only, EU-only, or customer-specified region |
| Encryption Keys | LegalFab-managed or customer-managed keys (BYOK) |
| Data Classification | Custom classification schemes per customer taxonomy |
| Retention Policies | Configurable retention aligned to customer requirements |

### Integration Security

| Integration Type | Security Controls |
|:-----------------|:------------------|
| Customer IdP | Encrypted SAML assertions, signed responses |
| Customer SIEM | Encrypted log forwarding, configurable event types |
| Customer Systems (MCP) | OAuth 2.0, mTLS, credential vault integration |

---

## 5. Governance & Transparency

### Dedicated Support

| Role | Responsibility |
|:-----|:---------------|
| Account Manager | Primary business relationship and escalation |
| Security Contact | Security-specific inquiries and incident communication |
| Technical Contact | Platform configuration and integration support |

### Transparency Mechanisms

| Mechanism | Description |
|:----------|:------------|
| Service Status | Real-time platform status dashboard |
| Planned Maintenance | 7-day advance notice for scheduled maintenance |
| Security Advisories | Proactive notification of relevant security issues |
| Subprocessor List | Published list of subprocessors with change notification |

### Change Management

| Change Type | Customer Notification |
|:------------|:----------------------|
| Security Patches | Applied per SLA; notification for customer-impacting changes |
| Feature Updates | Release notes published; opt-in preview for major features |
| Infrastructure Changes | 7-day notice for changes affecting availability |
| Subprocessor Changes | 30-day notice before engaging new subprocessors |

### Periodic Reviews

| Review Type | Frequency | Participants |
|:------------|:----------|:-------------|
| Service Review | Quarterly | Account Manager, Customer stakeholders |
| Security Review | Quarterly (optional) | Security teams from both parties |
| Compliance Review | Annual | Compliance/legal teams |

### Reporting

| Report | Frequency | Content |
|:-------|:----------|:--------|
| Service Report | Monthly | Availability, performance, usage metrics |
| Security Summary | Quarterly | Security posture, incidents, vulnerabilities addressed |
| Compliance Status | Annual | Compliance certifications, audit results |
| Access Audit | Quarterly | User access summary for customer review |

---

## Summary

LegalFab's managed service operations ensure customer security, regulatory, and compliance requirements are met through:

- **Clear Responsibility Model**: Defined boundaries between LegalFab and customer obligations
- **Continuous Security Operations**: 24/7 monitoring, proactive vulnerability management, defined incident response
- **Compliance Assurance**: SOC 2 Type II certification, regulatory alignment, audit support
- **Customer-Specific Controls**: SSO integration, configurable access controls, data residency options
- **Transparent Governance**: Regular reviews, proactive communication, change notification

For detailed technical security controls, see [07-Security-Operations](./07-Security-Operations.md) and [10-System-Compliance](./10-System-Compliance.md).

---
