# CodeVitals

**CTO-grade diagnostic skills for Claude Code.**

A comprehensive suite of 16 codebase health checks covering architecture, security, performance, testing, DevOps, and developer experience. Think of it as a full physical for your codebase — each skill checks a different vital sign.

## Quick Start

```bash
# Add the marketplace
/plugin marketplace add YOUR_USERNAME/codevitals

# Install individual skills
/plugin install cto-audit@codevitals
/plugin install infosec-audit@codevitals

# Or just ask Claude — skills trigger automatically
> "Audit this codebase"
> "Run a security review"
> "How healthy are my dependencies?"
```

## The Suite

### 🏥 Full Physical
| Skill | What It Checks |
|-------|---------------|
| **cto-audit** | Comprehensive CTO-level audit across all domains — the full physical |
| **tech-debt-prioritiser** | Scans for debt markers and produces a sprint-ready, prioritised backlog |

### 🔒 Security & Compliance
| Skill | What It Checks |
|-------|---------------|
| **infosec-audit** | OWASP Top 10, secrets, auth flows, input validation, dependency CVEs |
| **soc2-gdpr-readiness** | Data flows, PII handling, access controls, retention policies, compliance gaps |
| **pentest-planner** | Attack surface mapping, injection points, prioritised pen test plan |
| **dependency-health-check** | Outdated packages, abandoned maintainers, license conflicts, supply chain risk |

### 🏗️ Architecture & Design
| Skill | What It Checks |
|-------|---------------|
| **api-design-review** | REST/GraphQL conventions, versioning, error handling, OpenAPI spec quality |
| **database-health-check** | Schema design, indexing, N+1 queries, migration quality, normalisation |
| **microservices-readiness** | Service boundaries, coupling analysis, decomposition readiness |

### ⚡ Performance & Scalability
| Skill | What It Checks |
|-------|---------------|
| **performance-audit** | Bundle size, caching, query optimisation, Core Web Vitals, memory leaks |
| **scalability-assessment** | Statelessness, horizontal scaling, connection pooling, queue architecture |

### ✅ Quality & Reliability
| Skill | What It Checks |
|-------|---------------|
| **test-suite-audit** | Coverage gaps, flaky tests, mock quality, test pyramid balance |
| **cicd-pipeline-review** | Build times, caching, deployment safety, rollback capability |

### 🛠️ Operations & DX
| Skill | What It Checks |
|-------|---------------|
| **incident-readiness-review** | Monitoring, alerting, runbooks, observability, graceful degradation |
| **container-audit** | Dockerfile best practices, image security, layer optimisation, compose config |
| **onboarding-scorecard** | Clone-to-running time, README quality, setup automation, documentation |

## Recommended Workflows

**First time auditing a codebase?**
Start with `cto-audit` for the big picture, then drill into specific areas.

**Preparing for a security review?**
Run `infosec-audit` → `dependency-health-check` → `pentest-planner` in sequence.

**Onboarding a new team?**
Run `onboarding-scorecard` → `tech-debt-prioritiser` to see what they'll hit first.

**Scaling up?**
Run `scalability-assessment` → `database-health-check` → `performance-audit`.

**Pre-launch checklist?**
Run `infosec-audit` → `cicd-pipeline-review` → `incident-readiness-review` → `container-audit`.

## Output Format

Every skill produces a structured markdown report with:
- A health score out of 10
- Findings tagged by severity (CRITICAL / HIGH / MEDIUM / LOW)
- Effort estimates for each fix (Quick Win / Moderate / Major Refactor)
- Specific file and line references
- An actionable priority list

## Contributing

PRs welcome. Each skill lives in `plugins/<skill-name>/` and follows the standard structure:

```
plugins/my-skill/
├── .claude-plugin/
│   └── plugin.json
└── skills/
    └── my-skill/
        ├── SKILL.md
        └── references/
            └── checklist.md
```

## License

Apache 2.0
