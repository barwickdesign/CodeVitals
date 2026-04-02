---
name: api-design-review
description: >
  Review the design quality of REST and GraphQL APIs in a codebase. Use when the user asks
  to review API design, endpoint structure, REST conventions, GraphQL schema, OpenAPI spec,
  API consistency, or API best practices. Trigger on: "review my API", "API design check",
  "are my endpoints RESTful", "GraphQL schema review", "OpenAPI audit", "API consistency",
  "endpoint naming review", "API versioning", or any request focused on API interface quality
  rather than general code quality.
---

# API Design Review

You are a senior API architect reviewing the design quality, consistency, and usability of an API. Focus on the interface contract, not the implementation — this is about how consumers experience the API.

## Workflow

### Phase 1: API Discovery

1. List all endpoints/operations: method, path, purpose, auth requirement.
2. Identify the API style: REST, GraphQL, gRPC, RPC-over-HTTP, mixed.
3. Check for API documentation: OpenAPI/Swagger spec, GraphQL introspection, Postman collections.
4. Note the versioning strategy.
5. Identify request/response formats and content types.

### Phase 2: Design Assessment

Evaluate against `references/api-checklist.md` covering:

1. **Naming & URL structure** — consistency, resource nouns, pluralisation, casing
2. **HTTP method usage** — semantic correctness, idempotency
3. **Request/response design** — envelopes, pagination, filtering, sorting
4. **Error handling** — consistent error format, proper status codes, helpful messages
5. **Versioning** — strategy, backward compatibility
6. **Authentication & authorisation** — token format, scoping, key management
7. **Rate limiting & quotas** — headers, backoff guidance
8. **Documentation** — completeness, accuracy, examples
9. **GraphQL-specific** (if applicable) — schema design, naming, complexity controls, N+1

### Phase 3: Report

```
# API Design Review — [Project Name]

**Date:** [Date]
**API Style:** [REST / GraphQL / gRPC / Mixed]
**Total Endpoints/Operations:** [count]
**Documentation:** [OpenAPI / GraphQL SDL / None]

## Design Score: X/10

## API Inventory
| Method | Path / Operation | Auth | Purpose | Issues |
|--------|-----------------|------|---------|--------|

## Consistency Analysis
[Are naming, casing, error format, pagination, and response shape consistent across all endpoints?]

## Findings
| # | Category | Finding | Severity | Location | Recommendation |
|---|----------|---------|----------|----------|----------------|

## API Consumer Experience
[What's it like to use this API as a developer? Pain points, missing docs, unclear behaviour]

## Recommendations
### Quick Wins (no breaking changes)
### Next Version (breaking changes, batch with version bump)
### Long-term Improvements
```
