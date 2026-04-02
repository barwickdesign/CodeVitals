# API Design Checklist

## Naming & URL Structure
- Resource names are nouns, not verbs (/users not /getUsers)
- Consistent pluralisation (/users not mix of /user and /users)
- Consistent casing (kebab-case or camelCase, not both)
- Logical nesting for related resources (/users/:id/orders)
- Nesting depth ≤ 3 levels
- No trailing slashes (or consistently one way)
- No file extensions in URLs
- Query params for filtering, body for creation/updates

## HTTP Methods
- GET for reads (no side effects, cacheable)
- POST for creation (returns 201 + Location header)
- PUT for full replacement (idempotent)
- PATCH for partial updates
- DELETE for removal (idempotent, 204 or 200)
- No state changes on GET
- OPTIONS for CORS preflight

## Status Codes
- 200 for successful read/update
- 201 for successful creation
- 204 for successful deletion (no body)
- 400 for client validation errors
- 401 for unauthenticated requests
- 403 for unauthorised requests
- 404 for missing resources
- 409 for conflicts (duplicate creation, version mismatch)
- 422 for semantically invalid input
- 429 for rate limiting
- 500 for server errors (never leak internals)

## Request & Response Design
- Consistent response envelope (or consistent lack of one)
- Pagination: cursor-based preferred, offset acceptable; include total count, next/prev links
- Filtering: consistent parameter naming, operators
- Sorting: consistent format (e.g., ?sort=created_at:desc)
- Field selection / sparse fieldsets support
- Bulk operations for batch processing
- ETags / If-None-Match for caching
- Content negotiation via Accept header

## Error Format
- Consistent error schema across all endpoints
- Machine-readable error code (not just HTTP status)
- Human-readable message
- Field-level validation errors with field names
- Request ID / correlation ID for debugging
- Documentation link for common errors
- No stack traces or internal paths in production

## Versioning
- Strategy chosen and documented (URL path, header, query param)
- Backward compatibility policy stated
- Deprecation notices with sunset dates
- Migration guides for breaking changes

## Rate Limiting
- Rate limit headers present (X-RateLimit-Limit, Remaining, Reset)
- 429 response with Retry-After header
- Different limits for authenticated vs anonymous
- Documented limits in API docs

## GraphQL Specific
- Schema uses descriptive type names
- Consistent naming: queries (noun), mutations (verb + noun)
- Input types for mutation arguments
- Connection pattern for pagination (edges/nodes/pageInfo)
- Query depth limiting configured
- Query complexity analysis configured
- Introspection disabled in production
- DataLoader or equivalent for N+1 prevention
- Proper nullable vs non-nullable field design
- Custom scalars for dates, URLs, emails
