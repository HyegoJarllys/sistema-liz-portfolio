**System Overview**

Sistema LIZ is a production-oriented AI assistant designed for public service and institutional environments, where accuracy, traceability, and governance are mandatory.

The system combines Retrieval-Augmented Generation (RAG) with a cloud-native, serverless architecture, ensuring that all responses are grounded in validated documents while remaining scalable and cost-efficient.

This document provides a conceptual and functional overview of the system, independent of implementation details.

**Design Principles**

The system was built around the following principles:

Accuracy over creativity
Responses must be derived strictly from approved documents.

Separation of concerns
Conversational inference, retrieval, and analytics are isolated to avoid cross-impact.

Low latency for users
All non-essential processing is handled asynchronously.

Operational transparency
Every interaction can be analyzed, monitored, and audited.

Privacy by design
No personally identifiable information is persisted.

*High-Level Functional Flow*

At a conceptual level, the system operates as follows:

A user submits a message through a conversational interface.

The backend receives the request and performs a retrieval step against a curated document index.

Relevant documents are injected into the prompt context.

A large language model generates a response constrained to the retrieved content.

The response is returned synchronously to the user.

Interaction metadata is published asynchronously for analytics and governance.

This flow ensures predictable behavior, controlled outputs, and non-blocking observability.

**Core System Components**

*Conversational API*

Stateless HTTP endpoint

Handles user requests and responses

Designed for horizontal scalability

Enforces payload limits and rate control

*Retrieval Layer (RAG)*

Managed document index with semantic search

Only approved documents are eligible for retrieval

Retrieval results are explicitly passed to the language model

*Language Model Layer*

Generates responses using retrieved context

Configured to avoid speculative or out-of-scope answers

Operates under strict prompt constraints (not exposed publicly)

*Asynchronous Analytics Pipeline*

Interaction events are published after response delivery

Analytics processing does not affect user latency

Enables usage tracking, quality monitoring, and cost attribution

**Non-Functional Characteristics**

*Scalability*

Fully serverless design

Automatic horizontal scaling

Safe minimum capacity for predictable cold-start behavior

*Reliability*

Graceful degradation on dependency failures

Clear error contracts for client applications

Retry and timeout strategies applied per component

*Security*

IAM-based access control

No secrets embedded in source code

Clear boundary between public API and internal services

*Intended Use Cases*

Citizen support and information services

Internal institutional assistants

Knowledge base querying for regulated domains

Operational dashboards driven by conversational usage

The system is not designed for open-ended chat or creative generation.

*Known Constraints*

Responses are limited to the scope of indexed documents

System behavior depends on document quality and coverage

Analytics reflect usage patterns, not user intent or identity

These constraints are intentional and aligned with governance requirements.

**Relationship to Other Documents**

Getting started and demos: docs/01-quickstart.md

Detailed architecture and trade-offs: docs/02-architecture.md

API contract: docs/03-api.md

Analytics and dashboards: docs/04-analytics.md

Security and LGPD considerations: docs/05-security-lgpd.md