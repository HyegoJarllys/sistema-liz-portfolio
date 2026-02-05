**Architecture Overview**

Sistema LIZ adopts a cloud-native, serverless, and event-driven architecture, optimized for low-latency conversational workloads and high observability in regulated environments.

The architecture deliberately separates:

User-facing inference

Retrieval and grounding

Analytics and governance

This separation ensures that failures or spikes in one domain do not propagate to others.

**Architectural Goals**

The system architecture was designed to meet the following goals:

Predictable latency for conversational requests

Strong grounding and hallucination reduction

Horizontal scalability without manual intervention

Cost control through managed services

Observability and auditability by default

Minimal operational overhead

**High-Level Component Diagram (Conceptual)**
Client
  │
  ▼
Conversational API (Stateless)
  │
  ├─► Retrieval Layer (Document Search)
  │        │
  │        └─► Approved Knowledge Base
  │
  ├─► Language Model (Grounded Generation)
  │
  └─► Response to Client
           │
           ▼
   Event Publication (Async)
           │
           ▼
   Analytics Pipeline

This flow guarantees that analytics processing never blocks user responses.

*Component Responsibilities*
1. Conversational API

Role

Entry point for all user interactions

Stateless request handling

Enforcement of payload size and rate limits

Key Characteristics

Horizontally scalable

Short-lived request lifecycle

Explicit error contracts

2. Retrieval Layer (RAG)

Role

Semantic retrieval of relevant documents

Enforces document-level access constraints

Supplies grounding context to the language model

Design Decision

Retrieval is mandatory for every request

The model cannot answer outside retrieved content

This is the primary mechanism for hallucination reduction.

3. Language Model Layer

Role

Generates responses strictly constrained by retrieved context

Applies prompt-level safety and scope controls

Important Note

Prompt configurations and reasoning rules are proprietary and intentionally excluded from this repository

4. Asynchronous Analytics Pipeline

Role

Capture interaction metadata

Enable dashboards, reporting, and system monitoring

Support governance and cost attribution

Key Design Choice

Events are published after the user response is returned

Analytics failures do not impact inference availability

*Data Flow Separation*

The system enforces a strict separation between:

Flow Type	Characteristics
Inference	Synchronous, latency-sensitive
Analytics	Asynchronous, failure-tolerant

This separation avoids the common anti-pattern of coupling observability with user experience.

*Scalability Strategy*

Serverless compute for automatic horizontal scaling

Stateless services to simplify deployment

Safe minimum capacity to mitigate cold starts

Independent scaling for inference and analytics components

*Reliability & Fault Tolerance*

Timeouts and retries applied per dependency

Graceful degradation when retrieval or analytics are unavailable

Clear distinction between user-facing errors and internal failures

*Security Boundaries*

IAM-based service-to-service access

No secrets stored in source control

Clear trust boundary between public API and internal services

Analytics pipeline isolated from inference path

*Cost Control Considerations*

Architectural decisions were guided by cost predictability:

Managed services over self-hosted components

Asynchronous workloads for non-critical paths

Request-level cost attribution via analytics events

Ability to enforce quotas and rate limits upstream

**Trade-Offs & Rationale**
Decision	                               Trade-Off
Mandatory retrieval	Reduced flexibility  increased reliability
Serverless stack	                     Slight cold-start risk, lower ops cost
Async analytics	Eventual consistency     better UX
Managed AI services	Vendor lock-in       faster delivery

These trade-offs were intentionally chosen based on the target domain.

*What This Document Does Not Cover*

Infrastructure-as-code specifics

Prompt engineering details

Document ingestion pipelines

Institution-specific configurations

These topics are either proprietary or environment-dependent.

*Related Documentation*

System overview: docs/00-overview.md

Quickstart demo: docs/01-quickstart.md

API contract: docs/03-api.md

Analytics pipeline: docs/04-analytics.md

Security & LGPD: docs/05-security-lgpd.md