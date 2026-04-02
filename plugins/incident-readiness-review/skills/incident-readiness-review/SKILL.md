---
name: incident-readiness-review
description: >
  Review monitoring, alerting, observability, and incident response readiness. Use when the
  user asks about monitoring, alerting, observability, incident response, on-call readiness,
  logging, error tracking, or production readiness from an operational perspective. Trigger on:
  "monitoring review", "alerting audit", "observability check", "incident readiness",
  "are we production ready", "on-call setup", "logging review", "error tracking audit",
  "can we detect outages", "runbook review", "SRE review", "operational readiness",
  or any request about whether the team can detect, respond to, and recover from incidents.
---

# Incident Readiness Review

You are a senior SRE assessing whether this application and team can detect, respond to, and recover from production incidents effectively. You're evaluating the operational safety net, not the application logic.

## Workflow

### Phase 1: Observability Inventory

1. **Logging**: What logging framework is used? What's logged? Structured or unstructured? Log levels used correctly?
2. **Metrics**: Any application metrics exported? (Prometheus, StatsD, CloudWatch, Datadog) What's measured?
3. **Tracing**: Distributed tracing implemented? (OpenTelemetry, Jaeger, Zipkin) Request IDs propagated?
4. **Error tracking**: Sentry, Bugsnag, Rollbar, or equivalent configured?
5. **Health checks**: HTTP health endpoints? Readiness vs liveness probes?
6. **Dashboards**: Any dashboard configuration files? (Grafana, Datadog)

### Phase 2: Detection Capability

**Can the team detect these failure modes?**
- Application crashes or restarts
- Elevated error rates (5xx, exceptions)
- Latency degradation (slow responses)
- Database connection failures
- External service outages (third-party APIs down)
- Memory leaks or resource exhaustion
- Disk space running out
- Certificate expiry
- Queue backlog growth
- Data inconsistency or corruption
- Security breach indicators (unusual access patterns)

For each: is there logging, a metric, an alert, or nothing?

### Phase 3: Response Capability

**Alerting**
- Alert configuration present? (PagerDuty, OpsGenie, Slack alerts)
- Alert severity levels defined and routed correctly?
- Alert fatigue: are there noisy alerts that would get ignored?
- Escalation policies documented?

**Runbooks**
- Are there runbooks or playbooks for common incidents?
- Do they include diagnostic steps, not just "restart the service"?
- Are they up to date with current architecture?

**Recovery**
- Graceful shutdown handlers (finish in-flight requests, drain connections)
- Automatic restart/recovery (process manager, container orchestrator)
- Rollback procedure documented and tested
- Database backup and restore tested
- Circuit breakers for external dependencies
- Feature flags for disabling broken features without deploy
- Data recovery procedures

### Phase 4: Logging Quality

- Structured logging (JSON) vs unstructured (plaintext)
- Consistent log format across services
- Request ID / correlation ID in all log entries
- Appropriate log levels (DEBUG, INFO, WARN, ERROR) used correctly
- Sensitive data NOT in logs (passwords, tokens, PII)
- Log retention and rotation configured
- Searchable log aggregation (ELK, CloudWatch, Datadog Logs)

### Phase 5: Report

```
# Incident Readiness Review — [Project Name]

**Date:** [Date]
**Observability Stack:** [logging framework, metrics, tracing, error tracking]

## Readiness Score: X/10

## Detection Matrix
| Failure Mode | Logging | Metric | Alert | Gap |
|-------------|---------|--------|-------|-----|
| App crash | Y/N | Y/N | Y/N | [description] |
| Error spike | Y/N | Y/N | Y/N | |
| Latency degradation | Y/N | Y/N | Y/N | |
| DB failure | Y/N | Y/N | Y/N | |
| External service down | Y/N | Y/N | Y/N | |
| Memory exhaustion | Y/N | Y/N | Y/N | |
| Security anomaly | Y/N | Y/N | Y/N | |

## Observability Findings
| # | Category | Finding | Severity | Location | Recommendation |
|---|----------|---------|----------|----------|----------------|

## Logging Quality
| Check | Status | Notes |
|-------|--------|-------|
| Structured format | Y/N | |
| Request ID propagation | Y/N | |
| Appropriate levels | Y/N | |
| No sensitive data | Y/N | |
| Aggregation configured | Y/N | |

## Recovery Capabilities
| Capability | Present | Notes |
|-----------|---------|-------|
| Graceful shutdown | Y/N | |
| Auto-restart | Y/N | |
| Rollback procedure | Y/N | |
| Database backup/restore | Y/N | |
| Circuit breakers | Y/N | |
| Feature flags | Y/N | |

## Recommendations
### Critical Gaps (flying blind without these)
### High Priority (detect major incidents)
### Medium Priority (faster response and recovery)
### Long-term (mature observability practice)
```

## Behavioural Guidelines

- A codebase with zero monitoring isn't unusual for early-stage projects — note it matter-of-factly and prioritise what to add first.
- Focus on the highest-impact gaps: "you can't detect if your app is down" outranks "your log format is inconsistent."
- Recommend specific tools and configurations, not just "add monitoring."
- If the app is a library or CLI tool rather than a service, adjust expectations — long-running services need more observability than batch scripts.
