# Report Template

Generate the final audit report using this exact structure. Every section is required unless explicitly noted as conditional.

---

## Output Format

Produce the report as a single markdown document. If the user requests a different format (PDF, docx), produce markdown first and then convert.

---

## Report Structure

```
# CTO Technical Audit — [Project Name]

**Audit Date:** [Date]
**Repository:** [Repo URL or path]
**Stack:** [Primary language(s), framework(s), database(s)]
**Auditor:** Claude (AI-assisted CTO audit)

---

## Executive Summary

**Overall Health Score: X/10**

[2-3 sentence summary of the project's state. What is this project, what stage is it at, and what's the overall verdict?]

### Top 5 Strengths
1. [Specific strength with brief explanation]
2. ...
3. ...
4. ...
5. ...

### Top 5 Risks
1. [SEVERITY] [Specific risk with brief explanation]
2. ...
3. ...
4. ...
5. ...

### If You Can Only Do 3 Things
1. [Most impactful action — what, where, and why]
2. [Second most impactful action]
3. [Third most impactful action]

---

## Detailed Findings

### 1. Architecture & Design

**Rating: X/10**

[Paragraph summarising the architectural approach, what works, and what doesn't.]

| # | Finding | Severity | Effort | Location |
|---|---------|----------|--------|----------|
| 1 | [Description] | CRITICAL/HIGH/MEDIUM/LOW | Quick Win/Moderate/Major | `file:line` |
| 2 | ... | ... | ... | ... |

[Repeat the paragraph + table format for each domain:]

### 2. Code Quality & Standards
### 3. Security
### 4. Performance & Scalability
### 5. Testing & Reliability
### 6. DevOps & Infrastructure
### 7. Documentation & Developer Experience
### 8. Dependencies & Supply Chain

---

## Tech Debt Register

All findings consolidated and ranked by priority. This is the team's action backlog.

| Priority | Domain | Finding | Severity | Effort | Location | Suggested Fix |
|----------|--------|---------|----------|--------|----------|---------------|
| 1 | Security | [Description] | CRITICAL | Quick Win | `file:line` | [What to do] |
| 2 | ... | ... | ... | ... | ... | ... |

Sort by: CRITICAL first, then HIGH, then by effort (Quick Wins first within same severity).

---

## Prioritised Roadmap

### Next 7 Days (Urgent)
- [ ] [Action item — specific and assignable]
- [ ] ...

### Next 30 Days (Important)
- [ ] [Action item]
- [ ] ...

### Next 60 Days (Strategic)
- [ ] [Action item]
- [ ] ...

### Next 90 Days (Foundational)
- [ ] [Action item]
- [ ] ...

### If You Hire 3 Engineers Tomorrow
Here's what to assign them:
- **Engineer 1 (Security/Infra):** [Specific focus area and tasks]
- **Engineer 2 (Quality/Testing):** [Specific focus area and tasks]
- **Engineer 3 (Features/DX):** [Specific focus area and tasks]

---

## Appendix

### Files Reviewed
[List the key files examined during the audit, grouped by domain]

### Tools & Methodology
This audit was conducted by systematically examining the repository structure, configuration files, source code, test suites, CI/CD pipelines, and documentation. Findings are based on code inspection and static analysis reasoning, not runtime profiling.

### Limitations
[Note anything you couldn't assess — e.g. "No access to production metrics", "Database schema not visible", "Private dependencies could not be inspected"]
```

---

## Scoring Guide

Use this rubric for the overall health score and per-domain ratings:

- **9-10**: Exceptional. Production-ready, well-documented, secure, and maintainable. Minor nitpicks only.
- **7-8**: Good. Solid fundamentals with some areas for improvement. Safe to ship and iterate.
- **5-6**: Adequate. Works but has meaningful gaps in quality, security, or reliability. Needs investment.
- **3-4**: Concerning. Significant issues that pose real risk. Needs focused remediation before scaling.
- **1-2**: Critical. Fundamental problems that threaten stability, security, or maintainability. Stop and fix.

Be honest. Most real-world codebases land between 4 and 7. A score of 8+ should be genuinely impressive. Don't grade on a curve — grade against what a production-quality codebase should look like.
