# RSS Feed Reader Constitution

## Core Principles

### I. Security-First Input Handling
Validate all user inputs strictly. All feed URLs and user-provided data MUST be sanitized before processing. In MVP, assume URLs are valid but reject obviously malformed input. For Extended-MVP and beyond, implement proper URL validation and feed content sanitization. Never trust external feed data; implement safe parsing with error boundaries.

### II. Incremental Delivery with Clear Scope
Build MVP first (subscription management only) before adding complexity. Each phase clearly defines what is IN scope and what is DEFERRED. MVP must not include feed fetching, parsing, persistence, or removal capabilities—these belong in Extended-MVP or post-MVP. This discipline keeps development fast and prevents scope creep.

### III. Code Quality Through Testing and Clarity
Unit tests MUST cover core business logic (subscription management, API contracts). Integration tests MUST verify API communication and feed parsing (Extended-MVP phase). Tests are written before or alongside implementation. Code MUST be readable: clear variable names, small focused methods, separation of concerns between backend (API, data) and frontend (UI, state).

### IV. Separation of Concerns: Backend and Frontend
Backend (ASP.NET Core Web API) handles data management and (in Extended-MVP) feed operations. Frontend (Blazor WebAssembly) handles UI and user interaction. Each layer MUST be independently testable. API contracts are explicit and versioned. Frontend MUST never directly fetch or parse feeds—all complex operations go through the backend.

### V. Maintainability Through Simplicity (YAGNI)
Start simple: in-memory storage for MVP, no premature optimization or extra features. Add complexity only when extending to the next phase. Keep dependencies minimal. All architectural decisions MUST be documented with rationale. Code reviews MUST verify adherence to these principles.

## Architecture and Technology Stack

ASP.NET Core Web API backend with Blazor WebAssembly frontend. This combination enables rapid MVP development while supporting future production enhancements (persistence, background polling, advanced features). Both technologies are cross-platform (Windows, macOS, Linux) and use C#, allowing code sharing where appropriate.

### Backend Responsibilities (MVP)
- Expose REST API endpoints for subscription management
- Store subscriptions in memory (List<string> model)
- Return subscription list to frontend
- Handle CORS for frontend access

### Frontend Responsibilities (MVP)
- Simple UI with input field to add subscription by URL
- Display subscription list
- API communication (add, retrieve subscriptions)

### Phase 2 (Extended-MVP) Additions
Backend adds feed fetching, parsing (System.ServiceModel.Syndication), and item retrieval.  
Frontend adds manual refresh button and item display (title and link).

## Development Workflow and Quality Gates

1. **Before Implementation**: Specification and task planning MUST align with MVP scope and principles.
2. **During Development**: Code changes MUST include unit tests for business logic. API contracts MUST be tested. Configuration (e.g., CORS, backend URL) MUST be verified before testing.
3. **Pre-Commit**: All tests MUST pass. No merge of incomplete features outside the current phase scope.
4. **Documentation**: Phase 2 (Blazor template cleanup) MUST be completed and verified before any UI implementation.

## Governance

This constitution supersedes conflicting practices. Amendments require documentation of rationale and migration plan. All new features MUST verify compliance with these principles. Deviations require explicit justification. This document is the source of truth for project governance; when ambiguous, escalate to stakeholder discussion rather than deciding independently.

**Version**: 1.0.0 | **Ratified**: 2026-05-10 | **Last Amended**: 2026-05-10
