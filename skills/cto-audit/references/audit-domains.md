# Audit Domains — Detailed Checklist

Use this as your investigation guide for each domain. Not every item applies to every codebase — skip what's irrelevant, but check everything that could apply.

---

## 1. Architecture & Design

**What to look for:**
- Overall pattern: monolith, microservices, serverless, modular monolith, event-driven?
- Is there a clear separation of concerns? (e.g. controllers vs services vs data access)
- How do major components communicate? (direct calls, message queues, REST, gRPC, events)
- Dependency direction — do high-level modules depend on low-level ones? (dependency inversion)
- Circular dependencies between modules or packages
- God classes or god modules that do too much
- Appropriate use of design patterns (and misuse — over-engineering counts)
- Database schema design if visible (migrations, models, ORMs)
- API design: RESTful conventions, consistent naming, versioning strategy
- Configuration management: how are env vars, feature flags, and secrets handled?

**Where to look:** Project structure, import/require graphs, route definitions, middleware chains, service layers, database models/migrations.

---

## 2. Code Quality & Standards

**What to look for:**
- Consistent code style across the project (or evidence of style drift between contributors)
- Linter and formatter configs present and enforced?
- Naming conventions: are variables, functions, classes, and files named clearly and consistently?
- DRY violations: copy-pasted logic, near-duplicate functions
- Dead code: unused imports, unreachable branches, commented-out blocks, deprecated functions still present
- Function/method length — anything over ~50 lines deserves scrutiny
- Cyclomatic complexity — deeply nested conditionals, long switch statements
- Error handling: are errors caught, logged, and propagated consistently? Silent catches?
- Magic numbers and hardcoded strings that should be constants
- Type safety: if using TypeScript/Python type hints, are they used consistently? Any `any` abuse?
- Code comments: are they useful or just restating the code? Are they outdated?

**Where to look:** Core business logic files, utility/helper modules, API handlers, data processing pipelines.

---

## 3. Security

**What to look for:**
- Hardcoded secrets, API keys, tokens, or passwords (check `.env` files committed to repo, config files, test fixtures)
- `.gitignore` coverage — are sensitive files excluded?
- Input validation: are user inputs validated and sanitised before use?
- SQL injection: raw queries with string interpolation? Parameterised queries used?
- XSS: is user-generated content escaped before rendering?
- CSRF: are state-changing endpoints protected?
- Authentication: how are sessions/tokens managed? JWT expiry? Refresh token rotation?
- Authorisation: are there proper access controls? Can a regular user access admin endpoints?
- Rate limiting on public endpoints
- CORS configuration — overly permissive?
- Dependency vulnerabilities: run `npm audit`, `pip audit`, or equivalent mentally. Are major deps outdated?
- File upload handling: size limits, type validation, storage location
- Logging: are sensitive values (passwords, tokens, PII) being logged?
- HTTPS enforcement, secure cookie flags, security headers (CSP, HSTS, X-Frame-Options)

**Where to look:** Auth middleware, route handlers, database queries, file upload endpoints, CORS config, environment files, dependency manifests.

---

## 4. Performance & Scalability

**What to look for:**
- N+1 query patterns (loading related records in a loop instead of batch/join)
- Missing database indexes on frequently queried columns
- Unoptimised queries: full table scans, SELECT *, unnecessary JOINs
- Blocking I/O in async contexts (sync file reads, blocking HTTP calls)
- Missing caching where it would help (repeated expensive computations, frequent DB reads for static data)
- Memory leaks: event listeners not cleaned up, growing in-memory stores, unclosed connections
- Large payload responses without pagination
- Image/file processing without streaming
- Frontend: bundle size, code splitting, lazy loading, unnecessary re-renders
- Connection pooling for databases and external services
- Graceful degradation under load — circuit breakers, timeouts, retry logic
- Horizontal scaling readiness: stateless services? Sticky sessions?

**Where to look:** Database query layers, API response handlers, background job processors, frontend bundle config, connection setup code.

---

## 5. Testing & Reliability

**What to look for:**
- Test presence: are there tests at all? What types? (unit, integration, e2e, contract)
- Test coverage: which critical paths are tested? Which aren't?
- Test quality: do tests verify meaningful behaviour or just check that code runs without throwing?
- Test isolation: do tests depend on external services, shared state, or execution order?
- Flaky test indicators: sleep/delay calls, race conditions, time-dependent assertions
- Mocking strategy: is it appropriate? Over-mocking that hides real bugs?
- Edge case coverage: empty inputs, boundary values, error paths, concurrent access
- CI/CD pipeline: does it run tests on every PR? Are there quality gates?
- Build reproducibility: are builds deterministic? Lockfiles committed?
- Error recovery: retry logic, dead letter queues, graceful shutdown handlers
- Health checks and readiness probes

**Where to look:** Test directories, CI config files, test utilities/helpers, fixtures/factories.

---

## 6. DevOps & Infrastructure

**What to look for:**
- Dockerfile quality: multi-stage builds? Running as non-root? Minimal base image? Layer caching optimised?
- Docker Compose for local dev: is it easy to spin up the full stack?
- Environment config: how are env vars managed across environments? Any env-specific logic in code?
- Secrets management: vault, cloud secrets manager, or just env vars?
- Deployment strategy: blue-green, rolling, canary? Or just YOLO?
- Rollback capability: can you revert a bad deploy quickly?
- Infrastructure as Code: Terraform, Pulumi, CloudFormation, or manual setup?
- Monitoring: application metrics, error tracking (Sentry, Datadog, etc.), log aggregation
- Alerting: are there alerts for critical failures? Or just hope someone notices?
- Database migrations: are they reversible? Tested? Applied automatically on deploy?
- Backup strategy for databases and critical data
- SSL/TLS certificate management

**Where to look:** Dockerfile, docker-compose.yml, CI/CD configs, Terraform/IaC directories, Kubernetes manifests, deployment scripts.

---

## 7. Documentation & Developer Experience

**What to look for:**
- README: does it explain what the project does, how to set it up, and how to contribute?
- Setup instructions: can a new developer go from clone to running in under 30 minutes?
- API documentation: OpenAPI/Swagger spec? Postman collection? Or nothing?
- Architecture documentation: diagrams, ADRs, design docs?
- Inline comments: present where logic is complex? Or either absent or trivially restating code?
- CONTRIBUTING.md or development guidelines
- Code of conduct, license file
- Changelog or release notes
- Local development tooling: scripts, Makefile targets, dev containers?

**Where to look:** Root-level markdown files, docs/ directory, wiki (if referenced), Makefile, scripts/ directory.

---

## 8. Dependencies & Supply Chain

**What to look for:**
- Lockfile committed and up to date?
- Outdated dependencies: how far behind are major deps?
- Unnecessary dependencies: libraries included for trivial functionality that could be a few lines of code
- Dependency count: is the dependency tree bloated?
- License compliance: any GPL or restrictive licenses in a proprietary project?
- Pinned versions vs ranges: is there a strategy?
- Monorepo dependency management (if applicable): shared versions? Hoisting issues?
- Post-install scripts in dependencies (supply chain risk)

**Where to look:** package.json, package-lock.json, yarn.lock, requirements.txt, Pipfile.lock, go.sum, Cargo.lock, Gemfile.lock.
