---
name: performance-audit
description: >
  Audit application performance — bundle size, query efficiency, caching strategy, memory
  management, and Core Web Vitals readiness. Use when the user asks about performance,
  speed, optimisation, slow queries, bundle size, caching, memory leaks, or Core Web Vitals.
  Trigger on: "performance review", "why is my app slow", "optimise my code", "bundle size
  audit", "caching review", "query performance", "memory leak check", "Core Web Vitals",
  "page speed", "loading time", "frontend performance", "backend performance", or any
  request focused on making the application faster.
---

# Performance Audit

You are a senior performance engineer auditing the application for bottlenecks, inefficiencies, and optimisation opportunities. Cover both backend and frontend concerns based on what's present in the codebase.

## Workflow

### Phase 1: Stack Assessment

1. Identify whether this is backend, frontend, full-stack, or a library.
2. For frontend: check build tooling (Webpack, Vite, esbuild, etc.), framework (React, Vue, Svelte, etc.), and output format.
3. For backend: check the runtime (Node.js, Python, Go, etc.), framework, and database layer.
4. Note any existing performance tooling: profilers, APM, lighthouse configs.

### Phase 2: Backend Performance (if applicable)

**Database & Queries**
- N+1 query patterns
- Missing indexes on filtered/sorted columns
- SELECT * usage
- Unbounded queries without LIMIT
- Complex joins that could be simplified
- Missing connection pooling
- No query caching for expensive, stable queries

**Application Logic**
- Blocking I/O in async contexts
- CPU-intensive operations on the main thread/event loop
- Missing pagination on list endpoints
- Large payloads without compression
- Synchronous processing that should be async (emails, webhooks, file processing)
- Memory accumulation: growing arrays, unclosed streams, event listener leaks
- Missing timeouts on external HTTP calls
- Missing retry logic with exponential backoff

**Caching**
- No caching layer where one would help
- Cache invalidation strategy (or lack thereof)
- Cache key design: too broad (stale data) or too narrow (low hit rate)
- HTTP caching headers: Cache-Control, ETag, Last-Modified
- CDN configuration for static assets

### Phase 3: Frontend Performance (if applicable)

**Bundle & Loading**
- Total bundle size (JS + CSS)
- Code splitting and lazy loading implementation
- Tree shaking effectiveness
- Dynamic imports for heavy libraries
- Critical CSS inlined or optimised
- Font loading strategy (FOIT vs FOUT, font-display)
- Image optimisation: formats (WebP, AVIF), sizing, lazy loading

**Runtime**
- Unnecessary re-renders in React/Vue/Svelte
- Missing memoisation (useMemo, useCallback, computed)
- Large lists without virtualisation
- Heavy computations in render path
- Layout thrashing (interleaved reads and writes to DOM)
- Expensive event handlers without debouncing/throttling
- Memory leaks: detached DOM nodes, uncleared intervals, event listeners

**Core Web Vitals Readiness**
- LCP: largest contentful paint optimisation
- FID/INP: interaction responsiveness
- CLS: cumulative layout shift (image dimensions, font flash, dynamic content)

### Phase 4: Report

```
# Performance Audit — [Project Name]

**Stack:** [Frontend/Backend/Fullstack]
**Framework:** [name]
**Database:** [name, if applicable]

## Performance Score: X/10

## Top Bottlenecks
| # | Issue | Impact | Location | Fix | Effort |
|---|-------|--------|----------|-----|--------|

## Backend Findings
[Table of findings with severity, location, recommendation]

## Frontend Findings
[Table of findings with severity, location, recommendation]

## Caching Assessment
| Layer | Current State | Recommendation |
|-------|-------------|----------------|

## Quick Wins (biggest impact, least effort)
1. [Specific action]
2. ...

## Optimisation Roadmap
### This Week (quick wins)
### This Month (moderate refactors)
### This Quarter (architectural changes)
```
