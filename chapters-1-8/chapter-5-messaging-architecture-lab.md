# Chapter 5 Lab - Messaging Architecture Prompt & Skill

## Lab Goal

ใช้ Architecture Agent ช่วยออกแบบ messaging architecture สำหรับ consolidated chat / Unified Inbox โดยใช้ `Next.js`, `Go`, `RabbitMQ`, `MongoDB`, `Redis` และ `ClickHouse` แล้วบันทึกผลเป็น architecture docs และ ADR.

## Target Skill

`/design-messaging-architecture`

## Scenario

ทีมต้องการรวม messages จาก LINE, Facebook, WhatsApp, Slack และ SMS เข้าสู่ Unified Inbox.

Tech stack:

- `Next.js` สำหรับ Unified Inbox UI
- `Go` สำหรับ API Gateway และ Message Router
- `RabbitMQ` สำหรับ routing และ fanout
- `MongoDB` สำหรับ message storage
- `Redis` สำหรับ session cache และ rate limiter
- `ClickHouse` สำหรับ analytics

## Step-by-step Lab

### Step 1 - Create architecture branch

```bash
git switch -c lab/chapter-5-messaging-architecture
mkdir -p docs/architecture/adr
```

### Step 2 - Capture architecture context

สร้าง `docs/architecture/messaging-context.md`.

```markdown
# Messaging Architecture Context

## Business Goal

Support agents must see messages from multiple channels in one Unified Inbox.

## Channels

- LINE
- Facebook
- WhatsApp
- Slack
- SMS

## Required Capabilities

- Normalize inbound payloads into one message model.
- Store message history.
- Route events to storage, analytics, and notification consumers.
- Cache active sessions.
- Rate-limit abusive traffic.
- Produce analytics by channel and time window.
```

### Step 3 - Generate architecture with prompt

Use this prompt with Architecture Agent.

```text
Task:
Design messaging architecture for a consolidated chat / Unified Inbox platform.

Action:
Use the given tech stack and produce architecture decisions, message flow, schemas, risks, and validation checklist.

Goal:
Create reviewable architecture docs and ADR that Developer, Tester, and DevOps Agents can use.

Context:
- UI: Next.js Unified Inbox
- Backend: Go API Gateway and Message Router
- Routing: RabbitMQ fanout exchange
- Storage: MongoDB UnifiedMessage collection
- Cache: Redis session cache and rate limiter
- Analytics: ClickHouse event pipeline

Required Output:
1. End-to-end message flow
2. RabbitMQ exchange and queue design
3. MongoDB UnifiedMessage schema
4. Redis key design for session cache and rate limiter
5. ClickHouse analytics event schema
6. Failure isolation and retry strategy
7. Idempotency and duplicate prevention
8. Backpressure strategy
9. Monitoring signals
10. ADR with context, decision, alternatives, consequences

Narrowing:
- Keep MVP scope practical.
- Technical words remain in English.
- Use Markdown.
- Include a final architecture review checklist.
```

### Step 4 - Save architecture flow

Save output to:

```text
docs/architecture/messaging-flow.md
```

Expected sections:

```markdown
# Messaging Flow

## 1. Overview
## 2. Channel Adapter Input
## 3. Go API Gateway
## 4. RabbitMQ Fanout Exchange
## 5. Storage Queue to MongoDB
## 6. Analytics Queue to ClickHouse
## 7. Notification Queue
## 8. Redis Session Cache
## 9. Failure and Retry Strategy
## 10. Monitoring Signals
```

### Step 5 - Generate message schema

Prompt:

```text
Task:
Create a MongoDB UnifiedMessage schema and ClickHouse analytics event schema.

Action:
Define fields, types, indexes, idempotency keys, retention considerations, and example documents.

Goal:
Produce schema docs that Dev Agent and Tester Agent can use to implement and verify message persistence and analytics.
```

Save output to:

```text
docs/architecture/message-schema.md
```

### Step 6 - Generate ADR

Prompt:

```text
Task:
Write an Architecture Decision Record for the messaging architecture.

Action:
Document why the team uses RabbitMQ, MongoDB, Redis, and ClickHouse. Compare alternatives and list consequences.

Goal:
Create a traceable ADR that explains the decision for future maintainers.
```

Save output to:

```text
docs/architecture/adr/adr-messaging-architecture.md
```

## Skill - `/design-messaging-architecture`

```markdown
# /design-messaging-architecture

## Purpose

Design messaging architecture for multi-channel systems using queues, storage, cache, analytics, and operational safeguards.

## Trigger

Use this skill when:

- A feature spans multiple message channels.
- The team needs queue topology or message flow.
- A new channel adapter affects storage, cache, analytics, or notification.
- Architecture decision must be captured in ADR.

## Inputs

Required:

- Business goal
- Channels
- Tech stack
- Data retention needs
- Latency or throughput target

Optional:

- Existing schemas
- Current queue topology
- Known failure modes
- Security constraints
- Analytics requirements

## Workflow

1. Read context and constraints.
2. Map end-to-end message flow.
3. Design RabbitMQ exchange, queues, routing, retry, and dead-letter behavior.
4. Define MongoDB UnifiedMessage schema and indexes.
5. Define Redis session cache and rate limiter keys.
6. Define ClickHouse analytics event schema and ingest strategy.
7. Identify failure isolation, idempotency, backpressure, and monitoring.
8. Write ADR with alternatives and consequences.
9. Produce architecture review checklist.

## Quality Rules

- Each component must have one clear responsibility.
- Message writes must be idempotent.
- Retry strategy must avoid duplicate side effects.
- Analytics failure must not block message storage.
- Cache fallback must be defined.
- Monitoring signals must include queue depth, error rate, latency, and ingest lag.
- ADR must include context, decision, alternatives, consequences, and links.
```

## Architecture Review Checklist

| Check | Yes/No | Notes |
|---|---|---|
| RabbitMQ exchange and queues are clear |  |  |
| MongoDB `UnifiedMessage` schema is defined |  |  |
| Redis session cache keys and TTL are defined |  |  |
| Redis rate limiter strategy is defined |  |  |
| ClickHouse analytics schema is defined |  |  |
| Idempotency key is defined |  |  |
| Retry and dead-letter behavior are defined |  |  |
| Backpressure behavior is defined |  |  |
| Monitoring signals are defined |  |  |
| ADR includes alternatives and consequences |  |  |

## Expected Deliverables

```text
docs/architecture/messaging-flow.md
docs/architecture/message-schema.md
docs/architecture/adr/adr-messaging-architecture.md
```

## Extension Exercise

เพิ่ม requirement ว่า WhatsApp webhook ต้อง verify signature และ customer phone number เป็น PII. ให้ update architecture, schema, monitoring และ ADR ให้รองรับ security requirement นี้.
