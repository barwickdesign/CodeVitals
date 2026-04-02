---
name: cicd-pipeline-review
description: >
  Review CI/CD pipeline efficiency, safety, and maturity. Use when the user asks about their
  build pipeline, deployment process, CI configuration, GitHub Actions, GitLab CI, Jenkins,
  or deployment strategy. Trigger on: "review my CI/CD", "pipeline audit", "build time
  optimisation", "deployment review", "is my CI good", "GitHub Actions review", "pipeline
  security", "deployment strategy check", or any request about continuous integration and
  deployment practices.
---

# CI/CD Pipeline Review

You are a DevOps engineer reviewing the CI/CD pipeline for efficiency, safety, and maturity. Examine workflow files, deployment scripts, and configuration to produce actionable improvements.

## Workflow

### Phase 1: Pipeline Discovery

1. Find all CI/CD configuration: `.github/workflows/`, `.gitlab-ci.yml`, `Jenkinsfile`, `Dockerfile`, `docker-compose.yml`, `Makefile`, deployment scripts, Terraform/IaC files.
2. Map the pipeline stages: lint → test → build → deploy. What runs when?
3. Identify triggers: on PR, on merge, on tag, on schedule, manual.
4. Note environments: dev, staging, production. How does code flow between them?
5. Check for secrets management in CI.

### Phase 2: Assessment

**Speed & Efficiency**
- Total pipeline duration for a typical PR
- Parallelisation: are independent jobs running concurrently?
- Caching: dependency caches, build caches, Docker layer caches
- Unnecessary steps: are tests or builds running when they don't need to?
- Conditional execution: do paths filter to only run relevant checks?
- Artifact reuse: is the same thing built multiple times?

**Safety & Reliability**
- Quality gates: must tests pass before merge? Coverage thresholds?
- Branch protection: are direct pushes to main blocked?
- Deployment approval: manual gates for production?
- Rollback capability: can a bad deploy be reverted quickly?
- Blue-green, canary, or rolling deployment strategy?
- Database migration safety: are migrations tested? Reversible?
- Smoke tests after deployment
- Dependency lockfile integrity check

**Security**
- Secrets stored in CI provider (not in code)
- Minimal permissions on CI tokens and service accounts
- Dependency vulnerability scanning in pipeline
- SAST/DAST tools integrated
- Container image scanning
- No secrets printed in logs
- Third-party action pinning (SHA vs tag)

**Maturity Indicators**
- Infrastructure as Code for pipeline infrastructure
- Environment parity: does staging match production?
- Feature flags for gradual rollout
- Automated changelog and release notes
- Monitoring integration: deploys correlated with metrics
- Notification on failure (Slack, email, PagerDuty)

### Phase 3: Report

```
# CI/CD Pipeline Review — [Project Name]

**CI Platform:** [GitHub Actions / GitLab CI / Jenkins / etc.]
**Pipeline Count:** [X workflows / jobs]
**Avg PR Pipeline Duration:** [estimated]

## Maturity Score: X/10

## Pipeline Map
[Describe the flow: trigger → stages → environments]

## Findings
| # | Category | Finding | Severity | File | Recommendation |
|---|----------|---------|----------|------|----------------|

## Speed Optimisations
| Optimisation | Estimated Time Saved | Effort | Location |
|-------------|---------------------|--------|----------|

## Safety Gaps
| Gap | Risk | Fix |
|-----|------|-----|

## Recommendations
### Quick Wins (caching, parallelisation)
### Safety Improvements (gates, rollbacks)
### Maturity Upgrades (monitoring, feature flags)
```
