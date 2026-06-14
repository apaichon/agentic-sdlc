# Chapter 7 Lab - Test Scenarios & Test Plan

## Lab Goal

ใช้ Tester Agent สร้าง test scenarios และ test plan จาก PRD, architecture docs และ implementation task list เพื่อให้ทีมมี release confidence ก่อนส่ง feature เข้า production.

## Target Skill

`/draft-test-plan`

## Scenario

ทีมต้อง test WhatsApp Adapter สำหรับ consolidated chat / Unified Inbox.

Inputs จากบทก่อนหน้า:

- Chapter 4: `docs/product/whatsapp-adapter-prd.md`
- Chapter 5: `docs/architecture/messaging-flow.md`
- Chapter 6: `docs/implementation/whatsapp-adapter-tasks.md`
- Chapter 6: `docs/implementation/code-conventions.md`

## Step-by-step Lab

### Step 1 - Create test branch

```bash
git switch -c lab/chapter-7-test-plan
mkdir -p docs/test
```

### Step 2 - Collect source documents

สร้าง source checklist:

```markdown
# Test Plan Source Checklist

- [ ] PRD exists
- [ ] User stories and acceptance criteria exist
- [ ] Architecture flow exists
- [ ] Message schema exists
- [ ] Implementation tasks exist
- [ ] Code conventions exist
- [ ] Known risks are listed
```

### Step 3 - Draft test plan

Use this prompt with Tester Agent.

```text
Task:
Draft a test plan for the WhatsApp Adapter feature.

Action:
Read the PRD, user stories, architecture docs, implementation task list, and code conventions. Create a risk-based test strategy, test scenarios, test data plan, automation priority, and release confidence checklist.

Goal:
Produce test artifacts that Tester Agent, Developer Agent, and Human QA can use to verify behavior before release.

Context:
- Feature: WhatsApp Adapter for Unified Inbox
- UI: Next.js inbox
- Backend: Go API Gateway and Message Router
- Queue: RabbitMQ
- Storage: MongoDB
- Cache: Redis
- Analytics: ClickHouse

Required Output:
1. Test strategy summary
2. Risk matrix
3. Test scenarios by level
4. Given/When/Then scenario table
5. Test data plan
6. Automation priority
7. PostToolUse verification plan
8. Release confidence checklist

Test levels:
- unit
- integration
- contract
- E2E
- performance
- security
- recovery

Narrowing:
- Keep technical words in English.
- Use Markdown.
- Make every critical scenario measurable.
- Map every high-risk behavior to at least one automated test.
```

Save output to:

```text
docs/test/whatsapp-adapter-test-plan.md
```

### Step 4 - Generate test scenarios

Prompt:

```text
Task:
Create detailed test scenarios for WhatsApp Adapter.

Action:
Generate Given/When/Then scenarios grouped by unit, integration, contract, E2E, performance, security, and recovery tests.

Goal:
Produce scenarios that can be converted into automated tests and manual exploratory checks.
```

Save output to:

```text
docs/test/whatsapp-adapter-test-scenarios.md
```

### Step 5 - Generate release confidence checklist

Prompt:

```text
Task:
Create release confidence checklist for WhatsApp Adapter.

Action:
Define pass/fail criteria for critical tests, integration health, contract compatibility, observability, rollback readiness, and known risks.

Goal:
Help Human QA and PM decide if the feature is ready for release.
```

Save output to:

```text
docs/test/release-confidence-checklist.md
```

## Skill - `/draft-test-plan`

```markdown
# /draft-test-plan

## Purpose

Draft risk-based test strategy, test scenarios, test data plan, automation priority, and release confidence checklist from PRD, architecture docs, and implementation task list.

## Trigger

Use this skill when:

- PRD and acceptance criteria exist.
- Architecture and implementation plan exist.
- Team needs test scenarios before or during implementation.
- Release confidence requires risk-based evidence.

## Inputs

Required:

- PRD
- User stories
- Acceptance criteria
- Architecture document
- Implementation task list
- Known risks

Optional:

- Existing test framework
- Test data constraints
- Performance targets
- Security requirements
- Incident history

## Workflow

1. Read PRD and acceptance criteria.
2. Read architecture and implementation tasks.
3. Identify risk by impact and probability.
4. Map risk to test level.
5. Draft Given/When/Then scenarios.
6. Define test data and mocks/containers.
7. Prioritize automation.
8. Define PostToolUse verification.
9. Create release confidence checklist.

## Quality Rules

- High-risk behavior must have automated coverage.
- Contract boundaries must be tested.
- E2E tests must cover critical user flows only.
- Performance targets must be measurable.
- Security scenarios must include invalid signature and PII handling.
- Recovery scenarios must include queue failure, retry, and duplicate message prevention.
```

## Test Plan Review Checklist

| Check | Yes/No | Notes |
|---|---|---|
| High-risk items are mapped to tests |  |  |
| Given/When/Then scenarios are clear |  |  |
| Contract tests cover adapter interface |  |  |
| Integration tests cover RabbitMQ, MongoDB, Redis |  |  |
| E2E tests cover critical inbox flow |  |  |
| Performance targets are measurable |  |  |
| Security scenarios are included |  |  |
| Recovery scenarios are included |  |  |
| Release confidence checklist is clear |  |  |

## Expected Deliverables

```text
docs/test/whatsapp-adapter-test-plan.md
docs/test/whatsapp-adapter-test-scenarios.md
docs/test/release-confidence-checklist.md
```

## Extension Exercise

Ask Tester Agent to identify which scenarios should run in `PostToolUse`, PR CI, staging, and pre-release smoke test.
