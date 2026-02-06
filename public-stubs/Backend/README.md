# Backend (Public Stub)

This folder is a **public structural stub** of the Sistema LIZ backend.

It exists to demonstrate:
- architectural organization
- responsibilities by module
- production-minded layering

This repository intentionally excludes:
- proprietary prompts
- internal heuristics and classifiers
- production configs and secrets
- client-specific datasets and ingestion code

The real implementation is maintained in a private repository.

---

## Responsibilities

The backend is responsible for:

- Receiving user requests (`/chat`)
- Running retrieval (RAG) against a managed document index
- Calling the LLM with grounded context
- Returning a structured response with source references
- Emitting analytics events asynchronously (non-blocking)
- Producing structured logs for observability

---

## High-Level API Contract

Request (conceptual):
- `message` (or `mensagem`)
- `user_id` (anonymous / hashed)

Response (conceptual):
- `response` (or `resposta`)
- `sources` (list of grounded documents)

See: `docs/03-api.md` and `demo/`

---

## Key Design Notes (Public)

- Stateless request handling (scale horizontally)
- Mandatory retrieval for grounding
- Async analytics emission after response delivery
- No PII stored; privacy-by-design

See: `docs/02-architecture.md`, `docs/04-analytics.md`, `docs/05-security-lgpd.md`

---

## Repository Mapping

The file `pseudo_structure.txt` describes the intended production-grade folder layout and module boundaries.