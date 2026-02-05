**Security & Privacy Overview**

Sistema LIZ was designed for environments where data protection, access control, and auditability are mandatory.

Security and privacy are treated as foundational architectural concerns, not as optional features layered on top of the system.

**Core Security Principles**

The system follows these guiding principles:

Least privilege
Each component has only the permissions strictly required for its role.

Separation of trust boundaries
User-facing components are isolated from internal services and analytics pipelines.

Defense in depth
Multiple layers of control exist to reduce blast radius in case of failure.

No implicit trust
All service-to-service communication is authenticated and authorized.

**Data Privacy by Design**
Data Minimization

The system intentionally limits data collection to what is strictly necessary:

No personal identifiers (names, emails, documents) are stored

User interactions are associated only with anonymous or hashed identifiers

No long-term conversational state is persisted

Purpose Limitation

Collected data is used exclusively for:

System operation

Performance monitoring

Cost analysis

Service improvement

Analytics data is not repurposed for user profiling or behavioral tracking.

**User Identification Strategy**
Aspect	                 Approach
User ID	                 Client-provided, anonymous or hashed
PII Storage	             Not allowed
Message Retention      	Disabled or strictly limited
Analytics Linking   	Aggregated, non-identifiable

Clients are explicitly responsible for ensuring that user_id values do not contain personal data.

**LGPD Alignment**

Sistema LIZ aligns with the following LGPD principles:

Adequacy: Data usage aligns with the system’s stated purpose

Necessity: Only minimal data is collected

Transparency: System behavior is explainable and auditable

Security: Technical and organizational safeguards are applied

Prevention: Architecture reduces the likelihood of data misuse

**Access Control & IAM**

IAM roles are scoped per service

No shared credentials between components

Secrets are managed externally and never committed to source control

Analytics access is restricted to authorized roles

This reduces lateral movement risk and simplifies auditing.

**Network & Infrastructure Security**

Public access is limited to the API gateway or entry service

Internal services communicate over private channels

No direct external access to analytics or storage layers

Infrastructure details are environment-specific and intentionally abstracted.

**Logging & Auditability**

Logs are structured and scoped per component

Sensitive content is excluded from logs

Security-relevant events are traceable

Audit trails support incident investigation without exposing user data

**Failure & Incident Considerations**

The system is designed to fail safely:

Security failures do not expose internal data

Analytics outages do not affect inference availability

Errors returned to clients are sanitized and non-informative

**What Is Explicitly Out of Scope**

This public documentation does not include:

Encryption key management details

Internal network topology

Production IAM role definitions

Security incident response playbooks

These elements are environment-specific and restricted by design.

**Why This Matters in Regulated Environments**

By embedding privacy and security at the architectural level, Sistema LIZ:

Reduces compliance risk

Simplifies audits

Increases institutional trust

Enables safe scaling across departments or clients

**Related Documentation**

Analytics & governance: docs/04-analytics.md

Operations & observability: docs/07-ops-observability.md

Architecture decisions: docs/02-architecture.md

FAQ: docs/09-faq.md