# Sanitization Checklist (Public Release)

Use this checklist before publishing updates to the public repository.

## Identifiers & Endpoints
- [ ] No real Cloud Run URLs (use `https://<backend-host>/...`)
- [ ] No GCP project IDs, dataset/table IDs, datastore IDs
- [ ] No topic/subscription names tied to real deployments

## Secrets & Credentials
- [ ] No API keys, tokens, `.env` files
- [ ] No service account emails, JSON credentials, or key paths

## Customer Data & Documents
- [ ] No real municipal/institution documents
- [ ] No names of clients, locations, or contract terms
- [ ] No internal policies that reveal sensitive operations

## Code & IP
- [ ] No full prompts or proprietary prompt chains
- [ ] No internal heuristics, scoring, or classifiers
- [ ] No ingestion/indexing scripts used in production

## Logs & Examples
- [ ] Examples contain no PII and no real identifiers
- [ ] Sample responses are generic and sanitized
- [ ] Error examples do not reveal internal topology

## Final Verification
- [ ] Repository search for: `apikey`, `token`, `secret`, `project`, `dataset`, `datastore`, `gcr.io`, `run.app`
- [ ] Confirm placeholders are used consistently