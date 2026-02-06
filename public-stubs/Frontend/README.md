# Frontend (Public Stub)

This folder is a **public structural stub** of the Sistema LIZ frontend.

It demonstrates:
- integration patterns with the backend `/chat` endpoint
- safe handling of anonymous user identifiers
- UI flow for institutional service scenarios

The real UI implementation may vary by deployment (web widget, Streamlit, admin panels, etc.).
No production URLs or secrets are included.

---

## Responsibilities

- Collect user questions in a simple interface
- Generate and persist an anonymous `user_id` client-side
- Call the backend API (`POST /chat`)
- Render the response and (optionally) sources
- Provide basic user feedback on errors (429/503)

---

## UX Notes (Institutional)

- Neutral and respectful tone
- Clear error messages without exposing internal details
- Optional escalation guidance (e.g., contact official channels)

---

## Repository Mapping

The file `pseudo_structure.txt` describes a clean frontend structure suitable for multiple UI implementations.