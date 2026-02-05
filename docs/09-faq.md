**Frequently Asked Questions (FAQ)**
Is this a production system or a proof of concept?

This system was designed and operated with production constraints in mind.
The public repository represents a sanitized portfolio version, while production deployments include additional configurations, safeguards, and proprietary components.

**Why use Retrieval-Augmented Generation (RAG) instead of a pure LLM?**

Because the target domain prioritizes:

Accuracy

Traceability

Auditability

RAG ensures that responses are grounded in approved documents, reducing hallucinations and enabling governance.
Pure generative approaches were intentionally avoided.

**Does the system store user conversations?**

No.

No long-term conversational state is persisted

No personal data is stored

Analytics capture only minimal, anonymized metadata

This design aligns with privacy-by-design principles.

**How is latency kept low with analytics enabled?**

Analytics processing is fully asynchronous.

User responses are returned immediately

Analytics events are emitted after response delivery

Failures in analytics do not impact user experience

This separation is a deliberate architectural decision.

What happens if a downstream service fails?

The system is designed to fail gracefully:

Retrieval or analytics failures do not crash the API

Errors are isolated to their respective components

Clear, non-informative error messages are returned to clients

This prevents cascading failures.

**Is the system stateful?**

No.

The API is stateless

Each request is processed independently

Any conversational context must be handled client-side

This simplifies scaling and reduces operational complexity.

**How does the system handle scalability?**

Scalability is achieved through:

Serverless components

Horizontal scaling

Stateless request handling

Independent scaling of inference and analytics paths

There is no need for manual capacity planning.

**How are costs controlled?**

Cost control is achieved through:

Pay-per-use services

Mandatory retrieval to limit token usage

Asynchronous processing for non-critical workloads

Monitoring and alerting on usage thresholds

Detailed cost modeling is documented separately.

**Why are some implementation details missing?**

This repository is a portfolio showcase, not a full open-source release.

Intentionally excluded elements include:

Proprietary prompts

Internal heuristics

Production credentials

Client-specific configurations

This protects intellectual property and security.

**Can this system be adapted to other domains?**

Yes.

The architecture is domain-agnostic and can be adapted to:

Internal knowledge bases

Regulated industries

Institutional support systems

Adaptation primarily involves document curation and governance rules.

What are the main limitations?

Responses are limited to indexed documents

Answer quality depends on document quality

The system is not designed for creative or speculative outputs

These limitations are intentional.

**Is this system open to further development?**

Yes.

The roadmap outlines incremental and governed evolution, prioritizing:

Stability

Observability

Compliance

Cost predictability

**Related Documentation**

System overview: docs/00-overview.md

Architecture: docs/02-architecture.md

Analytics: docs/04-analytics.md

Security & privacy: docs/05-security-lgpd.md

Roadmap: docs/08-roadmap.md

**Final Note**

This FAQ exists to remove ambiguity.

If a question is not answered here, it is likely:

Environment-specific

Proprietary

Or intentionally abstracted for security reasons