# Chapter 6 Lab - Implementation Plan & Code Convention

## Lab Goal

ใช้ Dev Agent สร้าง implementation plan, task list และ code conventions จาก PRD และ architecture document เพื่อให้ทีมเริ่ม implementation แบบ TDD และ Clean Architecture ได้อย่างปลอดภัย.

## Target Skill

`/generate-implementation-plan`

## Scenario

ทีมต้อง implement WhatsApp Adapter สำหรับ Unified Inbox.

Inputs จากบทก่อนหน้า:

- Chapter 4: `docs/product/whatsapp-adapter-prd.md`
- Chapter 4: `docs/product/whatsapp-adapter-user-stories.md`
- Chapter 5: `docs/architecture/messaging-flow.md`
- Chapter 5: `docs/architecture/message-schema.md`
- Chapter 5: `docs/architecture/adr/adr-messaging-architecture.md`

Tech stack:

- `Go` service and Clean Architecture
- `MongoDB` repository
- `RabbitMQ` publisher/consumer
- `Redis` session cache
- `ClickHouse` analytics pipeline
- `Next.js` inbox UI integration

## Step-by-step Lab

### Step 1 - Create implementation branch

```bash
git switch -c lab/chapter-6-implementation-plan
mkdir -p docs/implementation
```

### Step 2 - Collect source documents

สร้าง checklist เพื่อยืนยันว่าเอกสารต้นทางพร้อม:

```markdown
# Implementation Source Checklist

- [ ] PRD exists
- [ ] User stories exist
- [ ] Messaging flow exists
- [ ] Message schema exists
- [ ] ADR exists
- [ ] Acceptance criteria are testable
- [ ] Architecture dependencies are clear
```

### Step 3 - Generate implementation plan

Use this prompt with Dev Agent.

```text
Task:
Generate an implementation plan for the WhatsApp Adapter feature.

Action:
Read the PRD, user stories, messaging architecture, message schema, and ADR. Convert them into a layered implementation plan, task list, TDD sequence, code conventions, verification commands, and risk checklist.

Goal:
Produce implementation artifacts that Developer Agent, Tester Agent, and Reviewer can execute and verify without guessing product or architecture intent.

Context:
- Feature: WhatsApp Adapter for Unified Inbox
- Language: Go
- Architecture: Clean Architecture
- UI integration: Next.js
- Queue: RabbitMQ
- Storage: MongoDB
- Cache: Redis
- Analytics: ClickHouse

Required Output:
1. Implementation summary
2. Layer-by-layer task breakdown
3. File and package plan
4. Code convention checklist
5. TDD task sequence
6. Test strategy by layer
7. Verification commands
8. Risk and rollback checklist
9. Definition of Done

Narrowing:
- Keep technical words in English.
- Use Markdown.
- Do not implement code yet.
- Split any task that crosses too many layers.
- Call out assumptions and open questions.
```

Save output to:

```text
docs/implementation/whatsapp-adapter-plan.md
```

### Step 4 - Generate executable task list

Prompt:

```text
Task:
Convert the implementation plan into an executable task list.

Action:
Create ordered tasks grouped by layer:
- domain
- service
- adapter
- repository
- handler
- tests
- observability
- documentation

For each task include:
- owner role
- files to create or modify
- expected test
- verification command
- dependency
- definition of done

Goal:
Produce a task list that can be executed by AI Agent or human developer with review checkpoints.
```

Save output to:

```text
docs/implementation/whatsapp-adapter-tasks.md
```

### Step 5 - Generate code conventions

Prompt:

```text
Task:
Create code conventions for implementing WhatsApp Adapter in this repository.

Action:
Define naming, package boundaries, interface rules, error handling, logging, config, testing, and git conventions.

Goal:
Produce conventions that keep AI-generated code consistent with Clean Architecture and team standards.
```

Save output to:

```text
docs/implementation/code-conventions.md
```

## Skill - `/generate-implementation-plan`

```markdown
# /generate-implementation-plan

## Purpose

Generate implementation plan, task list, and code conventions from PRD, user stories, architecture document, schema, and ADR.

## Trigger

Use this skill when:

- PRD is approved.
- Architecture document or ADR exists.
- Team needs task list before coding.
- AI Agent needs implementation boundaries and verification steps.

## Inputs

Required:

- PRD
- User stories
- Acceptance criteria
- Architecture document
- Message schema or API contract
- ADR

Optional:

- Existing code conventions
- Test strategy
- Deployment constraints
- Security constraints

## Workflow

1. Read PRD and identify product intent.
2. Read architecture docs and identify system boundaries.
3. Map requirements to Clean Architecture layers.
4. Split work by domain, service, adapter, repository, handler, tests, observability, and docs.
5. Define package/file plan.
6. Define code conventions.
7. Create TDD-first task sequence.
8. Add verification commands.
9. Add risk checklist and Definition of Done.

## Quality Rules

- Domain must not import infrastructure.
- Services depend on interfaces, not concrete adapters.
- Repositories hide database details.
- Adapters translate external payloads into domain models.
- Every task must have verification command.
- Every user story must map to at least one test.
- Open questions must be explicit before implementation starts.
```

## Implementation Review Checklist

| Check | Yes/No | Notes |
|---|---|---|
| PRD and architecture docs were read |  |  |
| Tasks are split by Clean Architecture layer |  |  |
| File/package plan is clear |  |  |
| Code conventions are explicit |  |  |
| TDD sequence starts with failing tests |  |  |
| Verification commands are listed |  |  |
| Risks and assumptions are visible |  |  |
| Definition of Done is measurable |  |  |

## Expected Deliverables

```text
docs/implementation/whatsapp-adapter-plan.md
docs/implementation/whatsapp-adapter-tasks.md
docs/implementation/code-conventions.md
```

## Extension Exercise

Ask Reviewer Agent to inspect the task list and find tasks that are too large, missing tests, or violating Clean Architecture boundaries.
