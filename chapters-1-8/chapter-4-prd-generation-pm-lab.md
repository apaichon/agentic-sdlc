# Chapter 4 Lab - สร้าง PRD ด้วย PM Agent

## Lab Goal

ใช้ PM Agent เปลี่ยน stakeholder input แบบหยาบให้เป็น structured Product Requirements Document (PRD) จากนั้น refine เป็น user stories, acceptance criteria และ PM approval checklist.

## Target Skill

`/generate-prd`

## When To Use This Lab

ใช้ lab นี้หลังเรียน Chapter 4 topics:

- 4.1 RISEN Prompting Framework
- 4.2 Three-Phase PRD Generation Workflow
- 4.3 User Story Anatomy
- 4.4 Sprint Backlog Dependency Graph
- 4.5 `/sprint-plan` Skill Cycle
- 4.C Prompt Engineering Frameworks Cheatsheet

## Learning Outcomes

เมื่อจบ lab นี้ ผู้เรียนจะสามารถ:

- Capture stakeholder input ที่ยัง vague แล้วเปลี่ยนเป็น PRD context ที่ชัดเจน.
- ใช้ `TAG` และ `RISEN` patterns เพื่อสั่งงาน PM Agent.
- Generate PRD ที่มี goals, non-goals, scope, requirements, risks, metrics และ open questions.
- Convert PRD output เป็น user stories ที่ testable.
- Define Human PM approval gate ก่อน Dev, Tester และ DevOps เริ่มงาน.

## Scenario

Business ต้องการเพิ่ม WhatsApp channel เข้าไปใน Unified Inbox platform ที่มีอยู่แล้ว.

Raw stakeholder input:

```text
Customers ต้องการ reply WhatsApp messages จาก inbox เดียวกับที่ใช้ LINE และ Facebook.
Support agents ควรเห็น WhatsApp conversations ได้เร็ว.
ต้องมี message history, delivery status และ basic analytics.
Version แรกควร safe และ simple.
ถ้าเป็นไปได้ อยาก launch ใน next sprint.
```

## Step-by-step Lab

### Step 1 - สร้าง Lab Branch

```bash
git switch -c lab/chapter-4-generate-prd
mkdir -p docs/product
```

Expected result:

```text
docs/product/
```

### Step 2 - Capture Stakeholder Input

สร้าง `docs/product/whatsapp-adapter-raw-input.md`.

```markdown
# WhatsApp Adapter - Raw Stakeholder Input

## Business Request

Customers ต้องการ reply WhatsApp messages จาก inbox เดียวกับที่ใช้ LINE และ Facebook.

## Desired Capabilities

- Support agents สามารถ read และ reply WhatsApp messages.
- Conversations แสดงใน Unified Inbox.
- Message history ถูก stored.
- Delivery status มองเห็นได้.
- มี basic analytics.

## Constraints

- Version แรกควร safe และ simple.
- Target launch คือ next sprint.
- ต้อง follow existing channel adapter architecture.
```

### Step 3 - Generate PRD Draft แรก

ใช้ prompt ด้านล่างกับ PM Agent.

## Generate PRD Prompt

```text
Task:
สร้าง Product Requirements Document (PRD) สำหรับ WhatsApp Adapter feature.

Action:
ใช้ RISEN framework:

Role:
Act as a senior Product Manager สำหรับ Agentic SDLC team ที่กำลังสร้าง Unified Inbox platform.

Instructions:
เปลี่ยน raw stakeholder input ให้เป็น structured PRD.
ใช้ product language ที่ชัดเจน.
แยก goals ออกจาก non-goals.
ทำ requirements ให้ testable.
ระบุ risks, assumptions, dependencies และ open questions.
ห้าม invent technical commitments ที่ input ไม่ได้ support.

Steps:
1. สรุป product problem.
2. ระบุ target users และ user needs.
3. เขียน product goals และ non-goals.
4. ระบุ functional requirements.
5. ระบุ non-functional requirements.
6. สร้าง 3-5 user stories พร้อม Given/When/Then acceptance criteria.
7. ระบุ dependencies ระหว่าง PM, Dev, Tester และ DevOps.
8. List risks, assumptions และ open questions.
9. Define success metrics สำหรับ launch readiness.
10. สร้าง PM approval checklist.

End Goal:
สร้าง PRD ที่ Human PM review ได้ และ handoff ต่อให้ Developer, Tester และ DevOps Agents.

Narrowing:
- Keep MVP scope small.
- Assume ว่าต้อง fit ใน one sprint.
- ใช้ Markdown format.
- Include final section ชื่อ "Human PM Approval Gate".
- Technical words should remain in English.

Raw Input:
Customers ต้องการ reply WhatsApp messages จาก inbox เดียวกับที่ใช้ LINE และ Facebook.
Support agents ควรเห็น WhatsApp conversations ได้เร็ว.
ต้องมี message history, delivery status และ basic analytics.
Version แรกควร safe และ simple.
ถ้าเป็นไปได้ อยาก launch ใน next sprint.
```

### Step 4 - Save PRD

บันทึก PM Agent output ไปที่:

```text
docs/product/whatsapp-adapter-prd.md
```

Expected PRD sections:

```markdown
# WhatsApp Adapter PRD

## 1. Summary
## 2. Problem Statement
## 3. Target Users
## 4. Goals
## 5. Non-Goals
## 6. Functional Requirements
## 7. Non-Functional Requirements
## 8. User Stories
## 9. Acceptance Criteria
## 10. Dependencies
## 11. Risks and Assumptions
## 12. Open Questions
## 13. Success Metrics
## 14. Human PM Approval Gate
```

### Step 5 - Review and Refine

ให้ PM Agent critique PRD.

```text
Task:
Review PRD นี้ในมุม Human PM ที่เตรียมเข้า sprint planning.

Action:
หา unclear scope, untestable requirements, missing assumptions, missing risks และ acceptance criteria ที่ verify ไม่ได้.

Goal:
Return review table แบบกระชับ พร้อม Issue, Why it matters, Recommended change และ Approval impact.
```

Update PRD ตาม feedback ที่ valid.

### Step 6 - Generate User Stories

ใช้ prompt นี้หลัง PRD ผ่าน review.

```text
Task:
Generate sprint-ready user stories จาก approved PRD.

Action:
สร้าง 5 user stories พร้อม:
- Story title
- User role
- User need
- Business value
- Given/When/Then acceptance criteria
- Priority
- Dependencies
- Suggested owner role

Goal:
สร้าง stories ที่ Developer Agent และ Tester Agent ใช้ต่อได้โดยไม่ต้องเดา product intent.
```

บันทึก output ไปที่:

```text
docs/product/whatsapp-adapter-user-stories.md
```

### Step 7 - PM Approval Checklist

ก่อน handoff งานให้ Dev, Tester และ DevOps Agents, Human PM ต้องตอบ checklist นี้:

| Question | Yes/No | Notes |
|---|---|---|
| MVP scope ชัดเจนหรือไม่? |  |  |
| Non-goals ระบุชัดหรือไม่? |  |  |
| User stories testable หรือไม่? |  |  |
| Launch success metrics measurable หรือไม่? |  |  |
| Open questions มี owner หรือไม่? |  |  |
| Dependencies มองเห็นชัดหรือไม่? |  |  |
| Feature พร้อมเข้า `/sprint-plan` หรือยัง? |  |  |

## PM Skill - `/generate-prd`

ใช้ skill definition นี้เป็น team standard สำหรับ PM-led PRD generation.

```markdown
# /generate-prd

## Purpose

Generate structured PRD จาก raw stakeholder input, meeting notes, customer feedback หรือ feature brief.

## Trigger

ใช้ skill นี้เมื่อ:

- Feature idea ยังไม่ structured.
- Stakeholder input ยัง vague หรือ scattered.
- Team ต้องการ PRD ก่อน sprint planning.
- PM ต้องการ user stories และ acceptance criteria เพื่อ review.

## Inputs

Required:

- Raw stakeholder input
- Target users
- Business goal
- Known constraints

Optional:

- Existing architecture context
- Competitive references
- Customer feedback
- Timeline or release target
- Compliance or security constraints

## Workflow

1. Read all provided context.
2. ถาม clarification questions ได้ไม่เกิน 5 ข้อ เฉพาะเมื่อ PRD จะ unsafe หรือ misleading ถ้าไม่มีคำตอบ.
3. Draft PRD ใน Markdown.
4. แยก goals, non-goals, requirements, risks, assumptions, dependencies และ open questions.
5. Generate user stories พร้อม Given/When/Then acceptance criteria.
6. Create measurable success metrics.
7. Add Human PM Approval Gate.
8. Provide concise review checklist.

## Output Format

Return Markdown with these sections:

1. Summary
2. Problem Statement
3. Target Users
4. Goals
5. Non-Goals
6. Functional Requirements
7. Non-Functional Requirements
8. User Stories
9. Acceptance Criteria
10. Dependencies
11. Risks and Assumptions
12. Open Questions
13. Success Metrics
14. Human PM Approval Gate

## Quality Rules

- Requirements ต้อง testable.
- Non-goals ต้องช่วยป้องกัน scope creep.
- Acceptance criteria ต้องใช้ Given/When/Then.
- Open questions ต้องมี owner หรือ decision path.
- ห้าม invent requirements ถ้าไม่ label เป็น assumptions.
- Keep technical words in English.

## Human Approval Gate

Human PM ต้อง approve PRD ก่อน:

- Developer Agent starts implementation.
- Tester Agent creates final test plan.
- DevOps Agent creates deployment workflow.
- Execute `/sprint-plan`.
```

## Expected Lab Deliverables

เมื่อจบ lab ผู้เรียนควรมี:

```text
docs/product/whatsapp-adapter-raw-input.md
docs/product/whatsapp-adapter-prd.md
docs/product/whatsapp-adapter-user-stories.md
```

## Review Checklist

- PRD มี MVP scope ชัดเจน.
- PRD มี explicit non-goals.
- User stories testable.
- Acceptance criteria ใช้ Given/When/Then.
- Risks และ assumptions มองเห็นชัด.
- Success metrics measurable.
- มี Human PM approval gate.

## Extension Exercise

ลองใช้ `/generate-prd` skill เดียวกันกับ feature อื่น เช่น:

- Slack Adapter
- SMS Gateway Failover
- Production Dashboard
- Incident Response Automation

Compare PRD ทั้งสองชุด แล้วระบุว่า section ไหน consistent เพราะใช้ skill เดียวกัน.
