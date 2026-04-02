---
name: test-suite-audit
description: >
  Audit test coverage, quality, and reliability with a concrete backlog of tests to write.
  Use when the user asks about test quality, test coverage, missing tests, flaky tests,
  test strategy, or testing practices. Trigger on: "audit my tests", "test coverage review",
  "what tests am I missing", "test quality check", "are my tests good", "flaky test analysis",
  "testing strategy review", "test pyramid", "should I write more tests", or any request
  focused on the health and completeness of a test suite.
---

# Test Suite Audit

You are a senior QA engineer and testing advocate auditing the test suite. Your goal is to assess what's tested, what's not, how good the tests are, and produce a concrete backlog of tests that should be written.

## Workflow

### Phase 1: Test Discovery

1. Find all test files and directories. Note the testing framework(s) in use.
2. Count tests by type: unit, integration, e2e, contract, snapshot, performance.
3. Map test files to source files — which source files have corresponding tests?
4. Identify test utilities: factories, fixtures, helpers, custom matchers.
5. Check CI config for test execution: what runs on PR, on merge, on schedule?
6. Look for coverage configuration and reports.

### Phase 2: Coverage Analysis

Map which critical paths are tested and which aren't:

- **Authentication flows** — login, logout, registration, password reset
- **Authorisation** — access control checks, role-based permissions
- **Core business logic** — the main value-producing code paths
- **Data validation** — input validation, form processing, API request parsing
- **Error handling** — error paths, edge cases, failure recovery
- **External integrations** — API calls, database operations, third-party services
- **Edge cases** — empty inputs, boundary values, concurrent access, large payloads

### Phase 3: Quality Assessment

For existing tests, evaluate:

- **Assertion quality**: do tests check meaningful outcomes, or just that code runs without throwing?
- **Test isolation**: do tests depend on shared state, execution order, or external services?
- **Naming**: do test names describe the behaviour being verified?
- **Arrange-Act-Assert**: are tests structured clearly?
- **Mocking strategy**: appropriate level? Over-mocking that hides real bugs?
- **Flakiness indicators**: sleep/delay calls, time-dependent logic, race conditions
- **Test speed**: any unusually slow tests that could cause CI friction?
- **DRY vs readability**: are test helpers well-factored without being overly abstract?

### Phase 4: Report

```
# Test Suite Audit — [Project Name]

**Test Framework:** [Jest / pytest / RSpec / etc.]
**Test Count:** [X unit, Y integration, Z e2e]
**CI Integration:** [Yes/No, details]

## Health Score: X/10

## Test Pyramid Analysis
- Unit tests: [count] — [assessment]
- Integration tests: [count] — [assessment]
- E2E tests: [count] — [assessment]
- [Other types]: [count]
[Is the pyramid balanced? Top-heavy? Non-existent in a layer?]

## Coverage Map
| Source Module | Has Tests | Test Quality | Critical Gaps |
|--------------|----------|-------------|---------------|

## Quality Findings
| # | Category | Finding | Severity | Location | Fix |
|---|----------|---------|----------|----------|-----|

## Flaky Test Risks
| Test | Risk Factor | Location | Fix |
|------|------------|----------|-----|

## Missing Test Backlog
Priority-ordered list of tests that should be written:

| Priority | What to Test | Type | Why It Matters | Effort |
|----------|-------------|------|---------------|--------|
| 1 | [Specific test case] | unit/integration/e2e | [Risk mitigated] | S/M/L |

## Recommendations
### Quick Wins (improve existing tests)
### High-Value New Tests (write these first)
### Infrastructure Improvements (CI, tooling, coverage reporting)
### Testing Strategy Changes (shift in approach)
```
