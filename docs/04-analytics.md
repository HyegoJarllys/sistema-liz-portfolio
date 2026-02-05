**Analytics Overview**

Sistema LIZ was designed with analytics as a first-class concern, not as an afterthought.

The analytics layer exists to support:

Operational visibility

Governance and auditing

Cost attribution

Continuous system improvement

A key architectural requirement is that analytics must never impact user-facing latency or availability.

**Design Principles**

The analytics pipeline follows these principles:

Asynchronous by default
No analytics processing blocks the conversational response.

Minimal data collection
Only metadata strictly necessary for analysis is captured.

Privacy-first
No personal or identifiable user data is stored.

Operational usefulness
Metrics are collected with clear questions in mind, not “just in case”.

*Analytics Flow (Conceptual)*

The user request is processed and a response is returned.

After the response is delivered, an interaction event is emitted.

The event is processed asynchronously by the analytics pipeline.

Aggregated data is stored for reporting and dashboards.

Failures in this flow do not affect the conversational API.

*Event Model (Abstracted)*

Each interaction generates a single analytics event containing:

Field	        Description
timestamp	    Request completion time
request_type	Type or category of interaction
response_status	Success or error outcome
latency_ms  	End-to-end response time
source_count	Number of documents used
cost_estimate	Approximate cost attribution
user_id	Anonymous or hashed identifier

Exact schemas and field names are environment-specific and intentionally omitted.

*Key Metrics Collected*
Usage Metrics

Total requests per period

Requests per channel or integration

Peak usage windows

Performance Metrics

Average and percentile latencies (p50 / p95)

Error rates by status code

Cold start impact (where applicable)

Quality Indicators

Responses with zero retrieved sources

High fallback or error frequencies

Document coverage gaps

Cost Metrics

Estimated cost per request

Cost distribution by usage pattern

High-cost outlier detection

*Dashboards & Reporting*

Analytics data enables dashboards for different stakeholders:

Operational Dashboards

System health and availability

Error and latency trends

Traffic spikes and anomalies

Management Dashboards

Usage growth

Cost trends

Topic frequency and demand patterns

These dashboards support data-driven decisions, not manual inspection.

*Privacy & Compliance Considerations*

No raw user messages are persisted

User identifiers are anonymized or hashed

Analytics data is retained only for operational purposes

Data access is restricted by role and purpose

This design aligns with data minimization and purpose limitation principles.

*Failure Handling*

The analytics pipeline is designed to be failure-tolerant:

Event publication failures are logged but ignored by the API

Temporary analytics outages do not degrade user experience

Backpressure is handled through asynchronous buffering

*Why This Matters*

By decoupling analytics from inference, the system achieves:

Predictable response times

Safer experimentation and iteration

Clear operational insight without architectural risk

This approach avoids a common anti-pattern where monitoring becomes a source of instability.

*Related Documentation*

API Contract: docs/03-api.md

Architecture: docs/02-architecture.md

Operations & Observability: docs/07-ops-observability.md

Security & LGPD: docs/05-security-lgpd.md