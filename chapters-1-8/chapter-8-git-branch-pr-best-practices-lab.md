# Chapter 8 Lab - Git Branch & PR Best Practices

## Lab Goal

ออกแบบ Git branch, worktree และ PR workflow สำหรับทีม Agentic SDLC ขนาด 10+ คน ที่มี PM, Dev, Tester และ DevOps ทำงานพร้อมกันโดยไม่ชนกัน.

## Scenario

ทีมกำลังทำ WhatsApp Adapter / consolidated chat feature โดยมีสมาชิกมากกว่า 10 คน:

- PM team: PRD, user stories, acceptance criteria
- Dev team: implementation, refactor, code review
- Tester team: test scenarios, automation, release confidence
- DevOps team: CI/CD, deployment, monitoring, rollback

## Branch Naming Standard

```text
<type>/<ticket-id>-short-description
```

Examples:

```text
docs/US-042-prd-stories
feature/US-042-whatsapp-adapter
test/US-042-contract-tests
ops/US-042-ci-deploy
fix/INC-014-message-duplicate
```

Recommended branch types:

| Type | Owner | Purpose |
|---|---|---|
| `docs/` | PM | PRD, stories, acceptance criteria, release notes |
| `feature/` | Dev | Product implementation |
| `test/` | Tester | Test scenarios, automation, E2E, contract tests |
| `ops/` | DevOps | CI/CD, deployment, monitoring, rollback |
| `fix/` | Dev/Test/DevOps | Bug or incident fix |
| `refactor/` | Dev | Internal cleanup without behavior change |

## PR Naming Standard

```text
[ROLE][TICKET] Short PR title
```

Examples:

```text
[PM][US-042] WhatsApp Adapter PRD and Stories
[DEV][US-042] Implement WhatsApp Adapter Core
[TEST][US-042] Add Adapter Contract and E2E Tests
[OPS][US-042] Add CI Deploy and Monitoring
```

## Step-by-step Lab

### Step 1 - Create epic and ownership map

Create:

```text
docs/planning/US-042-ownership-map.md
```

Include:

| Workstream | Owner Role | Branch | Main Artifacts |
|---|---|---|---|
| Product scope | PM | `docs/US-042-prd-stories` | PRD, stories, acceptance criteria |
| Core implementation | Dev | `feature/US-042-whatsapp-adapter` | Go adapter, service, repository |
| Test coverage | Tester | `test/US-042-contract-tests` | contract, integration, E2E tests |
| Delivery | DevOps | `ops/US-042-ci-deploy` | CI/CD, deploy config, monitoring |

### Step 2 - Create branches

```bash
git switch main
git pull --ff-only

git switch -c docs/US-042-prd-stories
git switch main
git switch -c feature/US-042-whatsapp-adapter
git switch main
git switch -c test/US-042-contract-tests
git switch main
git switch -c ops/US-042-ci-deploy
```

### Step 3 - Create worktrees for parallel work

```bash
git worktree add ../agent-pm docs/US-042-prd-stories
git worktree add ../agent-dev feature/US-042-whatsapp-adapter
git worktree add ../agent-test test/US-042-contract-tests
git worktree add ../agent-ops ops/US-042-ci-deploy
```

### Step 4 - Define protected and shared files

| File Area | Owner | Rule |
|---|---|---|
| `docs/product/` | PM | Dev/Test may comment but PM owns final content |
| `internal/` | Dev | Tester may add test helpers only after agreement |
| `tests/` | Tester | Dev may add unit tests for implementation |
| `.github/workflows/` | DevOps | Changes require DevOps review |
| `docs/operations/` | DevOps | PM/Test may request updates |
| `CLAUDE.md` | Tech Lead | Changes require cross-role review |

### Step 5 - Open draft PR early

Each branch opens draft PR before implementation is complete.

Draft PR must include:

- linked ticket/story
- owner role
- affected files
- expected reviewers
- risk notes
- checklist still pending

### Step 6 - PR checklist

| Check | PM | Dev | Tester | DevOps |
|---|---:|---:|---:|---:|
| Linked issue/story | ✓ | ✓ | ✓ | ✓ |
| Scope is clear | ✓ |  |  |  |
| Code follows convention |  | ✓ |  |  |
| Tests added or updated |  | ✓ | ✓ |  |
| CI passed |  | ✓ | ✓ | ✓ |
| Docs updated | ✓ | ✓ | ✓ | ✓ |
| Monitoring/rollback checked |  |  |  | ✓ |
| Reviewer assigned | ✓ | ✓ | ✓ | ✓ |

### Step 7 - Resync and merge order

Recommended merge order:

```text
1. docs/US-042-prd-stories
2. feature/US-042-whatsapp-adapter
3. test/US-042-contract-tests
4. ops/US-042-ci-deploy
```

Rules:

- Rebase or merge from `main` before final review.
- Rerun CI after base branch changes.
- Do not merge `ops/` before implementation and test branches are stable.
- Do not merge feature branch if PM scope changed and PRD was not updated.

## Skill - `/plan-git-branch-pr-workflow`

```markdown
# /plan-git-branch-pr-workflow

## Purpose

Create branch naming, worktree layout, PR checklist, ownership rules, and merge order for multi-role Agentic SDLC teams.

## Trigger

Use this skill when:

- More than one role works in parallel.
- Team size is more than 5 people.
- AI Agents or humans need separate branches.
- PRs must be coordinated across PM, Dev, Tester, and DevOps.

## Inputs

Required:

- Ticket or epic ID
- Feature name
- Role list
- Artifact list
- Shared files
- Release target

## Workflow

1. Identify workstreams by role.
2. Assign branch names.
3. Create worktree commands.
4. Define file ownership.
5. Define draft PR template.
6. Define review checklist per role.
7. Define CI and resync rules.
8. Define merge order.
9. Define final release checklist.

## Quality Rules

- Branch names must include type and ticket ID.
- Each branch must have one primary owner.
- Shared files need explicit coordination.
- Draft PR opens early.
- CI must pass after final rebase.
- Merge order must follow dependency order.
```

## Final PR Checklist

| Check | Yes/No | Notes |
|---|---|---|
| Branch name follows convention |  |  |
| PR title follows convention |  |  |
| Linked issue/story exists |  |  |
| Owner and reviewers assigned |  |  |
| Protected files reviewed by owner |  |  |
| Tests run and CI passed |  |  |
| Conflicts resolved after resync |  |  |
| Docs updated |  |  |
| Deployment and rollback checked |  |  |
| PM, Dev, Tester, DevOps approvals complete |  |  |

## Expected Deliverables

```text
docs/planning/US-042-ownership-map.md
docs/planning/US-042-branch-plan.md
docs/planning/US-042-pr-checklist.md
```
