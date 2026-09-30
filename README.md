# Npontu Trust

**Npontu Trust** is an in-house KYC/AML orchestration platform designed to provide identity verification, business verification, AML screening, crypto wallet screening, case management, and auditable verification decisions.

The initial implementation is focused on **Ghana**, with the architecture designed to support future expansion into **Nigeria and Kenya**.

## Overview

Npontu Trust is being built to replace Npontu's dependence on third-party KYC/AML verification services and provide greater control over:

- Verification workflows
- Identity and business verification
- AML screening
- Evidence and decision management
- Provider integrations
- Case management
- Audit trails
- Usage and verification costs

The MVP follows a **screening-first** approach built around the core flow:

**Capture → Verify → Screen → Decide**

---

## MVP Features

### KYC — Identity Verification

- Ghana Card verification
- Passport verification
- Document image capture
- Liveness/biometric capture
- NIA-backed identity verification
- NFC Passive Authentication where supported
- Optical/OCR fallback
- Server-side re-verification

### KYB — Business Verification

- Ghana business registry lookup
- Business registration verification
- Business-related verification data

### AML & Screening

- Sanctions screening
- PEP screening
- Adverse-media screening
- Crypto wallet/blockchain-address screening
- Africa-tuned name matching
- Periodic/continuous re-screening

### Decisioning

The platform produces explicit verification outcomes:

- `ALLOW`
- `REVIEW`
- `BLOCK`

Every decision must include a reason code and maintain an auditable record.

### Case Management

The operations console provides:

- Case list
- Evidence review
- Audit trail
- Flagged applicant review
- Manual decision handling

### Developer Platform

- Tenant-scoped REST API
- Verification sessions
- API authentication
- Webhooks
- HMAC-SHA256 signed webhook payloads
- Usage analytics
- Cost tracking

---

## Architecture

Npontu Trust is organized into seven layers:

| Layer | Responsibility |
|---|---|
| 1. Client | Web/mobile capture and biometric capture |
| 2. API / Tenant Boundary | Authentication and tenant-scoped APIs |
| 3. Workflow Orchestrator | Verification sequencing and retries |
| 4. Provider Adapter Layer | Integrations with external verification providers |
| 5. Evidence & Decision Services | Evidence storage, policy engine and decisions |
| 6. Operations & Customer Integration | Case review, audit trail, webhooks and analytics |
| 7. Security & Reliability | Encryption, RBAC, logging and reliability |

The provider adapter layer is designed to keep external providers replaceable and reduce vendor lock-in.

---

## Technology Stack

The project recommends the following stack:

| Area | Technology |
|---|---|
| Backend/API | Node.js + TypeScript or Python + FastAPI |
| Database | PostgreSQL |
| Frontend | React + TypeScript |
| Evidence Storage | S3-compatible encrypted object storage |
| Queue/Orchestration | Redis-backed or SQS-style message queue |
| Webhooks | HMAC-SHA256 |
| Observability | Structured logging + metrics |
| Client Capture | TypeScript/React web SDK |

The backend choice between Node.js/TypeScript and Python/FastAPI is intended to be confirmed against the team's existing engineering experience.

---

## Core Entities

The main system entities include:

- Tenant
- Applicant
- VerificationSession
- Check
- ProviderAdapter
- Evidence
- Decision
- Case
- Webhook
- AuditLog

These entities form the foundation of the verification, decisioning, case-management, and audit workflows.

---

## External Integrations

The platform is designed around provider adapters so individual vendors can be replaced without restructuring the core platform.

Potential integrations include:

- **NIA** — Ghana Card identity verification
- Ghana business registry
- Document/biometric verification providers
- Sanctions/PEP/adverse-media providers
- Crypto screening providers

Candidate providers identified in the project requirements include providers such as Smile ID, Sumsub, Jumio, Onfido, Chainalysis, Notabene, and sanctions-data providers.

Provider selection is subject to the discovery, legal, technical, and commercial requirements defined in the project plan.

---

## Security & Compliance

Security and compliance are core parts of the platform architecture.

The requirements include:

- Tenant isolation
- Role-based access control
- Encryption
- Secure evidence storage
- Signed webhooks
- Audit logging
- Structured system logging
- Data-processing agreements for production providers
- DPC-compliant processing records
- Traceable verification decisions

The project also targets groundwork for future **SOC 2 Type II / ISO 27001 readiness**.

---

## API

The platform exposes a tenant-scoped REST API.

The initial API structure includes verification session operations such as:

```text
/v1/sessions
```

The API is intended to support:

1. Session creation
2. Applicant verification
3. Verification checks
4. Decision retrieval
5. Webhook notifications
6. Evidence and case workflows

All API endpoints must remain tenant-scoped.

---

## Verification Flow

A typical verification workflow follows:

```text
Applicant
    ↓
Client Capture SDK
    ↓
Verification Session
    ↓
Workflow Orchestrator
    ↓
Provider Adapters
    ├── Document/Biometric Verification
    ├── NIA Verification
    ├── Business Registry
    ├── Sanctions / PEP / Adverse Media
    └── Crypto Screening
    ↓
Evidence
    ↓
Policy Engine
    ↓
ALLOW / REVIEW / BLOCK
    ↓
Case & Audit Trail
    ↓
Webhook / API Response
```

---

## Roadmap

The project is planned around **13 two-week sprints**, from Sprint 0 through Sprint 12, organized around four gates.

### Sprint 0 — Discovery & Setup

- NIA access process
- DPC registration
- Provider selection
- Repository and CI/CD setup
- Development and staging environments
- Technology-stack confirmation

**Gate 1 — Customer & Legal Discovery**

---

### Sprints 1–2 — Foundation

- Tenant management
- Authentication
- RBAC
- Core database schema
- Verification session API

### Sprints 3–4 — Core Verification

- Web capture SDK
- Document/biometric provider
- NIA integration
- Server-side re-verification
- NFC Passive Authentication
- HMAC webhook delivery

### Sprints 5–6 — Policy & Decisioning

- Policy engine
- `ALLOW / REVIEW / BLOCK` decisions
- Reason codes
- Evidence storage
- Operations console
- KYB registry integration
- Usage and cost analytics

### Sprint 7 — Screening

- Sanctions screening
- PEP screening
- Adverse-media screening
- Crypto wallet screening
- Name matching
- Re-screening workflows

### Sprint 8 — Gate 2

**Thin Vertical Prototype**

Run the complete flow:

```text
Capture → NIA → Screening → Decision
```

against one low-volume internal client in parallel with the existing provider.

### Sprints 9–10 — Hardening & Compliance

- DPC processing records
- Provider data-processing agreements
- Full RBAC
- Native mobile SDKs
- goAML-format SAR/STR module
- Self-service pricing
- Sandbox

### Sprint 11 — Gate 3

**Measured Pilot**

Expand to the broader Ghana client base and measure:

- Verification accuracy
- Turnaround time
- Cost per completed verification

### Sprint 12 — Gate 4

**Commercial Readiness**

- SLA/uptime commitments
- Security/compliance review
- SOC 2 / ISO 27001 groundwork
- Transika migration proposal

---

## MVP Scope

The MVP is intended to prove the complete verification loop for one internal, lowest-volume workflow before broader rollout.

### Included

- KYC
- KYB
- NIA verification
- Document/biometric verification
- NFC Passive Authentication
- Sanctions/PEP/adverse-media screening
- Crypto screening
- Policy decisions
- Case management
- Evidence management
- Audit trails
- Webhooks
- Usage/cost analytics
- Tenant/API infrastructure

### Later / Fast-Follow

The requirements identify several capabilities for later phases, including:

- No-code workflow builder
- Native mobile SDKs
- Customer-facing dashboard
- goAML SAR/STR filing
- Self-service pricing
- Always-on sandbox
- Additional country/document coverage

---

## Project Status

Npontu Trust is currently in the **planning and foundation stage**, with the PRD, requirements specification, architecture, technology recommendations, and sprint roadmap defined.

The next implementation phase is the **Discovery & Setup sprint**, including repository setup, CI/CD, environments, provider discovery, and confirmation of the final technology stack.

---

## Project Documents

The project documentation includes:

- `Npontu Trust - PRD.md`
- `Npontu Trust - Requirements SRS.md`
- `Npontu Trust - Sprint Plan.md`

These documents define the product requirements, technical requirements, architecture, and delivery roadmap.
