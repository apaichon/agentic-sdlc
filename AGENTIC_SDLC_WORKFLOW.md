# Recommended Agentic SDLC Workflow

This document defines a practical workflow for running an Agentic SDLC with human roles and AI agents across Product Management, Development, Testing, DevOps, branching, and documentation.

Core principle:

> Human owns accountability. AI Agent owns acceleration. Git owns traceability.

---

## 1. Operating Model

Agentic SDLC is not only using AI to write code. It is a team workflow where AI agents help each role produce reviewable artifacts faster, while humans keep ownership of decisions, risk, and approval.

The recommended model is:

```text
Human defines intent
AI Agent drafts artifact
Human reviews and decides
AI Agent iterates
Git records the final artifact and decision trail
```

AI agents should not directly push to `main`.

Recommended rule:

```text
AI writes branch
AI opens PR
CI validates
Human reviews
Human merges
```

---

## 2. Repository Structure

Use Git as the source of truth for both code and documents.

Recommended structure:

```text
/
  CLAUDE.md
  docs/
    product/
      prd.md
      user-stories.md
      sprint-plan.md
    architecture/
      adr/
      diagrams/
    operations/
      runbooks/
      incident-reports/
      deploy-checklists/
    test-reports/
  internal/
  tests/
    unit/
    integration/
    contract/
    e2e/
  .github/
    workflows/
  .claude/
    pm.md
    dev.md
    tester.md
    devops.md
    skills/
```

Important files:

- `CLAUDE.md`: global project rules, architecture, coding standards, team conventions
- `.claude/pm.md`: PRD, backlog, and acceptance criteria rules
- `.claude/dev.md`: coding, architecture, TDD, and review rules
- `.claude/tester.md`: test strategy, coverage, and contract test rules
- `.claude/devops.md`: CI/CD, deployment, monitoring, rollback, and incident rules

---

## 3. Branch Strategy

Use short-lived branches per work item.

Branch naming:

```text
<type>/<ticket-id>-short-description
```

Examples:

```text
feature/US-042-line-adapter
fix/INC-014-sms-timeout
docs/ADR-007-rabbitmq-fanout
test/US-050-adapter-contract-tests
ops/DEPLOY-003-blue-green
```

Recommended branch types:

| Type | Purpose |
|---|---|
| `feature/` | Product feature implementation |
| `fix/` | Bug or incident fix |
| `docs/` | PRD, ADR, runbook, or documentation update |
| `test/` | Test strategy, test suite, or coverage work |
| `ops/` | CI/CD, deployment, infrastructure, monitoring |
| `refactor/` | Internal cleanup without intended behavior change |

For parallel AI work, use `git worktree`:

```bash
git worktree add ../agent-dev feature/US-042-line-adapter
git worktree add ../agent-test test/US-042-contract-tests
git worktree add ../agent-ops ops/US-042-ci-deploy
```

This prevents multiple AI sessions from editing the same working directory.

---

## 4. Role Workflow

## 4.1 PM Human + PM Agent

Human PM owns:

- Product priority
- Scope decisions
- Trade-offs
- Final PRD approval

PM Agent produces:

- PRD draft
- User stories
- Acceptance criteria
- Sprint plan
- Dependency map

Artifacts:

```text
docs/product/prd.md
docs/product/user-stories.md
docs/product/sprint-plan.md
```

Recommended flow:

```text
Human PM writes feature brief
PM Agent drafts PRD
Human PM reviews scope
PM Agent creates user stories and acceptance criteria
Human PM approves sprint scope
```

---

## 4.2 Developer Human + Developer Agent

Human Developer owns:

- Architecture decisions
- Code review
- Merge approval
- Production risk judgment

Developer Agent produces:

- Implementation plan
- Code
- Refactor proposal
- ADR draft
- PR description

Artifacts:

```text
internal/
docs/architecture/adr/
```

Recommended flow:

```text
Developer Agent reads PRD + CLAUDE.md
Developer Agent drafts implementation plan
Developer Agent writes failing tests or interface first
Developer Agent implements code
Developer Agent runs local checks
Developer Agent opens PR
Human Developer reviews
```

---

## 4.3 Tester Human + Tester Agent

Human Tester owns:

- Test strategy
- Risk prioritization
- Release confidence

Tester Agent produces:

- Unit test cases
- Integration tests
- Contract tests
- E2E scenarios
- Test report

Artifacts:

```text
tests/unit/
tests/integration/
tests/contract/
tests/e2e/
docs/test-reports/
```

Recommended flow:

```text
Tester Agent reads acceptance criteria
Tester Agent maps risk matrix
Tester Agent creates test plan
Tester Agent writes automated tests
Tester Agent runs tests
Tester Agent summarizes coverage gaps
Human Tester signs off
```

---

## 4.4 DevOps Human + DevOps Agent

Human DevOps owns:

- Infrastructure decisions
- Secrets and access policy
- Release approval
- Rollback decision

DevOps Agent produces:

- Dockerfile
- docker-compose setup
- GitHub Actions workflow
- Deployment runbook
- Monitoring dashboard spec
- Rollback checklist

Artifacts:

```text
.github/workflows/
docs/operations/runbooks/
docs/operations/deploy-checklists/
```

Recommended flow:

```text
DevOps Agent creates CI/CD pipeline
DevOps Agent adds deployment checks
DevOps Agent defines monitoring and alerts
DevOps Agent creates rollback plan
Human DevOps approves release
```

---

## 5. End-to-End Agentic SDLC Flow

Recommended full workflow:

```text
1. Human PM defines feature brief
2. PM Agent creates PRD and user stories
3. Human PM approves scope
4. Architect or Developer Agent creates design and ADR
5. Human Developer approves architecture
6. Tester Agent creates test strategy
7. Developer Agent implements feature
8. Tester Agent validates with tests
9. DevOps Agent prepares CI/CD and deploy path
10. Human Dev, Tester, and DevOps review PR
11. Merge to main
12. Deploy via controlled release
13. Monitor production
14. Incident or retro learnings update CLAUDE.md, skills, tests, and runbooks
```

Recommended stage gates:

| Stage | Required Human Approval |
|---|---|
| PRD approval | PM |
| Architecture approval | Developer / Architect |
| Test strategy approval | Tester |
| Deployment approval | DevOps |
| Merge approval | Code owner |
| Production go/no-go | Release owner |

---

## 6. Pull Request Rules

Every PR should include:

- Summary
- Linked story or issue
- Files changed
- Tests run
- Risks
- Rollback plan
- AI-generated artifacts used
- Human reviewer checklist

Recommended PR template:

```markdown
## Summary

Short description of the change.

## Linked Work

- Story:
- PRD:
- ADR:

## Changes

- 

## Tests Run

- [ ] Unit tests
- [ ] Integration tests
- [ ] Contract tests
- [ ] E2E tests
- [ ] CI pipeline

## Risks

- 

## Rollback Plan

- 

## AI Assistance

- Agent used:
- Skills used:
- Artifacts generated:

## Human Review Checklist

- [ ] Acceptance criteria covered
- [ ] Code reviewed
- [ ] Tests reviewed
- [ ] Security risk reviewed
- [ ] Operational impact reviewed
- [ ] Rollback path acceptable
```

---

## 7. Document Management Rules

Documents are part of the system and must be versioned.

Rules:

- PRD changes go through PR
- ADRs are immutable after accepted; create a new ADR to supersede old decisions
- Runbooks must be updated in the same PR as operational changes
- `CLAUDE.md` changes require human review
- AI-generated docs must be reviewed before merge
- Incident learnings must update docs, tests, hooks, or skills when appropriate

Recommended document lifecycle:

```text
Draft
Review
Approved
Versioned in Git
Updated through PR only
```

---

## 8. ADR Management

Store ADRs in:

```text
docs/architecture/adr/
```

Example ADR files:

```text
ADR-001-use-rabbitmq-fanout.md
ADR-002-use-mongodb-message-store.md
ADR-003-use-redis-session-cache.md
ADR-004-use-clickhouse-analytics.md
```

ADR status values:

```text
Proposed
Accepted
Superseded
Deprecated
```

Recommended ADR template:

```markdown
# ADR-000: Decision Title

## Status

Proposed | Accepted | Superseded | Deprecated

## Context

What problem are we solving?

## Decision

What did we decide?

## Alternatives Considered

- Option A:
- Option B:
- Option C:

## Consequences

Positive:

- 

Negative:

- 

## Links

- PR:
- Issue:
- Related ADR:
```

---

## 9. Human vs AI Responsibility Boundary

| Area | Human Owns | AI Agent Helps With |
|---|---|---|
| Product scope | Final priority | PRD draft, stories |
| Architecture | Final decision | Options, diagrams, ADR draft |
| Code | Merge approval | Implementation, refactor |
| Testing | Risk strategy | Test generation, reports |
| Deployment | Go/no-go | Pipeline, checklist |
| Incidents | Accountability | Timeline, post-mortem draft |
| Documentation | Approval | First draft, updates |
| `CLAUDE.md` | Rule approval | Suggested updates |

Decision rule:

```text
If the decision changes product scope, architecture direction, production risk, or customer impact, a human must approve it.
```

---

## 10. Recommended AI Agent Skills

| Role | Recommended Skills |
|---|---|
| PM Agent | `prd-generation`, `story-refinement`, `sprint-planning`, `dependency-mapping` |
| Developer Agent | `implementation-plan`, `tdd-cycle`, `clean-architecture-review`, `adr-draft` |
| Tester Agent | `test-strategy`, `contract-test-design`, `risk-matrix`, `coverage-analysis` |
| DevOps Agent | `ci-pipeline-design`, `dockerfile-hardening`, `deployment-runbook`, `rollback-plan` |
| SRE / Incident Agent | `incident-response`, `trace-analysis`, `alert-noise-reduction`, `postmortem-draft` |

---

## 11. Recommended Workflow Modes

Use the right collaboration mode for the task.

| Mode | Use When | Example |
|---|---|---|
| Sync | Ambiguity is high | Architecture decision, incident triage |
| Async | Task is clear | Generate tests, update docs |
| Parallel | Work is independent | Dev implements while Tester writes tests |
| Resync | Parallel work needs alignment | Merge findings before implementation |

Rule:

```text
If Agent A's output is Agent B's input, do not run them in parallel.
```

---

## 12. Quality Gates

Minimum quality gates before merge:

- PRD or story linked
- Acceptance criteria covered
- Tests added or updated
- CI passes
- Security risk reviewed
- Operational impact reviewed
- Rollback plan documented
- Human reviewer approved

Minimum quality gates before production:

- Deployment runbook exists
- Monitoring dashboard exists
- Alert routing exists
- Rollback path tested or documented
- On-call owner identified
- Go/no-go decision recorded

---

## 13. Best Practices

- Keep branches short-lived
- Use PRs for both code and documentation
- Keep `CLAUDE.md` concise but current
- Use ADRs for architecture decisions
- Use runbooks for operational procedures
- Use worktrees for parallel AI sessions
- Require human review for production-impacting changes
- Convert incidents and retrospectives into durable project rules

Final operating rule:

> AI may draft, analyze, implement, and test. Humans approve direction, risk, and release.
