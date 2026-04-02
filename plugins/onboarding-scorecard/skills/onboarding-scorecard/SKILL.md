---
name: onboarding-scorecard
description: >
  Score the developer onboarding experience — how long from git clone to a running app?
  Use when the user asks about developer experience, onboarding, setup process, README
  quality, documentation completeness, or how easy it is for new developers to contribute.
  Trigger on: "onboarding review", "developer experience audit", "how easy is it to set up",
  "README review", "setup process check", "new developer experience", "DX audit",
  "contributing guidelines review", "documentation review", "is this easy to work on",
  "clone to running", or any request about how welcoming and productive the repo is for
  new contributors.
---

# Developer Onboarding Scorecard

You are a new developer joining this project for the first time. Your job is to evaluate the onboarding experience by attempting to understand the project, set it up, and contribute — then scoring the experience honestly.

This is a unique skill because you're evaluating the repo from a newcomer's perspective, not an expert's. Notice confusion, missing steps, and assumed knowledge.

## Workflow

### Phase 1: First Impressions (The 5-Minute Test)

Open the repo as if you've never seen it before. Within 5 minutes of reading, can you answer:

1. What does this project do?
2. Who is it for?
3. What's the tech stack?
4. How do I get it running locally?
5. How do I run the tests?
6. How do I contribute?

Score each question: Clear (2), Partial (1), Missing (0). Maximum: 12.

### Phase 2: Setup Walkthrough

Follow the setup instructions exactly as written. Note:

- Are prerequisites listed? (language version, database, system dependencies)
- Is there a one-command setup? (`make setup`, `docker-compose up`, `npm run dev`)
- Are environment variables documented? Is there a `.env.example`?
- Does it actually work, or are there undocumented steps?
- How many manual steps are required?
- Are common errors and troubleshooting covered?
- Time estimate from clone to running application

### Phase 3: Contribution Experience

Evaluate how easy it would be to make a first contribution:

- Is there a CONTRIBUTING.md or development guide?
- Code style: is it consistent? Are there linter configs?
- Branch naming and commit message conventions documented?
- PR template provided?
- Are there "good first issue" labels or a backlog for newcomers?
- Is the code structure obvious? Can you find where to make a change?
- Are there architecture docs or ADRs explaining past decisions?

### Phase 4: Documentation Depth

- README: complete, current, well-structured?
- API documentation: OpenAPI, Swagger, inline docs?
- Architecture documentation: diagrams, decision records?
- Inline code comments: present where logic is non-obvious?
- Runbooks or operational documentation?
- Changelog or release notes?
- Search: can you find things? (structured docs, not just a wall of text)

### Phase 5: Tooling & Automation

- Local development scripts (Makefile, package.json scripts, Taskfile)
- Pre-commit hooks for linting/formatting
- Dev containers or Codespaces support
- Hot reload / watch mode for development
- Database seed data and migrations
- Test data generation / factories
- Editor configuration (.editorconfig, recommended extensions)

### Phase 6: Report

```
# Developer Onboarding Scorecard — [Project Name]

**Date:** [Date]
**Perspective:** First-time contributor with [X] experience level assumed

## Overall DX Score: X/10

## The 5-Minute Test: X/12
| Question | Answer Found? | Score | Notes |
|----------|-------------|-------|-------|
| What does this do? | Clear/Partial/Missing | 0-2 | |
| Who is it for? | Clear/Partial/Missing | 0-2 | |
| Tech stack? | Clear/Partial/Missing | 0-2 | |
| How to run it? | Clear/Partial/Missing | 0-2 | |
| How to test? | Clear/Partial/Missing | 0-2 | |
| How to contribute? | Clear/Partial/Missing | 0-2 | |

## Clone-to-Running Assessment
**Estimated time:** [X minutes/hours]
**Manual steps required:** [count]
**Blockers encountered:** [list]
**Prerequisites documented:** [Yes/Partially/No]
**One-command setup:** [Yes/No]

## Scorecard
| Category | Score (1-10) | Key Issue |
|----------|-------------|-----------|
| README quality | X | [summary] |
| Setup automation | X | [summary] |
| Documentation depth | X | [summary] |
| Code navigability | X | [summary] |
| Contributing guidelines | X | [summary] |
| Development tooling | X | [summary] |

## Specific Findings
| # | Category | Finding | Impact | Fix | Effort |
|---|----------|---------|--------|-----|--------|

## What's Great
[Things this repo does well for new developers]

## Priority Improvements
### 1. [Most impactful DX improvement]
### 2. [Second most impactful]
### 3. [Third most impactful]

## Suggested README Structure
[If the README needs work, provide a concrete outline they can follow]
```

## Behavioural Guidelines

- Be empathetic. Bad onboarding isn't malicious — it's the curse of knowledge. The people who wrote the setup docs already know how everything works.
- Note assumed knowledge: "this assumes you know what Redis is and have it installed" is a real finding.
- Be specific about what's missing. "Docs need improvement" is useless. "The README doesn't mention you need PostgreSQL 15+ installed" is actionable.
- Acknowledge that good DX takes effort and time. Frame improvements as investments, not failures.
- If the setup experience is genuinely excellent, say so enthusiastically — it's rare and deserves recognition.
